#Codemods

Codemod'lar kod tabanınızda programlı olarak çalışan dönüşümlerdir. Bu, her dosyayı manuel olarak gözden geçirmek zorunda kalmadan çok sayıda değişikliğin programlı olarak uygulanmasına olanak tanır.

Next.js, bir API güncellendiğinde veya kullanımdan kaldırıldığında Next.js kod tabanınızı yükseltmenize yardımcı olmak için Codemod dönüşümleri sağlar.

## Kullanım

Terminalinizde, projenizin klasörüne gidin (`cd`) ve ardından çalıştırın:

```bash
npx @next/codemod <transform> <path>
```

`<transform>` ve `<path>` öğelerinin uygun değerlerle değiştirilmesi.

- `transform` - dönüşümün adı
- `path` - dönüştürülecek dosyalar veya dizin
- `--dry` Kuru çalıştırma yapın, hiçbir kod düzenlenmeyecektir
- `--print` Karşılaştırma için değiştirilen çıktıyı yazdırır

## Next.js Codemods

## 13.2

### Yerleşik Yazı Tipini Kullanın

#### `built-in-next-font`

```bash
npx @next/codemod@latest built-in-next-font .
```

Bu codemod `@next/font` paketini kaldırır ve `@next/font` içe aktarımlarını yerleşik `next/font`'a dönüştürür.

Örneğin:

```bash
import { Inter } from '@next/font/google'
```

Aşağıdakine dönüşür:

```bash
import { Inter } from 'next/font/google'
```

## 13.0

### Next Görüntü Aktarımlarını Yeniden Adlandır

#### `next-image-to-legacy-image`

```bash
npx @next/codemod@latest next-image-to-legacy-image .
```

Mevcut Next.js 10, 11 veya 12 uygulamalarındaki `next/image` içe aktarımlarını Next.js 13'te `next/legacy/image` olarak güvenli bir şekilde yeniden adlandırır. Ayrıca `next/future/image` öğesini `next/image` olarak yeniden adlandırır.

Örneğin:

```js
/// pages/index.js

import Image1 from "next/image";
import Image2 from "next/future/image";

export default function Home() {
  return (
    <div>
      <Image1 src="/test.jpg" width="200" height="300" />
      <Image2 src="/test.png" width="500" height="400" />
    </div>
  );
}
```

Aşağıdakine dönüşür:

```js
/// pages/index.js

// 'next/image', 'next/legacy/image' olur
import Image1 from "next/legacy/image";
// 'next/future/image', 'next/image' olur
import Image2 from "next/image";

export default function Home() {
  return (
    <div>
      <Image1 src="/test.jpg" width="200" height="300" />
      <Image2 src="/test.png" width="500" height="400" />
    </div>
  );
}
```

### Yeni Görüntü Bileşenine Geçiş Yapın

#### `next-image-experimental`

```bash
npx @next/codemod@latest next-image-experimental .
```

Dangerously, satır içi stiller ekleyerek ve kullanılmayan sahne öğelerini kaldırarak `next/legacy/image` öğesinden yeni `next/image` öğesine geçiş yapar.

- `layout` prop'unu kaldırır ve `style` ekler.
- `objectFit` prop'unu kaldırır ve `style` ekler.
- `objectPosition` prop'unu kaldırır ve `style` ekler.
- `lazyBoundary` prop'unu kaldırır.
- `lazyRoot` prop'unu kaldırır.

### Link Bileşenlerinden `<a>` Etiketlerini Kaldırma

#### `new-link`

```bash
npx @next/codemod@latest new-link .
```

Link Bileşenleri içindeki `<a>` etiketlerini kaldırın veya otomatik olarak düzeltilemeyen Bağlantılara bir `legacyBehavior` prop ekleyin.

Örneğin:

```js
<Link href="/about">
  <a>About</a>
</Link>
// buna dönüşür
<Link href="/about">
  About
</Link>

<Link href="/about">
  <a onClick={() => console.log('clicked')}>About</a>
</Link>
// buna dönüşür
<Link href="/about" onClick={() => console.log('clicked')}>
  About
</Link>
```

Otomatik düzeltmenin uygulanamadığı durumlarda, `legacyBehavior` özelliği eklenir. Bu, uygulamanızın söz konusu bağlantı için eski davranışı kullanarak çalışmaya devam etmesini sağlar.

```js
const Component = () => <a>About</a>

<Link href="/about">
  <Component />
</Link>
// aşağıdakine dönüşür
<Link href="/about" legacyBehavior>
  <Component />
</Link>
```

## 11

### CRA'dan geçiş yapın

#### `cra-to-next`

```bash
npx @next/codemod cra-to-next
```

Bir Create React App projesini Next.js'ye geçirir; bir Pages Router ve davranışla eşleşmesi için gerekli yapılandırmayı oluşturur. SSR sırasında `window` kullanımı nedeniyle uyumluluğun bozulmasını önlemek için başlangıçta yalnızca istemci tarafı oluşturmadan yararlanılır ve Next.js'ye özgü özelliklerin kademeli olarak benimsenmesine izin vermek için sorunsuz bir şekilde etkinleştirilebilir.

Lütfen bu dönüşümle ilgili geri bildirimlerinizi [bu tartışmada](https://github.com/vercel/next.js/discussions/25858) paylaşın.

## 10

### Add React imports

#### `add-missing-react-import`

```bash
npx @next/codemod add-missing-react-import
```

`React`'i içe aktarmayan dosyaları, yeni [React JSX dönüşümünün](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) çalışması için içe aktarmayı içerecek şekilde dönüştürür.

Örneğin:

```js
export default class Home extends React.Component {
  render() {
    return <div>Hello World</div>;
  }
}
```

Aşağıdakine dönüşür:

```js
import React from "react";
export default class Home extends React.Component {
  render() {
    return <div>Hello World</div>;
  }
}
```

## 9

### Anonim Bileşenleri Adlandırılmış Bileşenlere Dönüştürme

#### `name-default-component`

```bash
npx @next/codemod name-default-component
```

### 9 ve üzeri sürümler.

[Fast Refresh](https://nextjs.org/blog/next-9-4#fast-refresh) ile çalıştıklarından emin olmak için anonim bileşenleri adlandırılmış bileşenlere dönüştürür.

Örneğin:

```js
export default function () {
  return <div>Hello World</div>;
}
```

Aşağıdakine dönüşür:

```js
export default function MyComponent() {
  return <div>Hello World</div>;
}
```

Bileşen, dosyanın adına göre camel-cased bir ada sahip olur ve arrow fonksiyonlarıyla da çalışır.

## 8

### AMP HOC'yi sayfa yapılandırmasına dönüştürme

#### `withamp-to-config`

```bash
npx @next/codemod withamp-to-config
```

`withAmp` HOC'yi Next.js 9 sayfa yapılandırmasına dönüştürür.

Örneğin:

```js
// Öncesi
import { withAmp } from "next/amp";

function Home() {
  return <h1>My AMP Page</h1>;
}

export default withAmp(Home);
```

```js
// Sonrası
export default function Home() {
  return <h1>My AMP Page</h1>;
}

export const config = {
  amp: true,
};
```

## 6

### `withrouter` kullanın

#### `url-to-withrouter`

```bash
npx @next/codemod url-to-withrouter
```

Üst düzey sayfalarda kullanımdan kaldırılan otomatik olarak enjekte edilen `url` özelliğini `withRouter` ve enjekte ettiği `router` özelliğini kullanmaya dönüştürür. Daha fazlasını buradan okuyun: https://nextjs.org/docs/messages/url-deprecated

Örneğin:

```js
// Öncesi

import React from "react";
export default class extends React.Component {
  render() {
    const { pathname } = this.props.url;
    return <div>Current pathname: {pathname}</div>;
  }
}
```

```js
// Sonrası

import React from "react";
import { withRouter } from "next/router";
export default withRouter(
  class extends React.Component {
    render() {
      const { pathname } = this.props.router;
      return <div>Current pathname: {pathname}</div>;
    }
  }
);
```

Bu bir vakadır. Dönüştürülen (ve test edilen) tüm vakalar [**testfixtures** dizininde](https://github.com/vercel/next.js/tree/canary/packages/next-codemod/transforms/__testfixtures__/url-to-withrouter) bulunabilir.
