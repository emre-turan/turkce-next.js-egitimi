# Sass

Next.js, hem `.scss` hem de `.sass` uzantılarını kullanarak Sass için yerleşik desteğe sahiptir. `module.scss` veya `.module.sass` uzantısı aracılığıyla bileşen düzeyinde Sass kullanabilirsiniz.

İlk olarak, [`sass`](https://github.com/sass/sass) yükleyin:

```terminal
npm install --save-dev sass
```

**Bilmekte fayda var:**

Sass, her biri kendi uzantısına sahip [iki farklı sözdizimini](https://sass-lang.com/documentation/syntax) destekler. `.scss` uzantısı [SCSS sözdizimini](https://sass-lang.com/documentation/syntax#scss) kullanmanızı gerektirirken, `.sass` uzantısı [Girintili Sözdizimini ("Sass")](https://sass-lang.com/documentation/syntax#the-indented-syntax) kullanmanızı gerektirir.

Hangisini seçeceğinizden emin değilseniz, CSS'nin bir üst kümesi olan ve Girintili Sözdizimini ("Sass") öğrenmenizi gerektirmeyen `.scss` uzantısı ile başlayın.

## Sass Seçeneklerini Özelleştirme

Sass derleyicisini yapılandırmak istiyorsanız `next.config.js` dosyasında `sassOptions` seçeneğini kullanın.

```js
next.config.js;

const path = require("path");

module.exports = {
  sassOptions: {
    includePaths: [path.join(__dirname, "styles")],
  },
};
```

## Sass Değişkenleri

Next.js, CSS Modülü dosyalarından dışa aktarılan Sass değişkenlerini destekler.

Örneğin, dışa aktarılan `primaryColor` Sass değişkenini kullanarak:

```scss

app/variables.module.scss

$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

```js
app / page.js;

// maps to root `/` URL

import variables from "./variables.module.scss";

export default function Page() {
  return <h1 style={{ color: variables.primaryColor }}>Hello, Next.js!</h1>;
}
```
