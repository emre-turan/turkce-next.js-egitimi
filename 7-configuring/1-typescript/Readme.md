# TypeScript

Next.js, React uygulamanızı oluşturmak için TypeScript öncelikli bir geliştirme deneyimi sunar.

Gerekli paketleri otomatik olarak yüklemek ve uygun ayarları yapılandırmak için yerleşik TypeScript desteği ile birlikte gelir.

Editörünüz için bir [TypeScript Eklentisinin](https://nextjs.org/docs/app/building-your-application/configuring/typescript#typescript-plugin) yanı sıra.

🎥 İzleyin: Yerleşik TypeScript eklentisi hakkında bilgi edinin → [YouTube (3 dakika)](https://www.youtube.com/watch?v=pqMqn9fKEf8)

## Yeni Projeler

`create-next-app` artık varsayılan olarak TypeScript ile birlikte geliyor.

```bash
// Terminal
npx create-next-app@latest
```

## Mevcut Projeler

Bir dosyayı `.ts` / `.tsx` olarak yeniden adlandırarak projenize TypeScript ekleyin. Gerekli bağımlılıkları otomatik olarak yüklemek ve önerilen yapılandırma seçeneklerini içeren bir `tsconfig.json` dosyası eklemek için `next dev` ve `next build`'i çalıştırın.

Zaten bir `jsconfig.json` dosyanız varsa, eski `jsconfig.json` dosyasındaki paths derleyici seçeneğini yeni `tsconfig.json` dosyasına kopyalayın ve eski `jsconfig.json` dosyasını silin.

## TypeScript Eklentisi

Next.js, VSCode ve diğer kod düzenleyicilerin gelişmiş tür denetimi ve otomatik tamamlama için kullanabileceği özel bir TypeScript eklentisi ve tür denetleyicisi içerir.

Eklentiyi VS Code'da şu şekilde etkinleştirebilirsiniz:

1. Komut paletini açma (`Ctrl/⌘ + Shift + P`)
2. "TypeScript: TypeScript Sürümünü Seçin"
3. "Çalışma Alanı Sürümünü Kullan" seçiliyor

<img alt="typescript" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ftypescript-command-palette.png&w=1920&q=75&dpl=dpl_6Yq4y5XKQAGCqykadPGURhWiWZCpJ"/><br/>

Şimdi, dosyaları düzenlerken, özel eklenti etkinleştirilecektir. Bir sonraki `next build` çalıştırıldığında, özel tür denetleyicisi kullanılacaktır.

### Eklenti Özellikleri

TypeScript eklentisi şu konularda yardımcı olabilir:

- [Segment yapılandırma seçenekleri](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config) için geçersiz değerler geçilirse uyarı gösterme.
- Mevcut seçenekleri ve bağlam içi belgeleri gösterme.
- "use client" yönergesinin doğru kullanıldığından emin olmak.
- İstemci kancalarının (`useState` gibi) yalnızca İstemci Bileşenlerinde kullanılmasını sağlama.

**Bilmekte fayda var:** Gelecekte daha fazla özellik eklenecektir.

## Minimum TypeScript Sürümü

[İçe aktarma adlarında tür değiştiriciler](https://devblogs.microsoft.com/typescript/announcing-typescript-4-5/#type-on-import-names) ve [performans iyileştirmeleri](https://devblogs.microsoft.com/typescript/announcing-typescript-4-5/#real-path-sync-native) gibi sözdizimi özelliklerini elde etmek için TypeScript'in en az `v4.5.2` sürümünde olmanız şiddetle tavsiye edilir.

## Statik Olarak Yazılan Bağlantılar (Statically Typed Links)

Next.js, `next/link` kullanırken yazım hatalarını ve diğer hataları önlemek için bağlantıları statik olarak yazabilir ve sayfalar arasında gezinirken yazım güvenliğini artırır.

Bu özelliğe dahil olmak için `experimental.typedRoutes` özelliğinin etkinleştirilmesi ve projenin TypeScript kullanıyor olması gerekir.

```js
// next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    typedRoutes: true,
  },
};

module.exports = nextConfig;
```

Next.js, `.next/types` içinde uygulamanızdaki mevcut tüm rotalar hakkında bilgi içeren bir bağlantı tanımı oluşturacak ve TypeScript bu bağlantıyı geçersiz bağlantılar hakkında düzenleyicinize geri bildirim sağlamak için kullanabilecektir.

Şu anda, deneysel destek dinamik segmentler de dahil olmak üzere herhangi bir string literalini içermektedir. Literal olmayan dizeler için, şu anda `href`'i `as Route` ile manuel olarak atmanız gerekir:

```ts
import type { Route } from 'next';
import Link from 'next/link'

// href geçerli bir rota ise TypeScript hatası yok
<Link href="/about" />
<Link href="/blog/nextjs" />
<Link href={`/blog/${slug}`} />
<Link href={('/blog' + slug) as Route} />

// href geçerli bir rota değilse TypeScript hata verir
<Link href="/aboot" />s
```

`next/link`'i saran özel bir bileşende `href` kabul etmek için bir generic kullanın:

```ts
import type { Route } from "next";
import Link from "next/link";

function Card<T extends string>({ href }: { href: Route<T> | URL }) {
  return (
    <Link href={href}>
      <div>My Card</div>
    </Link>
  );
}
```

**Nasıl çalışıyor?**

Next.js, `next dev` veya `next build`'i çalıştırırken `.next` içinde uygulamanızdaki mevcut tüm rotalar hakkında bilgi içeren gizli bir `.d.ts` dosyası oluşturur (`href` türü Bağlantı olan tüm geçerli rotalar). Bu `.d.ts` dosyası `tsconfig.json` dosyasına dahil edilir ve TypeScript derleyicisi bu `.d.ts` dosyasını kontrol eder ve editörünüzde geçersiz bağlantılar hakkında geri bildirim sağlar.

## Uçtan Uca Tip Güvenlik (End-to-End Type Safety)

Next.js 13 gelişmiş tip güvenliğine sahiptir. Buna şunlar dahildir:

1. **Fetch etme fonksiyonu ve sayfa arasında verileri serileştirme yoktur:** Sunucudaki bileşenlerde, düzenlerde ve sayfalarda doğrudan veri `fetch` edebilirsiniz. Bu verilerin React'te tüketilmek üzere istemci tarafına aktarılması için serileştirilmesi (bir dizeye dönüştürülmesi) gerekmez. Bunun yerine, `app` varsayılan olarak Sunucu Bileşenlerini kullandığından, `Date`, `Map`, `Set` ve daha fazlası gibi değerleri herhangi bir ekstra adım olmadan kullanabiliriz. Önceden, Next.js'ye özgü türlerle sunucu ve istemci arasındaki sınırı manuel olarak yazmanız gerekiyordu.
2. **Bileşenler arasındaki veri akışı kolaylaştırıldı:** Kök düzenler lehine `_app`'nin kaldırılmasıyla, bileşenler ve sayfalar arasındaki veri akışını görselleştirmek artık daha kolay. Önceden, tek tek `pages` ve `_app` arasında akan verilerin yazılması zordu ve kafa karıştırıcı hatalara yol açabiliyordu. Next.js 13'teki ortak konumlu fetch etme ile bu artık bir sorun olmaktan çıktı.

Next.js'de veri fetch etme artık veritabanınız veya içerik sağlayıcı seçiminiz hakkında kuralcı olmadan mümkün olduğunca uçtan uca tip güvenliği sağlıyor.

Yanıt verilerini normal TypeScript ile beklediğiniz gibi yazabiliyoruz. Örneğin:

```ts
// app/page.tsx

async function getData() {
  const res = await fetch("https://api.example.com/...");
  // Dönüş değeri *seri hale getirilmez*
  // Tarih, Harita, Set vb. döndürebilirsiniz.
  return res.json();
}

export default async function Page() {
  const name = await getData();

  return "...";
}
```

Uçtan uca tam tip güvenliği için, bu aynı zamanda veritabanınızın veya içerik sağlayıcınızın TypeScript'i desteklemesini gerektirir. Bu, bir [ORM](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) veya tip güvenli sorgu oluşturucu kullanarak olabilir.

## Async Sunucu Bileşeni TypeScript Hatası

TypeScript ile bir `async` Sunucu Bileşeni kullanmak için TypeScript `5.1.3` veya üstünü ve `@types/react` `18.2.8` veya üstünü kullandığınızdan emin olun.

TypeScript'in eski bir sürümünü kullanıyorsanız, `'Promise<Element>' geçerli bir JSX öğesi türü değil` hatası görebilirsiniz. TypeScript ve `@types/react`'in en son sürümüne güncelleme yapmak bu sorunu çözmelidir.

## Sunucu ve İstemci Bileşenleri Arasında Veri Geçişi

Bir Sunucu ve İstemci Bileşeni arasında prop'lar aracılığıyla veri aktarırken, veriler tarayıcıda kullanılmak üzere hala serileştirilir (bir dizeye dönüştürülür). Ancak, özel bir türe ihtiyaç duymaz. Bileşenler arasında diğer prop'ları geçirmekle aynı şekilde yazılır.

Ayrıca, render edilmemiş veriler sunucu ve istemci arasında geçiş yapmadığından (sunucuda kalır) serileştirilmesi gereken daha az kod vardır. Bu artık sadece Sunucu Bileşenleri desteği ile mümkündür.

## Yol takma adları ve baseUrl (Path aliases and baseUrl)

Next.js otomatik olarak `tsconfig.json` `"paths"` ve `"baseUrl"` seçeneklerini destekler.

Bu özellik hakkında daha fazla bilgiyi [Modül Yolu takma adları belgesinde](https://nextjs.org/docs/app/building-your-application/configuring/absolute-imports-and-module-aliases) bulabilirsiniz.

## `next.config.js` dosyasında tür denetimi

`next.config.js` dosyası Babel veya TypeScript tarafından ayrıştırılmadığı için bir JavaScript dosyası olmalıdır, ancak aşağıdaki gibi JSDoc kullanarak IDE'nize bazı tür denetimi ekleyebilirsiniz:

```js
// @ts-check

/**
 * @type {import('next').NextConfig}
 **/
const nextConfig = {
  /* yapılandırma seçenekleri burada */
};

module.exports = nextConfig;
```

## Artımlı tip denetimi (Incremental type checking)

`v10.2.1` sürümünden beri Next.js, `tsconfig.json` dosyanızda etkinleştirildiğinde [artımlı tür denetimini](https://www.typescriptlang.org/tsconfig#incremental) desteklediğinden, bu, daha büyük uygulamalarda tür denetimini hızlandırmaya yardımcı olabilir.

## TypeScript Hatalarını Yok Sayma

Next.js, projenizde TypeScript hataları olduğunda üretim derlemenizde (`next build`) başarısız olur.

Next.js'nin uygulamanızda hatalar olsa bile tehlikeli bir şekilde üretim kodu üretmesini istiyorsanız, yerleşik tür denetimi adımını devre dışı bırakabilirsiniz.

Devre dışı bırakılmışsa, derleme veya dağıtım işleminizin bir parçası olarak tür denetimlerini çalıştırdığınızdan emin olun, aksi takdirde bu çok tehlikeli olabilir.

`next.config.js` dosyasını açın ve `typescript` yapılandırmasında `ignoreBuildErrors` seçeneğini etkinleştirin:

```js
// next.config.js

module.exports = {
  typescript: {
    !! UYARI !!!
    // Tehlikeli bir şekilde üretim derlemelerinin başarıyla tamamlanmasına izin ver
    // projenizde tip hataları var.
    // !! UYARI!!
    ignoreBuildErrors: true,
  },
};
```
