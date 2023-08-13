# Taslak Modu (Draft Mode)

Statik oluşturma, sayfalarınız headless bir CMS'den veri aldığında kullanışlıdır. Ancak, headless CMS'nizde bir taslak yazarken ve taslağı hemen sayfanızda görüntülemek istediğinizde ideal değildir. Next.js'nin bu sayfaları derleme zamanı yerine istek zamanında oluşturmasını ve yayınlanan içerik yerine taslak içeriği getirmesini istersiniz. Next.js'in yalnızca bu özel durum için dinamik oluşturmaya geçmesini istersiniz.

Next.js, bu sorunu çözen Taslak Modu adlı bir özelliğe sahiptir. İşte nasıl kullanılacağına dair talimatlar.

## Adım 1: Rota İşleyiciyi oluşturun ve erişin (Create and access the route handler)

İlk olarak, bir Rota İşleyicisi oluşturun. Herhangi bir isme sahip olabilir - örneğin `app/api/draft/route.ts`

Ardından, `next/headers` öğesinden `draftMode` öğesini içe aktarın ve `enable()` yöntemini çağırın.

```ts
//app/api/draft/route.ts

// taslak modunu etkinleştiren rota işleyicisi
import { draftMode } from "next/headers";

export async function GET(request: Request) {
  draftMode().enable();
  return new Response("Draft mode is enabled");
}
```

Bu, taslak modunu etkinleştirmek için bir çerez ayarlayacaktır. Bu çerezi içeren sonraki istekler, statik olarak oluşturulan sayfaların davranışını değiştirerek Taslak Modunu tetikleyecektir (bu konuda daha sonra daha fazla bilgi verilecektir).

Bunu `/api/draft` adresini ziyaret ederek ve tarayıcınızın geliştirici araçlarına bakarak manuel olarak test edebilirsiniz. `Set-Cookie` yanıt başlığının `__prerender_bypass` adlı bir çerez içerdiğine dikkat edin.

### Headless CMS'nizden güvenli bir şekilde erişme

Pratikte, bu Rota İşleyiciyi headless CMS'nizden güvenli bir şekilde çağırmak istersiniz. Belirli adımlar hangi headless CMS'yi kullandığınıza bağlı olarak değişecektir, ancak burada atabileceğiniz bazı genel adımlar vardır.

Bu adımlar, kullandığınız headless CMS'nin özel taslak URL'leri ayarlamayı desteklediğini varsaymaktadır. Desteklemiyorsa, taslak URL'lerinizi güvence altına almak için bu yöntemi yine de kullanabilirsiniz, ancak taslak URL'yi manuel olarak oluşturmanız ve erişmeniz gerekir.

**İlk olarak**, seçtiğiniz bir token oluşturucuyu kullanarak gizli bir token dizesi oluşturmalısınız. Bu sır yalnızca Next.js uygulamanız ve headless CMS'niz tarafından bilinecektir. Bu sır, CMS'nize erişimi olmayan kişilerin taslak URL'lere erişmesini engeller.

**İkinci olarak**, headless CMS'niz özel taslak URL'lerin ayarlanmasını destekliyorsa, taslak URL olarak aşağıdakileri belirtin. Bu, Rota İşleyicinizin `app/api/draft/route.ts` adresinde bulunduğunu varsayar

```Terminal

https://<siteniz>/api/draft?secret=<token>&slug=<path>
```

- `<siteniz>` dağıtım alanınız olmalıdır.
- `<token>`, oluşturduğunuz gizli belirteç ile değiştirilmelidir.
- `<path>` görüntülemek istediğiniz sayfanın yolu olmalıdır. Eğer `/posts/foo` sayfasını görüntülemek istiyorsanız, `&slug=/posts/foo` kullanmalısınız.

Headless CMS'niz taslak URL'ye bir değişken eklemenize izin verebilir, böylece `<path>` CMS'nin verilerine göre dinamik olarak şu şekilde ayarlanabilir: `&slug=/posts/{entry.fields.slug}`

`Son olarak,` Rota İşleyicide:

- Gizli bilginin eşleşip eşleşmediğini ve `slug` parametresinin var olup olmadığını kontrol edin (yoksa istek başarısız olmalıdır).
- Çerezi ayarlamak için `draftMode.enable()` işlevini çağırın.
- Ardından tarayıcıyı `slug` tarafından belirtilen yola yönlendirin.

```ts
//app/api/draft/route.ts

// secret ve slug ile rota işleyicisi
import { draftMode } from 'next/headers'
import { redirect } from 'next/navigation'

export async function GET(request: İstek) {
// Sorgu dizesi parametrelerini ayrıştır
const { searchParams } = yeni URL(request.url)
const secret = searchParams.get('secret')
const slug = searchParams.get('slug')

// Gizli ve sonraki parametreleri kontrol edin
// Bu sır yalnızca bu rota işleyicisi ve CMS tarafından bilinmelidir
if (secret !== 'MY_SECRET_TOKEN' || !slug) {
return new Response('Invalid token', { status: 401 })
}

// Sağlanan `slug`ın var olup olmadığını kontrol etmek için headless CMS'yi getirin
// getPostBySlug, headless CMS'ye gerekli getirme mantığını uygulayacaktır
const post = await getPostBySlug(slug)

// Eğer slug mevcut değilse taslak modunun etkinleştirilmesini engelleyin
if (!post) {
return new Response('Invalid slug', { status: 401 })
}

// Çerezi ayarlayarak Taslak Modunu etkinleştirin
draftMode().enable()

// Getirilen gönderideki yola yönlendir
// Açık yönlendirme güvenlik açıklarına yol açabileceğinden searchParams.slug adresine yönlendirme yapmıyoruz
redirect(post.slug)
}
```

Başarılı olursa, tarayıcı taslak modu çerezi ile görüntülemek istediğiniz yola yönlendirilecektir.

## Adım 2: Sayfayı güncelleyin

Bir sonraki adım, sayfanızı `draftMode().isEnabled` değerini kontrol edecek şekilde güncellemektir.

Çerezin ayarlandığı bir sayfayı talep ederseniz, veriler istek zamanında (derleme zamanı yerine) getirilecektir.

Ayrıca, `isEnabled` değeri `true` olacaktır.

```ts
//app/page.tsx

// veri getiren sayfa
import { draftMode } from "next/headers";

async function getData() {
  const { isEnabled } = draftMode();

  const url = isEnabled
    ? "https://draft.example.com"
    : "https://production.example.com";

  const res = await fetch(url);

  return res.json();
}

export default async function Page() {
  const { title, desc } = await getData();

  return (
    <main>
      <h1>{title}</h1>
      <p>{desc}</p>
    </main>
  );
}
```

İşte bu kadar! Taslak Rota İşleyicisine (`secret` ve `slug` ile) headless CMS'nizden veya manuel olarak erişirseniz, artık taslak içeriği görebilmeniz gerekir. Ve taslağınızı yayınlamadan güncellerseniz, taslağı görüntüleyebilmeniz gerekir.

Bunu headless CMS'nizde taslak URL'si olarak ayarlayın veya manuel olarak erişin ve taslağı görebilmeniz gerekir.

```terminal
https://<your-site>/api/draft?secret=<token>&slug=<path>
```

## Daha Fazla Detay

### Taslak Modu çerezini temizleyin

Varsayılan olarak, Taslak Modu oturumu tarayıcı kapatıldığında sona erer.

Taslak Modu çerezini manuel olarak temizlemek için `draftMode().disable()` çağrısı yapan bir Rota İşleyicisi oluşturun:

```ts
//app/api/disable-draft/route.ts;

import { draftMode } from "next/headers";

export async function GET(request: İstek) {
  draftMode().disable();
  return new Response("Taslak modu devre dışı");
}
```

Ardından, Rota İşleyiciyi çağırmak için `/api/disable-draft` adresine bir istek gönderin. Bu rotayı `next/link` kullanarak çağırıyorsanız, prefetch'te çerezin yanlışlıkla silinmesini önlemek için `prefetch={false}` değerini geçmelisiniz.

### `next build` için benzersiz

`next build`'i her çalıştırdığınızda yeni bir bypass çerez değeri oluşturulacaktır.

Bu, bypass çerezinin tahmin edilememesini sağlar.

**Bilmekte fayda var:** Taslak Modunu HTTP üzerinden yerel olarak test etmek için tarayıcınızın üçüncü taraf çerezlerine ve yerel depolama erişimine izin vermesi gerekir.
