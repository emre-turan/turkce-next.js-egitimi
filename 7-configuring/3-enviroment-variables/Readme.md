# Ortam Değişkenleri (Environment Variables)

Next.js, aşağıdakileri yapmanıza olanak tanıyan ortam değişkenleri için yerleşik destekle birlikte gelir:

- Ortam değişkenlerini yüklemek için `.env.local` kullanın
- `NEXT_PUBLIC_` ile önekleyerek tarayıcı için ortam değişkenlerini paketleyin

## Ortam Değişkenlerini Yükleme

Next.js, ortam değişkenlerini `.env.local`'den `process.env`'ye yüklemek için yerleşik desteğe sahiptir.

```bash
// .env.local


DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

Bu, `process.env.DB_HOST`, `process.env.DB_USER` ve `process.env.DB_PASS` dosyalarını otomatik olarak Node.js ortamına yükler ve bunları Rota İşleyicilerinde kullanmanıza olanak tanır.

Örneğin:

```js
// app/api/route.js

export async function GET() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  });
  // ...
}
```

### Diğer Değişkenlere Referans Verme

Next.js, `.env*` dosyalarınızın içindeki `$VARIABLE` gibi diğer değişkenlere referans vermek için `$` kullanan değişkenleri otomatik olarak genişletecektir. Bu, diğer gizliliklere referans vermenizi sağlar. Örneğin:

```bash
// .env
TWITTER_USER=nextjs
TWITTER_URL=https://twitter.com/$TWITTER_USER
```

Yukarıdaki örnekte, `process.env.TWITTER_URL` `https://twitter.com/nextjs` olarak ayarlanacaktır.

**Bilmekte fayda var:** Gerçek değerinde `$` olan bir değişken kullanmanız gerekiyorsa, bunun öncelenmesi gerekir, örneğin `\$`.

## Tarayıcı için Ortam Değişkenlerinin Paketlenmesi

Non-`NEXT_PUBLIC_` ortam değişkenleri yalnızca Node.js ortamında kullanılabilir, yani tarayıcı tarafından erişilemezler (istemci farklı bir ortamda çalışır).

Bir ortam değişkeninin değerini tarayıcıda erişilebilir kılmak için Next.js, derleme sırasında istemciye teslim edilen js paketine bir değer "satır içi" ekleyebilir ve `process.env.[variable]`'a yapılan tüm referansları sabit kodlanmış bir değerle değiştirebilir. Bunu yapmasını söylemek için değişkenin önüne `NEXT_PUBLIC_` eklemeniz yeterlidir. Örneğin:

```terminal
NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk
```
