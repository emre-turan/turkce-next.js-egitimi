# CSS-in-JS

**Uyarı:** Çalışma zamanı JavaScript gerektiren CSS-in-JS kütüphaneleri şu anda Sunucu Bileşenleri'nde desteklenmemektedir. CSS-in-JS'yi Sunucu Bileşenleri ve Akış gibi daha yeni React özellikleriyle kullanmak, kütüphane yazarlarının [eşzamanlı render etme](https://react.dev/blog/2022/03/29/react-v18#what-is-concurrent-react) dahil olmak üzere React'in en son sürümünü desteklemesini gerektirir.

React Sunucu Bileşenleri ve akış mimarisi desteğiyle CSS ve JavaScript varlıklarını işlemek için yukarı akış API'leri üzerinde React ekibiyle birlikte çalışıyoruz.

Aşağıdaki kütüphaneler `app` dizinindeki İstemci Bileşenlerinde desteklenmektedir (alfabetik olarak):

- [`kuma-ui`](https://kuma-ui.com/)
- [`@mui/material`](https://mui.com/material-ui/guides/next-js-app-router/)
- [`pandacss`](https://panda-css.com/)
- [`styled-jsx`](https://nextjs.org/docs/app/building-your-application/styling/css-in-js#styled-jsx)
- [`styled-components`](https://nextjs.org/docs/app/building-your-application/styling/css-in-js#styled-components)
- [`style9`](https://github.com/johanholmerin/style9)
- [`tamagui`](https://tamagui.dev/docs/guides/next-js#server-components)
- [`vanilya-extract`](https://github.com/vercel/next.js/tree/canary/examples/with-vanilla-extract)

Aşağıdakiler şu anda destek üzerinde çalışmaktadır:

- [`emotion`](https://github.com/emotion-js/emotion/issues/2928)

**Bilmekte fayda var:** Farklı CSS-in-JS kütüphanelerini test ediyoruz ve React 18 özelliklerini ve/veya `app` dizinini destekleyen kütüphaneler için daha fazla örnek ekleyeceğiz.

## Uygulamada CSS-in-JS'yi yapılandırma (Configuring CSS-in-JS in `app`)

CSS-in-JS'nin yapılandırılması üç adımlı bir katılım sürecidir:

- Bir render etme'deki tüm CSS kurallarını toplamak için bir stil kayıt defteri.
- Kuralları, onları kullanabilecek herhangi bir içerikten önce enjekte etmek için yeni `useServerInsertedHTML` kancası.
- İlk sunucu tarafı oluşturma sırasında uygulamanızı stil kayıt defteri ile saran bir İstemci Bileşeni.

### styled-jsx

İstemci Bileşenlerinde `styled-jsx` kullanmak için `v5.1.0` kullanılması gerekir. İlk olarak, yeni bir kayıt defteri oluşturun:

```js
app / registry.tsx;

("use client");

import React, { useState } from "react";
import { useServerInsertedHTML } from "next/navigation";
import { StyleRegistry, createStyleRegistry } from "styled-jsx";

export default function StyledJsxRegistry({
  children,
}: {
  children: React.ReactNode,
}) {
  // Only create stylesheet once with lazy initial state
  // x-ref: https://reactjs.org/docs/hooks-reference.html#lazy-initial-state
  const [jsxStyleRegistry] = useState(() => createStyleRegistry());

  useServerInsertedHTML(() => {
    const styles = jsxStyleRegistry.styles();
    jsxStyleRegistry.flush();
    return <>{styles}</>;
  });

  return <StyleRegistry registry={jsxStyleRegistry}>{children}</StyleRegistry>;
}
```

Ardından, kök düzeninizi kayıt defteri ile sarın:

```js
app / layout.tsx;

import StyledJsxRegistry from "./registry";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html>
      <body>
        <StyledJsxRegistry>{children}</StyledJsxRegistry>
      </body>
    </html>
  );
}
```

### Styled Components

Aşağıda `styled-components@v6.0.0-rc.1` veya daha büyük bir adresin nasıl yapılandırılacağına dair bir örnek verilmiştir:

İlk olarak, `styled-components` API'sini kullanarak render etme sırasında oluşturulan tüm CSS stil kurallarını toplayacak global bir kayıt bileşeni ve bu kuralları döndürecek bir fonksiyon oluşturun. Ardından, kayıt defterinde toplanan stilleri kök mizanpajdaki `<head>` HTML etiketine enjekte etmek için `useServerInsertedHTML` kancasını kullanın.

```js
lib / registry.tsx;

("use client");

import React, { useState } from "react";
import { useServerInsertedHTML } from "next/navigation";
import { ServerStyleSheet, StyleSheetManager } from "styled-components";

export default function StyledComponentsRegistry({
  children,
}: {
  children: React.ReactNode,
}) {
  // Only create stylesheet once with lazy initial state
  // x-ref: https://reactjs.org/docs/hooks-reference.html#lazy-initial-state
  const [styledComponentsStyleSheet] = useState(() => new ServerStyleSheet());

  useServerInsertedHTML(() => {
    const styles = styledComponentsStyleSheet.getStyleElement();
    styledComponentsStyleSheet.instance.clearTag();
    return <>{styles}</>;
  });

  if (typeof window !== "undefined") return <>{children}</>;

  return (
    <StyleSheetManager sheet={styledComponentsStyleSheet.instance}>
      {children}
    </StyleSheetManager>
  );
}
```

Kök düzenin `children` öğelerini stil kayıt defteri bileşeniyle sarın:

```js
app / layout.tsx;

import StyledComponentsRegistry from "./lib/registry";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html>
      <body>
        <StyledComponentsRegistry>{children}</StyledComponentsRegistry>
      </body>
    </html>
  );
}
```

**Bilmekte fayda var:**

- Sunucu render etme sırasında, stiller global bir kayıt defterine çıkarılır ve HTML'nizin `<head>` bölümüne aktarılır. Bu, stil kurallarının onları kullanabilecek tüm içeriklerden önce yerleştirilmesini sağlar. Gelecekte, stilleri nereye enjekte edeceğimizi belirlemek için yakında çıkacak bir React özelliğini kullanabiliriz.
- Akış sırasında, her bir yığından gelen stiller toplanacak ve mevcut stillere eklenecektir. İstemci tarafı hidrasyon tamamlandıktan sonra, `styled-components` her zamanki gibi devralacak ve başka dinamik stiller enjekte edecektir.
- Stil kaydı için özellikle ağacın en üst seviyesinde bir İstemci Bileşeni kullanıyoruz çünkü CSS kurallarını bu şekilde çıkarmak daha verimli. Bu, sonraki sunucu render etme'lerinde stillerin yeniden oluşturulmasını ve Sunucu Bileşeni yükünde gönderilmesini önler.
