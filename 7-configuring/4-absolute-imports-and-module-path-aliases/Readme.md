# Mutlak İçe Aktarmalar ve Modül Yolu Takma Adları (Absolute Imports and Module Path Aliases)

Next.js, `tsconfig.json` ve `jsconfig.json` dosyalarının `"paths"` ve `"baseUrl"` seçenekleri için yerleşik destek sunar.

Bu seçenekler, proje dizinlerini mutlak yollara takma ad olarak eklemenize olanak tanıyarak modülleri içe aktarmayı kolaylaştırır. Örneğin:

```ts
// önce
import { Button } from "../../../components/button";

// sonra
import { Button } from "@/components/button";
```

**bilmekte fayda var:** `create-next-app`, bu seçenekleri sizin için yapılandırmayı önerir.

## Mutlak İçe Aktarmalar (Absolute Imports)

`baseUrl` yapılandırma seçeneği, projenin kökünden doğrudan içe aktarmanıza olanak tanır.

Bu yapılandırmanın bir örneği:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": "."
  }
}
```

```typescript
// components/button.tsx;

export default function Button() {
  return <button>Click me</button>;
}
```

```js
// app / page.tsx;

import Button from "components/button";

export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  );
}
```

### Modül Takma Adları (Module Aliases)

`baseUrl` yolu yapılandırmasına ek olarak, `"paths"` seçeneğini kullanarak modül yollarını "alias" olarak kullanabilirsiniz.

Örneğin, aşağıdaki yapılandırma, `@/components/*`'ı `components/*`'a eşler:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/components/_": ["components/_"]
    }
  }
}
```

```ts
// components/button.tsx

export default function Button() {
  return <button>Click me</button>;
}
```

```ts
/// app/page.tsx

import Button from "@/components/button";

export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  );
}
```

`"paths"` her biri `baseUrl` konumuna görelidir. Örneğin:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": "src/",
    "paths": {
      "@/styles/_": ["styles/_"],
      "@/components/_": ["components/_"]
    }
  }
}
```

```js
// pages/index.js

import Button from "@/components/button";
import "@/styles/styles.css";
import Helper from "utils/helper";

export default function HomePage() {
  return (
    <Helper>
      <h1>Hello World</h1>
      <Button />
    </Helper>
  );
}
```
