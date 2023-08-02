# Enstrümantasyon

Projenizin kök dizinindeki (veya kullanıyorsanız `src` klasörünün içindeki) `instrumentation.ts` (veya `.js`) dosyasından `register` adlı bir işlevi dışa aktarırsanız, yeni bir Next.js sunucu örneği önyüklendiğinde bu işlevi çağırırız.

**Bilmekte fayda var:**

- Bu özellik deneyseldir. Kullanmak için, `next.config.js` dosyanızda `experimental.instrumentationHook = true;` tanımlayarak açıkça tercih etmelisiniz.
- `instrumentation` dosyası, `app` veya `pages` dizini içinde değil, projenizin kök dizininde olmalıdır. Eğer `src` klasörünü kullanıyorsanız, dosyayı `pages` ve `app` ile birlikte `src`'nin içine yerleştirin.
- Bir son ek eklemek için `pageExtensions` yapılandırma seçeneğini kullanırsanız, `instrumentation` dosya adını da eşleşecek şekilde güncellemeniz gerekecektir.
- Kullanabileceğiniz temel bir [with-opentelemetry](https://github.com/vercel/next.js/tree/canary/examples/with-opentelemetry) örneği oluşturduk.

`register` işleviniz deploy edildiğinde, her soğuk önyüklemede çağrılacaktır (ancak her ortamda tam olarak bir kez).

Bazen, neden olacağı yan etkiler nedeniyle kodunuzda bir dosyayı içe aktarmak yararlı olabilir. Örneğin, bir dizi global değişkeni tanımlayan bir dosyayı içe aktarabilir, ancak içe aktarılan dosyayı kodunuzda asla açıkça kullanmayabilirsiniz. Yine de paketin bildirdiği global değişkenlere erişiminiz olacaktır.

Aşağıdaki örnekte gösterildiği gibi, `register` işlevinizde kullanmak isteyebileceğiniz `instrumentation.ts` dosyasında yan etkileri olan dosyaları içe aktarabilirsiniz:

```ts
// your-project/instrumentation.ts;

import { init } from "package-init";

export function register() {
  init();
}
```

Ancak, yan etkileri olan dosyaları içe aktarmak için bunun yerine `register` işlevinizin içinden `import` etmeyi kullanmanızı öneririz. Aşağıdaki örnek, bir `register` fonksiyonunda `import`'un temel bir kullanımını göstermektedir:

```ts
// your-project/instrumentation.ts
export async function register() {
  await import("package-with-side-effect");
}
```

Bunu yaparak, tüm yan etkilerinizi kodunuzda tek bir yerde toplayabilir ve dosyaların içe aktarılmasından kaynaklanan istenmeyen sonuçlardan kaçınabilirsiniz.

Tüm ortamlarda `register` diyoruz, bu nedenle hem `edge` hem de `nodejs`'i desteklemeyen herhangi bir kodu koşullu olarak içe aktarmak gerekir. Geçerli ortamı almak için `NEXT_RUNTIME` ortam değişkenini kullanabilirsiniz. Ortama özgü bir kodu içe aktarmak şu şekilde görünecektir:

```ts
// your-project/instrumentation.ts

export async function register() {
  if (process.env.NEXT_RUNTIME === "nodejs") {
    await import("./instrumentation-node");
  }

  if (process.env.NEXT_RUNTIME === "edge") {
    await import("./instrumentation-edge");
  }
}
```
