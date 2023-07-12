# Verileri Yeniden Doğrulama (Revalidating)

Next.js, sitenizin tamamını yeniden oluşturmanıza gerek kalmadan belirli statik rotaları güncellemenizi sağlar. Revalidation (Incremental Static Regeneration olarak da bilinir), milyonlarca sayfaya ölçeklenirken statik avantajlarını korumanıza olanak tanır.

Next.js'de iki tür yeniden doğrulama vardır:

- **Arka plan:** Verileri belirli bir zaman aralığında yeniden doğrular.
- **İsteğe bağlı:** Güncelleme gibi bir olaya bağlı olarak verileri yeniden doğrular.

## Arka Plan Revalidasyonu (Background Revalidation)

Önbelleğe alınan verileri belirli bir aralıkta yeniden doğrulamak için `fetch()` işlevinde `next.revalidate` seçeneğini kullanarak bir kaynağın önbellek ömrünü (saniye cinsinden) ayarlayabilirsiniz.

```js
fetch("https://...", { next: { revalidate: 60 } });
```
