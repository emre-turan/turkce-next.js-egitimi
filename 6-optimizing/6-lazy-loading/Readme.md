# Tembel Yükleme (Lazy Loading)

Next.js'deki [tembel yükleme](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading), bir rotayı oluşturmak için gereken JavaScript miktarını azaltarak bir uygulamanın ilk yükleme performansını artırmaya yardımcı olur.

İstemci Bileşenlerinin ve içe aktarılan kitaplıkların yüklenmesini ertelemenize ve bunları yalnızca gerektiğinde istemci paketine dahil etmenize olanak tanır. Örneğin, bir kullanıcı açmak için tıklayana kadar bir modalin yüklenmesini ertelemek isteyebilirsiniz.

Next.js'de tembel yüklemeyi uygulayabileceğiniz iki yol vardır:

1. `next/dynamic` ile Dinamik İçe Aktarımları Kullanma
2. [Suspense](https://react.dev/reference/react/Suspense) ile [`React.lazy()`](https://react.dev/reference/react/lazy) Kullanımı

Varsayılan olarak, Sunucu Bileşenleri otomatik olarak [code split](https://developer.mozilla.org/en-US/docs/Glossary/Code_splitting) edebilir ve kullanıcı arayüzü parçalarını sunucudan istemciye aşamalı olarak göndermek için akışı kullanabilirsiniz. Tembel yükleme İstemci Bileşenleri için geçerlidir.

## `next/dynamic`

`next/dynamic`, [`React.lazy()`](https://react.dev/reference/react/lazy) ve [Suspense](https://react.dev/reference/react/Suspense)'in bir bileşimidir. Artımlı geçişe izin vermek için `app` ve `pages` dizinlerinde aynı şekilde davranır.

## Örnekler

### İstemci Bileşenlerini İçe Aktarma (Importing Client Components)

```js
// app/page.js

"use client";

import { useState } from "react";
import dynamic from "next/dynamic";

// Client Components:
const ComponentA = dynamic(() => import("../components/A"));
const ComponentB = dynamic(() => import("../components/B"));
const ComponentC = dynamic(() => import("../components/C"), { ssr: false });

export default function ClientComponentExample() {
  const [showMore, setShowMore] = useState(false);

  return (
    <div>
      {/* Hemen yükleyin, ancak ayrı bir istemci paketinde */}
      <ComponentA />

      {/* Talep üzerine yükleyin, yalnızca koşul karşılandığında/karşılanırsa */}
      {showMore && <ComponentB />}
      <button onClick={() => setShowMore(!showMore)}>Toggle</button>

      {/* Yalnızca istemci tarafına yükleyin */}
      <ComponentC />
    </div>
  );
}
```

### SSR'yi Atlama (Skipping SSR)

`React.lazy()` ve [Suspense](https://react.dev/reference/react/Suspense) kullanıldığında, İstemci Bileşenleri varsayılan olarak önceden render edilecektir (SSR).

Bir İstemci Bileşeni için ön render etmeyi devre dışı bırakmak istiyorsanız, ssr seçeneğini false olarak ayarlayabilirsiniz:

```js
const ComponentC = dynamic(() => import("../components/C"), { ssr: false });
```

### Sunucu Bileşenlerini İçe Aktarma (Importing Server Components)

Bir Sunucu Bileşenini dinamik olarak içe aktarırsanız, Sunucu Bileşeninin kendisi değil, yalnızca Sunucu Bileşeninin alt bileşenleri olan İstemci Bileşenleri lazy-load edilecektir.

```js
// app/page.js

import dynamic from "next/dynamic";

// Server Component:
const ServerComponent = dynamic(() => import("../components/ServerComponent"));

export default function ServerComponentExample() {
  return (
    <div>
      <ServerComponent />
    </div>
  );
}
```

### Harici Kütüphaneleri Yükleme

Harici kütüphaneler [`import()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) fonksiyonu kullanılarak isteğe bağlı olarak yüklenebilir. Bu örnekte bulanık arama için `fuse.js` harici kütüphanesi kullanılmaktadır. Modül, yalnızca kullanıcı arama girdisini yazdıktan sonra istemciye yüklenir.

```js
// app/page.js

"use client";

import { useState } from "react";

const names = ["Tim", "Joe", "Bel", "Lee"];

export default function Page() {
  const [results, setResults] = useState();

  return (
    <div>
      <input
        type="text"
        placeholder="Search"
        onChange={async (e) => {
          const { value } = e.currentTarget;
          // Dynamically load fuse.js
          const Fuse = (await import("fuse.js")).default;
          const fuse = new Fuse(names);

          setResults(fuse.search(value));
        }}
      />
      <pre>Results: {JSON.stringify(results, null, 2)}</pre>
    </div>
  );
}
```

### Özel bir yükleme bileşeni ekleme (Adding a custom loading component)

```js
// app/page.js

import dynamic from "next/dynamic";

const WithCustomLoading = dynamic(
  () => import("../components/WithCustomLoading"),
  {
    loading: () => <p>Loading...</p>,
  }
);

export default function Page() {
  return (
    <div>
      {/* <WithCustomLoading/> yüklenirken yükleme bileşeni oluşturulacaktır */}
      <WithCustomLoading />
    </div>
  );
}
```

### Adlandırılmış Dışa Aktarmaları İçe Aktarma (Importing Named Exports)

Adlandırılmış bir dışa aktarımı dinamik olarak içe aktarmak için, [`import()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) işlevi tarafından döndürülen Promise'den geri döndürebilirsiniz:

```js
// components/hello.js

"use client";

export function Hello() {
  return <p>Hello!</p>;
}
```

```js
// app/page.js

import dynamic from "next/dynamic";

const ClientComponent = dynamic(() =>
  import("../components/hello").then((mod) => mod.Hello)
);
```
