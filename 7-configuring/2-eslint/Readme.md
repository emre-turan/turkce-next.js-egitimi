# ESLint

Next.js, kutudan çıkar çıkmaz entegre bir [ESLint](https://eslint.org/) deneyimi sağlar. `next lint`'i `package.json` dosyasına bir betik olarak ekleyin:

```json
{
  "scripts": {
    "lint": "next lint"
  }
}
```

Ardından `npm run lint` veya `yarn lint` komutunu çalıştırın:

```bash
yarn lint
```

Uygulamanızda henüz ESLint yapılandırılmadıysa, kurulum ve yapılandırma süreci boyunca size rehberlik edilecektir.

```bash
yarn lint
```

Bunun gibi bir komut istemi göreceksiniz:

? How would you like to configure ESLint?

❯ Strict (recommended)
Base
Cancel

Aşağıdaki üç seçenekten biri seçilebilir:

- **Strict:** Next.js'nin temel ESLint yapılandırması ile birlikte daha katı bir [Core Web Vitals kural kümesi](https://nextjs.org/docs/app/building-your-application/configuring/eslint#core-web-vitals) içerir. Bu, ESLint'i ilk kez kuran geliştiriciler için önerilen yapılandırmadır.

```bash
// .eslintrc.json

{
"extends": "next/core-web-vitals"
}
```

- **Base:** Next.js'nin temel ESLint yapılandırmasını içerir.

```bash
// .eslintrc.json

{
  "extends": "next"
}
```

- **Cancel:** Herhangi bir ESLint yapılandırması içermez. Bu seçeneği yalnızca kendi özel ESLint yapılandırmanızı kurmayı planlıyorsanız seçin.

İki yapılandırma seçeneğinden biri seçilirse Next.js, uygulamanızda geliştirme bağımlılıkları olarak `eslint` ve `eslint-config-next`'i otomatik olarak yükleyecek ve projenizin kök dizininde seçtiğiniz yapılandırmayı içeren bir `.eslintrc.json` dosyası oluşturacaktır.

Artık hataları yakalamak için ESLint'i her çalıştırmak istediğinizde `next lint`'i çalıştırabilirsiniz. ESLint kurulduktan sonra, her derleme sırasında otomatik olarak çalışacaktır (`next build`). Hatalar derlemeyi başarısız kılarken, uyarılar başarısız olmayacaktır.

`next build` sırasında ESLint'in çalışmasını istemiyorsanız, [ESLint'i Yoksayma](https://nextjs.org/docs/app/api-reference/next-config-js/eslint) belgesine bakın.

Geliştirme sırasında uyarıları ve hataları doğrudan kod düzenleyicinizde görüntülemek için uygun bir [entegrasyon](https://eslint.org/docs/user-guide/integrations#editors) kullanmanızı öneririz.

## ESLint Yapılandırması

Varsayılan yapılandırma (`eslint-config-next`) Next.js'de en iyi kullanıma hazır lintleme deneyimine sahip olmak için ihtiyacınız olan her şeyi içerir. Uygulamanızda ESLint zaten yapılandırılmadıysa, bu yapılandırmayla birlikte ESLint'i kurmak için `next lint`'i kullanmanızı öneririz.

`eslint-config-next`'i diğer ESLint yapılandırmalarıyla birlikte kullanmak isterseniz, herhangi bir çakışmaya neden olmadan bunu nasıl yapacağınızı öğrenmek için [Ek Yapılandırmalar](https://nextjs.org/docs/app/building-your-application/configuring/eslint#additional-configurations) bölümüne bakın.

Aşağıdaki ESLint eklentilerinden önerilen kural kümelerinin tümü `eslint-config-next` içinde kullanılır:

- [`eslint-plugin-react`](https://www.npmjs.com/package/eslint-plugin-react)
- [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks)
- [`eslint-plugin-next`](https://www.npmjs.com/package/@next/eslint-plugin-next)

Bu, `next.config.js` dosyasındaki yapılandırmaya göre öncelikli olacaktır.

## ESLint Eklentisi (ESlint Plugin)

Next.js, bir Next.js uygulamasındaki yaygın sorunları ve problemleri yakalamayı mümkün kılan temel yapılandırma içinde zaten paketlenmiş olan bir ESLint eklentisi, [eslint-plugin-next](https://www.npmjs.com/package/@next/eslint-plugin-next) sağlar. Kuralların tamamı aşağıdaki gibidir:

| Kural                                                    | Açıklama                                                                                              |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| @next/next/google-font-display                           | Google Fonts ile font-display davranışını zorlar.                                                     |
| @next/next/google-font-preconnect                        | Google Fonts ile `preconnect` kullanımını sağlar.                                                     |
| @next/next/inline-script-id                              | Satır içi içeriğe sahip `next/script` bileşenlerinde `id` niteliğini zorunlu kılın.                   |
| @next/next/next-script-for-ga                            | Google Analytics için satır içi script kullanırken `next/script` bileşenini tercih eder.              |
| @next/next/no-assign-module-variable                     | `module` değişkenine atama yapılmasını önler.                                                         |
| @next/next/no-async-client-component                     | İstemci bileşenlerinin async fonksiyonlar olmasını önler.                                             |
| @next/next/no-before-interactive-script-outside-document | `next/script`'in `beforeInteractive` stratejisinin `pages/_document.js` dışında kullanılmasını önler. |
| @next/next/no-css-tags                                   | Manuel stil sayfası etiketlerini önler.                                                               |
| @next/next/no-document-import-in-page                    | `next/document`'ın ` dışında içe aktarılmasını önler.                                                 |
| @next/next/no-duplicate-head                             | `pages/_document.js`'de `<Head>` kullanımının çoğaltılmasını önler.                                   |
| @next/next/no-head-element                               | `<head>` elementinin kullanımını önler.                                                               |
| @next/next/no-head-import-in-document                    | `pages/_document.js`'de `next/head` kullanımını önler.                                                |
| @next/next/no-html-link-for-pages                        | Dahili Next.js sayfalarına gitmek için `<a>` elementlerinin kullanılmasını önler.                     |
| @next/next/no-img-element                                | Daha yavaş LCP ve daha yüksek bant genişliği nedeniyle `<img>` elementinin kullanılmasını önler.      |
| @next/next/no-page-custom-font                           | Sadece sayfa özel fontlarını önler.                                                                   |
| @next/next/no-script-component-in-head                   | `next/head` bileşeninde `next/script` kullanımını önler.                                              |
| @next/next/no-styled-jsx-in-document                     | `pages/_document.js`'de `styled-jsx` kullanımını önler.                                               |
| @next/next/no-sync-scripts                               | Senkronize scriptleri önler.                                                                          |
| @next/next/no-title-in-document-head                     | `next/document`'tan Head bileşeni ile `<title>` kullanımını önler.                                    |
| @next/next/no-typos                                      | Next.js'in veri getirme fonksiyonlarında yaygın yazım hatalarını önler                                |
| @next/next/no-unwanted-polyfillio                        | Polyfill.io'dan çoğaltılmış polyfill'leri önler.                                                      |

Uygulamanızda zaten ESLint yapılandırılmışsa, birkaç koşul karşılanmadığı sürece `eslint-config-next`'i dahil etmek yerine doğrudan bu eklentiden genişletmenizi öneririz. Daha fazla bilgi için [Önerilen Eklenti Kural Seti](https://nextjs.org/docs/app/building-your-application/configuring/eslint#recommended-plugin-ruleset)'ne bakın.

### Özel Ayarlar

#### `rootDir`

Next.js'nin kök dizininizde yüklü olmadığı bir projede (monorepo gibi) `eslint-plugin-next` kullanıyorsanız, `eslint-plugin-next`'e `.eslintrc` dosyanızdaki `settings` özelliğini kullanarak Next.js uygulamanızı nerede bulacağını söyleyebilirsiniz:

```json
// .eslintrc.json

{
  "extends": "next",
  "settings": {
    "next": {
      "rootDir": "packages/my-app/"
    }
  }
}
```

`rootDir` bir yol (göreli veya mutlak), bir glob (örn. `"packages/\*/"`) veya bir yol ve/veya glob dizisi olabilir.

## Özel Dizinleri ve Dosyaları Lintleme

Next.js varsayılan olarak `pages/`, `app/`, `components/`, `lib/` ve `src/` dizinlerindeki tüm dosyalar için ESLint'i çalıştıracaktır. Ancak, üretim derlemeleri için `next.config.js` dosyasındaki `eslint` yapılandırmasında `dirs` seçeneğini kullanarak hangi dizinleri kullanacağınızı belirtebilirsiniz:

```js
// next.config.js

module.exports = {
  eslint: {
    dirs: ["pages", "utils"], // Üretim derlemeleri sırasında ESLint'i yalnızca 'pages' ve 'utils' dizinlerinde çalıştırın (next build)
  },
};
```

Benzer şekilde, `--dir` ve `--file` bayrakları `next lint` için belirli dizinleri ve dosyaları lintlemek için kullanılabilir:

```bash
next lint --dir pages --dir utils --file bar.js
```

## Önbellekleme (Caching)

Performansı artırmak için, ESLint tarafından işlenen dosyaların bilgileri varsayılan olarak önbelleğe alınır. Bu bilgiler `.next/cache` dosyasında veya tanımladığınız derleme dizininde saklanır. Tek bir kaynak dosyanın içeriğinden daha fazlasına bağlı olan herhangi bir ESLint kuralı ekliyorsanız ve önbelleği devre dışı bırakmanız gerekiyorsa, `next lint` ile `--no-cache` bayrağını kullanın.

```bash
next lint --no-cache
```

## Kuralları Devre Dışı Bırakma (Disabling Rules)

Desteklenen eklentiler (`react`, `react-hooks`, `next`) tarafından sağlanan herhangi bir kuralı değiştirmek veya devre dışı bırakmak isterseniz, `.eslintrc` dosyanızdaki rules özelliğini kullanarak bunları doğrudan değiştirebilirsiniz:

```json
// .eslintrc.json

{
  "extends": "next",
  "rules": {
    "react/no-unescaped-entities": "off",
    "@next/next/no-page-custom-font": "off"
  }
}
```

### Core Web Vitals

`next/core-web-vitals` kural kümesi, `next lint` ilk kez çalıştırıldığında ve strict seçeneği seçildiğinde etkinleştirilir.

```bash
{
  "extends": "next/core-web-vitals"
}
```

`next/core-web-vitals`, `eslint-plugin-next`'i [Core Web Vitals](https://web.dev/vitals/)'ı etkiliyorsa varsayılan olarak uyarı olan bir dizi kuralda hata verecek şekilde günceller.

`Next/core-web-vitals` giriş noktası, Create Next App ile oluşturulan yeni uygulamalar için otomatik olarak dahil edilir.

## Diğer Araçlarla Kullanım (Using with Other Tools)

### Prettier

ESLint ayrıca mevcut [Prettier](https://prettier.io/) kurulumunuzla çakışabilecek kod biçimlendirme kuralları da içerir. ESLint ve Prettier'in birlikte çalışmasını sağlamak için ESLint yapılandırmanıza [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)'i eklemenizi öneririz.

İlk olarak, bağımlılığı yükleyin:

```bash
npm install --save-dev eslint-config-prettier

yarn add --dev eslint-config-prettier
```

Ardından, mevcut ESLint yapılandırmanıza `prettier` ekleyin:

```json
// .eslintrc.json
{
  "extends": ["next", "prettier"]
}
```

### lint-staged

Aşamalı git dosyalarında linter çalıştırmak için [lint-staged](https://github.com/okonet/lint-staged) ile `next lint` kullanmak isterseniz, `--file` bayrağının kullanımını belirtmek için projenizin kök dizinindeki `.lintstagedrc.js` dosyasına aşağıdakileri eklemeniz gerekir.

```js
// .lintstagedrc.js

const path = require("path");

const buildEslintCommand = (filenames) =>
  `next lint --fix --file ${filenames
    .map((f) => path.relative(process.cwd(), f))
    .join(" --file ")}`;

module.exports = {
  "*.{js,jsx,ts,tsx}": [buildEslintCommand],
};
```

## Mevcut Yapılandırmayı Taşıma (Migrating Existing Configuration)

### Önerilen Eklenti Kural Seti (Recommended Plugin Rule Set)

Uygulamanızda zaten ESLint yapılandırılmışsa ve aşağıdaki koşullardan herhangi biri doğruysa:

- Aşağıdaki eklentilerden bir veya daha fazlasını zaten yüklediniz (ayrı olarak veya `airbnb` veya `react-app` gibi farklı bir yapılandırma aracılığıyla):
  - `react`
  - `react-hooks`
  - `jsx-a11y`
  - `import`
- Babel'in Next.js içinde yapılandırılma şeklinden farklı olan belirli `parserOptions` tanımladınız (Babel yapılandırmanızı özelleştirmediğiniz sürece bu önerilmez)
- İçe aktarmaları işlemek için tanımlanmış Node.js ve/veya TypeScript [çözümleyicileriyle](https://github.com/benmosher/eslint-plugin-import#resolvers) birlikte `eslint-plugin-import` yüklü

Ardından, bu özelliklerin [`eslint-config-next`](https://github.com/vercel/next.js/blob/canary/packages/eslint-config-next/index.js) içinde nasıl yapılandırıldığını tercih ediyorsanız bu ayarları kaldırmanızı veya bunun yerine doğrudan Next.js ESLint eklentisinden genişletmenizi öneririz:

```json
module.exports = {
  extends: [
    //...
    'plugin:@next/next/recommended',
  ],
};
```

Eklenti, `next lint`'i çalıştırmaya gerek kalmadan projenize normal şekilde kurulabilir:

```bash
npm install --save-dev @next/eslint-plugin-next

yarn add --dev @next/eslint-plugin-next
```

### Ek Konfigürasyonlar

Zaten ayrı bir ESLint yapılandırması kullanıyorsanız ve `eslint-config-next`'i dahil etmek istiyorsanız, diğer yapılandırmalardan sonra en son genişletildiğinden emin olun. Örneğin:

```json
// .eslintrc.json

{
  "extends": ["eslint:recommended", "next"]
}
```

`next` yapılandırma, `parser`, `plugins` ve `settings` özellikleri için varsayılan değerlerin ayarlanmasını zaten ele alır. Kullanım durumunuz için farklı bir yapılandırmaya ihtiyaç duymadığınız sürece bu özelliklerden herhangi birini manuel olarak yeniden beyan etmenize gerek yoktur.

Başka paylaşılabilir yapılandırmalar eklerseniz, bu özelliklerin üzerine yazılmadığından veya değiştirilmediğinden emin olmanız gerekir. Aksi takdirde, `next` yapılandırmayla davranış paylaşan tüm yapılandırmaları kaldırmanızı veya yukarıda belirtildiği gibi doğrudan Next.js ESLint eklentisinden genişletmenizi öneririz.
