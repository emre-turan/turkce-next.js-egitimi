# Metadata

Next.js, gelişmiş SEO ve web paylaşılabilirliği için uygulama meta verilerinizi (örneğin HTML head öğenizin içindeki `meta` ve `link` etiketleri) tanımlamak için kullanılabilecek bir Meta Veri API'sine sahiptir.

Uygulamanıza meta veri eklemenin iki yolu vardır:

- **Yapılandırma Tabanlı Meta Veriler:** Statik bir `meta` veri nesnesini veya dinamik bir `generateMetadata` işlevini bir `layout.js` veya `page.js` dosyasına aktarın
- **Dosya Tabanlı Meta Veriler:** Rota segmentlerine statik veya dinamik olarak oluşturulan özel dosyalar ekleyin.

Bu iki seçenekle de Next.js sayfalarınız için ilgili `<head>` öğelerini otomatik olarak oluşturacaktır. `ImageResponse` yapıcısını kullanarak dinamik OG görüntüleri de oluşturabilirsiniz

## Statik Meta Veriler

Statik meta verileri tanımlamak için bir `layout.js` veya static `page.js` dosyasından bir Meta Veri nesnesini dışa aktarın.

```js
// layout.tsx / page.tsx

import { Metadata } from "next";

export const metadata: Metadata = {
  title: "...",
  description: "...",
};

export default function Page() {}
```

## Dinamik Meta Veriler

Dinamik değerler gerektiren meta verileri `fetch` etmek için `generateMetadata` işlevini kullanabilirsiniz.

```js
// app/products/[id]/page.tsx

import { Metadata, ResolvingMetadata } from 'next'

type Props = {
  params: { id: string }
  searchParams: { [key: string]: string | string[] | undefined }
}

export async function generateMetadata(
  { params, searchParams }: Props,
  parent?: ResolvingMetadata
): Promise<Metadata> {
  // read route params
  const id = params.id

  // fetch data
  const product = await fetch(`https://.../${id}`).then((res) => res.json())

  // isteğe bağlı olarak ana meta verilere erişim ve genişletme (değiştirmek yerine)
  const previousImages = (await parent).openGraph?.images || []

  return {
    title: product.title,
    openGraph: {
      images: ['/some-specific-page-image.jpg', ...previousImages],
    },
  }
}

export default function Page({ params, searchParams }: Props) {}
```

**Bilmekte fayda var:**

- `generateMetadata` aracılığıyla hem statik hem de dinamik meta veriler yalnızca Sunucu Bileşenlerinde desteklenir.
- Next.js, bir rota render ederken `generateMetadata`, `generateStaticParam`, Layouts, Pages ve Sunucu Bileşenlerinde aynı veriler için getirme isteklerini otomatik olarak tekilleştirir. `fetch` kullanılamıyorsa React `cache` kullanılabilir
- Next.js, istemciye UI akışı yapmadan önce `generateMetadata` içindeki veri getirme işleminin tamamlanmasını bekler. Bu, akışlı bir yanıtın ilk bölümünün `<head>` etiketlerini içermesini garanti eder.

## Dosya tabanlı meta veriler

Bu özel dosyalar meta veriler için kullanılabilir:

- favicon.ico, apple-icon.jpg ve icon.jpg
- opengraph-image.jpg ve twitter-image.jpg
- robots.txt
- sitemap.xml

Bunları statik meta veriler için kullanabilir veya bu dosyaları kodla programlı olarak oluşturabilirsiniz.

## Davranış

Dosya tabanlı meta veriler daha yüksek önceliğe sahiptir ve yapılandırma tabanlı meta verileri geçersiz kılar.

### Varsayılan Alanlar

Bir rota meta veri tanımlamasa bile her zaman eklenen iki varsayılan `meta` etiket vardır:

- [Meta charset etiketi](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#attr-charset) web sitesi için karakter kodlamasını ayarlar.
- [Meta viewport etiketi](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag), web sitesinin farklı cihazlara göre ayarlanması için görüntü alanı genişliğini ve ölçeğini ayarlar.

```bash
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

**Bilmekte fayda var:** Varsayılan `viewport` meta etiketinin üzerine yazabilirsiniz.

### Sıralama (Ordering)

Meta veriler, kök segmentten başlayarak son page.js segmentine en yakın segmente kadar sırayla değerlendirilir. Örneğin:

1. `app/layout.tsx` (Kök Düzen)
2. `app/blog/layout.tsx` (İç İçe Blog Düzeni)
3. `app/blog/[slug]/page.tsx` (Blog Sayfası)

### Birleştirme

Değerlendirme sırasını takiben, aynı rotadaki birden fazla segmentten dışa aktarılan Meta Veri nesneleri, bir rotanın nihai meta veri çıktısını oluşturmak için yüzeysel olarak birleştirilir. Yinelenen anahtarlar sıralamalarına göre değiştirilir.

Bu, daha önceki bir segmentte tanımlanan `openGraph` ve `robotlar` gibi iç içe geçmiş alanlara sahip meta verilerin, bunları tanımlayan son segment tarafından üzerine yazıldığı anlamına gelir.

#### Alanların üzerine yazma (Overwriting Fields)

```js
// app/layout.js
export const metadata = {
  title: "Acme",
  openGraph: {
    title: "Acme",
    description: "Acme is a...",
  },
};
```

```js
// app/blog/page.js
export const metadata = {
  title: "Blog",
  openGraph: {
    title: "Blog",
  },
};

// Output:
// <title>Blog</title>
// <meta property="og:title" content="Blog" />
```

Yukarıdaki örnekte:

- `app/layout.js` dosyasındaki `title`, `app/blog/page.js` dosyasındaki title ile değiştirilir.
- `app/layout.js`'deki tüm `openGraph` alanları `app/blog/page.js`'de değiştirilir çünkü `app/blog/page.js` `openGraph` meta verilerini ayarlar. `openGraph.description`'ın olmadığına dikkat edin.

Bazı iç içe geçmiş alanları segmentler arasında paylaşırken diğerlerinin üzerine yazmak isterseniz, bunları ayrı bir değişkene çekebilirsiniz:

```js
// app/shared-metadata.js
export const openGraphImage = { images: ["http://..."] };
```

```js
// app/page.js

import { openGraphImage } from "./shared-metadata";

export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: "Home",
  },
};
```

```js
import { openGraphImage } from "../shared-metadata";

export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: "About",
  },
};
```

Yukarıdaki örnekte, OG görüntüsü `app/layout.js` ve `app/about/page.js` arasında paylaşılırken başlıklar farklıdır.

#### Devralınan alanlar (Inheriting fields)

```js
// app/layout.js

export const metadata = {
  title: "Acme",
  openGraph: {
    title: "Acme",
    description: "Acme is a...",
  },
};
```

```js
// app/about/page.js

export const metadata = {
  title: "About",
};

// Output:
// <title>About</title>
// <meta property="og:title" content="Acme" />
// <meta property="og:description" content="Acme is a..." />
```

**Notlar:**

- `app/layout.js`'deki `title`, `app/about/page.js`'deki `title` ile değiştirilir.
- `app/about/page.js` `openGraph` meta verilerini ayarlamadığı için `app/layout.js`'deki tüm `openGraph` alanları `app/about/page.js`'de miras alınır.

## Dinamik Görüntü Oluşturma (Dynamic Image Generation)

`ImageResponse` yapıcısı, JSX ve CSS kullanarak dinamik görüntüler oluşturmanıza olanak tanır. Bu, Open Graph görüntüleri, Twitter kartları ve daha fazlası gibi sosyal medya görüntüleri oluşturmak için kullanışlıdır.

`ImageResponse`, Edge Runtime'ı kullanır ve Next.js, edge'de önbelleğe alınan görüntülere doğru başlıkları otomatik olarak ekleyerek performansı artırmaya ve yeniden hesaplamayı azaltmaya yardımcı olur.

`ImageResponse`'u kullanmak için `next/server`'dan içe aktarabilirsiniz:

```js
// app/about/route.js

import { ImageResponse } from "next/server";

export const runtime = "edge";

export async function GET() {
  return new ImageResponse(
    (
      <div
        style={{
          fontSize: 128,
          background: "white",
          width: "100%",
          height: "100%",
          display: "flex",
          textAlign: "center",
          alignItems: "center",
          justifyContent: "center",
        }}
      >
        Hello world!
      </div>
    ),
    {
      width: 1200,
      height: 600,
    }
  );
}
```

`ImageResponse`, Rota İşleyicileri ve dosya tabanlı Meta Veriler dahil olmak üzere diğer Next.js API'leri ile iyi bir şekilde entegre olur. Örneğin, derleme zamanında veya istek zamanında dinamik olarak Open Graph görüntüleri oluşturmak için `ImageResponse`'u bir `opengraph-image.tsx` dosyasında kullanabilirsiniz.

`ImageResponse`, flexbox ve mutlak konumlandırma, özel yazı tipleri, metin kaydırma, merkezleme ve iç içe görüntüler gibi yaygın CSS özelliklerini destekler.

**Bilmekte fayda var:**

- Örnekler [Vercel OG Playground](https://og-playground.vercel.app/)'da mevcuttur.
- `ImageResponse`, HTML ve CSS'yi PNG'ye dönüştürmek için [@vercel/og](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation), [Satori](https://github.com/vercel/satori) ve Resvg kullanır
- Yalnızca Edge Çalışma Zamanı desteklenir. Varsayılan Node.js çalışma zamanı çalışmayacaktır.
- Yalnızca flexbox ve CSS özelliklerinin bir alt kümesi desteklenir. Gelişmiş düzenler (örn. `display: grid`) çalışmayacaktır.
- Maksimum paket boyutu `500KB`. Paket boyutu JSX, CSS, yazı tipleri, resimler ve diğer tüm varlıkları içerir. Sınırı aşarsanız, varlıkların boyutunu küçültmeyi veya çalışma zamanında getirmeyi düşünün.
- Yalnızca `ttf`, `otf` ve `woff` yazı tipi biçimleri desteklenir. Font ayrıştırma hızını en üst düzeye çıkarmak için `woff` yerine `ttf` veya `otf` tercih edilir.

## JSON-LD

[JSON-LD](https://json-ld.org/), içeriğinizi anlamak için arama motorları tarafından kullanılabilen yapılandırılmış veriler için bir formattır. Örneğin, bir kişiyi, bir olayı, bir organizasyonu, bir filmi, bir kitabı, bir tarifi ve diğer birçok varlık türünü tanımlamak için kullanabilirsiniz.

JSON-LD için şu anki önerimiz, yapılandırılmış verileri `layout.js` veya `page.js` bileşenlerinizde bir `<script>` etiketi olarak işlemektir.

Örneğin:

```js
// app/products/[id]/page.tsx

export default async function Page({ params }) {
  const product = await getProduct(params.id);

  const jsonLd = {
    "@context": "https://schema.org",
    "@type": "Product",
    name: product.name,
    image: product.image,
    description: product.description,
  };

  return (
    <section>
      {/_ Add JSON-LD to your page _/}
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      {/_ ... _/}
    </section>
  );
}
```

Yapılandırılmış verilerinizi Google için [Zengin Sonuçlar Testi](https://search.google.com/test/rich-results) veya [genel Şema İşaretleme Doğrulayıcısı](https://validator.schema.org/) ile doğrulayabilir ve test edebilirsiniz.

JSON-LD'nizi, [schema-dts](https://www.npmjs.com/package/schema-dts) gibi topluluk paketlerini kullanarak TypeScript ile yazabilirsiniz:

```js
import { Product, WithContext } from "schema-dts";

const jsonLd: WithContext<Product> = {
  "@context": "https://schema.org",
  "@type": "Product",
  name: "Next.js Sticker",
  image: "https://nextjs.org/imgs/sticker.png",
  description: "Dynamic at the speed of static.",
};
```
