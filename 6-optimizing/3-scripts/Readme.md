# Komut Dosyası Optimizasyonu (Script Optimization)

## Düzen Komut Dosyaları (Layout Scripts)

Birden fazla rota için üçüncü taraf bir komut dosyası yüklemek için `next/script` dosyasını içe aktarın ve komut dosyasını doğrudan düzen bileşeninize ekleyin:

```js
// app/dashboard/layout.tsx

import Script from "next/script";

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <>
      <section>{children}</section>
      <Script src="https://example.com/script.js" />
    </>
  );
}
```

Üçüncü taraf komut dosyası, kullanıcı tarafından klasör rotasına (örn. `dashboard/page.js`) veya iç içe geçmiş herhangi bir rotaya (örn. `dashboard/settings/page.js`) erişildiğinde getirilir. Next.js, kullanıcı aynı düzende birden fazla rota arasında gezinse bile komut dosyasının yalnızca bir kez yüklenmesini sağlar.

## Uygulama Komut Dosyaları (Application Scripts)

Tüm rotalar için üçüncü taraf bir komut dosyası yüklemek için `next/script` dosyasını içe aktarın ve komut dosyasını doğrudan kök düzeninize ekleyin:

```js
// app/layout.tsx
import Script from "next/script";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <Script src="https://example.com/script.js" />
    </html>
  );
}
```

Bu komut dosyası, uygulamanızdaki herhangi bir rotaya erişildiğinde yüklenir ve yürütülür. Next.js, kullanıcı birden fazla sayfa arasında gezinse bile betiğin yalnızca bir kez yüklenmesini sağlayacaktır.

**Öneri:** Performans üzerindeki gereksiz etkiyi en aza indirmek için üçüncü taraf komut dosyalarını yalnızca belirli sayfalara veya düzenlere eklemenizi öneririz.

## Strateji (Strategy)

`next/script`'in varsayılan davranışı herhangi bir sayfa veya düzende üçüncü taraf komut dosyalarını yüklemenize izin verse de, `strategy` özelliğini kullanarak yükleme davranışına ince ayar yapabilirsiniz:

- `beforeInteractive`: Kodu herhangi bir Next.js kodundan önce ve herhangi bir sayfa hidrasyonu gerçekleşmeden önce yükleyin.
- `afterInteractive`: (varsayılan) Kodu erken ancak sayfada bir miktar hidrasyon gerçekleştikten sonra yükleyin.
- `lazyOnload`: Tarayıcı boşta kaldığında kodu daha sonra yükleyin.
- `worker`: (deneysel) Komut dosyasını bir web çalışanına yükleyin.

## Komut Dosyalarını Bir Web İşçisine Boşaltma (Deneysel) (Offloading Scripts to a Web Worker (Experimental))

**Uyarı:** `worker` stratejisi henüz kararlı değildir ve henüz `app` dizini ile çalışmaz. Dikkatli kullanın.

`worker` stratejisini kullanan komut dosyaları [Partytown](https://partytown.builder.io/) ile bir web çalışanına yüklenir ve yürütülür. Bu, ana iş parçacığını uygulama kodunuzun geri kalanına ayırarak sitenizin performansını artırabilir.

Bu strateji hala deneyseldir ve yalnızca `next.config.js` dosyasında `nextScriptWorkers` bayrağı etkinleştirilirse kullanılabilir:

```js
// next.config.js

module.exports = {
  experimental: {
    nextScriptWorkers: true,
  },
};
```

Ardından, `next`'i çalıştırın (normalde `npm run dev` veya `yarn dev`) ve Next.js kurulumu tamamlamak için gerekli paketlerin kurulumunda size rehberlik edecektir:

```bash
npm run dev # or yarn dev
```

Bunun gibi talimatlar göreceksiniz: Lütfen `npm install @builder.io/partytown` komutunu çalıştırarak Partytown'ı yükleyin

Kurulum tamamlandığında, `strategy="worker"` tanımlaması uygulamanızda Partytown'ı otomatik olarak başlatacak ve komut dosyasını bir web worker'a yükleyecektir.

```js
// pages/home.tsx

import Script from "next/script";

export default function Home() {
  return (
    <>
      <Script src="https://example.com/script.js" strategy="worker" />
    </>
  );
}
```

Bir web çalışanına üçüncü taraf bir komut dosyası yüklerken dikkate alınması gereken bir dizi ödünleşme vardır. Daha fazla bilgi için lütfen Partytown'ın [tradeoffs](https://partytown.builder.io/trade-offs) belgelerine bakın.

## Satır İçi Komut Dosyaları (Inline Scripts)

Satır içi komut dosyaları veya harici bir dosyadan yüklenmeyen komut dosyaları da Komut Dosyası bileşeni tarafından desteklenir. JavaScript'i küme parantezleri içine yerleştirerek yazılabilirler:

```js
<Script id="show-banner">
  {`document.getElementById('banner').classList.remove('hidden')`}
</Script>
```

Ya da `dangerouslySetInnerHTML` özelliğini kullanarak:

```js
<Script
  id="show-banner"
  dangerouslySetInnerHTML={{
    __html: `document.getElementById('banner').classList.remove('hidden')`,
  }}
/>
```

**Uyarı:** Next.js'nin komut dosyasını izlemesi ve optimize etmesi için satır içi komut dosyaları için bir `id` özelliği atanmalıdır.

## Ek Kodun Yürütülmesi (Executing Additional Code)

Olay işleyicileri, belirli bir olay gerçekleştikten sonra ek kod çalıştırmak için Script bileşeniyle birlikte kullanılabilir:

- `onLoad`: Kodun yüklenmesi tamamlandıktan sonra kodu çalıştırın.
- `onReady`: Kodun yüklenmesi bittikten sonra ve bileşen her takıldığında kodu çalıştırın.
- `onError`: Kod yüklenemezse kodu çalıştırın.

Bu işleyiciler yalnızca `next/script` içe aktarıldığında ve kodun ilk satırı olarak `"use client"` tanımlanan bir İstemci Bileşeni içinde kullanıldığında çalışır:

```js
// app/page.tsx;

("use client");

import Script from "next/script";

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        onLoad={() => {
          console.log("Script has loaded");
        }}
      />
    </>
  );
}
```

## Ek Özellikler

Bir `<script>` öğesine atanabilecek, Kod bileşeni tarafından kullanılmayan, [nonce](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/nonce) veya [özel veri nitelikleri](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*) gibi birçok DOM niteliği vardır. Herhangi bir ek niteliğin eklenmesi, HTML'ye dahil edilen son, optimize edilmiş `<script>` öğesine otomatik olarak iletecektir.

```js
// app/page.tsx;

import Script from "next/script";

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        id="example-script"
        nonce="XUENAJFW"
        data-test="script"
      />
    </>
  );
}
```
