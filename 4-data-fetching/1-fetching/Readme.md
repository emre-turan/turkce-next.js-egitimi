# Veri Getirme (Data Fetching)

Next.js App Router, fonksiyonu `async` olarak işaretleyerek ve [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) için `await` kullanarak verileri doğrudan React bileşenlerinizden almanıza olanak tanır.

Veri getirme, [`fetch()` Web API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)'si ve React Sunucu Bileşenleri üzerine inşa edilmiştir. `fetch()` kullanıldığında, istekler varsayılan olarak otomatik olarak düşülür.

Next.js, her isteğin kendi önbelleğe alma ve yeniden doğrulamasını ayarlamasına izin vermek için `fetch` options nesnesini genişletir.

## Sunucu Bileşenlerinde `async` ve `await`

Sunucu Bileşenlerinde veri almak için `async` ve `await` kullanabilirsiniz.

```tsx
async function getData() {
  const res = await fetch("https://api.example.com/...");
  // Dönüş değeri *seri hale getirilmez*
  // Tarih, Harita, Set, vb. döndürebilirsiniz.

  // Öneri: hataları ele alın
  if (!res.ok) {
    // Bu, en yakın `error.js` Hata Sınırını etkinleştirecektir
    throw new Error("Failed to fetch data");
  }

  return res.json();
}

export default async function Page() {
  const data = await getData();

  return <main></main>;
}
```

**Bilmekte fayda var:**

TypeScript ile bir `async` Sunucu Bileşeni kullanmak için TypeScript `5.1.3` veya üstünü ve `@types/react` `18.2.8` veya üstünü kullandığınızdan emin olun.

## Sunucu Bileşeni İşlevleri

Next.js, Sunucu Bileşenlerinde veri getirirken ihtiyaç duyabileceğiniz yararlı sunucu işlevleri sağlar:

- `cookies()`
- `headers()`

## İstemci Bileşenlerinde `use`

`use`, kavramsal olarak `await`'e benzer bir promise kabul eden yeni bir React fonksiyonudur. `use`, bir fonksiyon tarafından döndürülen promise'i bileşenler, hook'lar ve Suspense ile uyumlu bir şekilde işler. [React RFC](https://github.com/acdlite/rfcs/blob/first-class-promises/text/0000-first-class-support-for-promises.md#usepromise)'de `use` hakkında daha fazla bilgi edinin.

`fetch` işleminin `use`'a sarılması şu anda İstemci Bileşenlerinde önerilmemektedir ve birden fazla yeniden render etmeyi tetikleyebilir. Şimdilik, bir İstemci Bileşeninde veri getirmeniz gerekiyorsa, [SWR](https://swr.vercel.app/) veya [React Query](https://tanstack.com/query/v4) gibi üçüncü taraf bir kütüphane kullanmanızı öneririz.

## Statik Veri Getirme (Static Data Fetching)

Varsayılan olarak, `fetch` otomatik olarak verileri süresiz olarak getirecek ve önbelleğe alacaktır.

```tsx
fetch("https://..."); // cache: 'force-cache' varsayılandır
```

## Verileri Yeniden Doğrulama (Revalidating Data)

Önbelleğe alınan verileri belirli bir zaman aralığında yeniden doğrulamak için `fetch()` işlevinde `next.revalidate` seçeneğini kullanarak bir kaynağın önbellek ömrünü (saniye cinsinden) ayarlayabilirsiniz.

```tsx
fetch("https://...", { next: { revalidate: 10 } });
```

## Dinamik Veri Getirme (Dynamic Data Fetching)

Her `fetch` isteğinde yeni veri almak için `cache: 'no-store'` seçeneğini kullanın.

```tsx
fetch("https://...", { cache: "no-store" });
```

## Veri Getirme Kalıpları (Data Fetching Patterns)

### Paralel Veri Getirme (Parallel Data Fetching)

İstemci-sunucu şelalelerini en aza indirmek için, verileri paralel olarak almak üzere bu modeli öneriyoruz:

```tsx
import Albums from "./albums";

async function getArtist(username: string) {
  const res = await fetch(`https://api.example.com/artist/${username}`);
  return res.json();
}

async function getArtistAlbums(username: string) {
  const res = await fetch(`https://api.example.com/artist/${username}/albums`);
  return res.json();
}

export default async function Page({
  params: { username },
}: {
  params: { username: string };
}) {
  // Her iki talebi de paralel olarak başlatın
  const artistData = getArtist(username);
  const albumsData = getArtistAlbums(username);

  // Sözlerin çözülmesini bekleyin
  const [artist, albums] = await Promise.all([artistData, albumsData]);

  return (
    <>
      <h1>{artist.name}</h1>
      <Albums list={albums}></Albums>
    </>
  );
}
```

Sunucu Bileşeninde `await`'i çağırmadan önce getirme işlemini başlatarak, her istek aynı anda istekleri getirmeye başlayabilir. Bu, bileşenleri şelalelerden kaçınabileceğiniz şekilde ayarlar.

Her iki isteği paralel olarak başlatarak zamandan tasarruf edebiliriz, ancak kullanıcı her iki söz de çözümlenene kadar işlenen sonucu göremez.

Kullanıcı deneyimini iyileştirmek için, render çalışmasını bölmek ve sonucun bir kısmını mümkün olan en kısa sürede göstermek üzere bir askı sınırı ekleyebilirsiniz:

```tsx
import { getArtist, getArtistAlbums, type Album } from "./api";

export default async function Page({
  params: { username },
}: {
  params: { username: string };
}) {
  // Her iki talebi de paralel olarak başlatın
  const artistData = getArtist(username);
  const albumData = getArtistAlbums(username);

  // Önce sanatçının sözünün yerine gelmesini bekleyin
  const artist = await artistData;

  return (
    <>
      <h1>{artist.name}</h1>
      {/* Önce sanatçı bilgilerini gönderin,
          ve albümleri bir gerilim sınırına sarın */}
      <Suspense fallback={<div>Loading...</div>}>
        <Albums promise={albumData} />
      </Suspense>
    </>
  );
}

// Album Bileşeni
async function Albums({ promise }: { promise: Promise<Album[]> }) {
  // Albüm sözünün çözülmesini bekleyin
  const albums = await promise;

  return (
    <ul>
      {albums.map((album) => (
        <li key={album.id}>{album.name}</li>
      ))}
    </ul>
  );
}
```

### Sıralı Veri Getirme (Sequential Data Fetching)

Verileri sıralı olarak getirmek için, doğrudan ihtiyaç duyan bileşenin içinden getirebilir veya getirme işleminin sonucunu ihtiyaç duyan bileşenin içinde bekleyebilirsiniz:

```tsx
// ...

async function Playlists({ artistID }: { artistID: string }) {
  // Wait for the playlists
  const playlists = await getArtistPlaylists(artistID);

  return (
    <ul>
      {playlists.map((playlist) => (
        <li key={playlist.id}>{playlist.name}</li>
      ))}
    </ul>
  );
}

export default async function Page({
  params: { username },
}: {
  params: { username: string };
}) {
  // Wait for the artist
  const artist = await getArtist(username);

  return (
    <>
      <h1>{artist.name}</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <Playlists artistID={artist.id} />
      </Suspense>
    </>
  );
}
```

Bileşen içinde veri getirerek, rotadaki her bir getirme isteği ve iç içe geçmiş segment, önceki istek veya segment tamamlanana kadar veri getirmeye ve oluşturmaya başlayamaz.

### Bir Rotada Oluşturmayı Engelleme (Blocking Rendering in a Route)

Verileri bir layoutta getirerek, altındaki tüm rota segmentleri için işleme yalnızca veriler yüklendikten sonra başlayabilir.

`pages` dizininde, sunucu oluşturma kullanan sayfalar `getServerSideProps` bitene kadar tarayıcı yükleme döndürücüsünü gösterecek, ardından o sayfa için React bileşenini oluşturacaktı. Bu, "ya hep ya hiç" veri getirme olarak tanımlanabilir. Ya sayfanız için tüm verilere sahip olurdunuz ya da hiçbirine sahip olmazdınız.

`app` dizininde, keşfedebileceğiniz ek seçenekler vardır:

1. İlk olarak, veri getirme işlevinizden gelen sonucu aktarırken sunucudan anlık bir yükleme durumu göstermek için `loading.js` kullanabilirsiniz.
2. İkinci olarak, veri getirme işlemini bileşen ağacında daha aşağıya taşıyarak yalnızca sayfanın ihtiyaç duyulan bölümleri için görüntülemeyi engelleyebilirsiniz. Örneğin, veri getirmeyi kök düzende getirmek yerine belirli bir bileşene taşıyabilirsiniz.

Mümkün olduğunda, verileri onu kullanan segmentte almak en iyisidir. Bu aynı zamanda sayfanın tamamı için değil, yalnızca yüklenen kısmı için bir yükleme durumu göstermenize olanak tanır.

## `fetch()` olmadan Veri Getirme (Data Fetching without `fetch()`)

ORM veya veritabanı istemcisi gibi üçüncü taraf bir kütüphane kullanıyorsanız, `fetch` isteklerini doğrudan kullanma ve yapılandırma olanağına her zaman sahip olmayabilirsiniz.

`fetch` özelliğini kullanamadığınız ancak yine de bir düzen veya sayfanın önbelleğe alma veya yeniden doğrulama davranışını kontrol etmek istediğiniz durumlarda, segmentin varsayılan önbelleğe alma davranışına güvenebilir veya segment önbelleği yapılandırmasını kullanabilirsiniz.

### Varsayılan Önbelleğe Alma Davranışı (Default Caching Behavior)

Doğrudan `fetch` kullanmayan herhangi bir veri getirme kütüphanesi bir rotanın önbelleğe alınmasını etkilemeyecek ve rota segmentine bağlı olarak statik veya dinamik olacaktır.

Segment statikse (varsayılan), isteğin çıktısı segmentin geri kalanıyla birlikte önbelleğe alınır ve yeniden doğrulanır (yapılandırılmışsa). Segment dinamikse, isteğin çıktısı önbelleğe alınmaz ve segment işlendiğinde her istekte yeniden taranır.

## Segment Önbellek Yapılandırması (Segment Cache Configuration)

Geçici bir çözüm olarak, üçüncü taraf sorgularının önbelleğe alma davranışı yapılandırılana kadar, tüm segmentin önbellek davranışını özelleştirmek için segment yapılandırmasını kullanabilirsiniz.

```tsx
import prisma from "./lib/prisma";

export const revalidate = 3600; // her saat yeniden doğrulama

async function getPosts() {
  const posts = await prisma.post.findMany();
  return posts;
}

export default async function Page() {
  const posts = await getPosts();
  // ...
}
```
