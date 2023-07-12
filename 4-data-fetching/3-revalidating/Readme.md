# Verileri Yeniden Doğrulama (Revalidating)

Next.js, sitenizin tamamını yeniden oluşturmanıza gerek kalmadan belirli statik rotaları güncellemenizi sağlar. Revalidation (Incremental Static Regeneration olarak da bilinir), milyonlarca sayfaya ölçeklenirken statik avantajlarını korumanıza olanak tanır.

Next.js'de iki tür yeniden doğrulama vardır:

- **Arka plan:** Verileri belirli bir zaman aralığında yeniden doğrular.
- **İsteğe bağlı:** Güncelleme gibi bir olaya bağlı olarak verileri yeniden doğrular.

## Arka Plan Revalidasyonu (Background Revalidation)

Önbelleğe alınan verileri belirli bir aralıkta yeniden doğrulamak için `fetch()` işlevinde `next.revalidate` seçeneğini kullanarak bir kaynağın `cache` ömrünü (saniye cinsinden) ayarlayabilirsiniz.

```ts
fetch("https://...", { next: { revalidate: 60 } });
```

`fetch` kullanmayan verileri yeniden doğrulamak istiyorsanız (yani harici bir paket veya sorgu oluşturucu kullanarak), rota segmenti yapılandırmasını kullanabilirsiniz.

```ts
export const revalidate = 60; // bu sayfayı her 60 saniyede bir yeniden doğrula
```

### Nasıl çalışır?

1. Derleme sırasında statik olarak işlenmiş olan rotaya bir istek yapıldığında, başlangıçta önbelleğe alınmış veriler gösterilir.
2. İlk istekten sonra ve 60 saniyeden önce rotaya yapılan tüm istekler de önbelleğe alınır ve anlık olarak gösterilir.
3. 60 saniyelik pencereden sonra, bir sonraki istek hala önbelleğe alınmış (eski) verileri gösterecektir.
4. Next.js arka planda verilerin yenilenmesini tetikleyecektir.
5. Rota başarıyla oluşturulduktan sonra Next.js önbelleği geçersiz kılacak ve güncellenmiş rotayı gösterecektir. Arka planda yenileme başarısız olursa, eski veriler hala değiştirilmemiş olacaktır.

Oluşturulmamış bir rota segmentine bir istek yapıldığında, Next.js ilk istekte rotayı dinamik olarak oluşturacaktır. Daha sonraki istekler önbellekten statik rota segmentlerini sunacaktır.

**Bilmekte fayda var:** Yukarı akış veri sağlayıcınızda önbelleğin varsayılan olarak etkin olup olmadığını kontrol edin. Devre dışı bırakmanız gerekebilir (örn. `useCdn: false`), aksi takdirde bir yeniden doğrulama ISR önbelleğini güncellemek için yeni verileri çekemez. Önbellekleme, `Cache-Control` başlığını döndürdüğünde bir CDN'de (talep edilen bir uç nokta için) gerçekleşebilir. Vercel üzerindeki [ISR önbelleği global olarak sürdürür ve geri alma işlemlerini](https://vercel.com/docs/concepts/incremental-static-regeneration/overview) gerçekleştirir.

## İsteğe Bağlı Yeniden Doğrulama (On-Demand Revalidation)

`revalidate` süresini `60` olarak ayarlarsanız, tüm ziyaretçiler sitenizin oluşturulan aynı sürümünü bir dakika boyunca görür. Önbelleği geçersiz kılmanın tek yolu, bir dakika geçtikten sonra birinin sayfayı ziyaret etmesidir.

Next.js Uygulama Yönlendiricisi, bir rota veya önbellek etiketine dayalı olarak içeriğin isteğe bağlı olarak yeniden doğrulanmasını destekler. Bu, belirli getirmeler için Next.js önbelleğini manuel olarak temizlemenize olanak tanıyarak sitenizi ne zaman güncelleyeceğinizi kolaylaştırır:

- Başlıksız CMS'nizden içerik oluşturulur veya güncellenir.
- E-ticaret meta verileri değişir (fiyat, açıklama, kategori, yorumlar vb.).

## İsteğe Bağlı Yeniden Doğrulama Kullanımı (Using On-Demand Revalidation)

Veriler isteğe bağlı olarak yola (`revalidatePath`) veya önbellek etiketine (`revalidateTag`) göre yeniden doğrulanabilir.

Örneğin, aşağıdaki `fetch` işlemi önbellek etiket `koleksiyonunu` ekler:

```ts
export default async function Page() {
  const res = await fetch("https://...", { next: { tags: ["collection"] } });
  const data = await res.json();
  // ...
}
```

Önbelleğe alınan bu veriler daha sonra bir Rota İşleyicide `revalidateTag` çağrısı yapılarak talep üzerine yeniden doğrulanabilir.

```ts
import { NextRequest, NextResponse } from "next/server";
import { revalidateTag } from "next/cache";

export async function GET(request: NextRequest) {
  const tag = request.nextUrl.searchParams.get("tag");
  revalidateTag(tag);
  return NextResponse.json({ revalidated: true, now: Date.now() });
}
```

## Hata İşleme ve Yeniden Doğrulama

Verileri yeniden doğrulamaya çalışırken bir hata atılırsa, başarıyla oluşturulan son veriler önbellekten sunulmaya devam eder. Sonraki bir sonraki istekte, Next.js verileri yeniden doğrulamayı yeniden deneyecektir.
