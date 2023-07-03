# Statik ve Dinamik Render Etme (Static and Dynamic Rendering)

Next.js'de bir rota statik veya dinamik olarak render edilebilir.

- Statik bir rotada, bileşenler derleme zamanında sunucuda render edilir. Çalışmanın sonucu önbelleğe alınır ve sonraki isteklerde yeniden kullanılır.
- Dinamik bir rotada, bileşenler istek zamanında sunucuda render edilir.

## Statik Render Etme (Varsayılan)

Varsayılan olarak Next.js, performansı artırmak için rotaları statik olarak render eder. Bu, tüm işleme işinin önceden yapıldığı ve kullanıcıya coğrafi olarak daha yakın bir İçerik Dağıtım Ağı'ndan (CDN) sunulabileceği anlamına gelir.

## Statik Veri Getirme (Varsayılan)

Next.js varsayılan olarak, önbelleğe alma davranışını özellikle devre dışı bırakmayan `fetch()` isteklerinin sonucunu önbelleğe alacaktır. Bu, bir `cache` seçeneği belirlemeyen fetch isteklerinin `force-cache` seçeneğini kullanacağı anlamına gelir.

Rotadaki herhangi bir getirme isteği `revalidate` seçeneğini kullanırsa, rota revalidation sırasında statik olarak yeniden render edilir.

## Dinamik Render Etme

Statik render etme sırasında, dinamik bir işlev veya dinamik bir `fetch()` isteği (no caching) keşfedilirse, Next.js istek anında tüm rotayı dinamik olarak render etmeye geçecektir. Önbelleğe alınan tüm veri istekleri dinamik render etme sırasında yeniden kullanılabilir.

Bu tablo, dinamik işlevlerin ve önbelleğe almanın bir rotanın render etme davranışını nasıl etkilediğini özetlemektedir:

| Data Fetching   | Dinamik Fonksiyonlar | Render Etme |
| --------------- | -------------------- | ----------- |
| Statik (Cached) | Hayır                | Statik      |
| Statik (Cached) | Evet                 | Dinamik     |
| Not Cached      | Hayır                | Dinamik     |
| Not Cached      | Evet                 | Dinamik     |

Veri getirmenin önbelleğe alınıp alınmadığına bakılmaksızın, dinamik işlevlerin rotayı her zaman dinamik görüntülemeye nasıl tercih ettiğine dikkat edin. Başka bir deyişle, statik render etme yalnızca veri getirme davranışına değil, aynı zamanda rotada kullanılan dinamik işlevlere de bağlıdır.

Bilmekte fayda var: Gelecekte Next.js, bir rotadaki düzenlerin ve sayfaların tüm rota yerine bağımsız olarak statik veya dinamik olarak oluşturulabileceği hibrit sunucu tarafı oluşturmayı tanıtacaktır.

## Dinamik Fonksiyonlar (Dynamic Functions)

Dinamik fonksiyonlar, kullanıcının çerezleri, mevcut istek başlıkları veya URL'nin arama paramları gibi yalnızca istek sırasında bilinebilecek bilgilere dayanır. Next.js'de bu dinamik fonksiyonlar şunlardır:

- Bir Sunucu Bileşeninde `cookies()` veya `headers()` kullanılması, istek anında tüm rotayı dinamik render etmeye tercih edecektir.
- İstemci Bileşenlerinde `useSearchParams()` kullanılması statik render etmeyi atlar ve bunun yerine tüm İstemci Bileşenlerini istemcideki en yakın üst Suspense sınırına kadar render eder.
  - `useSearchParams()` kullanan İstemci Bileşenini bir `<Suspense/>` sınırına sarmanızı öneririz. Bu, üzerindeki tüm İstemci Bileşenlerinin statik olarak render edilmesini sağlayacaktır.
- `searchParams` Pages prop'unu kullanmak, sayfayı istek anında dinamik render etmeye tercih edecektir.

## Dinamik Veri Getirme

Dinamik veri getirme işlemleri, önbellek seçeneğini `'no-store'` veya `revalidate` değerini 0 olarak ayarlayarak önbellekleme davranışını özellikle devre dışı bırakan `fetch()` istekleridir.

Bir düzen veya sayfadaki tüm `fetch` istekleri için önbelleğe alma seçenekleri segment yapılandırma nesnesi kullanılarak da ayarlanabilir.

