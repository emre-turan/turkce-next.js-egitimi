# OpenTelemetry

**Bilmekte fayda var:** Bu özellik deneyseldir, `next.config.js` dosyanızda `experimental.instrumentationHook = true;` sağlayarak açıkça katılmanız gerekir.

Next.js uygulamanızın davranışını ve performansını anlamak ve optimize etmek için gözlemlenebilirlik çok önemlidir.

Uygulamalar daha karmaşık hale geldikçe, ortaya çıkabilecek sorunları belirlemek ve teşhis etmek giderek zorlaşmaktadır. Geliştiriciler, günlük kaydı ve metrikler gibi gözlemlenebilirlik araçlarından yararlanarak uygulamalarının davranışları hakkında içgörü kazanabilir ve optimizasyon alanlarını belirleyebilir. Gözlemlenebilirlik sayesinde, geliştiriciler sorunları büyük sorunlara dönüşmeden önce proaktif olarak ele alabilir ve daha iyi bir kullanıcı deneyimi sağlayabilir. Bu nedenle, performansı artırmak, kaynakları optimize etmek ve kullanıcı deneyimini geliştirmek için Next.js uygulamalarınızda gözlemlenebilirliği kullanmanız şiddetle tavsiye edilir.

Uygulamalarınızı enstrümante etmek için OpenTelemetry kullanmanızı öneririz. Bu, kodunuzu değiştirmeden gözlemlenebilirlik sağlayıcınızı değiştirmenize olanak tanıyan, uygulamaları enstrümante etmenin platformdan bağımsız bir yoludur. OpenTelemetry ve nasıl çalıştığı hakkında daha fazla bilgi için Resmi [OpenTelemetry](https://opentelemetry.io/docs/) dokümanlarını okuyun.

Bu dokümanda _Span, Trace veya Exporter_ gibi terimler kullanılmaktadır, bunların hepsi [OpenTelemetry Observability Primer](https://opentelemetry.io/docs/concepts/observability-primer/)'da bulunabilir.

Next.js, OpenTelemetry enstrümantasyonunu kutudan çıkar çıkmaz destekler, bu da Next.js'nin kendisini zaten enstrümante ettiğimiz anlamına gelir. OpenTelemetry'yi etkinleştirdiğinizde `getStaticProps` gibi tüm kodlarınızı otomatik olarak yararlı niteliklere sahip span'lara saracağız.

Bilmekte fayda var: Şu anda OpenTelemetry bağlamalarını yalnızca sunucusuz işlevlerde destekliyoruz. `edge` veya istemci tarafı kodu için herhangi bir destek sağlamıyoruz.

## Başlarken

OpenTelemetry genişletilebilir ancak düzgün bir şekilde kurmak oldukça ayrıntılı olabilir. Bu yüzden hızlı bir şekilde başlamanıza yardımcı olacak `@vercel/otel` paketini hazırladık. Genişletilebilir değildir ve kurulumunuzu özelleştirmeniz gerekiyorsa OpenTelemetry'yi manuel olarak yapılandırmalısınız.

### `@vercel/otel`'i kullanma

Başlamak için `@vercel/otel`'i yüklemeniz gerekir:

```bash
npm install @vercel/otel
```

Ardından, projenin kök dizininde (veya kullanıyorsanız `src` klasörünün içinde) özel bir `instrumentation.ts` (veya `.js`) dosyası oluşturun:

```ts
// your-project/instrumentation.ts

import { registerOTel } from "@vercel/otel";

export function register() {
  registerOTel("next-app");
}
```

**Bilmekte fayda var:**

- `instrumentation` dosyası, `app` veya `pages` dizininin içinde değil, projenizin kök dizininde olmalıdır. Eğer `src` klasörünü kullanıyorsanız, dosyayı `pages` ve `app` ile birlikte `src` içine yerleştirin.
- Bir son ek eklemek için [`pageExtensions yapılandırma seçeneğini`](https://nextjs.org/docs/app/api-reference/next-config-js/pageExtensions) kullanırsanız, `instrumentation` dosya adını da eşleşecek şekilde güncellemeniz gerekecektir.
- Kullanabileceğiniz temel bir [with-opentelemetry](https://github.com/vercel/next.js/tree/canary/examples/with-opentelemetry) örneği oluşturduk.

### Manuel OpenTelemetry yapılandırması

Sarmalayıcımız `@vercel/otel` ihtiyaçlarınızı karşılamıyorsa, OpenTelemetry'yi manuel olarak yapılandırabilirsiniz.

Öncelikle OpenTelemetry paketlerini yüklemeniz gerekir:

```bash
npm install @opentelemetry/sdk-node @opentelemetry/resources @opentelemetry/semantic-conventions @opentelemetry/sdk-trace-node @opentelemetry/exporter-trace-otlp-http
```

Artık `NodeSDK`'yı `instrumentation.ts` dosyanızda başlatabilirsiniz. OpenTelemetry API'leri edge çalışma zamanı ile uyumlu değildir, bu nedenle bunları yalnızca `process.env.NEXT_RUNTIME === 'nodejs'` olduğunda içe aktardığınızdan emin olmanız gerekir. Yalnızca node kullanırken koşullu olarak içe aktardığınız yeni bir `instrumentation.node.ts` dosyası oluşturmanızı öneririz:

```ts
// instrumentation.ts

export async function register() {
  if (process.env.NEXT_RUNTIME === "nodejs") {
    await import("./instrumentation.node.ts");
  }
}
```

```ts
// instrumentation.node.ts

import { NodeSDK } from "@opentelemetry/sdk-node";
import { OTLPTraceExporter } from "@opentelemetry/exporter-trace-otlp-http";
import { Resource } from "@opentelemetry/resources";
import { SemanticResourceAttributes } from "@opentelemetry/semantic-conventions";
import { SimpleSpanProcessor } from "@opentelemetry/sdk-trace-node";

const sdk = new NodeSDK({
  resource: new Resource({
    [SemanticResourceAttributes.SERVICE_NAME]: "next-app",
  }),
  spanProcessor: new SimpleSpanProcessor(new OTLPTraceExporter()),
});
sdk.start();
```

Bunu yapmak `@vercel/otel` kullanmakla eşdeğerdir, ancak değiştirmek ve genişletmek mümkündür. Örneğin, `@opentelemetry/exporter-trace-otlp-http` yerine `@opentelemetry/exporter-trace-otlp-grpc` kullanabilir veya daha fazla kaynak özniteliği belirtebilirsiniz.

## Enstrümantasyonunuzu test etme (Testing your instrumentation)

OpenTelemetry izlerini yerel olarak test etmek için uyumlu bir arka uca sahip bir OpenTelemetry toplayıcısına ihtiyacınız vardır. [OpenTelemetry geliştirme ortamımızı](https://github.com/vercel/opentelemetry-collector-dev-setup) kullanmanızı öneririz.

Her şey yolunda giderse `GET /requested/pathname` olarak etiketlenmiş kök sunucu aralığını görebilmeniz gerekir. Söz konusu izlemeye ait diğer tüm yayılımlar bunun altında iç içe geçecektir.

Next.js varsayılan olarak yayılandan daha fazla aralığı izler. Daha fazla aralık görmek için `NEXT_OTEL_VERBOSE=1` olarak ayarlamalısınız.

## Deployment

### OpenTelemetry Collector Kullanımı

OpenTelemetry Collector ile dağıtım yaparken `@vercel/otel` adresini kullanabilirsiniz. Hem Vercel'de hem de kendi kendine barındırıldığında çalışacaktır.

#### Vercel üzerinde deploy etme

OpenTelemetry'nin Vercel'de kutudan çıktığı gibi çalıştığından emin olduk.

Projenizi bir gözlemlenebilirlik sağlayıcısına bağlamak için [Vercel belgelerini](https://vercel.com/docs/concepts/observability/otel-overview/quickstart) izleyin.

#### Kendi kendine barındırma (Self-hosting)

Diğer platformlara dağıtmak da kolaydır. Next.js uygulamanızdan telemetri verilerini almak ve işlemek için kendi OpenTelemetry Collector'ınızı kurmanız gerekecektir.

Bunu yapmak için, toplayıcıyı kurma ve Next.js uygulamanızdan veri alacak şekilde yapılandırma konusunda size yol gösterecek olan [OpenTelemetry Collector Getting Started](https://opentelemetry.io/docs/collector/getting-started/) kılavuzunu izleyin.

Toplayıcınızı kurup çalıştırdıktan sonra, Next.js uygulamanızı ilgili dağıtım kılavuzlarını izleyerek seçtiğiniz platforma dağıtabilirsiniz.

### Özel Dışa Aktarıcılar (Custom Exporters)

OpenTelemetry Collector kullanmanızı öneririz. Platformunuzda bu mümkün değilse, [manuel OpenTelemetry yapılandırması](https://nextjs.org/docs/pages/building-your-application/optimizing/open-telemetry#manual-opentelemetry-configuration) ile özel bir OpenTelemetry dışa aktarıcısı kullanabilirsiniz.

## Özel aralıklar (Custom Spans)

[OpenTelemetry API](https://opentelemetry.io/docs/instrumentation/js/instrumentation)'leri ile özel bir aralık ekleyebilirsiniz.

```bash
npm install @opentelemetry/api
```

Aşağıdaki örnekte GitHub yıldızlarını getiren ve getirme isteğinin sonucunu izlemek için özel bir `fetchGithubStars` aralığı ekleyen bir işlev gösterilmektedir:

```ts
import { trace } from "@opentelemetry/api";

export async function fetchGithubStars() {
  return await trace
    .getTracer("nextjs-example")
    .startActiveSpan("fetchGithubStars", async (span) => {
      try {
        return await getValue();
      } finally {
        span.end();
      }
    });
}
```

`register` fonksiyonu, kodunuz yeni bir ortamda çalışmadan önce yürütülecektir. Yeni açıklıklar oluşturmaya başlayabilirsiniz ve bunlar dışa aktarılan izlemeye doğru şekilde eklenmelidir.

## Next.js'de Varsayılan Aralıklar (Default Spans in Next.js)

Next.js, uygulamanızın performansı hakkında yararlı bilgiler sağlamak için otomatik olarak çeşitli aralıklar ayarlar.

Açıklıklardaki öznitelikler [OpenTelemetry semantik kurallarını](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/) takip eder. Ayrıca `next` ad alanı altında bazı özel öznitelikler ekliyoruz:

- `next.span_name` - yayılma adını çoğaltır
- `next.span_type` - her span türünün benzersiz bir tanımlayıcısı vardır
- `next.route` - İsteğin rota kalıbı (örneğin, `/[param]/user`).
- `next.page`
  - Bu, bir uygulama yönlendiricisi tarafından kullanılan dahili bir değerdir.
  - Bunu özel bir dosyaya giden bir yol olarak düşünebilirsiniz (`page.ts`, `layout.ts`, `loading.ts` ve diğerleri gibi)
  - Yalnızca `next.route` ile eşleştirildiğinde benzersiz bir tanımlayıcı olarak kullanılabilir çünkü `/layout` hem `/(groupA)/layout.ts` hem de `/(groupB)/layout.ts` dosyalarını tanımlamak için kullanılabilir

### `[http.method] [next.route]`

- `next.span_type`: `BaseServer.handleRequest`

Bu span, Next.js uygulamanıza gelen her istek için kök spanı temsil eder. İsteğin HTTP yöntemini, rotasını, hedefini ve durum kodunu izler.

Nitelikler:

- [Ortak HTTP öznitelikleri](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/http/#common-attributes)
  - `http.method`
  - `http.status_code`
- [Sunucu HTTP öznitelikleri](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/http/#http-server-semantic-conventions)
  - `http.route`
  - `http.target`
- `next.span_name`
- `next.span_type`
- `next.route`

### `render route (app) [next.route]`

- `next.span_type`: `AppRender.getBodyResult`.

Bu span, uygulama yönlendiricisinde bir rota oluşturma işlemini temsil eder.

Nitelikler:

- `next.span_name`
- `next.span_type`
- `next.route`

### `fetch [http.method] [http.url]`

- `next.span_type`: `AppRender.fetch`

Bu aralık, kodunuzda yürütülen getirme isteğini temsil eder.

Nitelikler:

- [Ortak HTTP öznitelikleri](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/http/#common-attributes)

  - `http.method`

- [İstemci HTTP öznitelikleri](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/http/#http-client)
  - `http.url`
  - `net.peer.name`
  - `net.peer.port` (yalnızca belirtilmişse)
- `next.span_name`
- `next.span_type`

### `executing api route (app) [next.route]`

- `next.span_type`: `AppRouteRouteHandlers.runHandler`.

Bu span, uygulama yönlendiricisinde bir API rota işleyicisinin yürütülmesini temsil eder.

Nitelikler:

- `next.span_name`
- `next.span_type`
- `next.route`

### `getStaticProps [next.route]`

- `next.span_type`: `Render.getStaticProps`.

Bu span, belirli bir rota için `getStaticProps`'un yürütülmesini temsil eder.

Nitelikler:

- `next.span_name`
- `next.span_type`
- `next.route`

### `render route (pages) [next.route]`

- `next.span_type`: `Render.renderDocument`.

Bu span, belirli bir rota için belge oluşturma işlemini temsil eder.

Nitelikler:

- `next.span_name`
- `next.span_type`
- `next.route`

### `generateMetadata [next.page]`

- `next.span_type`: `ResolveMetadata.generateMetadata`.

Bu span, belirli bir sayfa için meta veri oluşturma sürecini temsil eder (tek bir rota bu span'lardan birden fazlasına sahip olabilir).

Nitelikler:

- `next.span_name`
- `next.span_type`
- `next.page`
