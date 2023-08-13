# MDX

[Markdown](https://daringfireball.net/projects/markdown/syntax), metni biçimlendirmek için kullanılan hafif bir biçimlendirme dilidir. Düz metin sözdizimi kullanarak yazmanıza ve yapısal olarak geçerli HTML'ye dönüştürmenize olanak tanır. Genellikle web sitelerinde ve bloglarda içerik yazmak için kullanılır.

Siz aşağıdakini yazdığınızda...

```md
I **love** using [Next.js](https://nextjs.org/)
```

Çıktı:

```md
<p> <a href="https://nextjs.org/">Next.js</a></p> kullanmayı <strong>seviyorum</strong>
```

[MDX](https://mdxjs.com/), [JSX](https://react.dev/learn/writing-markup-with-jsx)'i doğrudan markdown dosyalarınıza yazmanıza olanak tanıyan bir markdown üst kümesidir. Dinamik etkileşim eklemenin ve içeriğinize React bileşenleri yerleştirmenin güçlü bir yoludur.

Next.js, hem uygulamanızın içindeki yerel MDX içeriğini hem de sunucudan dinamik olarak getirilen uzak MDX dosyalarını destekleyebilir. Next.js eklentisi, Sunucu Bileşenlerinde (`app`'de varsayılan) kullanım desteği de dahil olmak üzere Markdown ve React bileşenlerini HTML'ye dönüştürmeyi yönetir.

## `@next/mdx`

`@next/mdx` paketi, projelerinizin kök dizinindeki `next.config.js` dosyasında yapılandırılır. Yerel dosyalardan veri alır ve doğrudan `/pages` veya `/app` dizininizde `.mdx` uzantılı sayfalar oluşturmanıza olanak tanır.

## Başlarken

`@next/mdx` paketini yükleyin:

```bash
npm install @next/mdx @mdx-js/loader @mdx-js/react @types/mdx
```

Uygulamanızın kök dizininde (`app/` veya `src/` klasörünün üst dizini) `mdx-components.tsx` dosyasını oluşturun:

```tsx
///mdx-components.tsx

import type { MDXComponents } from "mdx/types";

// Bu dosya, MDX dosyalarında kullanılmak üzere
// özel React bileşenleri sağlamanıza olanak tanır.
// Diğer kütüphanelerdeki bileşenler de dahil olmak üzere
// istediğiniz herhangi bir react bileşenini
// içe aktarabilir ve kullanabilirsiniz.

// Bu dosya MDX'i `app` dizininde kullanmak için gereklidir.
export function useMDXComponents(components: MDXComponents): MDXComponents {
  return {
    // Yerleşik bileşenlerin özelleştirilmesine, örneğin stil eklenmesine izin verir.
    // h1: ({ children }) => <h1 style={{ fontSize: "100px" }}>{children}</h1>,
    ...components,
  };
}
```

`next.config.js` dosyasını `mdxRs` kullanacak şekilde güncelleyin:

```js
///next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    mdxRs: true,
  },
};

const withMDX = require("@next/mdx")();
module.exports = withMDX(nextConfig);
```

`app` dizininize MDX içerikli yeni bir dosya ekleyin:

```mdx
// app/hello.mdx

Merhaba, Next.js!

MDX dosyalarındaki React bileşenlerini içe aktarabilir ve kullanabilirsiniz.
```

İçeriği görüntülemek için `MDX` dosyasını bir `pages` içine aktarın:

```tsx
// app/page.tsx

import HelloWorld from "./hello.mdx";

export default function Page() {
  return <HelloWorld />;
}
```

## Uzaktan MDX (Remote MDX)

Markdown veya MDX dosyalarınız uygulamanızın içinde yaşamıyorsa, bunları sunucudan dinamik olarak getirebilirsiniz. Bu, bir CMS'den veya başka bir veri kaynağından içerik almak için kullanışlıdır.

MDX içeriğini almak için iki popüler topluluk paketi vardır: [`next-mdx-remote`](https://github.com/hashicorp/next-mdx-remote#react-server-components-rsc--nextjs-app-directory-support) ve [`contentlayer`](https://www.contentlayer.dev/). Örneğin, aşağıdaki örnek `next-mdx-remote` kullanmaktadır:

**Bilmekte fayda var:** Lütfen dikkatli olun. MDX, JavaScript olarak derlenir ve sunucuda yürütülür. MDX içeriğini yalnızca güvenilir bir kaynaktan almalısınız, aksi takdirde bu durum uzaktan kod yürütülmesine (RCE) yol açabilir.

```ts
// app/page.tsx

import { MDXRemote } from "next-mdx-remote/rsc";

export default async function Home() {
  const res = await fetch("https://...");
  const markdown = await res.text();
  return <MDXRemote source={markdown} />;
}
```

## Düzenlemeler (Layouts)

MDX içeriği etrafında bir düzen paylaşmak için Uygulama Yönlendiricisi ile [yerleşik düzen desteği](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#layouts)ni kullanabilirsiniz.

## Remark ve Rehype Eklentileri

MDX içeriğini dönüştürmek için isteğe bağlı olarak `remark` ve `rehype` eklentileri sağlayabilirsiniz. Örneğin, GitHub Flavored Markdown'ı desteklemek için `remark-gfm` kullanabilirsiniz.

`remark` ve `rehype` ekosistemi yalnızca ESM olduğundan, yapılandırma dosyası olarak `next.config.mjs` dosyasını kullanmanız gerekir.

```js
//next.config.mjs

import remarkGfm from "remark-gfm";
import createMDX from "@next/mdx";

/** @type {import('next').NextConfig} */
const nextConfig = {};

const withMDX = createMDX({
  options: {
    extension: /\.mdx?$/,
    remarkPlugins: [remarkGfm],
    rehypePlugins: [],
    // Eğer `MDXProvider` kullanıyorsanız, aşağıdaki satırı kaldırın.
    // providerImportSource: "@mdx-js/react",
  },
});
export default withMDX(nextConfig);
```

## Frontmatter

Frontmatter, bir sayfa hakkındaki verileri depolamak için kullanılabilen YAML benzeri bir anahtar/değer eşleştirmesidir. Öntanımlı olarak `@next/mdx` frontmatter'ı desteklemez, ancak MDX içeriğinize frontmatter eklemek için [gray-matter](https://github.com/jonschlinkert/gray-matter) gibi birçok çözüm vardır.

Sayfa meta verilerine `@next/mdx` ile erişmek için `.mdx` dosyası içinden bir meta nesnesini dışa aktarabilirsiniz:

```mdx
export const meta = {
  author: 'Rich Haines',
}
 
# My MDX pag

e
```

## Özel Unsurlar

Markdown kullanmanın hoş yönlerinden biri, yerel `HTML` öğeleriyle eşleşerek yazmayı hızlı ve sezgisel hale getirmesidir:

```md
Bu markdown'da bir listedir:

- Bir
- İki
- Üç
```

Yukarıdaki işlem aşağıdaki `HTML`'yi oluşturur:

```html
<p>Bu markdown'da bir listedir:</p>

<ul>
  <li>Bir</li>
  <li>İki</li>
  <li>Üç</li>
</ul>
```

Web sitenize veya uygulamanıza özel bir his vermek için kendi öğelerinizi şekillendirmek istediğinizde, kısa kodları aktarabilirsiniz. Bunlar, `HTML` öğelerine eşlenen kendi özel bileşenlerinizdir. Bunu yapmak için `MDXProvider`'ı kullanır ve bir components nesnesini prop olarak geçirirsiniz. Components nesnesindeki her nesne anahtarı bir `HTML` öğesi adıyla eşleşir.

Etkinleştirmek için `next.config.js` içinde `providerImportSource: "@mdx-js/react"` belirtmeniz gerekir:

```js
//next.config.js

const withMDX = require("@next/mdx")({
  // ...
  options: {
    providerImportSource: "@mdx-js/react",
  },
});
```

Ardından sağlayıcıyı sayfanızda ayarlayın

```js
//pages/index.js

import { MDXProvider } from "@mdx-js/react";
import Image from "next/image";
import { Heading, InlineCode, Pre, Table, Text } from "my-components";

const ResponsiveImage = (props) => (
  <Görüntü
    alt={props.alt}
    sizes="100vw"
    style={{ width: "100%", height: "auto" }}
    {...props}
  />
);

const bileşenler = {
  img: ResponsiveImage,
  h1: Heading.H1,
  h2: Heading.H2,
  p: Metin,
  Öncesi: Öncesi,
  kod: InlineCode,
};

export default function Post(props) {
  dönüş(
    <MDXProvider components={components}>
      <main {...props} />
    </MDXProvider>
  );
}
```

Site genelinde kullanıyorsanız, sağlayıcıyı `_app.js`'ye eklemek isteyebilirsiniz, böylece tüm MDX sayfaları özel öğe yapılandırmasını alır.

## Derin Anlatım: Markdown'ı HTML'e nasıl dönüştürürsünüz?

React, Markdown'ı yerel olarak anlamaz. Markdown düz metninin önce HTML'ye dönüştürülmesi gerekir. Bu, `remark` ve `rehype` ile gerçekleştirilebilir.

`remark`, markdown etrafında bir araç ekosistemidir. `rehype` da aynıdır, ancak HTML içindir. Örneğin, aşağıdaki kod parçacığı markdown'u HTML'ye dönüştürür:

```js
import { unified } from "unified";
import remarkParse from "remark-parse";
import remarkRehype from "remark-rehype";
import rehypeSanitize from "rehype-sanitize";
import rehypeStringify from "rehype-stringify";

main();

async function main() {
  const file = await unified()
    .use(remarkParse) // Markdown AST'ye dönüştürme
    .use(remarkRehype) // HTML AST'ye Dönüştürme
    .use(rehypeSanitize) // HTML girdisini sterilize edin
    .use(rehypeStringify) // AST'yi serileştirilmiş HTML'ye dönüştürme
    .process("Hello, Next.js!");

  console.log(String(file)); // <p>Hello, Next.js!</p>
}
```

`remark` ve `rehype` ekosistemi, [sözdizimi vurgulama](https://github.com/atomiks/rehype-pretty-code), [başlıkları bağlama](https://github.com/rehypejs/rehype-autolink-headings), [içindekiler tablosu oluşturma](https://github.com/remarkjs/remark-toc) ve daha fazlası için eklentiler içerir.

Aşağıda gösterildiği gibi `@next/mdx` kullanırken, sizin için halledildiğinden doğrudan `remark` ve `rehype` kullanmanıza gerek yoktur.

## Rust tabanlı MDX derleyicisini kullanma (Deneysel)

Next.js, Rust dilinde yazılmış yeni bir MDX derleyicisini desteklemektedir. Bu derleyici hala deneyseldir ve üretim kullanımı için önerilmez. Yeni derleyiciyi kullanmak için `next.config.js` dosyasını `withMDX`'e aktarırken yapılandırmanız gerekir:

```js
// next.config.js
module.exports = withMDX({
  experimental: {
    mdxRs: true,
  },
});
```

## Yararlı Bağlantılar

- [MDX](https://mdxjs.com/)
- [`@next/mdx`](https://www.npmjs.com/package/@next/mdx)
- [remark](https://github.com/remarkjs/remark)
- [rehype](https://github.com/rehypejs/rehype)

