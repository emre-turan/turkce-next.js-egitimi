# Yazı Tipi Optimizasyonu (Font Optimization)

`next/font` yazı tiplerinizi (özel yazı tipleri dahil) otomatik olarak optimize edecek ve gelişmiş gizlilik ve performans için harici ağ isteklerini kaldıracaktır.

🎥 **İzleyin:** next/font'un nasıl kullanılacağı hakkında daha fazla bilgi edinin → [YouTube (6 dakika)](https://www.youtube.com/watch?v=L8_98i_bMMA).

`next/font`, herhangi bir yazı tipi dosyası için yerleşik otomatik kendi kendine barındırma içerir. Bu, kullanılan temel CSS `size-adjust` özelliği sayesinde web fontlarını sıfır düzen kayması ile en iyi şekilde yükleyebileceğiniz anlamına gelir.

Bu yeni yazı tipi sistemi, performans ve gizliliği göz önünde bulundurarak tüm Google Yazı Tiplerini rahatça kullanmanıza da olanak tanır. CSS ve yazı tipi dosyaları derleme sırasında indirilir ve statik varlıklarınızın geri kalanıyla birlikte kendi kendine barındırılır. Tarayıcı tarafından Google'a hiçbir istek gönderilmez.

## Google Yazı Tipleri (Google Fonts)

Herhangi bir Google Yazı Tipini otomatik olarak kendi kendine barındırın. Yazı tipleri dağıtıma dahil edilir ve dağıtımınızla aynı etki alanından sunulur. Tarayıcı tarafından Google'a hiçbir istek gönderilmez.

Kullanmak istediğiniz yazı tipini next/font/google'dan bir işlev olarak içe aktararak başlayın. En iyi performans ve esneklik için [değişken yazı tipleri](https://fonts.google.com/variablefonts) kullanmanızı öneririz.

```js
// app/layout.tsx

import { Inter } from "next/font/google";

// Değişken bir yazı tipi yükleniyorsa, yazı tipi ağırlığını belirtmeniz gerekmez
const inter = Inter({
  subsets: ["latin"],
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={inter.className}>
      <body>{children}</body>
    </html>
  );
}
```

Değişken bir yazı tipi kullanamıyorsanız, bir ağırlık belirtmeniz gerekecektir:

```js
// app/layout.tsx

import { Roboto } from "next/font/google";

const roboto = Roboto({
  weight: "400",
  subsets: ["latin"],
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={roboto.className}>
      <body>{children}</body>
    </html>
  );
}
```

Bir dizi kullanarak birden fazla ağırlık ve/veya stil belirtebilirsiniz:

```js
// app/layout.tsx

const roboto = Roboto({
  weight: ["400", "700"],
  style: ["normal", "italic"],
  subsets: ["latin"],
  display: "swap",
});
```

**Bilmekte fayda var:** Birden fazla kelime içeren font adları için alt çizgi (\_) kullanın. Örneğin `Roboto Mono`, `Roboto_Mono` olarak içe aktarılmalıdır.

### Bir alt küme belirtme (Specifying a subset)

Google Yazı Tipleri otomatik olarak [alt kümelendirilir](https://fonts.google.com/knowledge/glossary/subsetting). Bu, yazı tipi dosyasının boyutunu azaltır ve performansı artırır. Bu alt kümelerden hangilerini önceden yüklemek istediğinizi tanımlamanız gerekir. `preload` doğruyken herhangi bir alt küme belirtilmemesi bir uyarı ile sonuçlanacaktır.

Bu, fonksiyon çağrısına eklenerek yapılabilir:

```js
const inter = Inter({ subsets: ["latin"] }); // latin alt kümesi
```

### Birden Fazla Yazı Tipi Kullanma (Using Multiple Fonts)

Uygulamanızda birden fazla yazı tipini içe aktarabilir ve kullanabilirsiniz. Kullanabileceğiniz iki yaklaşım vardır.

İlk yaklaşım, bir yazı tipini dışa aktaran, içe aktaran ve gerektiğinde `className`'ini uygulayan bir yardımcı program işlevi oluşturmaktır. Bu, yazı tipinin yalnızca işlendiğinde önceden yüklenmesini sağlar:

```js
// app/fonts.ts
import { Inter, Roboto_Mono } from "next/font/google";

export const inter = Inter({
  subsets: ["latin"],
  display: "swap",
});

export const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  display: "swap",
});
```

```js
// app/layout.tsx

import { inter } from "./fonts";

export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.className}>
      <body>
        <div>{children}</div>
      </body>
    </html>
  );
}
```

```js
// app/page.tsx

import { roboto_mono } from "./fonts";

export default function Page() {
  return (
    <>
      <h1 className={roboto_mono.className}>My page</h1>
    </>
  );
}
```

Yukarıdaki örnekte, `Inter` global olarak uygulanacak ve `Roboto Mono` gerektiğinde içe aktarılıp uygulanabilecektir.

Alternatif olarak, bir CSS değişkeni oluşturabilir ve bunu tercih ettiğiniz CSS çözümüyle kullanabilirsiniz:

```js
// app/layout.tsx

import { Inter, Roboto_Mono } from "next/font/google";
import styles from "./global.css";

const inter = Inter({
  subsets: ["latin"],
  variable: "--font-inter",
  display: "swap",
});

const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  variable: "--font-roboto-mono",
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={`${inter.variable} ${roboto_mono.variable}`}>
      <body>
        <h1>My App</h1>
        <div>{children}</div>
      </body>
    </html>
  );
}
```

```css
/* app/global.css */
html {
  font-family: var(--font-inter);
}

h1 {
  font-family: var(--font-roboto-mono);
}
```

Yukarıdaki örnekte, `Inter` global olarak uygulanacak ve tüm `<h1>` etiketleri `Roboto Mono` ile şekillendirilecektir.

**Öneri:** Her yeni yazı tipi kullanıcının indirmesi gereken ek bi kaynak olduğundan, birden fazla yazı tipini ihtiyatlı bir şekilde kullanın.

## Yerel Yazı Tipleri (Local Fonts)

`next/font/local` öğesini içe aktarın ve yerel yazı tipi dosyanızın `src`'sini belirtin. En iyi performans ve esneklik için [değişken fontlar](https://fonts.google.com/variablefonts) kullanmanızı öneririz.

```js
import localFont from "next/font/local";

// Yazı tipi dosyaları `app` içine yerleştirilebilir
const myFont = localFont({
  src: "./my-font.woff2",
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={myFont.className}>
      <body>{children}</body>
    </html>
  );
}
```

Tek bir font ailesi için birden fazla dosya kullanmak istiyorsanız, `src` bir dizi olabilir:

```js
const roboto = localFont({
  src: [
    {
      path: "./Roboto-Regular.woff2",
      weight: "400",
      style: "normal",
    },
    {
      path: "./Roboto-Italic.woff2",
      weight: "400",
      style: "italic",
    },
    {
      path: "./Roboto-Bold.woff2",
      weight: "700",
      style: "normal",
    },
    {
      path: "./Roboto-BoldItalic.woff2",
      weight: "700",
      style: "italic",
    },
  ],
});
```

## Tailwind CSS ile

`next/font`, bir CSS değişkeni aracılığıyla Tailwind CSS ile kullanılabilir.

Aşağıdaki örnekte, `next/font/google`'dan Inter yazı tipini kullanıyoruz (Google veya Yerel Yazı Tiplerinden herhangi bir yazı tipini kullanabilirsiniz). CSS değişken adınızı tanımlamak için fontunuzu `variable` seçeneği ile yükleyin ve `inter`'e atayın. Ardından, CSS değişkenini HTML belgenize eklemek için `inter.variable` kullanın.

```js
// app/layout.tsx

import { Inter, Roboto_Mono } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
  display: "swap",
  variable: "--font-inter",
});

const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  display: "swap",
  variable: "--font-roboto-mono",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={`${inter.variable} ${roboto_mono.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

Son olarak, CSS değişkenini Tailwind CSS yapılandırmanıza ekleyin:

```js
// tailwind.config.js

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ["var(--font-inter)"],
        mono: ["var(--font-roboto-mono)"],
      },
    },
  },
  plugins: [],
};
```

Artık fontu öğelerinize uygulamak için `font-sans` ve `font-mono` yardımcı sınıflarını kullanabilirsiniz.

## Ön Yükleme

Sitenizin bir sayfasında bir yazı tipi işlevi çağrıldığında, bu işlev genel olarak kullanılamaz ve tüm rotalara önceden yüklenmez. Bunun yerine, yazı tipi yalnızca kullanıldığı dosya türüne bağlı olarak ilgili rotalara önceden yüklenir:

- Benzersiz bir sayfaysa, o sayfanın benzersiz rotasına önceden yüklenir.
- Bir düzen ise, düzen tarafından sarılan tüm rotalara önceden yüklenir.
- Kök düzen ise, tüm rotalara önceden yüklenir.

## Yazı tiplerini yeniden kullanma

`localFont` veya Google font işlevini her çağırdığınızda, bu font uygulamanızda bir örnek olarak barındırılır. Bu nedenle, aynı font işlevini birden fazla dosyaya yüklerseniz, aynı fontun birden fazla örneği barındırılır. Bu durumda aşağıdakileri yapmanız önerilir:

- Yazı tipi yükleyici işlevini tek bir paylaşılan dosyada çağırın
- Sabit olarak dışa aktarın
- Bu yazı tipini kullanmak istediğiniz her dosyadaki sabiti içe aktarın
