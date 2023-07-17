# CSS Modülleri (CSS Modules)

Next.js, `.module.css` uzantısını kullanan CSS Modülleri için yerleşik desteğe sahiptir.

CSS Modülleri, otomatik olarak benzersiz bir sınıf adı oluşturarak CSS'yi yerel olarak kapsar. Bu, çakışma endişesi olmadan farklı dosyalarda aynı sınıf adını kullanmanıza olanak tanır. Bu davranış CSS Modüllerini bileşen düzeyinde CSS eklemek için ideal bir yol haline getirir.

## Örnek

CSS Modülleri, `app` dizini içindeki herhangi bir dosyaya aktarılabilir:

```js
import styles from "./styles.module.css";

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return <section className={styles.dashboard}>{children}</section>;
}
```

```css
.dashboard {
  padding: 24px;
}
```

CSS Modülleri isteğe bağlı bir özelliktir ve yalnızca `.module.css` uzantılı dosyalar için etkinleştirilir. Normal `<link>` stil sayfaları ve global CSS dosyaları hala desteklenmektedir.

Üretimde, tüm CSS Modülü dosyaları otomatik olarak birçok küçültülmüş ve kod bölünmüş `.css` dosyasına birleştirilecektir. Bu `.css` dosyaları uygulamanızdaki sıcak yürütme yollarını temsil eder ve uygulamanızın boyaması için minimum miktarda CSS yüklenmesini sağlar.

## Küresel Stiller (Global Styles)

Global stiller, `app` dizini içindeki herhangi bir düzene, sayfaya veya bileşene aktarılabilir.

**Bilmekte fayda var:** Bu, yalnızca `_app.js` dosyasının içindeki global stilleri içe aktarabileceğiniz `pages` dizininden farklıdır.

Örneğin, `app/global.css` adında bir stil sayfası düşünün:

```css
body {
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Kök düzen `(app/layout.js)` içinde, stilleri uygulamanızdaki her rotaya uygulamak için `global.css` stil sayfasını içe aktarın:

```js
// Bu stiller uygulamadaki her rota için geçerlidir
import "./global.css";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Harici Stil Sayfaları (External Stylesheets)

Harici paketler tarafından yayınlanan stil sayfaları, ortak konumlandırılmış bileşenler de dahil olmak üzere `app` dizininin herhangi bir yerine içe aktarılabilir:

```js
import "bootstrap/dist/css/bootstrap.css";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  );
}
```

**Bilmekte fayda var:** Harici stil sayfaları doğrudan bir npm paketinden içe aktarılmalı veya indirilmeli ve kod tabanınızla birlikte yerleştirilmelidir. `<link rel="stylesheet" />` kullanamazsınız.

## Ek Özellikler

Next.js, stil ekleme yazma deneyimini iyileştirmek için ek özellikler içerir:

- `Next Dev` ile yerel olarak çalıştırılırken, yerel stil sayfaları (genel veya CSS modülleri), düzenlemeler kaydedildikçe değişiklikleri anında yansıtmak için Hızlı Yenileme özelliğinden yararlanacaktır.
- `Next build` ile üretim için oluştururken, stilleri almak için gereken ağ isteklerinin sayısını azaltmak için CSS dosyaları daha az sayıda küçültülmüş `.css` dosyasında bir araya getirilecektir.
- JavaScript'i devre dışı bırakırsanız stiller üretim derlemesinde (`next start`) yüklenmeye devam eder. Ancak, Hızlı Yenileme'yi etkinleştirmek için  JavaScript'te `next dev` hala gereklidir.
