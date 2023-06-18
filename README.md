<h1 align="center">
  <img alt="logo" src="https://upload.wikimedia.org/wikipedia/commons/8/8e/Nextjs-logo.svg" width="224px"/>

Türkçe Next.js Eğitimi (App Router - Uygulama Yönlendiricisi)

</h1>

Bu repo, Next.js'in büyülü dünyasına adım atmak isteyenler için özenle hazırlanmış bir öğrenme yolculuğudur. Bu eğitim serisi, Next.js'in temel yapılarını ve özelliklerini, anlaşılır örnekler ve açıklamalarla ele alır.

Bu eğitim serisi, Next.js'i öğrenmek ve ustalaşmak isteyenlere, adım adım bir rehber sunmayı amaçlar. Her bir konu, detaylı ve anlaşılır bir şekilde ele alınmıştır, böylece okuyucuların Next.js'i etkin ve hızlı bir şekilde öğrenmeleri hedeflenir.

<!-- Bu eğitim serisini aynı zamanda (gitbook linki) web sitesinden de takip edebilirsiniz. -->

Eğer bu rehberi faydalı bulursanız ve daha fazla kişiye ulaşmasını isterseniz, repoya yıldız atabilir ve sosyal medya hesaplarınızda paylaşabilirsiniz. Her bir yıldız, bu eğitim serisinin daha fazla kişiye ulaşmasına yardımcı olur ⭐️

**Not:** Bu eğitimde next.js 13 ile birlikte gelen ve next ekibi tarafından tavsiye edilen `app router` özelliği ile ilgili bilgiler yer almaktadır.

Daha fazla bilgi için [buraya](https://nextjs.org/docs/app/building-your-application) tıklayabilirsiniz.

<br>

# Temel Özellikler

Next.js'in bazı temel özellikleri şunlardır:

| Özellik             | Açıklama                                                                                                                                                                                                   |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Yönlendirme**     | Düzenleri, iç içe yönlendirmeyi, yükleme durumlarını, hata işlemeyi ve daha fazlasını destekleyen; Sunucu Bileşenleri üzerine inşa edilmiş dosya sistemi tabanlı bir yönlendiricidir.                      |
| **İşleme(Render)**  | İstemci tarafı ve Sunucu tarafı işleme ile İstemci ve Sunucu Bileşenleri. Next.js ile sunucuda Statik ve Dinamik işleme ile daha da optimize edilmiştir. Edge ve Node.js çalışma zamanlarında akış sağlar. |
| **Veri Alımı**      | React Bileşenlerinde ve fetch() API'sinde async/await desteği ile basitleştirilmiş veri alımı. Bu, React ve Web Platformu ile uyumludur.                                                                   |
| **Stil**            | CSS Modülleri, Tailwind CSS ve CSS-in-JS dahil olmak üzere tercih ettiğiniz stil yöntemlerini destekler.                                                                                                   |
| **Optimizasyonlar** | Uygulamanızın Core Web Vitals ve Kullanıcı Deneyimini iyileştirmek için Resim, Font ve Script Optimizasyonları.                                                                                            |
| **Typescript**      | TypeScript için geliştirilmiş destek, daha iyi tip kontrolü ve daha verimli derleme, ayrıca özel TypeScript Eklentisi ve tip kontrolörü.                                                                   |
| **API Referansı**   | Next.js boyunca API tasarımında güncellemeler.                                                                                                                                                             |

<br>

# İçerik:

- [React Essentials](#reactın-temelleri-react-essentials)
- [Routing Fundamentals](#yönlendirme-temelleri-routing-fundamentals)

# React'ın Temelleri (React Essentials)

Next.js ile uygulama geliştirmek için React'in Sunucu Bileşenleri gibi yeni özelliklerine aşina olmak bize yardımcı olacaktır. Bu bölümde, Sunucu ve İstemci Bileşenleri arasındaki farkları, ne zaman kullanılacaklarını ve önerilen kalıpları inceleyeceğiz.

## Sunucu (Server) Bileşenleri

Sunucu (Server) ve İstemci (Client) Bileşenleri, geliştiricilerin sunucu ve istemciyi kapsayan uygulamalar oluşturmasına olanak tanıyarak istemci tarafı uygulamaların zengin etkileşimini geleneksel sunucu görüntülemenin gelişmiş performansıyla birleştirir.

## Sunucu Bileşenleri ile Düşünme

React'in kullanıcı arayüzü oluşturma konusundaki düşüncelerimizi değiştirmesine benzer şekilde, React Sunucu Bileşenleri de sunucu ve istemciden yararlanan hibrit uygulamalar oluşturmak için yeni bir zihinsel model sunuyor.

React, tüm uygulamanızı istemci tarafında işlemek yerine (Tek Sayfalı Uygulamalarda olduğu gibi), artık size bileşenlerinizi amaçlarına göre nerede işleyeceğinizi seçme esnekliği sunuyor.

<img alt="sunucu bileşenleri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fthinking-in-server-components.png&w=3840&q=75&dpl=dpl_sqd2P3Qu1LJeq8Pn8V3cFynj578V" /><br/>

Sayfayı daha küçük bileşenlere ayıracak olursak, bileşenlerin çoğunun etkileşimli olmadığını ve sunucuda Sunucu Bileşenleri olarak işlenebileceğini fark edeceksiniz. Daha küçük etkileşimli kullanıcı arayüzü parçaları için İstemci Bileşenlerini serpiştirebiliriz. Bu, Next.js'nin **sunucu öncelikli** yaklaşımıyla uyumludur.

## Neden Sunucu Bileşenleri?

Evet, Sunucu Bileşenlerinin ne olduğunu ve neden önemli olduklarını anlamak önemlidir. İstemci Bileşenlerinin aksine, Sunucu Bileşenleri, uygulamanın sunucu tarafında çalışır ve kullanıcının tarayıcısına sadece HTML gönderir. Bu, bir dizi fayda sağlar:

**Verimlilik:** Sunucu Bileşenleri, veri getirme işlemlerini sunucuya taşıyarak, veritabanınıza daha yakın bir yerde çalışmasını sağlar. Bu, veri getirme sürelerini azaltabilir ve uygulamanın genel performansını artırabilir.

**Performans:** Sunucu Bileşenleri, büyük JavaScript kütüphanelerini sunucuda tutarak, istemci tarafı JavaScript paketinin boyutunu azaltabilir. Bu, sayfa yükleme sürelerini hızlandırabilir ve kullanıcı deneyimini iyileştirebilir.

**Esneklik:** Sunucu Bileşenleri, geliştiricilere, PHP veya Ruby on Rails gibi geleneksel sunucu tarafı dilinde yazılmış bir uygulamayı oluşturma hissi verir, ancak bunu React'in bileşen tabanlı modeli ve gücü ile yapar.

**Ölçeklenebilirlik:** Sunucu Bileşenleri, uygulamanız büyüdükçe JavaScript paketinin boyutunu artırmaz. Bu, uygulamanın ölçeklenebilirliğini artırır ve büyük uygulamaların yönetilmesini kolaylaştırır.

Next.js ile, bir rota yüklendiğinde, ilk HTML sunucuda oluşturulur ve daha sonra tarayıcıda aşamalı olarak geliştirilir. Bu, uygulamanın hızlı bir şekilde yüklenmesini ve kullanıcı etkileşimine hızlı bir şekilde yanıt vermesini sağlar.

Sunucu Bileşenlerine geçiş yapmak, Next.js'in Uygulama Yönlendiricisi sayesinde kolaydır. Uygulama Yönlendiricisi, tüm bileşenleri varsayılan olarak Sunucu Bileşenleri olarak işler, bu da onları otomatik olarak benimsemenizi ve hızlı bir şekilde performans kazanmanızı sağlar. İsteğe bağlı olarak, 'use client' yönergesini kullanarak İstemci Bileşenlerini de tercih edebilirsiniz.

## İstemci (Client) Bileşenleri

İstemci Bileşenleri, uygulamanıza istemci tarafı etkileşim eklemenizi sağlar. Next.js'te, bunlar sunucuda önceden oluşturulur (Pre-Render) ve istemci tarafında canlandırılır (hydration). İstemci Bileşenlerini, Sayfalar Yönlendiricisindeki bileşenlerin her zaman çalıştığı şekilde olduğunu düşünebilirsiniz.

### "use client" yönergesi

`"use client"` yönergesi, Sunucu ve İstemci Bileşen modül grafiği arasında bir sınır belirlemek için kullanılır. Bu, kodun hangi kısmının sunucuda ve hangi kısmının istemci tarafında çalışacağını belirlememize yardımcı olur.

```typescript
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

`"use client"` ifadesi, sunucu ve istemci kodu arasında bir yerdedir. Bir dosyanın en üstüne, içe aktarmaların üzerine yerleştirilir ve sunucu tarafından yalnızca istemci kısmına geçtiği kesme noktasını tanımlar. Bir dosyada `"use client"` tanımlandığında, içine aktarılan tüm diğer modüller, çocuk bileşenler dahil, istemci paketinin bir parçası olarak kabul edilir.

Sunucu Bileşenleri varsayılan olduğundan, tüm bileşenler, `"use client"` yönergesiyle başlayan bir modülde tanımlanmadıkça veya içe aktarılmadıkça Sunucu Bileşeni modül grafiğinin bir parçasıdır.

Bilmekte fayda var:

- Sunucu Bileşeni modül grafiğindeki bileşenlerin yalnızca sunucuda oluşturulacağı garantilidir.
- İstemci Bileşeni modül grafiğindeki bileşenler öncelikle istemci üzerinde oluşturulur, ancak Next.js ile birlikte, bunlar ayrıca sunucuda önceden oluşturulabilir ve istemci üzerinde canlandırılabilir.
- `"use client"` yönergesi, herhangi bir içe aktarmadan önce bir dosyanın en üstünde tanımlanmalıdır.
- Her dosyada `"use client"` tanımlanmasına gerek yoktur. İstemci modül sınırının yalnızca bir kez, "giriş noktasında", tanımlanması gereklidir, böylece içine aktarılan tüm modüller bir İstemci Bileşeni olarak kabul edilir.

## İstemci Bileşenlerini Ne Zaman Kullanmalıyız?

Sunucu ve İstemci Bileşenleri arasındaki kararı basitleştirmek için, İstemci Bileşeni için bir kullanım durumu olana kadar Sunucu Bileşenlerini (uygulama dizininde varsayılan) kullanmanız önerilir.

Aşağıdaki tablo, Sunucu ve İstemci Bileşenleri için farklı kullanım durumlarını özetlemektedir:

| Ne yapmanız gerekiyor?                                                                   | Sunucu Bileşeni | İstemci Bileşeni |
| ---------------------------------------------------------------------------------------- | --------------- | ---------------- |
| Veri almak                                                                               | ✔️              |                  |
| Arka uç kaynaklarına (doğrudan) erişim                                                   | ✔️              |                  |
| Hassas bilgileri sunucuda tutmak (erişim tokenları, API anahtarları, vb.)                | ✔️              |                  |
| Büyük bağımlılıkları sunucuda tutmak / İstemci tarafı JavaScript'i azaltmak              | ✔️              |                  |
| Etkileşim ve olay dinleyicileri eklemek (onClick(), onChange(), vb.)                     |                 | ✔️               |
| Durum ve Yaşam Döngüsü Etkilerini kullanmak (useState(), useReducer(), useEffect(), vb.) |                 | ✔️               |
| Yalnızca tarayıcı API'lerini kullanmak                                                   |                 | ✔️               |
| Durum, etkiler veya yalnızca tarayıcı API'lerine bağlı özel kancaları (hook) kullanmak   |                 | ✔️               |
| [React Sınıf bileşenleri](https://react.dev/reference/react/Component) kullanmak         |                 | ✔️               |

## İstemci Bileşenlerini Yapraklara Taşıma

Uygulamanızın performansını optimize etmek için, İstemci Bileşenlerini mümkün olduğunca bileşen ağacınızın yapraklarına taşımanız önerilir. Bu, uygulamanızın genel JavaScript yükünü azaltır ve sayfa yükleme sürelerini hızlandırır.

Örneğin, statik öğelere sahip bir Yerleşim (Layout) bileşeniniz (örneğin logo, linkler vb.) ve durum kullanabilen etkileşimli bir arama çubuğunuz olabilir.

Tüm düzeni bir İstemci Bileşeni yapmak yerine, etkileşimli mantığı bir İstemci Bileşenine (örneğin `<SearchBar />`) taşıyın ve düzeninizi bir Sunucu Bileşeni olarak tutun. Bu, düzenin tüm bileşen Javascript'ini istemciye göndermek zorunda olmadığınız anlamına gelir.

```typescript
// SearchBar is a Client Component
import SearchBar from "./searchbar";
// Logo is a Server Component
import Logo from "./logo";

// Layout is a Server Component by default
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <nav>
        <Logo />
        <SearchBar />
      </nav>
      <main>{children}</main>
    </>
  );
}
```

## İstemci ve Sunucu Bileşenlerinin Oluşturulması

Sunucu ve İstemci Bileşenleri aynı bileşen ağacında birleştirilebilir.

React, perde arkasında render işlemini aşağıdaki gibi gerçekleştirir:

- **Sunucuda React**, sonucu istemciye göndermeden önce tüm Sunucu Bileşenlerini işler.

  - Buna İstemci Bileşenleri içinde yer alan Sunucu Bileşenleri de dahildir.
  - Bu aşamada karşılaşılan İstemci Bileşenleri atlanır.

- **İstemcide**, React İstemci Bileşenlerini işler ve Sunucu Bileşenlerinin işlenmiş sonucundaki yuvaları, sunucuda ve istemcide yapılan işi birleştirir.

  - Herhangi bir Sunucu Bileşeni bir İstemci Bileşeninin içine yerleştirilmişse, işlenen içerikler İstemci Bileşeninin içine doğru şekilde yerleştirilecektir.

**Bilmekte fayda var:**

Next.js'de, ilk sayfa yüklemesi sırasında, hem yukarıdaki adımdaki Sunucu Bileşenlerinin işlenmiş sonucu hem de İstemci Bileşenleri, daha hızlı bir ilk sayfa yüklemesi üretmek için sunucuda HTML olarak önceden işlenir.

## Sunucu Bileşenlerini İstemci Bileşenlerinin İçine Yerleştirme

Yukarıda özetlenen işleme akışı göz önüne alındığında, bir Sunucu Bileşeninin bir İstemci Bileşenine aktarılmasıyla ilgili bir kısıtlama vardır, çünkü bu yaklaşım ek bir sunucu gidiş gelişi gerektirecektir.

### Desteklenmeyen Model: Sunucu Bileşenlerini İstemci Bileşenlerinin İçine Aktarma

Aşağıdaki model desteklenmez. Bir Sunucu Bileşenini bir İstemci Bileşeninin içine **aktaramazsınız**:

```typescript
"use client";

import ExampleServerComponent from "./example-server-component";

export default function ExampleClientComponent({
  children,
}: {
  children: React.ReactNode;
}) {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>

      <ExampleServerComponent />
    </>
  );
}
```

### Önerilen Model: Sunucu Bileşenlerini İstemci Bileşenlerine Props Olarak Aktarma

Bunun yerine, İstemci Bileşenlerini tasarlarken Sunucu Bileşenleri için "delikleri" işaretlemek üzere React prop'larını kullanabilirsiniz.

Sunucu Bileşeni sunucuda render edilecek ve İstemci Bileşeni istemcide render edildiğinde, "delik", Sunucu Bileşeninin render edilmiş sonucu ile doldurulacaktır.

Yaygın bir model, "deliği" oluşturmak için React `children` prop'unu kullanmaktır. `<ExampleClientComponent>` öğesini genel bir `children` prop kabul edecek şekilde yeniden düzenleyebilir ve `<ExampleClientComponent>` öğesinin içe aktarımını ve açık yuvalanmasını bir üst bileşene taşıyabiliriz.

```typescript
"use client";

import { useState } from "react";

export default function ExampleClientComponent({
  children,
}: {
  children: React.ReactNode;
}) {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>

      {children}
    </>
  );
}
```

Şimdi, `<ExampleClientComponent>` çocukların (children) ne olduğu hakkında hiçbir bilgiye sahip değildir. Aslında, kendi perspektifinden bakıldığında, çocukların eninde sonunda bir Sunucu Bileşeni tarafından doldurulacağını bile bilmez.

`ExampleClientComponent`'in sahip olduğu tek sorumluluk, sonunda hangi çocukların nereye yerleştirileceğine karar vermektir.

Bir üst Sunucu Bileşeninde, hem `<ExampleClientComponent>` hem de `<ExampleServerComponent>` öğelerini içe aktarabilir ve `<ExampleServerComponent>` öğesini `<ExampleClientComponent>` öğesinin bir alt öğesi olarak geçirebilirsiniz:

```typescript
import ExampleClientComponent from "./example-client-component";
import ExampleServerComponent from "./example-server-component";

// Next.js'deki sayfalar varsayılan olarak Sunucu Bileşenleridir
export default function Page() {
  return (
    <ExampleClientComponent>
      <ExampleServerComponent />
    </ExampleClientComponent>
  );
}
```

Bu yaklaşımla, `<ExampleClientComponent>` ve `<ExampleServerComponent>` öğelerinin işlenmesi ayrıştırılır ve bağımsız olarak işlenebilir - İstemci Bileşenlerinden önce sunucuda işlenen Sunucu Bileşenleriyle uyumlu hale getirilir.

Bilmekte fayda var:

- Bu model, `children` prop ile [düzenlerde ve sayfalarda](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) zaten uygulanmaktadır, bu nedenle ek bir sarmalayıcı bileşen oluşturmanız gerekmez.
- React bileşenlerini (JSX) diğer bileşenlere aktarmak yeni bir kavram değildir ve her zaman React kompozisyon modelinin bir parçası olmuştur.
- Bu kompozisyon stratejisi, Sunucu ve İstemci Bileşenleri arasında çalışır çünkü prop'u alan bileşenin prop'un ne olduğu hakkında hiçbir bilgisi yoktur. Yalnızca kendisine aktarılan şeyin nereye yerleştirilmesi gerektiğinden sorumludur.

  - Bu da aktarılan prop'un bağımsız olarak, bu durumda sunucuda, İstemci Bileşeni istemcide render edilmeden çok önce render edilmesini sağlar.
  - Aynı "içeriği yukarı kaldırma" stratejisi, içe aktarılan iç içe geçmiş bir alt bileşeni yeniden işleyen bir üst bileşendeki durum değişikliklerini önlemek için kullanılmıştır.

- Sadece `children` prop ile sınırlı değilsiniz. JSX iletmek için herhangi bir prop kullanabilirsiniz.

## Sunucudan İstemci Bileşenlerine Props iletimi (Serileştirme)

Sunucudan İstemci Bileşenlerine aktarılan propların [serileştirilebilir](https://developer.mozilla.org/en-US/docs/Glossary/Serialization) olması gerekir. Bu, fonksiyonlar, Tarihler vb. gibi değerlerin doğrudan İstemci Bileşenlerine aktarılamayacağı anlamına gelir.

### Ağ Sınırı Nerede?

Uygulama yönlendiricisinde, ağ sınırı Sunucu Bileşenleri ile İstemci Bileşenleri arasındadır. Bu, sınırın `getStaticProps`/`getServerSideProps` ve Sayfa Bileşenleri arasında olduğu Sayfalardan farklıdır. Sunucu Bileşenleri içinde getirilen verilerin, bir İstemci Bileşenine aktarılmadığı sürece ağ sınırını geçmediğinden serileştirilmesi gerekmez.

## Sunucuya Özel Kodu İstemci Bileşenlerinin Dışında Tutmak (Zehirlenme)

JavaScript modülleri hem Sunucu hem de İstemci Bileşenleri arasında paylaşılabildiğinden, yalnızca sunucuda çalıştırılması amaçlanan kodun istemciye gizlice girmesi mümkündür.

Örneğin, aşağıdaki veri alma işlevini ele alalım:

```typescript
export async function getData() {
  const res = await fetch("https://external-service.com/data", {
    headers: {
      authorization: process.env.API_KEY,
    },
  });

  return res.json();
}
```

İlk bakışta, `getData` hem sunucuda hem de istemcide çalışıyor gibi görünür. Ancak `API_KEY` ortam değişkeninin önüne `NEXT_PUBLIC` eklenmediği için, bu değişken yalnızca sunucudan erişilebilen özel bir değişkendir. Next.js, güvenli bilgilerin sızmasını önlemek için istemci kodunda özel ortam değişkenlerini boş dizeyle değiştirir.

Sonuç olarak, `getData()` istemciye aktarılıp çalıştırılabilse de beklendiği gibi çalışmayacaktır. Değişkeni public yapmak fonksiyonun istemci üzerinde çalışmasını sağlarken, hassas bilgileri sızdıracaktır.

Bu nedenle, bu işlev yalnızca sunucuda çalıştırılmak üzere yazılmıştır.

## "server-only" paketi

Sunucu kodunun bu tür istenmeyen istemci kullanımını önlemek için, diğer geliştiricilere bu modüllerden birini yanlışlıkla bir İstemci Bileşenine içe aktarmaları durumunda derleme zamanı hatası vermek için `server-only` paketini kullanabiliriz.

`server-only` kullanmak için önce paketi yükleyin:

```terminal
npm install server-only
```

Ardından paketi yalnızca sunucu kodu içeren herhangi bir modülde içe aktarın:

```typescript
import "server-only";

export async function getData() {
  const res = await fetch("https://external-service.com/data", {
    headers: {
      authorization: process.env.API_KEY,
    },
  });

  return res.json();
}
```

Artık `getData()` işlevini içe aktaran herhangi bir İstemci Bileşeni, bu modülün yalnızca sunucuda kullanılabileceğini açıklayan bir derleme zamanı hatası alacaktır.

İlgili `client-only` paketi, yalnızca istemci kodu içeren modülleri işaretlemek için kullanılabilir - örneğin, `window` nesnesine erişen kod.

## Veri Almak (Data Fetching)

İstemci Bileşenlerinde veri almak mümkün olsa da, istemcide veri almak için özel bir nedeniniz olmadığı sürece Sunucu Bileşenlerinde veri almanızı öneririz. Veri getirme işlemini sunucuya taşımak daha iyi performans ve kullanıcı deneyimi sağlar.

## Üçüncü taraf paketleri

Sunucu Bileşenleri yeni olduğundan, ekosistemdeki üçüncü taraf paketler `useState`, `useEffect` ve `createContext` gibi yalnızca istemci özelliklerini kullanan bileşenlere `"use client"` yönergesini eklemeye yeni başlıyor.

Bugün, sadece istemci özelliklerini kullanan `npm` paketlerindeki birçok bileşen henüz bu yönergeye sahip değildir. Bu üçüncü taraf bileşenler, kendi İstemci Bileşenlerinizde `"use client"` yönergesine sahip oldukları için beklendiği gibi çalışacaktır, ancak Sunucu Bileşenlerinde çalışmayacaktır.

Örneğin, bir `<Carousel />` bileşeni olan varsayımsal `acme-carousel` paketini yüklediğinizi varsayalım. Bu bileşen `useState` kullanıyor, ancak henüz `"use client"` yönergesine sahip değil.

Bir İstemci Bileşeni içinde `<Carousel />` kullanırsanız, beklendiği gibi çalışacaktır:

```tsx
"use client";

import { useState } from "react";
import { Carousel } from "acme-carousel";

export default function Gallery() {
  let [isOpen, setIsOpen] = useState(false);

  return (
    <div>
      <button onClick={() => setIsOpen(true)}>View pictures</button>

      {/* Works, since Carousel is used within a Client Component */}
      {isOpen && <Carousel />}
    </div>
  );
}
```

Ancak, bunu doğrudan bir Sunucu Bileşeni içinde kullanmaya çalışırsanız bir hata görürsünüz:

```tsx
import { Carousel } from "acme-carousel";

export default function Page() {
  return (
    <div>
      <p>View pictures</p>

      {/* Error: `useState` can not be used within Server Components */}
      <Carousel />
    </div>
  );
}
```

Bunun nedeni Next.js'nin `<Carousel />`'in yalnızca istemci özelliklerini kullandığını bilmemesidir.

Bunu düzeltmek için, yalnızca istemci özelliklerine dayanan üçüncü taraf bileşenleri kendi İstemci Bileşenlerinize sarabilirsiniz:

```tsx
"use client";

import { Carousel } from "acme-carousel";

export default Carousel;
```

Artık `<Carousel />` öğesini doğrudan bir Sunucu Bileşeni içinde kullanabilirsiniz:

```tsx
import Carousel from "./carousel";

export default function Page() {
  return (
    <div>
      <p>View pictures</p>

      {/*  Works, since Carousel is a Client Component */}
      <Carousel />
    </div>
  );
}
```

Çoğu üçüncü taraf bileşeni sarmalamanız gerekmeyecektir çünkü bunlar büyük olasılıkla İstemci Bileşenleri içinde kullanılacaktır. Ancak, bir istisna sağlayıcı bileşenlerdir, çünkü bunlar React durumu ve bağlamına dayanır ve genellikle bir uygulamanın kökünde gereklidir.

## Bağlam

Çoğu React uygulaması, verileri bileşenler arasında paylaşmak için doğrudan `createContext` aracılığıyla veya üçüncü taraf kütüphanelerden içe aktarılan sağlayıcı bileşenler aracılığıyla dolaylı olarak bağlamı (context) kullanır.

Next.js 13'te bağlam, İstemci Bileşenleri içinde tamamen desteklenir, ancak doğrudan Sunucu Bileşenleri içinde **oluşturulamaz** veya **tüketilemez**. Bunun nedeni, Sunucu Bileşenlerinin React durumuna sahip olmaması (etkileşimli olmadıkları için) ve bağlamın öncelikle bazı React durumları güncellendikten sonra ağacın derinliklerindeki etkileşimli bileşenleri yeniden oluşturmak için kullanılmasıdır.

Sunucu Bileşenleri arasında veri paylaşımı için alternatifleri tartışacağız, ancak önce İstemci Bileşenleri içinde bağlamın nasıl kullanılacağına bir göz atalım.

### İstemci Bileşenlerinde Bağlam Kullanma

Tüm bağlam API'leri İstemci Bileşenleri içinde tam olarak desteklenmektedir:

```tsx
"use client";

import { createContext, useContext, useState } from "react";

const SidebarContext = createContext();

export function Sidebar() {
  const [isOpen, setIsOpen] = useState();

  return (
    <SidebarContext.Provider value={{ isOpen }}>
      <SidebarNav />
    </SidebarContext.Provider>
  );
}

function SidebarNav() {
  let { isOpen } = useContext(SidebarContext);

  return (
    <div>
      <p>Home</p>

      {isOpen && <Subnav />}
    </div>
  );
}
```

Ancak, bağlam sağlayıcıları genellikle geçerli tema gibi genel kaygıları paylaşmak için bir uygulamanın köküne yakın bir yerde oluşturulur. Sunucu Bileşenlerinde bağlam desteklenmediğinden, uygulamanızın kökünde bir bağlam oluşturmaya çalışmak hataya neden olacaktır:

```tsx
import { createContext } from "react";

//  createContext is not supported in Server Components
export const ThemeContext = createContext({});

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <ThemeContext.Provider value="dark">{children}</ThemeContext.Provider>
      </body>
    </html>
  );
}
```

Bunu düzeltmek için, bağlamınızı oluşturun ve sağlayıcısını bir İstemci Bileşeninin içinde oluşturun:

```tsx
"use client";

import { createContext } from "react";

export const ThemeContext = createContext({});

export default function ThemeProvider({ children }) {
  return <ThemeContext.Provider value="dark">{children}</ThemeContext.Provider>;
}
```

Sunucu Bileşeniniz artık bir İstemci Bileşeni olarak işaretlendiğinden sağlayıcınızı doğrudan oluşturabilecektir:

```tsx
import ThemeProvider from "./theme-provider";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <body>
        <ThemeProvider>{children}</ThemeProvider>
      </body>
    </html>
  );
}
```

Sağlayıcı kökte işlendiğinde, uygulamanızdaki diğer tüm İstemci Bileşenleri bu bağlamı kullanabilecektir.

Bilmekte fayda var:

Sağlayıcıları ağaçta mümkün olduğunca derinde oluşturmalısınız - `ThemeProvider`'ın tüm `<html>` belgesi yerine yalnızca `{children}` öğesini nasıl sardığına dikkat edin. Bu, Next.js'nin Sunucu Bileşenlerinizin statik kısımlarını optimize etmesini kolaylaştırır.

### Sunucu Bileşenlerinde üçüncü taraf bağlam sağlayıcılarını oluşturma

Üçüncü taraf `npm` paketleri genellikle uygulamanızın köküne yakın bir yerde işlenmesi gereken Sağlayıcılar içerir. Bu sağlayıcılar `"use client"` yönergesini içeriyorsa, doğrudan Sunucu Bileşenlerinizin içinde oluşturulabilirler. Ancak, Sunucu Bileşenleri çok yeni olduğundan, birçok üçüncü taraf sağlayıcı henüz yönergeyi eklememiş olacaktır.

`"use client"` seçeneğine sahip olmayan bir üçüncü taraf sağlayıcıyı render almaya çalışırsanız, bu bir hataya neden olur:

```tsx
import { ThemeProvider } from "acme-theme";

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {/*  Error: `createContext` can't be used in Server Components */}
        <ThemeProvider>{children}</ThemeProvider>
      </body>
    </html>
  );
}
```

Bunu düzeltmek için, üçüncü taraf sağlayıcıları kendi İstemci Bileşeninize sarın:

```tsx
"use client";

import { ThemeProvider } from "acme-theme";
import { AuthProvider } from "acme-auth";

export function Providers({ children }) {
  return (
    <ThemeProvider>
      <AuthProvider>{children}</AuthProvider>
    </ThemeProvider>
  );
}
```

Artık `<Providers />` öğesini doğrudan kök düzeninizin içine alabilir ve işleyebilirsiniz.

```tsx
import { Providers } from "./providers";

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

Sağlayıcılar kökte işlendiğinde, bu kütüphanelerdeki tüm bileşenler ve kancalar kendi İstemci Bileşenlerinizde beklendiği gibi çalışacaktır.

Üçüncü taraf bir kütüphane istemci koduna `"use client"` eklediğinde, sarmalayıcı İstemci Bileşenini kaldırabileceksiniz.

## Sunucu Bileşenleri arasında veri paylaşımı

Sunucu Bileşenleri etkileşimli olmadığından ve bu nedenle React durumundan okuma yapmadığından, veri paylaşmak için React bağlamına ihtiyacınız yoktur. Bunun yerine, birden fazla Sunucu Bileşeninin erişmesi gereken ortak veriler için yerel JavaScript kalıplarını kullanabilirsiniz. Örneğin, bir veritabanı bağlantısını birden fazla bileşen arasında paylaşmak için bir modül kullanılabilir:

```tsx
export const db = new DatabaseConnection();
```

```tsx
import { db } from "@utils/database";

export async function UsersLayout() {
  let users = await db.query();
  // ...
}
```

```tsx
import { db } from "@utils/database";

export async function DashboardPage() {
  let user = await db.query();
  // ...
}
```

Yukarıdaki örnekte, hem DashboardPage hem de UsersLayout veritabanı sorguları yapması gerekir. Bu bileşenlerin her biri `@utils/database` modülünü içe aktararak veritabanına erişimi paylaşır. Bu JavaScript modeline global singleton adı verilir.

## Alma isteklerini (Fetch Request) Sunucu Bileşenleri arasında paylaşma

Veri alırken, `ƒetch` işleminin sonucunu bir `page` veya `layout` ile bazı alt bileşenleri arasında paylaşmak isteyebilirsiniz. Bu, bileşenler arasında gereksiz bir bağlantıdır ve bileşenler arasında ileri geri `props` geçişine yol açabilir.

Bunun yerine, veri getirme işlemini veriyi tüketen bileşenin yanında konumlandırmak önerilir. `fetch` istekleri Sunucu Bileşenlerinde otomatik olarak ayrıştırılır, böylece her rota segmenti yinelenen istekler konusunda endişelenmeden tam olarak ihtiyaç duyduğu verileri talep edebilir. Next.js, `fetch` önbelleğinden aynı değeri okuyacaktır.

# Yönlendirme Temelleri (Routing Fundamentals)

Her uygulamanın iskeleti yönlendirmedir (routing). Bu bölümde size web için yönlendirmenin temel kavramları ve Next.js'de yönlendirmenin nasıl ele alınacağı anlatılacaktır.

## Terminoloji

Öncelikle, bu terimlerin dokümantasyon boyunca kullanıldığını göreceksiniz. İşte hızlı bir referans:

<img alt="yönlendirme-temelleri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fterminology-component-tree.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

- **Ağaç (tree)**: Hiyerarşik bir yapıyı görselleştirmek için kullanılan bir kural. Örneğin, üst ve alt bileşenleri olan bir bileşen ağacı, bir klasör yapısı vb.
- **Alt ağaç (Subtree)**: Yeni bir kökten (ilk) başlayan ve yapraklarda (son) biten bir ağacın parçası.
- **Kök (Root)**: Kök düzeni gibi bir ağaç veya alt ağaçtaki ilk düğüm.
- **Yaprak (Leaf)**: Bir URL yolundaki son bölüm gibi, bir alt ağaçta çocuğu olmayan düğümler.

<img alt="yönlendirme-temelleri-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fterminology-url-anatomy.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

- **URL Segmenti**: URL yolunun eğik çizgilerle ayrılmış bölümü.
- **URL Yolu (Path)**: URL'nin etki alanından sonra gelen kısmı (segmentlerden oluşur).

## Uygulama Yönlendiricisi (App Router)

Next.js, 13. sürümde React Sunucu Bileşenleri üzerine inşa edilen ve paylaşılan düzenleri, iç içe yönlendirmeyi, yükleme durumlarını, hata işlemeyi ve daha fazlasını destekleyen yeni bir **Uygulama Yönlendiricisi** sundu.

Uygulama Yönlendiricisi, `app` adlı yeni bir dizinde çalışır. `app` dizini, aşamalı uyarlamaya izin vermek için `pages` dizini ile birlikte çalışır. Bu, uygulamanızın bazı rotalarını yeni davranışa seçerken diğer rotaları önceki davranış için `pages` dizininde tutmanıza olanak tanır.

Bilmekte fayda var:

Uygulama Yönlendiricisi, Sayfa Yönlendiricisine göre önceliklidir. Dizinler arasındaki yönlendirmeler aynı URL yoluna çözümlenmemelidir ve bir çakışmayı önlemek için derleme zamanı hatasına neden olur.

<img alt="uygulama-yönlendiricisi" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnext-router-directories.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Varsayılan olarak, uygulama içindeki bileşenler React [Sunucu Bileşenleridir](#sunucu-server-bileşenleri). Bu bir performans optimizasyonudur ve bunları kolayca benimsemenizi sağlar ve ayrıca [İstemci Bileşenlerini](#i̇stemci-client-bileşenleri) de kullanabilirsiniz.

**Öneri**: Sunucu Bileşenleri konusunda yeniyseniz [Sunucu ve İstemci Bileşenleri](#reactın-temelleri-react-essentials) bölümüne göz atın.

## Klasörlerin ve Dosyaların Rolleri

Next.js dosya sistemi tabanlı bir yönlendirici kullanır:

- **Klasörler** rotaları tanımlamak için kullanılır. Rota, **kök klasörden** `page.js` dosyasını içeren son bir **yaprak klasöre** kadar dosya sistemi hiyerarşisini takip eden, iç içe geçmiş klasörlerden oluşan tek bir yoldur. [Rotaları Tanımlama]() bölümüne bakın.

**Dosyalar**, bir rota segmenti için gösterilen kullanıcı arayüzünü oluşturmak için kullanılır. Bkz. [özel dosyalar]().

## Rota Segmentleri

Bir rotadaki her klasör bir **rota segmentini** temsil eder. Her rota segmenti, bir **URL yolunda** karşılık gelen **segmentle** eşlenir.

<img alt="rota segmentleri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

## İç İçe Rotalar

İç içe bir rota oluşturmak için klasörleri birbirinin içine yerleştirebilirsiniz. Örneğin, uygulama dizininde iki yeni klasörü iç içe yerleştirerek yeni bir `/dashboard/settings` rotası ekleyebilirsiniz.

`dashboard/settings` rotası üç segmentten oluşur:

- `/` (Kök segment)
- `dashboard` (Segment)
- `settings` (Yaprak segmenti)

## Dosya Kuralları

Next.js, iç içe rotalarda belirli davranışlara sahip kullanıcı arayüzü oluşturmak için bir dizi özel dosya sağlar:

| Dosya Adı      | Açıklama                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------- |
| `layout`       | Bir segment ve alt segmentleri için paylaşılan kullanıcı arayüzü                              |
| `page`         | Bir rotanın benzersiz kullanıcı arayüzü ve rotaların herkesin erişimine açık hale getirilmesi |
| `loading`      | Bir segment ve alt segmentleri için `loading` kullanıcı arayüzü                               |
| `not-found`    | Bir segment ve alt segmentleri için `not-found` kullanıcı arayüzü                             |
| `error`        | Bir segment ve alt segmentleri için `error` kullanıcı arayüzü                                 |
| `global-error` | `global-error` Kullanıcı Arayüzü                                                              |
| `route`        | Sunucu tarafı API uç noktası                                                                  |
| `template`     | Özelleştirilmiş yeniden render edilen Layout Kullanıcı Arayüzü                                |
| `default`      | [Paralel Rotalar]() için Yedek Kullanıcı Arayüzü                                              |

Bilmenizde fayda var:

.js, .jsx veya .tsx dosya uzantıları bu özel dosyalar için kullanılabilir.

## Bileşen Hiyerarşisi

Bir rota segmentinin özel dosyalarında tanımlanan React bileşenleri belirli bir hiyerarşi içinde oluşturulur:

- `layout.js`
- `template.js`
- `error.js` (React hata sınırı)
- `loading.js` (React gerilim sınırı)
- `not-found.js` (React hata sınırı)
- `page.js` veya iç içe `layout.js`

<img alt="bileşen hiyerarşisi" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ffile-conventions-component-hierarchy.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

İç içe geçmiş bir rotada, bir segmentin bileşenleri üst segmentinin bileşenlerinin **içinde** iç içe geçecektir.

<img alt="bileşen hiyerarşisi-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-file-conventions-component-hierarchy.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

## Ortak Yerleşim

Özel dosyalara ek olarak, kendi dosyalarınızı (örneğin bileşenler, stiller, testler vb.) `app` dizinindeki klasörlerin içine yerleştirme seçeneğiniz vardır.

Bunun nedeni, klasörler rotaları tanımlarken, yalnızca `page.js` veya `route.js` tarafından döndürülen içeriklerin genel olarak adreslenebilir olmasıdır.

<img alt="ortak yerleşim" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-colocation.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

[Proje Organizasyonu ve Ortak Yerleşim]() hakkında daha fazla bilgi edinin.

## İstemci Tarafında Gezinme ile Sunucu Merkezli Yönlendirme

İstemci tarafı yönlendirme kullanan `pages` dizininin aksine, `app router`, [Sunucu Bileşenleri](#sunucu-server-bileşenleri) ve [sunucuda veri getirme]() ile uyum sağlamak için **sunucu merkezli yönlendirme** kullanır. Sunucu merkezli yönlendirme ile istemcinin bir rota haritası indirmesi gerekmez ve Sunucu Bileşenleri için aynı istek rotaları aramak için kullanılabilir. Bu optimizasyon tüm uygulamalar için yararlıdır, ancak çok sayıda rotaya sahip uygulamalar üzerinde daha büyük bir etkiye sahiptir.

Yönlendirme sunucu merkezli olmasına rağmen, yönlendirici, Tek Sayfalı Uygulama davranışına benzeyen [Bağlantı Bileşeni]() ile **istemci tarafında gezinmeyi** kullanır. Bu, bir kullanıcı yeni bir rotaya gittiğinde tarayıcının sayfayı yeniden yüklemeyeceği anlamına gelir. Bunun yerine, URL güncellenecek ve Next.js yalnızca değişen bölümleri oluşturacaktır.

Ayrıca, kullanıcılar uygulamada gezinirken, yönlendirici React Sunucu Bileşeni yükünün sonucunu **bellek içi istemci tarafı önbelleğinde** saklar. Önbellek, herhangi bir seviyede geçersiz kılmaya izin veren ve [React'in eşzamanlı render](https://react.dev/blog/2022/03/29/react-v18#what-is-concurrent-react)'ları arasında tutarlılık sağlayan rota segmentlerine bölünmüştür. Bu, belirli durumlarda, daha önce getirilmiş bir segmentin önbelleğinin yeniden kullanılabileceği ve performansı daha da artıracağı anlamına gelir.

[Bağlantı ve Gezinme]() hakkında daha fazla bilgi edinin.

## Kısmi Rendering

Kardeş rotalar arasında gezinirken (örneğin aşağıdaki `/dashboard/settings` ve `/dashboard/analytics`), Next.js yalnızca değişen rotalardaki düzenleri ve sayfaları getirecek ve oluşturacaktır. Alt ağaçtaki segmentlerin üzerindeki hiçbir şeyi yeniden **getirmeyecek veya yeniden oluşturmayacaktır**. Bu, bir düzeni paylaşan rotalarda, bir kullanıcı kardeş sayfalar arasında gezindiğinde düzenin korunacağı anlamına gelir.

<img alt="kısmi rendering" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fpartial-rendering.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Kısmi rendering olmadan, her gezinti tüm sayfanın sunucuda yeniden işlenmesine neden olur. Yalnızca güncellenen bölümün render edilmesi, aktarılan veri miktarını ve yürütme süresini azaltarak performansın artmasını sağlar.

## Gelişmiş Yönlendirme Kalıpları

Uygulama Yönlendirici ayrıca daha gelişmiş yönlendirme modellerini uygulamanıza yardımcı olacak bir dizi kural sunar. Bunlar şunları içerir:

- [Paralel Rotalar](): Aynı görünümde bağımsız olarak gezinilebilen iki veya daha fazla sayfayı aynı anda göstermenizi sağlar. Bunları, kendi alt navigasyonları olan bölünmüş görünümler için kullanabilirsiniz. Örn. gösterge tabloları.
- [Rotaları Kesme](): Bir rotayı kesmenize ve başka bir rota bağlamında göstermenize izin verir. Geçerli sayfanın bağlamını korumak önemli olduğunda bunları kullanabilirsiniz. Örneğin, bir görevi düzenlerken tüm görevleri görmek veya bir akıştaki bir fotoğrafı genişletmek.

Bu modeller, daha zengin ve daha karmaşık kullanıcı arayüzleri oluşturmanıza olanak tanıyarak, geçmişte küçük ekipler ve bireysel geliştiriciler tarafından uygulanması karmaşık olan özellikleri demokratikleştirir.

# Rotaların Tanımlanması

Devam etmeden önce [Yönlendirme Temelleri](#yönlendirme-temelleri-routing-fundamentals) bölümünün okunması önerilir.

Bu bölüm, Next.js uygulamanızda rotaları nasıl tanımlayacağınız ve düzenleyeceğiniz konusunda size rehberlik edecektir.

## Rotalar Oluşturma

Next.js, rotaları tanımlamak için **klasörlerin** kullanıldığı dosya sistemi tabanlı bir yönlendirici kullanır.

Her klasör, bir **URL** segmentiyle eşleşen bir [rota segmentini](#rota-segmentleri) temsil eder. [İç içe bir rota](#i̇ç-i̇çe-rotalar) oluşturmak için, klasörleri birbirinin içine yerleştirebilirsiniz.

<img alt="rotalar oluşturma" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Rota segmentlerini genel erişime açmak için özel bir [`page.js` dosyası](#sayfalar) kullanılır.

<img alt="rotalar oluşturma-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fdefining-routes.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Bu örnekte, `/dashboard/analytics` URL yolu, karşılık gelen bir `page.js` dosyasına sahip olmadığı için _genel erişime_ açık değildir. Bu klasör bileşenleri, stil sayfalarını, görüntüleri veya diğer ortak dosyaları depolamak için kullanılabilir.

## Kullanıcı Arayüzü Oluşturma

Her bir rota segmenti için kullanıcı arayüzü oluşturmak üzere [özel dosya kuralları](#dosya-kuralları) kullanılır. En yaygın olanları, bir rotaya özgü kullanıcı arayüzünü gösteren [sayfalar](#sayfalar) ve birden fazla rotada paylaşılan kullanıcı arayüzünü gösteren [düzenlerdir](#düzenler).

Örneğin, ilk sayfanızı oluşturmak için `app` dizininin içine bir `page.js` dosyası ekleyin ve bir React bileşenini dışa aktarın:

```tsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
```

# Sayfalar ve Düzenler

Next.js 13 içindeki Uygulama Yönlendiricisi, [sayfaları](#sayfalar), [paylaşılan düzenleri](#düzenler) ve [şablonları](#şablonlar) kolayca oluşturmak için yeni dosya kurallarını tanıttı. Bu bölüm, Next.js uygulamanızda bu özel dosyaları nasıl kullanacağınız konusunda size rehberlik edecektir.

## Sayfalar

Sayfa, bir rotaya **özgü** kullanıcı arayüzüdür. Bir `page.js` dosyasından bir bileşeni dışa aktararak sayfaları tanımlayabilirsiniz. Bir [rota tanımlamak](#rotaların-tanımlanması) için iç içe klasörler ve rotayı genel erişime açmak için bir `page.js` dosyası kullanın.

`app` dizini içine bir `page.js` dosyası ekleyerek ilk sayfanızı oluşturun:

<img alt="sayfalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fpage-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
// `app/page.tsx` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>;
}
```

```tsx
// `app/dashboard/page.tsx` is the UI for the `/dashboard` URL
export default function Page() {
  return <h1>Hello, Dashboard Page!</h1>;
}
```

## Düzenler

Düzen, birden fazla sayfa arasında **paylaşılan** kullanıcı arayüzüdür. Gezinme sırasında düzenler durumu korur, etkileşimli kalır ve yeniden oluşturulmaz. Düzenler iç içe de yerleştirilebilir.

Bir `layout.js` dosyasından bir React bileşenini dışa aktararak `default` olarak bir düzen tanımlayabilirsiniz. Bileşen, render sırasında bir alt düzen (varsa) veya bir alt sayfa ile doldurulacak bir `children` prop kabul etmelidir.

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Flayout-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}: {
  children: React.ReactNode;
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>

      {children}
    </section>
  );
}
```

Bilmekte fayda var:

- En üstteki düzen [Kök Düzen](#kök-düzeni-gerekli) olarak adlandırılır. Bu **gerekli** düzen, bir uygulamadaki tüm sayfalarda paylaşılır. Kök düzenler `html` ve `body` etiketlerini içermelidir.
- Herhangi bir rota segmenti isteğe bağlı olarak kendi Düzenini tanımlayabilir. Bu düzenler o segmentteki tüm sayfalarda paylaşılır.
- Bir rotadaki düzenler varsayılan olarak **iç içedir**. Her üst düzen, React `children` prop kullanarak altındaki alt düzenleri sarar.
- Paylaşılan düzenlere belirli rota segmentlerini dahil etmek ve hariç tutmak için [Rota Gruplarını](#rota-grupları-route-groups) kullanabilirsiniz.
- Düzenler varsayılan olarak Sunucu Bileşenleridir ancak İstemci Bileşeni olarak ayarlanabilir.
- Düzenler veri getirebilir.
- Bir üst düzen ile onun alt düzenleri arasında veri aktarımı mümkün değildir. Bununla birlikte, aynı verileri bir rotada birden fazla kez getirebilirsiniz ve React, performansı etkilemeden istekleri otomatik olarak çıkaracaktır.
- Düzenlerin geçerli rota segmentlerine erişimi yoktur. Rota segmentlerine erişmek için, bir İstemci - Bileşeninde `useSelectedLayoutSegment` veya `useSelectedLayoutSegments` kullanabilirsiniz.
- Düzenler için `.js`, `.jsx` veya `.tsx` dosya uzantıları kullanılabilir.
- Bir `layout.js` ve `page.js` dosyası aynı klasörde tanımlanabilir. Düzen, sayfayı saracaktır.

## Kök Düzeni (Gerekli)

Kök düzen, `app` dizininin en üst düzeyinde tanımlanır ve tüm rotalar için geçerlidir. Bu düzen, sunucudan döndürülen ilk HTML'yi değiştirmenize olanak tanır.

```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

Bilmekte fayda var:

- `app` dizini **mutlaka** bir kök düzen içermelidir.
- Next.js `<html>` ve `<body>` etiketlerini otomatik olarak oluşturmadığı için mutlaka kök düzen tanımlamalıdır.
- `<head>` HTML öğelerini yönetmek için [yerleşik SEO desteğini](#metadata) kullanabilirsiniz, örneğin, `<title>` öğesi.
- Birden fazla kök düzen oluşturmak için [rota gruplarını](#rota-grupları-route-groups) kullanabilirsiniz.
- Kök düzen varsayılan olarak bir [Sunucu Bileşenidir](#sunucu-server-bileşenleri) ve [İstemci Bileşeni](#i̇stemci-client-bileşenleri) olarak ayarlanamaz.

## İç içe Düzenler

Bir klasör içinde tanımlanan düzenler (örn. `app/dashboard/layout.js`) belirli rota segmentlerine (örn. `acme.com/dashboard`) uygulanır ve bu segmentler etkin olduğunda oluşturulur. Varsayılan olarak, dosya hiyerarşisindeki mizanpajlar **iç içe geçmiştir**, bu da children düzenlerini `children` prop'ları aracılığıyla sardıkları anlamına gelir.

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-layout.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return <section>{children}</section>;
}
```

Yukarıdaki iki düzeni birleştirecek olursanız, kök düzen (`app/layout.js`) gösterge tablosu düzenini (`app/dashboard/layout.js`) saracak ve bu da `app/dashboard/*` içindeki rota segmentlerini saracaktır.

İki düzen bu şekilde iç içe geçecektir:

<img alt="düzenler" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-layouts-ui.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

[Rota Gruplarını](#rota-grupları-route-groups), belirli rota segmentlerini paylaşılan düzenlere dahil etmek ve bu düzenlerden çıkarmak için kullanabilirsiniz.

## Şablonlar

Şablonlar, her bir alt düzeni veya sayfayı sarması bakımından düzenlere benzer. Rotalar arasında kalıcı olan ve durumu koruyan düzenlerin aksine, şablonlar gezinme sırasında alt öğelerinin her biri için yeni bir örnek oluşturur. Bu, bir kullanıcı bir şablonu paylaşan rotalar arasında gezindiğinde, bileşenin yeni bir örneğinin monte edildiği, DOM öğelerinin yeniden oluşturulduğu, durumun korunmadığı ve efektlerin yeniden senkronize edildiği anlamına gelir.

Bu belirli davranışlara ihtiyaç duyduğunuz durumlar olabilir ve şablonlar düzenlerden daha uygun bir seçenek olabilir. Örneğin:

- CSS veya animasyon kütüphaneleri kullanarak giriş/çıkış animasyonları.
- `useEffect` (örneğin sayfa görüntülemelerini kaydetme) ve `useState` (örneğin sayfa başına geri bildirim formu) kullanan özellikler.
- Varsayılan framework davranışını değiştirmek için. Örneğin, düzenlerin içindeki Askıya Alma Sınırları, geri dönüşü yalnızca Düzen ilk kez yüklendiğinde gösterir ve sayfalar arasında geçiş yaparken göstermez. Şablonlar için, geri dönüş her gezinmede gösterilir.

Öneri: Şablon kullanmak için özel bir neden yoksa Düzenleri kullanmanız önerilir.

Bir `template.js` dosyasından varsayılan bir React bileşeni dışa aktarılarak bir şablon tanımlanabilir. Bileşen, iç içe segmentler olacak bir `children` prop kabul etmelidir.

<img alt="şablonlar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ftemplate-special-file.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

```tsx
export default function Template({ children }: { children: React.ReactNode }) {
  return <div>{children}</div>;
}
```

Bir düzen ve şablona sahip bir rota segmentinin işlenmiş çıktısı bu şekilde olacaktır:

```tsx
<Layout>
  {/* Note that the template is given a unique key. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

## `<head>`'in değiştirilmesi

`app` dizininde, [yerleşik SEO desteğini](#metadata) kullanarak `başlık` ve `meta` gibi `<head>` HTML öğelerini değiştirebilirsiniz.

Meta veriler, bir `layout.js` veya `page.js` dosyasında bir meta veri nesnesi veya `generateMetadata` işlevi dışa aktarılarak tanımlanabilir.

```tsx
import { Metadata } from "next";

export const metadata: Metadata = {
  title: "Next.js",
};

export default function Page() {
  return "...";
}
```

Bilmekte fayda var: Kök düzenlere `<title>` ve `<meta>` gibi `<head>` etiketlerini manuel olarak **eklememelisiniz**. Bunun yerine, `<head>` öğelerini akışa alma ve çoğaltma gibi gelişmiş gereksinimleri otomatik olarak ele alan Metadata API'sini kullanmalısınız.

# Bağlama ve Gezinme (Linking and Navigating)

Next.js yönlendiricisi, istemci tarafında gezinme ile sunucu merkezli yönlendirme kullanır. Anlık yükleme durumlarını ve eş zamanlı görüntülemeyi destekler.

Rotalar arasında gezinmenin iki yolu vardır:

- `<Link>` Bileşeni
- `useRouter` Kancası

## `<Link>` Bileşeni

`<Link>`, rotalar arasında ön getirme ve istemci tarafında gezinme sağlamak için HTML `<a>` öğesini genişleten bir React bileşenidir. Next.js'de rotalar arasında gezinmenin birincil yoludur.

`<Link>`'i kullanmak için next/link'ten içe aktarın ve bileşene bir href prop iletin:

```tsx
import Link from "next/link";

export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>;
}
```

## Örnekler

### Dinamik Segmentlere Bağlantı

Dinamik segmentlere bağlantı verirken, bir bağlantı listesi oluşturmak için [şablon değişmezlerini ve enterpolasyonu](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) kullanabilirsiniz. Örneğin, blog gönderilerinin bir listesini oluşturmak için:

```tsx
import Link from "next/link";

export default function PostList({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${post.slug}`}>{post.title}</Link>
        </li>
      ))}
    </ul>
  );
}
```

### Aktif Bağlantıları Kontrol Etme

Bir bağlantının etkin olup olmadığını belirlemek için `usePathname()` işlevini kullanabilirsiniz. Örneğin, etkin bağlantıya bir sınıf eklemek için, geçerli yol adının bağlantının `href`'iyle eşleşip eşleşmediğini kontrol edebilirsiniz:

```tsx
"use client";

import { usePathname } from "next/navigation";
import { Link } from "next/link";

export function Navigation({ navLinks }) {
  const pathname = usePathname();

  return (
    <>
      {navLinks.map((link) => {
        const isActive = pathname.startsWith(link.href);

        return (
          <Link
            className={isActive ? "text-blue" : "text-black"}
            href={link.href}
            key={link.name}
          >
            {link.name}
          </Link>
        );
      })}
    </>
  );
}
```

### Bir kimliğe kaydırma (Scrolling to an `id`)

`<Link>`'in varsayılan davranışı, değişen rota segmentinin en üstüne kaydırmaktır. `href` içinde tanımlanmış bir `id` olduğunda, normal bir `<a>` etiketine benzer şekilde belirli id'ye kaydırılır.

Rota segmentinin en üstüne kaydırmayı önlemek için `scroll={false}` olarak ayarlayın ve `href` öğesine karma bir `id` ekleyin:

```tsx
<Link href="/#hashid" scroll={false}>
  Scroll to specific id.
</Link>
```

## `useRouter()` Hook

`useRouter` kancası, İstemci Bileşenleri içindeki rotaları programlı olarak değiştirmenize olanak tanır.

`useRouter`'ı kullanmak için `next/navigation`'dan içe aktarın ve İstemci Bileşeninizin içindeki kancayı çağırın:

```tsx
"use client";

import { useRouter } from "next/navigation";

export default function Page() {
  const router = useRouter();

  return (
    <button type="button" onClick={() => router.push("/dashboard")}>
      Dashboard
    </button>
  );
}
```

Öneri: `useRouter` kullanmak için özel bir gereksiniminiz olmadığı sürece rotalar arasında gezinmek için `<Link>` bileşenini kullanın.

## Navigasyon Nasıl Çalışır?

- `<Link>`kullanılarak veya `router.push()` çağrısı yapılarak bir rota geçişi başlatılır.
- Yönlendirici, tarayıcının adres çubuğundaki URL'yi günceller.
- Yönlendirici, istemci tarafı önbelleğindeki değişmeyen bölümleri (ör. paylaşılan düzenler) yeniden kullanarak gereksiz çalışmayı önler. Bu aynı zamanda kısmi işleme olarak da adlandırılır.
- Yumuşak gezinme koşulları karşılanırsa, yönlendirici yeni segmenti sunucu yerine önbellekten alır. Değilse, yönlendirici sert bir gezinme gerçekleştirir ve Sunucu Bileşeni yükünü sunucudan alır.
- Oluşturulursa, yük getirilirken sunucudan yükleme kullanıcı arayüzü gösterilir.
- Yönlendirici, yeni segmentleri istemcide işlemek için önbelleğe alınan veya yeni yükü kullanır.

### Oluşturulan Sunucu Bileşenlerinin İstemci Tarafında Önbelleğe Alınması

Yeni yönlendirici, Sunucu Bileşenlerinin (yük) işlenmiş sonucunu depolayan bir bellek içi istemci tarafı önbelleğine sahiptir. Önbellek, herhangi bir düzeyde geçersiz kılmaya izin veren ve eşzamanlı render işlemlerinde tutarlılık sağlayan rota segmentlerine bölünmüştür.

Kullanıcılar uygulamada gezinirken, yönlendirici daha önce getirilen segmentlerin ve önceden getirilen segmentlerin yükünü önbellekte depolayacaktır.

Bu, belirli durumlarda yönlendiricinin sunucuya yeni bir istekte bulunmak yerine önbelleği yeniden kullanabileceği anlamına gelir. Bu, verilerin yeniden alınmasını ve bileşenlerin gereksiz yere yeniden oluşturulmasını önleyerek performansı artırır.

### Önbelleğin Geçersiz Kılınması

Sunucu Eylemleri, verileri yola (`revalidatePath`) veya önbellek etiketine (`revalidateTag`) göre isteğe bağlı olarak yeniden doğrulamak için kullanılabilir.

### Prefetching

Prefetching, bir rotayı ziyaret edilmeden önce arka planda önceden yüklemenin bir yoludur. Önceden yüklenen rotaların işlenmiş sonucu yönlendiricinin istemci tarafı önbelleğine eklenir. Bu, önceden yüklenmiş bir rotaya gitmeyi neredeyse anlık hale getirir.

Varsayılan olarak, bileşeni kullanırken görünüm alanında görünür hale geldiklerinde rotalar önceden taranır. Bu, sayfa ilk yüklendiğinde veya kaydırma yoluyla gerçekleşebilir. Rotalar, `useRouter()` kancasının prefetch yöntemi kullanılarak programlı olarak da önceden alınabilir.

#### Statik ve Dinamik Rotalar:

- Rota statikse, rota segmentleri için tüm Sunucu Bileşeni yükleri önceden taranacaktır.
- Rota dinamikse, ilk paylaşılan düzenden ilk `loading.js` dosyasına kadar olan yük önceden taranır. Bu, tüm rotayı dinamik olarak önceden getirmenin maliyetini azaltır ve dinamik rotalar için anlık yükleme durumlarına izin verir.

### Yumuşak Navigasyon (Soft Navigation)

Gezinme sırasında, değiştirilen segmentler için önbellek yeniden kullanılır (varsa) ve veri için sunucuya yeni bir istek yapılmaz.

#### Yumuşak Navigasyon için Koşullar

Navigasyonda Next.js, navigasyon yaptığınız rota önceden taranmışsa ve dinamik segmentler içermiyorsa ya da mevcut rota ile aynı dinamik parametrelere sahipse yumuşak navigasyon kullanacaktır.

Örneğin, dinamik bir `[team]` segmenti içeren aşağıdaki rotayı düşünün: `/dashboard/[team]/*`. `dashboard/[team]/*` altındaki önbelleğe alınmış segmentler yalnızca `[team]` parametresi değiştiğinde geçersiz kılınacaktır.

- `/dashboard/team-red/*` adresinden `/dashboard/team-red/*` adresine gitmek yumuşak bir navigasyon olacaktır.
- `/dashboard/team-red/*` adresinden `/dashboard/team-blue/*` adresine gitmek zor bir navigasyon olacaktır.

### Sert Navigasyon (Hard Navigation)

Gezinme sırasında önbellek geçersiz kılınır ve sunucu verileri yeniden alır ve değiştirilen segmentleri yeniden işler.

### Geri/İleri Navigasyon

Geri ve ileri gezinme (popstate olayı) yumuşak bir gezinme davranışına sahiptir. Bu, istemci tarafı önbelleğinin yeniden kullanıldığı ve gezinmenin neredeyse anlık olduğu anlamına gelir.

### Odaklanma ve Kaydırma Yönetimi

Varsayılan olarak, Next.js odağı ayarlar ve gezinme sırasında değiştirilen segmenti görünüme kaydırır.

# Rota Grupları (Route Groups)

`app` dizininde, iç içe klasörler normalde URL yollarıyla eşlenir. Ancak, klasörün rotanın URL yoluna dahil edilmesini önlemek için bir klasörü Rota Grubu olarak işaretleyebilirsiniz.

Bu özellik, URL yolu yapısını etkilemeden rota segmentlerinizi ve proje dosyalarınızı mantıksal gruplar halinde düzenlemenizi sağlar. Bu, kodunuzun okunabilirliğini ve bakımını kolaylaştırır.

Rota grupları, aşağıdaki durumlar için özellikle kullanışlıdır:

- Rotaları gruplar halinde düzenleme: Bu, site bölümüne, amaca veya ekibe göre rotaları gruplamayı kolaylaştırır.
- Aynı rota segmenti düzeyinde iç içe düzenleri etkinleştirme: Bu, aynı segmentte birden fazla iç içe düzen oluşturmayı ve ortak bir segmentteki rotaların alt kümesine bir düzen eklemeyi mümkün kılar.

Bir klasörün adı parantez içine alınarak bir rota grubu oluşturulabilir: `(folderName)`

## Örnekler

### URL yolunu etkilemeden rotaları düzenleme

URL'yi etkilemeden rotaları düzenlemek için, ilgili rotaları bir arada tutmak üzere bir grup oluşturun. Parantez içindeki klasörler URL'den çıkarılacaktır (örneğin `(marketing)` veya `(shop)`).

<img alt="rota grupları" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-group-organisation.png&w=3840&q=75&dpl=dpl_4MG439i8vBzxyfi2msZH7XDinQ5W" /><br/>

`(marketing)` ve `(shop)` içindeki rotalar aynı URL hiyerarşisini paylaşsa da, klasörlerinin içine bir `layout.js` dosyası ekleyerek her grup için farklı bir düzen oluşturabilirsiniz.

<img alt="rota grupları" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-group-multiple-layouts.png&w=3840&q=75&dpl=dpl_4MG439i8vBzxyfi2msZH7XDinQ5W" /><br/>

### Belirli segmentleri bir düzene dahil etme

Belirli rotaları bir düzene dahil etmek için yeni bir rota grubu oluşturun (örn. `(shop)`) ve aynı düzeni paylaşan rotaları gruba taşıyın (örn. `account` ve `cart`). Grubun dışındaki rotalar düzeni paylaşmayacaktır (örn. `checkout`).

<img alt="rota grupları" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-group-opt-in-layouts.png&w=3840&q=75&dpl=dpl_4MG439i8vBzxyfi2msZH7XDinQ5W" /><br/>

### Çoklu kök düzenleri oluşturma

Birden fazla kök düzen oluşturmak için üst düzey `layout.js` dosyasını kaldırın ve her rota grubunun içine bir `layout.js` dosyası ekleyin. Bu, bir uygulamayı tamamen farklı bir kullanıcı arayüzüne veya deneyime sahip bölümlere ayırmak için kullanışlıdır. `<html>` ve `<body>` etiketlerinin her bir kök düzene eklenmesi gerekir.

<img alt="rota grupları" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-group-multiple-root-layouts.png&w=3840&q=75&dpl=dpl_4MG439i8vBzxyfi2msZH7XDinQ5W" /><br/>

Bilmekte fayda var:

- Rota gruplarının adlandırılması, organizasyon dışında özel bir öneme sahip değildir ve URL yolu üzerinde hiçbir etkisi yoktur.
- Bir rota grubu içeren rotalar, diğer rotalarla aynı URL yoluna çözümlenmemelidir. Yani, `(marketing)/about/page.js` ve `(shop)/about/page.js` rotaları her ikisi de `/about` olarak çözümlenir ve bu bir hataya neden olur.
- Eğer birden fazla kök düzeniniz varsa ve üst düzey bir `layout.js` dosyanız yoksa, ana `page.js` dosyanız rota gruplarından birinde tanımlanmalıdır. Örneğin: `app/(marketing)/page.js.`
- Birden fazla kök düzen arasında gezinmek tam sayfa yüklemesine neden olacaktır. Yani, `app/(shop)/layout.js` kullanan `/cart` sayfasından `app/(marketing)/layout.js` kullanan `/blog` sayfasına gitmek tam sayfa yüklemeye neden olur. Bu durum, yalnızca birden fazla kök düzen için geçerlidir ve istemci tarafı gezinmenin aksine çalışır.

## Metadata
