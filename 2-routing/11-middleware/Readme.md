# Ara Yazılım (Middleware)

Ara yazılım, bir istek tamamlanmadan önce kod çalıştırmanıza olanak tanır. Ardından, gelen isteğe bağlı olarak, yeniden yazarak, yönlendirerek, istek veya yanıt başlıklarını değiştirerek veya doğrudan yanıt vererek yanıtı değiştirebilirsiniz.

Ara yazılım, önbelleğe alınan içerik ve yollar eşleştirilmeden önce çalışır.

## Convention

Middleware'i tanımlamak için projenizin kök dizinindeki `middleware.ts` (veya `.js`) dosyasını kullanın. Örneğin, `pages` veya `app` ile aynı seviyede veya varsa `src` içinde.

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

// İçinde `await` kullanılıyorsa bu işlev `async` olarak işaretlenebilir
export function middleware(request: NextRequest) {
  return NextResponse.redirect(new URL("/home", request.url));
}

// See "Matching Paths" below to learn more
export const config = {
  matcher: "/about/:path*",
};
```

## Eşleşen Yollar (Matching Paths)

Ara yazılım, projenizdeki **her rota için** çağrılacaktır. Çalıştırma sırası aşağıdaki gibidir:

1. `next.config.js`'den `headers`
2. `next.config.js`'den `redirects`
3. Ara yazılım (`rewrites`, `redirects`, vb.)
4. `next.config.js` dosyasından `beforeFiles` (`rewrites`)
5. Dosya sistemi rotaları (`public/`, `_next/static/`, `pages/`, `app/`, vb.)
6. `next.config.js` dosyasından `afterFiles` (`rewrites`)
7. Dinamik Rotalar (`/blog/[slug]`)
8. `next.config.js`'den `fallback` (`rewrites`)

## Eşleştirici (Matcher)

`matcher`, Orta Yazılımı (middleware) belirli yollarda çalışacak şekilde filtrelemenize olanak tanır.

```ts
export const config = {
  matcher: "/about/:path*",
};
```

Bir dizi sözdizimiyle tek bir yolu veya birden fazla yolu eşleştirebilirsiniz:

```ts
export const config = {
  matcher: ["/about/:path*", "/dashboard/:path*"],
};
```

`matcher` yapılandırması tam regex'e izin verir, böylece negatif lookahead'ler veya karakter eşleştirme gibi eşleştirmeler desteklenir. Belirli yollar hariç tümünü eşleştirmek için negatif lookahead örneği burada görülebilir:

```ts
export const config = {
  matcher: [
    /*
     * Match all request paths except for the ones starting with:
     * - api (API yolları)
     * - _next/static (static dosyalar)
     * - _next/image (görüntü optimizasyon dosyaları)
     * - favicon.ico (favicon dosyası)
     */
    "/((?!api|_next/static|_next/image|favicon.ico).*)",
  ],
};
```

Bilmekte fayda var: `matcher` değerlerinin sabit olması gerekir, böylece derleme zamanında statik olarak analiz edilebilirler. Değişkenler gibi dinamik değerler göz ardı edilecektir.

### Yapılandırılmış eşleştiriciler:

1. ile başlamalıdır `/`
2. Adlandırılmış parametreler içerebilir: `/about/:path`, `/about/a` ve `/about/b` ile eşleşir ancak `/about/a/c` ile eşleşmez
3. Adlandırılmış parametreler üzerinde değiştiricilere sahip olabilir (`:` ile başlayan): `/about/:path*` `/about/a/b/c` ile eşleşir çünkü `*` sıfır veya daha fazladır. `?` sıfır veya bir ve `+` bir veya daha fazla
4. Parantez içine alınmış düzenli ifade kullanabilir: `/about/(.x)`, `/about/:pathx` ile aynıdır

[Path-to-regexp](https://github.com/pillarjs/path-to-regexp#path-to-regexp-1) belgeleri hakkında daha fazla bilgi edinin.

Bilmekte fayda var: Geriye dönük uyumluluk için Next.js her zaman `/public` öğesini `/public/index` olarak kabul eder. Bu nedenle, `/public/:path` eşleştiricisi eşleşecektir.

### Koşullu İfadeler (Conditional Statements)

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  if (request.nextUrl.pathname.startsWith("/about")) {
    return NextResponse.rewrite(new URL("/about-2", request.url));
  }

  if (request.nextUrl.pathname.startsWith("/dashboard")) {
    return NextResponse.rewrite(new URL("/dashboard/user", request.url));
  }
}
```

## NextResponse

`NextResponse` API şunları yapmanıza olanak tanır:

- gelen isteği farklı bir URL'ye yönlendirir.
- belirli bir URL'yi görüntüleyerek yanıtı yeniden yazın
- API Routes, `getServerSideProps` ve `rewrite` hedefleri için istek üstbilgilerini ayarlama
- Yanıt çerezlerini ayarlama
- Yanıt başlıklarını ayarlama

Middleware'den bir yanıt üretmek için şunları yapabilirsiniz:

1. Yanıt üreten bir rotaya (Sayfa veya Edge API Rotası) yeniden yazma
2. Doğrudan bir NextResponse döndürür.

## Çerez Kullanımı (Using Cookies)

Çerezler normal başlıklardır. Bir İstekte, `Cookie` başlığında saklanırlar. Yanıtta ise `Set-Cookie` başlığında bulunurlar. Next.js, `NextRequest` ve `NextResponse` üzerindeki `cookies` uzantısı aracılığıyla bu çerezlere erişmek ve bunları değiştirmek için uygun bir yol sağlar.

1. Gelen istekler için çerezler şu yöntemlerle birlikte gelir: `get`, `getAll`, `set` ve `delete` çerezleri. `has` ile bir çerezin varlığını kontrol edebilir veya `clear` ile tüm çerezleri kaldırabilirsiniz.
2. Giden yanıtlar için, çerezler aşağıdaki `get`, `getAll`, `set` ve `delete` yöntemlerine sahiptir.

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  // Gelen istekte bir "Cookie:nextjs=fast" başlığının bulunduğunu varsayın
  // RequestCookies` API'sini kullanarak istekten çerezleri alma
  let cookie = request.cookies.get("nextjs");
  console.log(cookie); // => { name: 'nextjs', value: 'fast', Path: '/' }
  const allCookies = request.cookies.getAll();
  console.log(allCookies); // => [{ name: 'nextjs', value: 'fast' }]

  request.cookies.has("nextjs"); // => true
  request.cookies.delete("nextjs");
  request.cookies.has("nextjs"); // => false

  // ResponseCookies` API'sini kullanarak yanıt üzerinde çerezleri ayarlama
  const response = NextResponse.next();
  response.cookies.set("vercel", "fast");
  response.cookies.set({
    name: "vercel",
    value: "fast",
    path: "/",
  });
  cookie = response.cookies.get("vercel");
  console.log(cookie); // => { name: 'vercel', value: 'fast', Path: '/' }
  // Giden yanıt bir `Set-Cookie:vercel=fast;path=/test` başlığına sahip olacaktır.

  return response;
}
```

## Üstbilgileri Ayarlama (Setting Headers)

`NextResponse` API'sini kullanarak istek ve yanıt başlıklarını ayarlayabilirsiniz (istek başlıklarının ayarlanması Next.js v13.0.0'dan beri mevcuttur).

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  // İstek başlıklarını klonlayın ve yeni bir `x-hello-from-middleware1` başlığı ayarlayın
  const requestHeaders = new Headers(request.headers);
  requestHeaders.set("x-hello-from-middleware1", "hello");

  // İstek başlıklarını NextResponse.rewrite içinde de ayarlayabilirsiniz
  const response = NextResponse.next({
    request: {
      // Yeni istek başlıkları
      headers: requestHeaders,
    },
  });

  // Yeni bir `x-hello-from-middleware2` yanıt başlığı ayarlayın
  response.headers.set("x-hello-from-middleware2", "hello");
  return response;
}
```

Bilmekte fayda var: Arka uç web sunucusu yapılandırmanıza bağlı olarak [431 Request Header Fields Too Large](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/431) hatasına neden olabileceğinden büyük başlıklar ayarlamaktan kaçının.

## Yanıt Üretme (Producing a Response)

Bir `Response` veya `NextResponse` örneği döndürerek Middleware'den doğrudan yanıt verebilirsiniz. (Bu Next.js v13.1.0'dan beri mevcuttur)

```ts
import { NextRequest, NextResponse } from "next/server";
import { isAuthenticated } from "@lib/auth";

// Ara yazılımı `/api/` ile başlayan yollarla sınırlayın
export const config = {
  matcher: "/api/:function*",
};

export function middleware(request: NextRequest) {
  // İsteği kontrol etmek için kimlik doğrulama işlevimizi çağırın
  if (!isAuthenticated(request)) {
    // Bir hata mesajı belirten JSON ile yanıt verin
    return new NextResponse(
      JSON.stringify({ success: false, message: "authentication failed" }),
      { status: 401, headers: { "content-type": "application/json" } }
    );
  }
}
```

## Gelişmiş Orta Yazılım Bayrakları (Advanced Middleware Flags)

Next.js'nin `v13.1` sürümünde, gelişmiş kullanım durumlarını ele almak için ara katman için `skipMiddlewareUrlNormalize` ve `skipTrailingSlashRedirect` olmak üzere iki ek bayrak tanıtıldı.

`skipTrailingSlashRedirect`, sondaki eğik çizgilerin eklenmesi veya kaldırılması için Next.js varsayılan yönlendirmelerinin devre dışı bırakılmasına olanak tanıyarak, bazı yollar için sondaki eğik çizginin korunmasına izin verebilen ancak diğerleri için izin vermeyen ara yazılım içinde özel işleme izin verir.

```ts
module.exports = {
  skipTrailingSlashRedirect: true,
};
```

```ts
const legacyPrefixes = ["/docs", "/blog"];

export default async function middleware(req) {
  const { pathname } = req.nextUrl;

  if (legacyPrefixes.some((prefix) => pathname.startsWith(prefix))) {
    return NextResponse.next();
  }

  // apply trailing slash handling
  if (
    !pathname.endsWith("/") &&
    !pathname.match(/((?!\.well-known(?:\/.*)?)(?:[^/]+\/)*[^/]+\.\w+)/)
  ) {
    req.nextUrl.pathname += "/";
    return NextResponse.redirect(req.nextUrl);
  }
}
```

`skipMiddlewareUrlNormalize`, Next.js'nin doğrudan ziyaretleri ve istemci geçişlerini aynı şekilde ele almak için yaptığı URL normalleştirmesini devre dışı bırakmaya olanak tanır. Bunun kilidini açtığı orijinal URL'yi kullanarak tam kontrole ihtiyaç duyduğunuz bazı gelişmiş durumlar vardır.

```ts
module.exports = {
  skipMiddlewareUrlNormalize: true,
};
```

```ts
export default async function middleware(req) {
  const { pathname } = req.nextUrl;

  // GET /_next/data/build-id/hello.json

  console.log(pathname);
  // bu bayrak ile /_next/data/build-id/hello.json
  //bayrak olmadan bu /hello olarak normalleştirilirdi
}
```
