# Sayfalar ve Düzenler

Next.js 13 içindeki Uygulama Yönlendiricisi, [sayfaları](#sayfalar), [paylaşılan düzenleri](#düzenler) ve [şablonları](#şablonlar) kolayca oluşturmak için yeni dosya kurallarını tanıttı. Bu bölüm, Next.js uygulamanızda bu özel dosyaları nasıl kullanacağınız konusunda size rehberlik edecektir.

## Sayfalar

Sayfa, bir rotaya **özgü** kullanıcı arayüzüdür. Bir `page.js` dosyasından bir bileşeni dışa aktararak sayfaları tanımlayabilirsiniz. Bir [rota tanımlamak](#rotaların-tanımlanması) için iç içe klasörler ve rotayı genel erişime açmak için bir `page.js` dosyası kullanın.

`app` dizini içine bir `page.js` dosyası ekleyerek ilk sayfanızı oluşturun:

<img alt="sayfalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fpage-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
// `app/page.tsx` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>;
}
```

```tsx
// `app/dashboard/page.tsx` is the UI for the `/dashboard` URL
export default function Page() {
  return <h1>Hello, Dashboard Page!</h1>;
}
```

## Düzenler

Düzen, birden fazla sayfa arasında **paylaşılan** kullanıcı arayüzüdür. Gezinme sırasında düzenler durumu korur, etkileşimli kalır ve yeniden oluşturulmaz. Düzenler iç içe de yerleştirilebilir.

Bir `layout.js` dosyasından bir React bileşenini dışa aktararak `default` olarak bir düzen tanımlayabilirsiniz. Bileşen, render sırasında bir alt düzen (varsa) veya bir alt sayfa ile doldurulacak bir `children` prop kabul etmelidir.

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Flayout-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}: {
  children: React.ReactNode;
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>

      {children}
    </section>
  );
}
```

Bilmekte fayda var:

- En üstteki düzen [Kök Düzen](#kök-düzeni-gerekli) olarak adlandırılır. Bu **gerekli** düzen, bir uygulamadaki tüm sayfalarda paylaşılır. Kök düzenler `html` ve `body` etiketlerini içermelidir.
- Herhangi bir rota segmenti isteğe bağlı olarak kendi Düzenini tanımlayabilir. Bu düzenler o segmentteki tüm sayfalarda paylaşılır.
- Bir rotadaki düzenler varsayılan olarak **iç içedir**. Her üst düzen, React `children` prop kullanarak altındaki alt düzenleri sarar.
- Paylaşılan düzenlere belirli rota segmentlerini dahil etmek ve hariç tutmak için [Rota Gruplarını](#rota-grupları) kullanabilirsiniz.
- Düzenler varsayılan olarak Sunucu Bileşenleridir ancak İstemci Bileşeni olarak ayarlanabilir.
- Düzenler veri getirebilir.
- Bir üst düzen ile onun alt düzenleri arasında veri aktarımı mümkün değildir. Bununla birlikte, aynı verileri bir rotada birden fazla kez getirebilirsiniz ve React, performansı etkilemeden istekleri otomatik olarak çıkaracaktır.
- Düzenlerin geçerli rota segmentlerine erişimi yoktur. Rota segmentlerine erişmek için, bir İstemci - Bileşeninde `useSelectedLayoutSegment` veya `useSelectedLayoutSegments` kullanabilirsiniz.
- Düzenler için `.js`, `.jsx` veya `.tsx` dosya uzantıları kullanılabilir.
- Bir `layout.js` ve `page.js` dosyası aynı klasörde tanımlanabilir. Düzen, sayfayı saracaktır.

## Kök Düzeni (Gerekli)

Kök düzen, `app` dizininin en üst düzeyinde tanımlanır ve tüm rotalar için geçerlidir. Bu düzen, sunucudan döndürülen ilk HTML'yi değiştirmenize olanak tanır.

```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

Bilmekte fayda var:

- `app` dizini **mutlaka** bir kök düzen içermelidir.
- Next.js `<html>` ve `<body>` etiketlerini otomatik olarak oluşturmadığı için mutlaka kök düzen tanımlamalıdır.
- `<head>` HTML öğelerini yönetmek için [yerleşik SEO desteğini](#metadata) kullanabilirsiniz, örneğin, `<title>` öğesi.
- Birden fazla kök düzen oluşturmak için [rota gruplarını](#rota-grupları) kullanabilirsiniz.
- Kök düzen varsayılan olarak bir [Sunucu Bileşenidir](#sunucu-server-bileşenleri) ve [İstemci Bileşeni](#i̇stemci-client-bileşenleri) olarak ayarlanamaz.

## İç içe Düzenler

Bir klasör içinde tanımlanan düzenler (örn. `app/dashboard/layout.js`) belirli rota segmentlerine (örn. `acme.com/dashboard`) uygulanır ve bu segmentler etkin olduğunda oluşturulur. Varsayılan olarak, dosya hiyerarşisindeki mizanpajlar **iç içe geçmiştir**, bu da children düzenlerini `children` prop'ları aracılığıyla sardıkları anlamına gelir.

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-layout.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return <section>{children}</section>;
}
```

Yukarıdaki iki düzeni birleştirecek olursanız, kök düzen (`app/layout.js`) gösterge tablosu düzenini (`app/dashboard/layout.js`) saracak ve bu da `app/dashboard/*` içindeki rota segmentlerini saracaktır.

İki düzen bu şekilde iç içe geçecektir:

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-layouts-ui.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

[Rota Gruplarını](#rota-grupları), belirli rota segmentlerini paylaşılan düzenlere dahil etmek ve bu düzenlerden çıkarmak için kullanabilirsiniz.

## Şablonlar

Şablonlar, her bir alt düzeni veya sayfayı sarması bakımından düzenlere benzer. Rotalar arasında kalıcı olan ve durumu koruyan düzenlerin aksine, şablonlar gezinme sırasında alt öğelerinin her biri için yeni bir örnek oluşturur. Bu, bir kullanıcı bir şablonu paylaşan rotalar arasında gezindiğinde, bileşenin yeni bir örneğinin monte edildiği, DOM öğelerinin yeniden oluşturulduğu, durumun korunmadığı ve efektlerin yeniden senkronize edildiği anlamına gelir.

Bu belirli davranışlara ihtiyaç duyduğunuz durumlar olabilir ve şablonlar düzenlerden daha uygun bir seçenek olabilir. Örneğin:

- CSS veya animasyon kütüphaneleri kullanarak giriş/çıkış animasyonları.
- `useEffect` (örneğin sayfa görüntülemelerini kaydetme) ve `useState` (örneğin sayfa başına geri bildirim formu) kullanan özellikler.
- Varsayılan framework davranışını değiştirmek için. Örneğin, düzenlerin içindeki Askıya Alma Sınırları, geri dönüşü yalnızca Düzen ilk kez yüklendiğinde gösterir ve sayfalar arasında geçiş yaparken göstermez. Şablonlar için, geri dönüş her gezinmede gösterilir.

Öneri: Şablon kullanmak için özel bir neden yoksa Düzenleri kullanmanız önerilir.

Bir `template.js` dosyasından varsayılan bir React bileşeni dışa aktarılarak bir şablon tanımlanabilir. Bileşen, iç içe segmentler olacak bir `children` prop kabul etmelidir.

<img alt="şablonlar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ftemplate-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function Template({ children }: { children: React.ReactNode }) {
  return <div>{children}</div>;
}
```

Bir düzen ve şablona sahip bir rota segmentinin işlenmiş çıktısı bu şekilde olacaktır:

```tsx
<Layout>
  {/* Note that the template is given a unique key. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

## `<head>`'in değiştirilmesi

`app` dizininde, [yerleşik SEO desteğini](#metadata) kullanarak `başlık` ve `meta` gibi `<head>` HTML öğelerini değiştirebilirsiniz.

Meta veriler, bir `layout.js` veya `page.js` dosyasında bir meta veri nesnesi veya `generateMetadata` işlevi dışa aktarılarak tanımlanabilir.

```tsx
import { Metadata } from "next";

export const metadata: Metadata = {
  title: "Next.js",
};

export default function Page() {
  return "...";
}
```

Bilmekte fayda var: Kök düzenlere `<title>` ve `<meta>` gibi `<head>` etiketlerini manuel olarak **eklememelisiniz**. Bunun yerine, `<head>` öğelerini akışa alma ve çoğaltma gibi gelişmiş gereksinimleri otomatik olarak ele alan Metadata API'sini kullanmalısınız.