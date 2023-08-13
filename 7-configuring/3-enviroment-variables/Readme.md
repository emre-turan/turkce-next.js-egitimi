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

Bu, Next.js'ye Node.js ortamındaki `process.env.NEXT_PUBLIC_ANALYTICS_ID`'ye yapılan tüm referansları `next build`'i çalıştırdığınız ortamdaki değerle değiştirmesini söyleyecek ve kodunuzun herhangi bir yerinde kullanmanıza izin verecektir. Tarayıcıya gönderilen tüm JavaScript'lerde satır içi olarak yer alacaktır.

**Not:** Oluşturulduktan sonra, uygulamanız artık bu ortam değişkenlerindeki değişikliklere yanıt vermeyecektir. Örneğin, bir ortamda oluşturulan slug'ları başka bir ortama tanıtmak için bir Heroku pipeline kullanıyorsanız veya tek bir Docker görüntüsü oluşturup birden fazla ortama dağıtıyorsanız, tüm `NEXT_PUBLIC_` değişkenleri derleme zamanında değerlendirilen değerle dondurulacaktır, bu nedenle proje oluşturulduğunda bu değerlerin uygun şekilde ayarlanması gerekir. Çalışma zamanı ortam değerlerine erişmeniz gerekiyorsa, bunları istemciye sağlamak için kendi API'nizi kurmanız gerekir (talep üzerine veya başlatma sırasında).

```js
import setupAnalyticsService from "../lib/my-analytics-service";

// 'NEXT_PUBLIC_ANALYTICS_ID', 'NEXT_PUBLIC_' ile ön ekli olduğu için burada kullanılabilir.
// Derleme sırasında `setupAnalyticsService('abcdefghijk')` olarak dönüştürülecektir.

setupAnalyticsService(process.env.NEXT_PUBLIC_ANALYTICS_ID);

function HomePage() {
  return <h1>Hello World</h1>;
}

export default HomePage;
```

Aşağıdaki gibi dinamik aramaların satır içi yapılmayacağını unutmayın:

```js
// Bu bir değişken kullandığı için satır içi yapılmayacaktır
const varName = "NEXT_PUBLIC_ANALYTICS_ID";
setupAnalyticsService(process.env[varName]);

// Bu bir değişken kullandığı için satır içi yapılmayacaktır
const env = process.env;
setupAnalyticsService(env.NEXT_PUBLIC_ANALYTICS_ID);
```

## Varsayılan Ortam Değişkenleri

Genel olarak yalnızca bir `.env.local` dosyası gereklidir. Ancak, bazen geliştirme (`next dev`) veya production (`next start`) ortamı için bazı varsayılanlar eklemek isteyebilirsiniz.

Next.js, `.env` (tüm ortamlar), `.env.development` (geliştirme ortamı) ve `.env.production` (production ortamı) içinde varsayılanları ayarlamanıza olanak tanır.

`.env.local` her zaman ayarlanan varsayılanları geçersiz kılar.

**Bilmenizde fayda var:** `.env`, `.env.development` ve `.env.production` dosyaları varsayılanları tanımladıkları için deponuza dahil edilmelidir. `.env*.local` dosyaları `.gitignore`'a eklenmelidir, çünkü bu dosyaların göz ardı edilmesi amaçlanmıştır. `.env.local` gizli dosyaların saklanabileceği yerdir.

## Vercel'de Ortam Değişkenleri

Next.js uygulamanızı [Vercel](https://vercel.com/)'e deploy ederken, Ortam Değişkenleri [Proje Ayarları](https://vercel.com/docs/concepts/projects/environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website)'nda yapılandırılabilir.

Her tür Ortam Değişkeni burada yapılandırılmalıdır. Geliştirmede kullanılan Ortam Değişkenleri bile - ki bunlar daha sonra [yerel cihazınıza indirilebilir](https://vercel.com/docs/concepts/projects/environment-variables#development-environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website).

[Geliştirme Ortam Değişkenlerini yapılandırdıysanız](https://vercel.com/docs/concepts/projects/environment-variables#development-environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website), aşağıdaki komutu kullanarak bunları yerel makinenizde kullanmak üzere bir `.env.local` içine çekebilirsiniz:

```Terminal
vercel env pull .env.local
```

## Test Ortamı Değişkenleri

`development` ve `production` ortamlarının yanı sıra 3. bir seçenek daha mevcuttur: `test`. Geliştirme veya production ortamları için varsayılanları ayarlayabileceğiniz gibi, aynı şeyi test ortamı için bir `.env.test` dosyası ile de yapabilirsiniz (ancak bu önceki ikisi kadar yaygın değildir). Next.js, `testing` ortamında `.env.development` veya `.env.production` dosyalarındaki ortam değişkenlerini yüklemeyecektir.

Bu, yalnızca test amacıyla belirli ortam değişkenlerini ayarlamanız gereken `jest` veya `cypress` gibi araçlarla testler çalıştırırken kullanışlıdır. `NODE_ENV` `test` olarak ayarlanırsa test varsayılan değerleri yüklenecektir, ancak test araçları bunu sizin için ele alacağından genellikle bunu manuel olarak yapmanız gerekmez.

`test` ortamı ile hem `development` hem de `production` arasında aklınızda bulundurmanız gereken küçük bir fark vardır: Testlerin herkes için aynı sonuçları üretmesini beklediğiniz için `.env.local` yüklenmeyecektir. Bu şekilde her test yürütmesi, `.env.local` (varsayılan seti geçersiz kılmak için tasarlanmıştır) dosyanızı yok sayarak farklı yürütmelerde aynı env varsayılanlarını kullanacaktır.

**Bilmenizde fayda var:** Varsayılan Ortam Değişkenlerine benzer şekilde, `.env.test` dosyası deponuza dahil edilmelidir, ancak `.env.test.local` dosyası dahil edilmemelidir, çünkü `.env*.local` dosyasının `.gitignore` aracılığıyla göz ardı edilmesi amaçlanmıştır.

Birim testlerini çalıştırırken, `@next/env` paketindeki `loadEnvConfig` işlevinden yararlanarak ortam değişkenlerinizi Next.js'nin yaptığı gibi yüklediğinizden emin olabilirsiniz.

```js
// // Aşağıdakiler, test kurulumunuz için bir Jest global kurulum dosyasında veya benzerinde kullanılabilir
import { loadEnvConfig } from "@next/env";

export default async () => {
  const projectDir = process.cwd();
  loadEnvConfig(projectDir);
};
```

## Ortam Değişkeni Yük Sırası

Ortam değişkenleri sırasıyla aşağıdaki yerlerde aranır ve değişken bulunduğunda durdurulur.

1. `process.env`
2. `.env.$(NODE_ENV).local`
3. `.env.local` (`NODE_ENV` `test` olduğunda kontrol edilmez.)
4. `.env.$(NODE_ENV)`
5. `.env`

Örneğin, `NODE_ENV` `development` ise ve hem `.env.development.local` hem de `.env`'de bir değişken tanımlarsanız, `.env.development.local`'deki değer kullanılır.

**Bilmekte fayda var:** `NODE_ENV` için izin verilen değerler `development`, `production` ve `test`tir.

## Bilmekte fayda var

- Eğer bir `/src` dizini kullanıyorsanız, `.env.*` dosyaları projenizin kök dizininde kalmalıdır.
- `NODE_ENV` ortam değişkeni atanmamışsa Next.js, `next dev` komutunu çalıştırırken otomatik olarak `development` veya diğer tüm komutlar için `production` ataması yapar.
