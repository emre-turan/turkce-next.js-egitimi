# Statik Dışa Aktarmalar (Static Exports)

Next.js, statik bir site veya Tek Sayfalı Uygulama (SPA) olarak başlamayı ve daha sonra isteğe bağlı olarak sunucu gerektiren özellikleri kullanmak için yükseltmeyi sağlar.

Next.js, `next build` çalıştırırken her rota için bir HTML dosyası oluşturur. Next.js, katı bir SPA'yı ayrı HTML dosyalarına bölerek istemci tarafında gereksiz JavaScript kodlarının yüklenmesini önleyebilir, paket boyutunu küçültebilir ve sayfanın daha hızlı yüklenmesini sağlayabilir.

Next.js bu statik dışa aktarımı desteklediğinden, HTML/CSS/JS statik varlıklarını sunabilen herhangi bir web sunucusunda dağıtılabilir ve barındırılabilir.

## Konfigürasyon

Statik dışa aktarmayı etkinleştirmek için `next.config.js` içindeki çıktı modunu değiştirin:

```js
// next.config.js
/**
 * @type {import('next').NextConfig}
 */
const nextConfig = {
  output: "export",

  // İsteğe bağlı: Bağlantıları `/me` -> `/me/` olarak değiştirin ve `/me.html` -> `/me/index.html` olarak yayın
  // trailingSlash: true,

  // İsteğe bağlı: Otomatik `/me` -> `/me/` kullanımını önleyin, bunun yerine `href`i koruyun
  // skipTrailingSlashRedirect: true,

  // İsteğe bağlı: Çıktı dizinini `out` -> `dist` olarak değiştirin
  // distDir: 'dist',
};

module.exports = nextConfig;
```

Next.js, `next build` çalıştırdıktan sonra uygulamanız için HTML/CSS/JS varlıklarını içeren bir `out` klasörü üretecektir.

## Desteklenen Özellikler

Next.js'nin çekirdeği statik dışa aktarımları desteklemek üzere tasarlanmıştır.

### Sunucu Bileşenleri

Statik dışa aktarma oluşturmak için `next build` çalıştırdığınızda, `app` dizini içinde tüketilen Sunucu Bileşenleri, geleneksel statik site oluşturmaya benzer şekilde derleme sırasında çalışacaktır.

Ortaya çıkan bileşen, ilk sayfa yüklemesi için statik HTML'ye ve rotalar arasında istemci gezintisi için statik bir yüke dönüştürülecektir. Dinamik sunucu işlevlerini kullanmadıkları sürece, statik dışa aktarmayı kullanırken Sunucu Bileşenleriniz için hiçbir değişiklik gerekmez.

```tsx
// app/page.tsx
export default async function Page() {
  // This fetch will run on the server during `next build`
  const res = await fetch("https://api.example.com/...");
  const data = await res.json();

  return <main>...</main>;
}
```

## İstemci Bileşenleri

İstemcide veri getirme işlemi gerçekleştirmek istiyorsanız, istekleri memoize etmek için [SWR](https://github.com/vercel/swr) ile bir İstemci Bileşeni kullanabilirsiniz.

```tsx
// app/other/page.tsx
"use client";

import useSWR from "swr";

const fetcher = (url: string) => fetch(url).then((r) => r.json());

export default function Page() {
  const { data, error } = useSWR(
    `https://jsonplaceholder.typicode.com/posts/1`,
    fetcher
  );
  if (error) return "Failed to load";
  if (!data) return "Loading...";

  return data.title;
}
```

Rota geçişleri istemci tarafında gerçekleştiğinden, bu geleneksel bir SPA gibi davranır. Örneğin, aşağıdaki dizin rotası istemcide farklı gönderilere gitmenizi sağlar:

```tsx
// app/page.tsx
import Link from "next/link";

export default function Page() {
  return (
    <>
      <h1>Index Page</h1>
      <hr />
      <ul>
        <li>
          <Link href="/post/1">Post 1</Link>
        </li>
        <li>
          <Link href="/post/2">Post 2</Link>
        </li>
      </ul>
    </>
  );
}
```

### Görüntü Optimizasyonu

`next/image` aracılığıyla Görüntü Optimizasyonu, `next.config.js`'de özel bir görüntü yükleyici tanımlayarak statik bir dışa aktarma ile kullanılabilir. Örneğin, Cloudinary gibi bir hizmetle görüntüleri optimize edebilirsiniz:

```js
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: "export",
  images: {
    loader: "custom",
    loaderFile: "./my-loader.ts",
  },
};

module.exports = nextConfig;
```

Bu özel yükleyici, görüntülerin uzak bir kaynaktan nasıl alınacağını tanımlayacaktır. Örneğin, aşağıdaki yükleyici Cloudinary için URL oluşturacaktır:

```ts
// my-loader.ts
export default function cloudinaryLoader({
  src,
  width,
  quality,
}: {
  src: string;
  width: number;
  quality?: number;
}) {
  const params = ["f_auto", "c_limit", `w_${width}`, `q_${quality || "auto"}`];
  return `https://res.cloudinary.com/demo/image/upload/${params.join(
    ","
  )}${src}`;
}
```

Daha sonra uygulamanızda `next/image` öğesini kullanarak Cloudinary'deki görüntüye göreli yollar tanımlayabilirsiniz:

```tsx
// app/page.tsx
import Image from "next/image";

export default function Page() {
  return <Image alt="turtles" src="/turtles.jpg" width={300} height={300} />;
}
```

### Rota İşleyicileri

Rota İşleyicileri `next build` çalıştırırken statik bir yanıt oluşturacaktır. Yalnızca `GET` HTTP fiili desteklenir. Bu, önbelleğe alınmış veya önbelleğe alınmamış verilerden statik HTML, JSON, TXT veya diğer dosyaları oluşturmak için kullanılabilir. Örneğin:

```js
// app/data.json/route.ts
import { NextResponse } from "next/server";

export async function GET() {
  return NextResponse.json({ name: "Lee" });
}
```

Yukarıdaki `app/data.json/route.ts` dosyası `next build` sırasında statik bir dosyaya dönüştürülecek ve `{ name: 'Lee' }` içeren `data.json` dosyası oluşturulacaktır.

Gelen istekten dinamik değerleri okumanız gerekiyorsa, statik bir dışa aktarma kullanamazsınız.

### Tarayıcı API'leri

İstemci Bileşenleri `next build` sırasında HTML'ye önceden oluşturulur. `window`, `localStorage` ve `navigator` gibi [Web API](https://developer.mozilla.org/en-US/docs/Web/API)'leri sunucuda bulunmadığından, bu API'lere yalnızca tarayıcıda çalışırken güvenli bir şekilde erişmeniz gerekir. Örneğin:

```tsx
'use client';

import { useEffect } from 'react';

export default function ClientComponent() {
  useEffect(() => {
    // You now have access to `window`
    console.log(window.innerHeight);
  }, [])

  return ...;
}
```

## Desteklenmeyen Özellikler

Node.js sunucusu gerektiren özellikler veya derleme işlemi sırasında hesaplanamayan dinamik mantık desteklenmez:

- dynamicParams ile `dynamicParams: true`
- `generateStaticParams()` olmadan Dinamik Rotalar
- İstek'e dayanan Rota İşleyicileri
- Çerezler
- Yeniden Yazma
- Yönlendirmeler
- Başlıklar
- Orta Yazılım
- Artımlı Statik Rejenerasyon
- Varsayılan `loader` ile Görüntü Optimizasyonu
- Taslak Modu

Bu özelliklerden herhangi birinin `next dev` ile kullanılmaya çalışılması, kök düzende `dynamic` seçeneğinin `error` olarak ayarlanmasına benzer şekilde bir hatayla sonuçlanacaktır.

```js
export const dynamic = "error";
```

## Dağıtım (Deploying)

Statik bir dışa aktarma ile Next.js, HTML/CSS/JS statik varlıkları sunabilen herhangi bir web sunucusunda dağıtılabilir ve barındırılabilir.

Next.js, `next build` çalıştırırken statik dışa aktarımı `out` klasörüne oluşturur. Artık `next export` kullanmaya gerek yoktur. Örneğin, aşağıdaki rotalara sahip olduğunuzu varsayalım:

- `/`
- `/blog/[id]`

Next.js, `next build` çalıştırdıktan sonra aşağıdaki dosyaları oluşturacaktır:

- `/out/index.html`
- `/out/404.html`
- `/out/blog/post-1.html`
- `/out/blog/post-2.html`

Nginx gibi statik bir ana bilgisayar kullanıyorsanız, gelen isteklerden doğru dosyalara yeniden yazmaları yapılandırabilirsiniz:

```nginx
# nginx.conf
server {
  listen 80;
  server_name acme.com;

  root /var/www/out;

  location / {
      try_files $uri $uri.html $uri/ =404;
  }

  # This is necessary when `trailingSlash: false`.
  # You can omit this when `trailingSlash: true`.
  location /blog/ {
      rewrite ^/blog/(.*)$ /blog/$1.html break;
  }

  error_page 404 /404.html;
  location = /404.html {
      internal;
  }
}
```
