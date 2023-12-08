# App Router Artırımlı Benimseme Kılavuzu

## Yükseltme

### Node.js Sürümü

Minimum Node.js sürümü artık v18.17'dir. Daha fazla bilgi için [Node.js belgelerine](https://nodejs.org/docs/latest-v18.x/api/) bakın.

### Next.js Sürümü

Next.js sürüm 13'e güncellemek için tercih ettiğiniz paket yöneticisini kullanarak aşağıdaki komutu çalıştırın:

```bash
npm install next@latest react@latest react-dom@latest
```

### ESLint Sürümü

ESLint kullanıyorsanız, ESLint sürümünüzü yükseltmeniz gerekir:

```bash
npm install -D eslint-config-next@latest
```

**Bilmekte fayda var:** ESLint değişikliklerinin etkili olması için VS Code'da ESLint sunucusunu yeniden başlatmanız gerekebilir. Komut Paletini açın (Mac'te `cmd+shift+p`; Windows'ta `ctrl+shift+p`) ve ESLint'i arayın: `ESLint: Restart ESLint Server`.

## Sonraki Adımlar

Güncellemeyi yaptıktan sonra, sonraki adımlar için aşağıdaki bölümlere bakın:

- [Yeni özellikleri yükseltin](https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration#upgrading-new-features): Geliştirilmiş Görüntü ve Bağlantı Bileşenleri gibi yeni özelliklere yükseltme yapmanıza yardımcı olacak bir kılavuz.
- [Sayfalardan uygulama dizinine geçiş](https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration#migrating-from-pages-to-app): Sayfalardan uygulama dizinine aşamalı olarak geçiş yapmanıza adım adım yardımcı olacak kılavuz.

## Yeni Özelliklere Yükseltilmesi

Next.js 13, yeni özellikler ve kurallar içeren yeni Uygulama Yönlendiricisini tanıttı. Yeni Yönlendirici, app dizininde bulunur ve pages dizini ile birlikte var olur.

Next.js 13'e yükseltmek için yeni Uygulama Yönlendiricisini kullanmanız gerekmez. Güncellenen Görüntü bileşeni, Bağlantı bileşeni, Komut Dosyası bileşeni ve Yazı Tipi optimizasyonu gibi her iki dizinde de çalışan yeni özelliklere sahip sayfaları kullanmaya devam edebilirsiniz.

### `<Image/>` Bileşeni

Next.js 12, geçici bir içe aktarma ile Görüntü Bileşeninde yeni iyileştirmeler sundu: `next/future/image`. Bu iyileştirmeler arasında daha az istemci tarafı JavaScript, görüntüleri genişletmek ve şekillendirmek için daha kolay yollar, daha iyi erişilebilirlik ve yerel tarayıcıda lazy loading yer alıyordu.

Sürüm 13'te, bu yeni davranış artık `next/image` için varsayılandır.

Yeni Görüntü Bileşenine geçiş yapmanıza yardımcı olacak iki kodmod vardır:

- [`next-image-to-legacy-image` codemod](https://nextjs.org/docs/app/building-your-application/upgrading/codemods#next-image-to-legacy-image): `next/image` içe aktarmalarını güvenli ve otomatik olarak `next/legacy/image` olarak yeniden adlandırır. Mevcut bileşenler aynı davranışı koruyacaktır.
- [`next-image-experimental` codemod](https://nextjs.org/docs/app/building-your-application/upgrading/codemods#next-image-experimental): Tehlikeli bir şekilde satır içi stiller ekler ve kullanılmayan propları kaldırır. Bu, mevcut bileşenlerin davranışını yeni varsayılanlarla eşleşecek şekilde değiştirecektir. Bu codemod'u kullanmak için önce `next-image-to-legacy-image` codemod'unu çalıştırmanız gerekir.

### `<Link>` Bileşeni

`<Link>` Bileşeni artık alt öğe olarak manuel olarak bir `<a>` etiketi eklemeyi gerektirmiyor. Bu davranış 12.2 sürümünde deneysel bir seçenek olarak eklenmişti ve artık varsayılandır. Next.js 13'te `<Link>` bileşeni her zaman `<a>` olarak görünür ve altta yatan etikete prop'ları yönlendirmenize olanak tanır.

Örneğin:

```js
import Link from 'next/link'

// Next.js 12: `<a>` iç içe geçmelidir, aksi takdirde hariç tutulur
<Link href="/about">
  <a>About</a>
</Link>

// Next.js 13: `<Link>` her zaman arka planda `<a>` oluşturur
<Link href="/about">
  About
</Link>
```

Bağlantılarınızı Next.js 13'e yükseltmek için `new-link codemod`'u kullanabilirsiniz.

### `<Script>` Bileşeni

`next/script`'in davranışı hem `pages` hem de `app` yönlendiricisini destekleyecek şekilde güncellendi, ancak sorunsuz bir geçiş sağlamak için bazı değişikliklerin yapılması gerekiyor:

- Daha önce `_document.js` dosyasına eklediğiniz `beforeInteractive` komut dosyalarını kök düzen dosyasına (`app/layout.tsx`) taşıyın.
- Deneysel `worker` stratejisi henüz `app` yönlendiricisinde çalışmamaktadır ve bu stratejiyle gösterilen komut dosyalarının kaldırılması ya da farklı bir strateji (örn. `lazyOnload`) kullanacak şekilde değiştirilmesi gerekecektir.
- `onLoad`, `onReady` ve `onError` işleyicileri Sunucu Bileşenlerinde çalışmayacaktır, bu nedenle bunları bir İstemci Bileşenine taşıdığınızdan veya tamamen kaldırdığınızdan emin olun.

### Yazı Tipi Optimizasyonu

Daha önce Next.js, [inlining font CSS](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) yaparak fontları optimize etmenize yardımcı oluyordu. Sürüm 13, mükemmel performans ve gizlilik sağlarken yazı tipi yükleme deneyiminizi özelleştirmenize olanak tanıyan yeni `next/font` modülünü sunar. `next/font` hem `pages` hem de `app` yönlendiricisinde desteklenir.

CSS inlining hala `pages` yönlendiricisinde çalışsa da, `app` yönlendiricisinde çalışmaz. Bunun yerine `next/font` kullanmalısınız.

`next/font` öğesinin nasıl kullanılacağını öğrenmek için [Yazı Tipi Optimizasyonu](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) sayfasına bakın.

## Sayfalardan uygulamaya geçiş

🎥 **İzleyin:** App Router'ı kademeli olarak nasıl benimseyeceğinizi öğrenin → [YouTube (16 dakika)](https://www.youtube.com/watch?v=YQMSietiFm0).

App Yönlendiricisine geçiş ile birlikte, Next.js'nin üzerine inşa edildiği Sunucu Bileşenleri, Suspense ve daha fazlası gibi React özelliklerini ilk kez kullanıyor olabilirsiniz. Özel dosyalar ve düzenler gibi yeni Next.js özellikleriyle birleştirildiğinde, geçiş, öğrenilmesi gereken yeni kavramlar, zihinsel modeller ve davranış değişiklikleri anlamına gelir.

Geçişinizi daha küçük adımlara bölerek bu güncellemelerin birleşik karmaşıklığını azaltmanızı öneririz. `app` dizini, sayfa sayfa geçişe izin vermek için `pages` dizini ile eşzamanlı olarak çalışacak şekilde tasarlanmıştır.

- Next.js'in uygulama dizini, iç içe geçmiş rotaları ve düzenleri destekler. Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application/routing) tıklayın.
- İç içe klasörler kullanarak rotaları tanımlayabilir ve özel bir `page.js` dosyası kullanarak bir rota segmentini genel olarak erişilebilir hale getirebilirsiniz. Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application/upgrading/app-router-migration#step-4-migrating-pages) tıklayın.
- Her rota segmenti için UI oluşturmak için özel dosya kuralları kullanılır. En yaygın özel dosyalar `page.js` ve `layout.js`'dir.
  - `page.js` dosyasını, bir rotaya özgü UI tanımlamak için kullanın.
  - `layout.js` dosyasını, birden fazla rotada paylaşılan UI tanımlamak için kullanın.
- Özel dosyalar için `.js`, `.jsx` veya `.tsx` dosya uzantıları kullanılabilir.
- Uygulama dizini içinde bileşenler, stiller, testler ve daha fazlası gibi diğer dosyaları bir arada bulundurabilirsiniz. Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application/routing) tıklayın.
- `getServerSideProps` ve `getStaticProps` gibi veri çekme fonksiyonları, uygulama içinde yeni bir API ile değiştirilmiştir. `getStaticPaths`, `generateStaticParams` ile değiştirilmiştir.
- `pages/_app.js` ve `pages/_document.js`, tek bir kök düzen olan `app/layout.js` ile değiştirilmiştir. Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#root-layout-required) tıklayın.
- `pages/_error.js`, daha ayrıntılı `error.js` özel dosyaları ile değiştirilmiştir. Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application/routing/error-handling) tıklayın.
- `pages/404.js`, `not-found.js` dosyası ile değiştirilmiştir.
- `pages/api/*` şu anda `pages` dizini içinde kalmaktadır.

### Adım 1: Uygulama dizinini oluşturma

En son Next.js sürümüne güncelleyin (13.4 veya üstü gerekir):

```bash
npm install next@latest
```

Ardından, projenizin kök dizininde (veya src/ dizininde) yeni bir uygulama dizini oluşturun.

### Adım 2: Root Layout Oluşturma

Uygulama dizini içinde yeni bir `app/layout.tsx` dosyası oluşturun. Bu, `app` içindeki tüm rotalar için geçerli olacak bir kök düzenidir.

```tsx
// app/layout.tsx
export default function RootLayout({
  // Layouts children prop'u kabul etmek zorundadır.
  // Bu, iç içe düzenler veya sayfalarla doldurulacaktır
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

- Uygulama dizini bir root layout içermelidir.
- Next.js bunları otomatik olarak oluşturmadığı için root layout `<html>` ve `<body>` etiketlerini tanımlamalıdır
- Root layout `pages/_app.tsx` ve `pages/_document.tsx` dosyalarının yerini alır.
- Düzen dosyaları için `.js`, `.jsx` veya `.tsx` uzantıları kullanılabilir.

`<head>` HTML öğelerini yönetmek için yerleşik SEO desteğini kullanabilirsiniz:

```tsx
// app/layout.tsx
import { Metadata } from "next";

export const metadata: Metadata = {
  title: "Home",
  description: "Welcome to Next.js",
};
```

#### `_document.js` ve `_app.js`'den taşıma

Mevcut bir `_app` veya `_document` dosyanız varsa, içeriği (örneğin global stiller) kök düzene (`app/layout.tsx`) kopyalayabilirsiniz. `app/layout.tsx` dosyasındaki stiller `pages/*` için geçerli olmayacaktır. `pages/*` rotalarınızın bozulmasını önlemek için taşıma sırasında `_app` `_document` dosyasını tutmalısınız. Tamamen taşındıktan sonra bunları güvenle silebilirsiniz.

Herhangi bir React Context sağlayıcısı kullanıyorsanız, bunların bir İstemci Bileşenine taşınması gerekecektir.

#### `getLayout()` şablonunu Layouts'a taşıma (İsteğe bağlı)

Next.js, sayfalar dizininde sayfa başına düzenler elde etmek için Sayfa bileşenlerine bir özellik eklemeyi önerdi. Bu model, uygulama dizininde iç içe düzenler için yerel destek ile değiştirilebilir.

### Adım 3: `next/head` kısmından taşınma

`Pages` dizininde, `next/head` React bileşeni başlık ve meta gibi `<head>` HTML öğelerini yönetmek için kullanılır. Uygulama dizininde, `next/head` yeni yerleşik SEO desteği ile değiştirilir.

Öncesi:

```tsx
// pages/index.tsx
import Head from "next/head";

export default function Page() {
  return (
    <>
      <Head>
        <title>My page title</title>
      </Head>
    </>
  );
}
```

Sonrası:

```tsx
// app/page.tsx
import { Metadata } from "next";

export const metadata: Metadata = {
  title: "My Page Title",
};

export default function Page() {
  return "...";
}
```

### Adım 4: Sayfalardan Taşıma

- Uygulama dizinindeki sayfalar varsayılan olarak Sunucu Bileşenleridir. Bu, sayfaların İstemci Bileşenleri olduğu pages dizininden farklıdır.
- Uygulamada veri fetch etme değişmiştir. `getServerSideProps`, `getStaticProps` ve `getInitialProps` daha basit bir API ile değiştirilmiştir.
- App dizini, rotaları tanımlamak için iç içe klasörler ve bir rota segmentini genel erişime açmak için özel bir `page.js` dosyası kullanır.
- | `pages` Directory | `app` Directory       | Route          |
  | ----------------- | --------------------- | -------------- |
  | `index.js`        | `page.js`             | `/`            |
  | `about.js`        | `about/page.js`       | `/about`       |
  | `blog/[slug].js`  | `blog/[slug]/page.js` | `/blog/post-1` |

Bir sayfanın taşınmasını iki ana adıma ayırmanızı öneririz:

- Adım 1: Varsayılan dışa aktarılmış Sayfa Bileşenini yeni bir İstemci Bileşenine taşıyın.
- Adım 2: Yeni İstemci Bileşenini uygulama dizini içindeki yeni bir `page.js` dosyasına aktarın.

**Bilmekte fayda var:** Bu en kolay geçiş yoludur çünkü pages dizinine en benzer davranışa sahiptir.

#### Adım 1: Yeni bir İstemci Bileşeni Oluşturun

Uygulama dizini içinde (örn. `app/home-page.tsx` veya benzeri) bir İstemci Bileşeni dışa aktaran yeni bir ayrı dosya oluşturun. İstemci Bileşenlerini tanımlamak için dosyanın en üstüne (tüm içe aktarmalardan önce) 'use client' yönergesini ekleyin.

Varsayılan dışa aktarılan sayfa bileşenini `pages/index.js` dosyasından `app/home-page.tsx` dosyasına taşıyın.

```tsx
// app/home-page.tsx
"use client";

// Bu bir İstemci Bileşenidir. Verileri prop olarak alır ve
// tıpkı Sayfa bileşenleri gibi durum ve efektlere erişimi vardır
// `pages` dizininde.
export default function HomePage({ recentPosts }) {
  return (
    <div>
      {recentPosts.map((post) => (
        <div key={post.id}>{post.title}</div>
      ))}
    </div>
  );
}
```

#### Adım 2: Yeni bir sayfa oluşturun

- Uygulama dizini içinde yeni bir `app/page.tsx` dosyası oluşturun. Bu varsayılan olarak bir Sunucu Bileşenidir.

- `Home-page.tsx` İstemci Bileşenini sayfaya aktarın.

- `pages/index.js` içinden veri getiriyorsanız, yeni veri getirme API'lerini kullanarak veri getirme mantığını doğrudan Sunucu Bileşenine taşıyın.

```tsx
// app/page.tsx
// İstemci Bileşeninizi İçe Aktarın
import HomePage from "./home-page";

async function getPosts() {
  const res = await fetch("https://...");
  const posts = await res.json();
  return posts;
}

export default async function Page() {
  // Verileri doğrudan bir Sunucu Bileşeninde getirme
  const recentPosts = await getPosts();
  // Getirilen verileri İstemci Bileşeninize iletme
  return <HomePage recentPosts={recentPosts} />;
}
```

- Önceki sayfanız `useRouter` kullandıysa, yeni yönlendirme kancalarına güncellemeniz gerekir.

- Geliştirme sunucunuzu başlatın ve `http://localhost:3000` adresini ziyaret edin. Artık uygulama dizini üzerinden sunulan mevcut dizin rotanızı görmelisiniz.

### Adım 5: Yönlendirme hooklarının Taşınması

Uygulama dizinindeki yeni davranışları desteklemek için yeni bir yönlendirici eklendi.

- Uygulama dizininde, `next/navigation`'dan içe aktarılan üç yeni hook kullanılmalıdır: `useRouter()`, `usePathname()`, ve `useSearchParams()`.

- Yeni `useRouter` hook `next/navigation`'dan içe aktarılmıştır ve `pages` dizininde `next/router`'dan içe aktarılan `useRouter` hook ile farklı davranış gösterir.
- `next/router`'dan içe aktarılan `useRouter` hook uygulama dizininde desteklenmez ancak `pages` dizininde kullanılmaya devam edilebilir.
- Yeni `useRouter`, `pathname` dizgisini döndürmez. Bunun yerine ayrı `usePathname` hook'unu kullanın.
- Yeni `useRouter`, `query` nesnesini döndürmez. Bunun yerine ayrı `useSearchParams` hook'unu kullanın.
- Sayfa değişikliklerini dinlemek için `useSearchParams` ve `usePathname`'ı birlikte kullanabilirsiniz.
- Bu yeni hooklar yalnızca İstemci Bileşenlerinde desteklenir. Sunucu Bileşenlerinde kullanılamazlar.

```tsx
"use client";

import { useRouter, usePathname, useSearchParams } from "next/navigation";

export default function ExampleClientComponent() {
  const router = useRouter();
  const pathname = usePathname();
  const searchParams = useSearchParams();

  // ...
}
```

Ek olarak, yeni `useRouter` hook'u aşağıdaki değişikliklere uğramıştır:

- `isFallback` kaldırılmıştır çünkü `fallback` yerine konulmuştur.
- `locale`, `locales`, `defaultLocales`, `domainLocales` değerleri kaldırılmıştır çünkü uygulama dizininde yerleşik i18n Next.js özellikleri artık gerekli değildir. i18n hakkında daha fazla bilgi edinin.
- `basePath` kaldırılmıştır. Alternatif, `useRouter`'ın bir parçası olmayacak. Henüz uygulanmamıştır.
- `asPath` kaldırılmıştır çünkü `as` kavramı yeni yönlendiriciden kaldırılmıştır.
- `isReady` kaldırılmıştır çünkü artık gerekli değildir. Statik renderlama sırasında, `useSearchParams()` kanca kullanan herhangi bir bileşen, ön işleme adımını atlayacak ve bunun yerine çalışma zamanında istemcide render edilecektir.

### Adım 6: Veri Getirme Yöntemlerini Taşıma

//Translation of this page is not completed and not merged yet.