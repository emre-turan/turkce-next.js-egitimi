# Uluslararasılaştırma (Internationalization)

Next.js, birden fazla dili desteklemek için içeriğin yönlendirilmesini ve oluşturulmasını yapılandırmanıza olanak tanır. Sitenizi farklı yerel ayarlara uyumlu hale getirmek, çevrilmiş içerik (yerelleştirme) ve uluslararasılaştırılmış rotaları içerir.

## Terminoloji

- Yerel ayar: Bir dizi dil ve biçimlendirme tercihi için bir tanımlayıcı. Bu genellikle kullanıcının tercih ettiği dili ve muhtemelen coğrafi bölgesini içerir.
  - `en-US`: Amerika Birleşik Devletleri'nde konuşulan İngilizce
  - `nl-NL`: Hollanda'da konuşulduğu şekliyle Hollandaca
  - `nl`: Hollandaca, belirli bir bölge yok

## Yönlendirmeye Genel Bakış (Routing Overview)

Hangi yerel ayarın kullanılacağını seçmek için kullanıcının tarayıcıdaki dil tercihlerini kullanmanız önerilir. Tercih ettiğiniz dili değiştirmek, uygulamanıza gelen `Accept-Language` başlığını değiştirecektir.

Örneğin, aşağıdaki kütüphaneleri kullanarak, Üstbilgilere, desteklemeyi planladığınız yerel ayarlara ve varsayılan yerel ayara göre hangi yerel ayarı seçeceğinizi belirlemek için gelen bir İsteğe bakabilirsiniz.

```ts
import { match } from "@formatjs/intl-localematcher";
import Negotiator from "negotiator";

let headers = { "accept-language": "en-US,en;q=0.5" };
let languages = new Negotiator({ headers }).languages();
let locales = ["en-US", "nl-NL", "nl"];
let defaultLocale = "en-US";

match(languages, locales, defaultLocale); // -> 'en-US'
```

Yönlendirme, alt yol (`/fr/products`) veya etki alanı (`my-site.fr/products`) ile uluslararasılaştırılabilir. Bu bilgilerle artık kullanıcıyı Middleware içindeki yerel ayara göre yönlendirebilirsiniz.

```ts
import { NextResponse } from 'next/server'

let locales = ['en-US', 'nl-NL', 'nl']

// Yukarıdakine benzer şekilde veya bir kütüphane kullanarak tercih edilen yerel ayarı alın
function getLocale(request) { ... }

export function middleware(request) {
  // Yol adında desteklenen herhangi bir yerel ayar olup olmadığını kontrol edin
  const pathname = request.nextUrl.pathname
  const pathnameIsMissingLocale = locales.every(
    (locale) => !pathname.startsWith(`/${locale}/`) && pathname !== `/${locale}`
  )

  // Yerel ayar yoksa yönlendirme
  if (pathnameIsMissingLocale) {
    const locale = getLocale(request)

    // örneğin gelen istek /products
    // Yeni URL artık /en-US/products şeklindedir
    return NextResponse.redirect(
      new URL(`/${locale}/${pathname}`, request.url)
    )
  }
}

export const config = {
  matcher: [
    // Tüm dahili yolları atla (_next)
    '/((?!_next).*)',
    // İsteğe bağlı: yalnızca kök (/) URL'de çalıştır
    // '/'
  ],
}
```

Son olarak, `app/` içindeki tüm özel dosyaların `app/[lang]` altında yuvalandığından emin olun. Bu, Next.js yönlendiricisinin rotadaki farklı yerel ayarları dinamik olarak işlemesini ve `lang` parametresini her düzene ve sayfaya iletmesini sağlar. Örneğin:

```ts
// Artık geçerli yerel ayara erişiminiz var
// örneğin /en-US/products -> `lang` "en-US "dir
export default async function Page({ params: { lang } }) {
  return ...
}
```

Kök düzen de yeni klasörün içine yerleştirilebilir (örn. `app/[lang]/layout.js`).

## Yerelleştirme (Localization)

Görüntülenen içeriğin kullanıcının tercih ettiği yerel ayara veya yerelleştirmeye göre değiştirilmesi Next.js'ye özgü bir şey değildir. Aşağıda açıklanan modeller herhangi bir web uygulamasında aynı şekilde çalışacaktır.

Uygulamamız içinde hem İngilizce hem de Hollandaca içeriği desteklemek istediğimizi varsayalım. Bize bazı anahtarlardan yerelleştirilmiş bir dizeye eşleme sağlayan nesneler olan iki farklı "sözlük" tutabiliriz. Örneğin:

```ts
{
  "products": {
    "cart": "Add to Cart"
  }
}
```

```ts
{
  "products": {
    "cart": "Voeg toe aan winkelwagen"
  }
}
```

Ardından, istenen yerel ayar için çevirileri yüklemek üzere bir `getDictionary` işlevi oluşturabiliriz:

```ts
import "server-only";

const dictionaries = {
  en: () => import("./dictionaries/en.json").then((module) => module.default),
  nl: () => import("./dictionaries/nl.json").then((module) => module.default),
};

export const getDictionary = async (locale) => dictionaries[locale]();
```

O anda seçili olan dil göz önüne alındığında, bir düzen veya sayfanın içindeki sözlüğü getirebiliriz.

```ts
import { getDictionary } from "./dictionaries";

export default async function Page({ params: { lang } }) {
  const dict = await getDictionary(lang); // en
  return <button>{dict.products.cart}</button>; // Add to Cart
}
```

`app/` dizinindeki tüm düzenler ve sayfalar varsayılan olarak Sunucu Bileşenleri olduğundan, çeviri dosyalarının boyutunun istemci tarafı JavaScript paket boyutumuzu etkilemesi konusunda endişelenmemize gerek yoktur. Bu kod yalnızca sunucuda çalışacak ve tarayıcıya yalnızca ortaya çıkan HTML gönderilecektir.

## Statik Üretim (Static Generation)

Belirli bir yerel ayar kümesi için statik rotalar oluşturmak üzere `generateStaticParams`'ı herhangi bir sayfa veya düzenle birlikte kullanabiliriz. Bu, örneğin kök düzeninde global olabilir:

```ts
export async function generateStaticParams() {
  return [{ lang: "en-US" }, { lang: "de" }];
}

export default function Root({ children, params }) {
  return (
    <html lang={params.lang}>
      <body>{children}</body>
    </html>
  );
}
```
