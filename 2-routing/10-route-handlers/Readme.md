# Rota İşleyicileri (Route Handlers)

Rota İşleyicileri, [Web İsteği](https://developer.mozilla.org/en-US/docs/Web/API/Request) ve [Yanıt API](https://developer.mozilla.org/en-US/docs/Web/API/Response)'lerini kullanarak belirli bir rota için özel istek işleyicileri oluşturmanıza olanak tanır.

<img alt="rota-işleyicileri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-special-file.png&w=3840&q=75&dpl=dpl_6xgH6dmXbqACWDkrZCJqapUPDxaP" /><br/>

Bilmekte fayda var: Rota İşleyicileri yalnızca `app` dizini içinde kullanılabilir. Bunlar, `pages` dizini içindeki API Rotalarına eşdeğerdir, yani API Rotalarını ve Rota İşleyicilerini birlikte kullanmanız **gerekmez**.

## Convention

Rota İşleyicileri, `app` dizini içindeki bir `route.js|ts` dosyasında tanımlanır:

```ts
export async function GET(request: Request) {}
```

Rota İşleyicileri, `page.js` ve `layout.js` dosyalarına benzer şekilde uygulama dizini içinde yuvalanabilir. Ancak `page.js` ile aynı rota segmenti seviyesinde bir `route.js` dosyası olamaz.

### Desteklenen HTTP Yöntemleri

Aşağıdaki [HTTP yöntemleri](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) desteklenmektedir: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD` ve `OPTIONS`. Desteklenmeyen bir yöntem çağrılırsa, Next.js `405 Method Not Allowed` yanıtı döndürür.

### Genişletilmiş NextRequest ve NextResponse API'leri

Yerel [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request) ve [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)'u desteklemenin yanı sıra. Next.js, gelişmiş kullanım durumları için uygun yardımcılar sağlamak üzere bunları `NextRequest` ve `NextResponse` ile genişletir.

## Davranış

### Statik Rota İşleyicileri

`Response` nesnesi ile `GET` yöntemi kullanıldığında Rota İşleyicileri varsayılan olarak statik olarak değerlendirilir.

```ts
import { NextResponse } from "next/server";

export async function GET() {
  const res = await fetch("https://data.mongodb-api.com/...", {
    headers: {
      "Content-Type": "application/json",
      "API-Key": process.env.DATA_API_KEY,
    },
  });
  const data = await res.json();

  return NextResponse.json({ data });
}
```

**TypeScript Uyarısı:** `Response.json()` geçerli olmasına rağmen, yerel TypeScript türleri şu anda bir hata gösteriyor, bunun yerine tipli yanıtlar için `NextResponse.json()` kullanabilirsiniz.

### Dinamik Rota İşleyicileri

Rota işleyicileri şu durumlarda dinamik olarak değerlendirilir:

- `Request` nesnesini `GET` yöntemiyle kullanma.
- Diğer HTTP yöntemlerinden herhangi birini kullanma.
- `cookies` ve `headers` gibi Dinamik İşlevlerin kullanılması.
- Segment Yapılandırma Seçenekleri dinamik modu manuel olarak belirtir.

Örneğin:

```ts
import { NextResponse } from "next/server";

export async function GET(request: Request) {
  const { searchParams } = new URL(request.url);
  const id = searchParams.get("id");
  const res = await fetch(`https://data.mongodb-api.com/product/${id}`, {
    headers: {
      "Content-Type": "application/json",
      "API-Key": process.env.DATA_API_KEY,
    },
  });
  const product = await res.json();

  return NextResponse.json({ product });
}
```

Benzer şekilde, `POST` yöntemi Rota İşleyicisinin dinamik olarak değerlendirilmesine neden olur.

```ts
import { NextResponse } from "next/server";

export async function POST() {
  const res = await fetch("https://data.mongodb-api.com/...", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "API-Key": process.env.DATA_API_KEY,
    },
    body: JSON.stringify({ time: new Date().toISOString() }),
  });

  const data = await res.json();

  return NextResponse.json(data);
}
```

**_Bilmekte fayda var:_** Önceden, API Rotaları form gönderimlerinin işlenmesi gibi kullanım durumları için kullanılabiliyordu. Rota İşleyicileri muhtemelen bu kullanım durumları için çözüm değildir. Hazır olduğunda bunun için mutasyonların kullanılmasını önereceğiz.

## Rota Çözümü (Route Resolution)

Bir `rotayı` en düşük seviyeli yönlendirme ilkeli olarak düşünebilirsiniz.

- Sayfa gibi düzenlere veya istemci tarafı gezinmelerine katılmazlar.
- page.js ile aynı rotada bir route.js dosyası olamaz.

| Page                 | Route              | Sonuç    |
| -------------------- | ------------------ | -------- |
| `app/page.js`        | `app/route.js`     | Geçersiz |
| `app/page.js`        | `app/api/route.js` | Geçerli  |
| `app/[user]/page.js` | `app/api/route.js` | Geçerli  |

```ts
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}

// ❌ Geçersiz
// `app/route.js`
export async function POST(request) {}
```

## Örnekler

Aşağıdaki örnekler, Route Handlers'ın diğer Next.js API'leri ve özellikleriyle nasıl birleştirileceğini göstermektedir.

### Statik Verileri Yeniden Doğrulama (Revalidating Static Data)

`next.revalidate` seçeneğini kullanarak statik veri getirme işlemlerini yeniden doğrulayabilirsiniz:

```ts
import { NextResponse } from "next/server";

export async function GET() {
  const res = await fetch("https://data.mongodb-api.com/...", {
    next: { revalidate: 60 }, // Revalidate every 60 seconds
  });
  const data = await res.json();

  return NextResponse.json(data);
}
```

Alternatif olarak, `revalidate` segment config seçeneğini kullanabilirsiniz:

```js
export const revalidate = 60;
```

## Dinamik Fonksiyonlar (Dynamic Functions)

Route Handlers, Next.js'deki `cookies` ve `headers` gibi dinamik işlevlerle kullanılabilir.

### Çerezler (Cookies)

Çerezleri `next/headers`'dan çerezlerle okuyabilirsiniz. Bu sunucu işlevi doğrudan bir Route Handler'da çağrılabilir veya başka bir işlevin içine yerleştirilebilir.

Bu `çerez` örneği salt okunurdur. Çerezleri ayarlamak için [Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) başlığını kullanarak yeni bir `Response` döndürmeniz gerekir.

```ts
import { cookies } from "next/headers";

export async function GET(request: Request) {
  const cookieStore = cookies();
  const token = cookieStore.get("token");

  return new Response("Hello, Next.js!", {
    status: 200,
    headers: { "Set-Cookie": `token=${token}` },
  });
}
```

Alternatif olarak, çerezleri okumak için temel Web API'lerinin üstündeki soyutlamaları kullanabilirsiniz (`NextRequest`):

```ts
import { type NextRequest } from "next/server";

export async function GET(request: NextRequest) {
  const token = request.cookies.get("token");
}
```

### Başlıklar (Headers)

Başlıkları `next/headers` içinden okuyabilirsiniz. Bu sunucu fonksiyonu doğrudan bir Route Handler içinde çağrılabilir veya başka bir fonksiyonun içine yerleştirilebilir.

Bu `headers` örneği salt okunurdur. Başlıkları ayarlamak için, yeni başlıklarla yeni bir `response` döndürmeniz gerekir.

```ts
import { headers } from "next/headers";

export async function GET(request: Request) {
  const headersList = headers();
  const referer = headersList.get("referer");

  return new Response("Hello, Next.js!", {
    status: 200,
    headers: { referer: referer },
  });
}
```

Alternatif olarak, başlıkları okumak için altta yatan Web API'lerinin üstündeki soyutlamaları kullanabilirsiniz (`NextRequest`):

```ts
import { type NextRequest } from "next/server";

export async function GET(request: NextRequest) {
  const requestHeaders = new Headers(request.headers);
}
```

### Yönlendirmeler (Redirects)

```ts
import { redirect } from "next/navigation";

export async function GET(request: Request) {
  redirect("https://nextjs.org/");
}
```

### Dinamik Rota Segmentleri (Dynamic Route Segments)

Rota İşleyicileri, dinamik verilerden istek işleyicileri oluşturmak için Dinamik Segmentleri kullanabilir.

```ts
export async function GET(
  request: Request,
  { params }: { params: { slug: string } }
) {
  const slug = params.slug; // 'a', 'b', or 'c'
}
```

| Rota (Route)                | Örnek URL  | Params          |
| --------------------------- | ---------- | --------------- |
| `app/items/[slug]/route.js` | `/items/a` | `{ slug: 'a' }` |
| `app/items/[slug]/route.js` | `/items/b` | `{ slug: 'b' }` |
| `app/items/[slug]/route.js` | `/items/c` | `{ slug: 'c' }` |

### Akış (Streaming)

Akış, yapay zeka tarafından oluşturulan içerik için OpenAI gibi Büyük Dil Modelleri (LLM'ler) ile birlikte yaygın olarak kullanılır. [AI SDK](https://sdk.vercel.ai/docs) hakkında daha fazla bilgi edinin.

```ts
import { Configuration, OpenAIApi } from "openai-edge";
import { OpenAIStream, StreamingTextResponse } from "ai";

const config = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
});
const openai = new OpenAIApi(config);

export const runtime = "edge";

export async function POST(req: Request) {
  const { prompt } = await req.json();
  const response = await openai.createCompletion({
    model: "text-davinci-003",
    stream: true,
    temperature: 0.6,
    prompt: "What is Next.js?",
  });

  const stream = OpenAIStream(response);
  return new StreamingTextResponse(stream);
}
```

Bu soyutlamalar bir akış oluşturmak için Web API'lerini kullanır. Temel Web API'lerini doğrudan da kullanabilirsiniz.

```ts
// https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream#convert_async_iterator_to_stream
function iteratorToStream(iterator: any) {
  return new ReadableStream({
    async pull(controller) {
      const { value, done } = await iterator.next();

      if (done) {
        controller.close();
      } else {
        controller.enqueue(value);
      }
    },
  });
}

function sleep(time: number) {
  return new Promise((resolve) => {
    setTimeout(resolve, time);
  });
}

const encoder = new TextEncoder();

async function* makeIterator() {
  yield encoder.encode("<p>One</p>");
  await sleep(200);
  yield encoder.encode("<p>Two</p>");
  await sleep(200);
  yield encoder.encode("<p>Three</p>");
}

export async function GET() {
  const iterator = makeIterator();
  const stream = iteratorToStream(iterator);

  return new Response(stream);
}
```

### Talep Gövdesi

Standart Web API yöntemlerini kullanarak `request` gövdesini okuyabilirsiniz:

```ts
import { NextResponse } from "next/server";

export async function POST(request: Request) {
  const res = await request.json();
  return NextResponse.json({ res });
}
```

### CORS

Standart Web API yöntemlerini kullanarak bir `response` üzerinde CORS başlıklarını ayarlayabilirsiniz:

```ts
export async function GET(request: Request) {
  return new Response("Hello, Next.js!", {
    status: 200,
    headers: {
      "Access-Control-Allow-Origin": "*",
      "Access-Control-Allow-Methods": "GET, POST, PUT, DELETE, OPTIONS",
      "Access-Control-Allow-Headers": "Content-Type, Authorization",
    },
  });
}
```

## Edge ve Node.js Çalışma Zamanları

Route Handlers, akış desteği de dahil olmak üzere hem Edge hem de Node.js çalışma zamanlarını sorunsuz bir şekilde desteklemek için izomorfik bir Web API'sine sahiptir. Rota İşleyicileri, Sayfalar ve Düzenlerle aynı rota segmenti yapılandırmasını kullandığından, genel amaçlı statik olarak yeniden oluşturulan Rota İşleyicileri gibi uzun zamandır beklenen özellikleri destekler.

Çalışma zamanını belirtmek için `runtime` segment config seçeneğini kullanabilirsiniz:

```ts
export const runtime = "edge"; // 'nodejs' varsayılandır.
```

## UI Dışı Yanıtlar

Kullanıcı arayüzü olmayan içeriği döndürmek için Rota İşleyicileri kullanabilirsiniz. `Sitemap.xml`, `robots.txt`, uygulama simgeleri ve açık grafik görüntülerinin tümünün yerleşik desteğe sahip olduğunu unutmayın.

```ts
export async function GET() {
  return new Response(`<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
 
<channel>
  <title>Next.js Documentation</title>
  <link>https://nextjs.org/docs</link>
  <description>The React Framework for the Web</description>
</channel>
 
</rss>`);
}
```

## Segment Yapılandırma Seçenekleri

Rota İşleyicileri, sayfalar ve düzenlerle aynı rota segmenti yapılandırmasını kullanır.

```ts
export const dynamic = "auto";
export const dynamicParams = true;
export const revalidate = false;
export const fetchCache = "auto";
export const runtime = "nodejs";
export const preferredRegion = "auto";
```
