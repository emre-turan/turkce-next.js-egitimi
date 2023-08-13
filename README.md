<h1 align="center">
  <img alt="logo" src="https://camo.githubusercontent.com/e1e113df83e7731fdb90f6f0ab2eeb155fd1b48c27d99814dcf1c23c0acdc6a2/68747470733a2f2f6173736574732e76657263656c2e636f6d2f696d6167652f75706c6f61642f76313636323133303535392f6e6578746a732f49636f6e5f6461726b5f6261636b67726f756e642e706e67" width="224px"/>
<br>

Next.js Uygulama Yönlendiricisi Dökümantasyonu (Next.js Documentation for App Router)

</h1>

Bu repo, Next.js'in büyülü dünyasına adım atmak isteyenler için özenle hazırlanmış bir öğrenme yolculuğudur. Bu eğitim serisi, Next.js'in temel yapılarını ve özelliklerini, anlaşılır örnekler ve açıklamalarla ele alır.

Bu eğitim serisi, Next.js'i öğrenmek ve ustalaşmak isteyenlere, adım adım bir rehber sunmayı amaçlar. Her bir konu, detaylı ve anlaşılır bir şekilde ele alınmıştır, böylece okuyucuların Next.js'i etkin ve hızlı bir şekilde öğrenmeleri hedeflenir.

Bu eğitim serisini aynı zamanda [gitbook](https://emre-turan.gitbook.io/next.js-doekuemani/) web sitesinden de takip edebilirsiniz.

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

- [React'ın Temelleri (React Essentials) ](#reactın-temelleri-react-essentials)
- [Yönlendirme Temelleri (Routing Fundamentals)](#yönlendirme-temelleri-routing-fundamentals)
- [Render Etme (Rendering) ](#render-etme-rendering)
- [Veri Getirme (Data Fetching)](#veri-getirme-data-fetching)
- [Şekillendirme (Styling)](#şekillendirme-styling)
- [Optimizasyonlar (Optimizations)](#optimizasyonlar-optimizations)
- [Yapılandırma (Configuring))](#yapılandırma-configuring)

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

- Bu model, `children` prop ile düzenlerde ve sayfalarda zaten uygulanmaktadır, bu nedenle ek bir sarmalayıcı bileşen oluşturmanız gerekmez.
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

## Terminoloji

<img alt="yönlendirme-temelleri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fterminology-component-tree.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ"/><br/>

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

Uygulama Yönlendiricisi, Sayfa Yönlendiricisine göre önceliklidir. Dizinler arasındaki yönlendirmeler aynı URL yoluna çözümlenmemelidir ve bir çakışmayı önlemek için derleme zamanı hatasına neden olur.

<img alt="uygulama-yönlendiricisi" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnext-router-directories.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Varsayılan olarak, uygulama içindeki bileşenler React Sunucu Bileşenleridir. Bu bir performans optimizasyonudur ve bunları kolayca benimsemenizi sağlar ve ayrıca İstemci Bileşenlerini de kullanabilirsiniz.

## Klasörlerin ve Dosyaların Rolleri

Next.js dosya sistemi tabanlı bir yönlendirici kullanır:

- **Klasörler** rotaları tanımlamak için kullanılır. Rota, **kök klasörden** `page.js` dosyasını içeren son bir **yaprak klasöre** kadar dosya sistemi hiyerarşisini takip eden, iç içe geçmiş klasörlerden oluşan tek bir yoldur.

- **Dosyalar**, bir rota segmenti için gösterilen kullanıcı arayüzünü oluşturmak için kullanılır.

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

## İstemci Tarafında Gezinme ile Sunucu Merkezli Yönlendirme

İstemci tarafı yönlendirme kullanan `pages` dizininin aksine, `app router`, Sunucu Bileşenleri ve sunucuda veri getirme ile uyum sağlamak için **sunucu merkezli yönlendirme** kullanır. Sunucu merkezli yönlendirme ile istemcinin bir rota haritası indirmesi gerekmez ve Sunucu Bileşenleri için aynı istek rotaları aramak için kullanılabilir. Bu optimizasyon tüm uygulamalar için yararlıdır, ancak çok sayıda rotaya sahip uygulamalar üzerinde daha büyük bir etkiye sahiptir.

Yönlendirme sunucu merkezli olmasına rağmen, yönlendirici, Tek Sayfalı Uygulama davranışına benzeyen Bağlantı Bileşeni ile **istemci tarafında gezinmeyi** kullanır. Bu, bir kullanıcı yeni bir rotaya gittiğinde tarayıcının sayfayı yeniden yüklemeyeceği anlamına gelir. Bunun yerine, URL güncellenecek ve Next.js yalnızca değişen bölümleri oluşturacaktır.

Ayrıca, kullanıcılar uygulamada gezinirken, yönlendirici React Sunucu Bileşeni yükünün sonucunu **bellek içi istemci tarafı önbelleğinde** saklar. Önbellek, herhangi bir seviyede geçersiz kılmaya izin veren ve React'in eşzamanlı render'ları arasında tutarlılık sağlayan rota segmentlerine bölünmüştür. Bu, belirli durumlarda, daha önce getirilmiş bir segmentin önbelleğinin yeniden kullanılabileceği ve performansı daha da artıracağı anlamına gelir.

## Kısmi Rendering

Kardeş rotalar arasında gezinirken (örneğin aşağıdaki `/dashboard/settings` ve `/dashboard/analytics`), Next.js yalnızca değişen rotalardaki düzenleri ve sayfaları getirecek ve oluşturacaktır. Alt ağaçtaki segmentlerin üzerindeki hiçbir şeyi yeniden **getirmeyecek veya yeniden oluşturmayacaktır**. Bu, bir düzeni paylaşan rotalarda, bir kullanıcı kardeş sayfalar arasında gezindiğinde düzenin korunacağı anlamına gelir.

<img alt="kısmi rendering" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fpartial-rendering.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Kısmi rendering olmadan, her gezinti tüm sayfanın sunucuda yeniden işlenmesine neden olur. Yalnızca güncellenen bölümün render edilmesi, aktarılan veri miktarını ve yürütme süresini azaltarak performansın artmasını sağlar.

## Gelişmiş Yönlendirme Kalıpları

Uygulama Yönlendirici ayrıca daha gelişmiş yönlendirme modellerini uygulamanıza yardımcı olacak bir dizi kural sunar. Bunlar şunları içerir:

- Paralel Rotalar: Aynı görünümde bağımsız olarak gezinilebilen iki veya daha fazla sayfayı aynı anda göstermenizi sağlar. Bunları, kendi alt navigasyonları olan bölünmüş görünümler için kullanabilirsiniz. Örn. gösterge tabloları.
- Rotaları Kesme: Bir rotayı kesmenize ve başka bir rota bağlamında göstermenize izin verir. Geçerli sayfanın bağlamını korumak önemli olduğunda bunları kullanabilirsiniz. Örneğin, bir görevi düzenlerken tüm görevleri görmek veya bir akıştaki bir fotoğrafı genişletmek.

# Rotaların Tanımlanması

## Rotalar Oluşturma

Next.js, rotaları tanımlamak için **klasörlerin** kullanıldığı dosya sistemi tabanlı bir yönlendirici kullanır.

Her klasör, bir **URL** segmentiyle eşleşen bir rota segmentini temsil eder. İç içe bir rota oluşturmak için, klasörleri birbirinin içine yerleştirebilirsiniz.

<img alt="rotalar oluşturma" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Rota segmentlerini genel erişime açmak için özel bir `page.js` dosyası kullanılır.

<img alt="rotalar oluşturma-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fdefining-routes.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Bu örnekte, `/dashboard/analytics` URL yolu, karşılık gelen bir `page.js` dosyasına sahip olmadığı için _genel erişime_ açık değildir. Bu klasör bileşenleri, stil sayfalarını, görüntüleri veya diğer ortak dosyaları depolamak için kullanılabilir.

## Kullanıcı Arayüzü Oluşturma

Her bir rota segmenti için kullanıcı arayüzü oluşturmak üzere özel dosya kuralları kullanılır. En yaygın olanları, bir rotaya özgü kullanıcı arayüzünü gösteren sayfalar ve birden fazla rotada paylaşılan kullanıcı arayüzünü gösteren düzenlerdir.

Örneğin, ilk sayfanızı oluşturmak için `app` dizininin içine bir `page.js` dosyası ekleyin ve bir React bileşenini dışa aktarın:

```tsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
```

# Sayfalar ve Düzenler

## Sayfalar

Sayfa, bir rotaya **özgü** kullanıcı arayüzüdür. Bir `page.js` dosyasından bir bileşeni dışa aktararak sayfaları tanımlayabilirsiniz. Bir rota tanımlamak için iç içe klasörler ve rotayı genel erişime açmak için bir `page.js` dosyası kullanın.

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

- En üstteki düzen Kök Düzen olarak adlandırılır. Bu **gerekli** düzen, bir uygulamadaki tüm sayfalarda paylaşılır. Kök düzenler `html` ve `body` etiketlerini içermelidir.
- Herhangi bir rota segmenti isteğe bağlı olarak kendi Düzenini tanımlayabilir. Bu düzenler o segmentteki tüm sayfalarda paylaşılır.
- Bir rotadaki düzenler varsayılan olarak **iç içedir**. Her üst düzen, React `children` prop kullanarak altındaki alt düzenleri sarar.
- Paylaşılan düzenlere belirli rota segmentlerini dahil etmek ve hariç tutmak için Rota Gruplarını kullanabilirsiniz.
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
- `<head>` HTML öğelerini yönetmek için yerleşik SEO desteğini kullanabilirsiniz, örneğin, `<title>` öğesi.
- Birden fazla kök düzen oluşturmak için rota gruplarınıkullanabilirsiniz.
- Kök düzen varsayılan olarak bir Sunucu Bileşenidir ve İstemci Bileşeni olarak ayarlanamaz.

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

Rota Gruplarını, belirli rota segmentlerini paylaşılan düzenlere dahil etmek ve bu düzenlerden çıkarmak için kullanabilirsiniz.

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

`app` dizininde, yerleşik SEO desteğini kullanarak `başlık` ve `meta` gibi `<head>` HTML öğelerini değiştirebilirsiniz.

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

# Dinamik Rotalar (Dynamic Routes)

Segment adlarını önceden tam olarak bilmediğinizde ve dinamik verilerden rotalar oluşturmak istediğinizde, istek zamanında doldurulan veya derleme zamanında önceden oluşturulan Dinamik Segmentleri kullanabilirsiniz.

Bir Dinamik Segment, bir klasörün adını köşeli parantezler içine alarak oluşturulabilir: `[folderName]`. Örneğin, `[id]` veya `[slug]`.

Dinamik Segmentler `layout`, `page`, `route` ve `generateMetadata` fonksiyonlarına `params` prop olarak aktarılır.

Örneğin, bir blog aşağıdaki `app/blog/[slug]/page.js` rotasını içerebilir; burada `[slug]` blog gönderileri için Dinamik Segmenttir.

```ts
export default function Page({ params }: { params: { slug: string } }) {
  return <div>My Post: {params.slug}</div>;
}
```

| Rota                         | Örnek URL     | `Params`                   |
| ---------------------------- | ------------- | -------------------------- |
| `app/shop/[...slug]/page.js` | `/shop/a`     | `{ slug: ['a'] }`          |
| `app/shop/[...slug]/page.js` | `/shop/a/b`   | `{ slug: ['a', 'b'] }`     |
| `app/shop/[...slug]/page.js` | `/shop/a/b/c` | `{ slug: ['a', 'b', 'c']}` |

## İsteğe Bağlı Her Şeyi Yakalayan Segmentler (Optional Catch-all Segments)

Catch-all Segmentleri, parametreyi çift köşeli parantez içine alarak isteğe bağlı hale getirilebilir: `[[...folderName]]`.

Örneğin, `app/shop/[[...slug]]/page.js`, `/shop/clothes`, `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`'e ek olarak `/shop` ile de eşleşecektir.

`Tümünü yakala` ve `isteğe bağlı tümünü yakala` segmentleri arasındaki fark, isteğe bağlı olduğunda parametre içermeyen rotanın da eşleştirilmesidir (yukarıdaki örnekte `/shop`).

| Route                          | Example URL   | `Params`                   |
| ------------------------------ | ------------- | -------------------------- |
| `app/shop/[[...slug]]/page.js` | `/shop`       | `{}`                       |
| `app/shop/[[...slug]]/page.js` | `/shop/a`     | `{ slug: ['a'] }`          |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b`   | `{ slug: ['a', 'b'] }`     |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b/c` | `{ slug: ['a', 'b', 'c']}` |

### TypeScript

TypeScript kullanırken, yapılandırılmış rota segmentinize bağlı olarak `params` için türler ekleyebilirsiniz.

```ts
export default function Page({ params }: { params: { slug: string } }) {
  return <h1>My Page</h1>;
}
```

| Route                               | `Params` Type Definition                 |
| ----------------------------------- | ---------------------------------------- |
| `app/blog/[slug]/page.js`           | `{ slug: string }`                       |
| `app/shop/[...slug]/page.js`        | `{ slug: string[] }`                     |
| `app/[categoryId]/[itemId]/page.js` | `{ categoryId: string, itemId: string }` |

# Kullanıcı Arayüzünü Yükleme ve Akış (Loading UI and Streaming)

Özel `loading.js` dosyası, React Suspense ile anlamlı bir Yükleme Kullanıcı Arayüzü oluşturmanıza yardımcı olur. Bu kural ile, bir rota segmentinin içeriği yüklenirken sunucudan anlık bir yükleme state'i gösterebilirsiniz, render alma işlemi tamamlandığında yeni içerik otomatik olarak değiştirilir.

<img alt="loading" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Floading-ui.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

## Anında Yükleme Durumları (Instant Loading States)

Anında yükleme state'i, gezinmenin hemen ardından gösterilen yedek kullanıcı arayüzüdür. İskeletler ve döndürücüler gibi yükleme göstergelerini veya kapak fotoğrafı, başlık vb. gibi gelecekteki ekranların küçük ama anlamlı bir bölümünü önceden render edebilirsiniz. Bu, kullanıcıların uygulamanın yanıt verdiğini anlamasına yardımcı olur ve daha iyi bir kullanıcı deneyimi sağlar.

Bir klasörün içine bir `loading.js` dosyası ekleyerek bir yükleme durumu oluşturun.

<img alt="loading-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Floading-special-file.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

```ts
export default function Loading() {
  // İskelet de dahil olmak üzere Loading içine herhangi bir kullanıcı arayüzü ekleyebilirsiniz.
  return <LoadingSkeleton />;
}
```

Aynı klasörde, `loading.js` dosyası `layout.js` dosyasının içine yerleştirilecektir. Otomatik olarak `page.js` dosyasını ve altındaki tüm alt elemanları bir `<Suspense>` sınırına saracaktır.

<img alt="loading-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Floading-overview.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

Bilmekte fayda var:

- Sunucu merkezli yönlendirmede bile navigasyon anında gerçekleşir.
- Navigasyon kesintiye uğramaz, yani rota değiştirirken başka bir rotaya geçmeden önce rotanın içeriğinin tamamen yüklenmesini beklemek gerekmez.
- Yeni rota segmentleri yüklenirken paylaşılan düzenler etkileşimli kalır.

**Öneri**: Next.js bu işlevi optimize ettiğinden, rota segmentleri (düzenler ve sayfalar) için `loading.js` kuralını kullanın.

## Gerilim ile Akış (Streaming with Suspense)

`loading.js`'e ek olarak, kendi UI bileşenleriniz için manuel olarak da Suspense Boundaries oluşturabilirsiniz. App Router, hem Node.js hem de Edge çalışma zamanları için [Suspense](https://react.dev/reference/react/Suspense) ile akışı destekler.

### Akış Nedir?

Akış'ın React ve Next.js'de nasıl çalıştığını öğrenmek için Sunucu Tarafı Render Etme (SSR) ve sınırlamalarını anlamak faydalı olacaktır.

SSR ile, bir kullanıcının bir sayfayı görebilmesi ve etkileşimde bulunabilmesi için tamamlanması gereken bir dizi adım vardır:

1. İlk olarak, belirli bir sayfa için tüm veriler sunucudan alınır.
2. Sunucu daha sonra sayfa için HTML render eder.
3. Sayfa için HTML, CSS ve JavaScript istemciye gönderilir.
4. Oluşturulan HTML ve CSS kullanılarak etkileşimli olmayan bir kullanıcı arayüzü gösterilir.
5. Son olarak, React kullanıcı arayüzünü [etkileşimli](https://react.dev/reference/react-dom/client/hydrateRoot#hydrating-server-rendered-html) hale getirir.

<img alt="loading-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fserver-rendering-without-streaming-chart.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

Bu adımlar sıralı ve engelleyicidir, yani sunucu ancak tüm veriler getirildikten sonra bir sayfanın HTML'sini render edebilir. İstemcide ise React, kullanıcı arayüzünü ancak sayfadaki tüm bileşenlerin kodu indirildikten sonra etkileşimli hale getirebilir.

React ve Next.js ile SSR, kullanıcıya mümkün olan en kısa sürede etkileşimli olmayan bir sayfa göstererek algılanan yükleme performansını iyileştirmeye yardımcı olur.

<img alt="loading-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fserver-rendering-without-streaming.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

Ancak, sayfanın kullanıcıya gösterilebilmesi için sunucuda tüm veri getirme işlemlerinin tamamlanması gerektiğinden bu süreç yine de yavaş olabilir.

**Akış**, sayfanın HTML'sini daha küçük parçalara ayırmanıza ve bu parçaları sunucudan istemciye aşamalı olarak göndermenize olanak tanır.

<img alt="loading-5" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fserver-rendering-with-streaming.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

Bu, herhangi bir kullanıcı arayüzü render edilmeden önce tüm verilerin yüklenmesini beklemeden sayfanın bazı bölümlerinin daha erken görüntülenmesini sağlar.

Akış, React'in bileşen modeliyle iyi çalışır çünkü her bileşen bir yığın olarak kabul edilebilir. Daha yüksek önceliğe sahip (örn. ürün bilgileri) veya veriye bağlı olmayan bileşenler önce gönderilebilir (örn. düzen) ve React hidrasyona daha erken başlayabilir. Daha düşük önceliğe sahip bileşenler (ör. incelemeler, ilgili ürünler), verileri alındıktan sonra aynı sunucu isteğinde gönderilebilir.

<img alt="loading-6" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fserver-rendering-with-streaming-chart.png&w=3840&q=75&dpl=dpl_DS6dPw9iM1MterzWfxufB6ivU12S" /><br/>

Akış, [İlk Bayta Kadar Geçen Süreyi (TTFB)](https://web.dev/ttfb/) ve [İlk İçerik Boyamasını (FCP)](https://web.dev/first-contentful-paint/) azaltabileceğinden, uzun veri isteklerinin sayfanın render edilmesini engellemesini önlemek istediğinizde özellikle faydalıdır. Ayrıca, özellikle yavaş cihazlarda [Etkileşim Süresini (TTI)](https://developer.chrome.com/en/docs/lighthouse/performance/interactive/) iyileştirmeye yardımcı olur.

**Örnek:**

`<Suspense>`, eşzamansız bir eylem (örneğin veri getirme) gerçekleştiren bir bileşeni sararak, eylem gerçekleşirken yedek kullanıcı arayüzünü (örneğin iskelet, döndürücü) göstererek ve ardından eylem tamamlandığında bileşeninizi değiştirerek çalışır.

```ts
import { Suspense } from "react";
import { PostFeed, Weather } from "./Components";

export default function Posts() {
  return (
    <section>
      <Suspense fallback={<p>Loading feed...</p>}>
        <PostFeed />
      </Suspense>
      <Suspense fallback={<p>Loading weather...</p>}>
        <Weather />
      </Suspense>
    </section>
  );
}
```

Suspense kullanarak şu avantajları elde edersiniz:

1. Streaming Server Rendering - HTML'in sunucudan istemciye aşamalı olarak render edilmesi.
2. Seçici Hidrasyon - React, kullanıcı etkileşimine göre hangi bileşenlerin önce etkileşimli hale getirileceğine öncelik verir.

Daha fazla Suspense örneği ve kullanım senaryosu için lütfen [React Dokümantasyonuna](https://react.dev/reference/react/Suspense) bakınız.

**SEO**

- Next.js, istemciye UI akışı yapmadan önce `generateMetadata` içindeki veri getirme işleminin tamamlanmasını bekler. Bu, akışlı bir yanıtın ilk bölümünün `<head>` etiketlerini içermesini garanti eder.
- Akış, sunucu tarafından render edildiği için SEO'yu etkilemez. Sayfanızın Google'ın web tarayıcılarında nasıl göründüğünü görmek ve serileştirilmiş HTML'yi ([kaynak](https://web.dev/rendering-on-the-web/#seo-considerations)) görüntülemek için Google'ın [Mobil Dostu Test](https://search.google.com/test/mobile-friendly) aracını kullanabilirsiniz.

# Hata İşleme (Error Handling)

`error.js` dosya kuralı, iç içe geçmiş rotalarda çalışma zamanı hatalarını zarif bir şekilde ele almanıza olanak tanır.

- Bir rota segmentini ve iç içe geçmiş alt segmentlerini otomatik olarak bir [React Hata Sınırına](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary) sarın.
- Ayrıntılılığı ayarlamak için dosya sistemi hiyerarşisini kullanarak belirli segmentlere uyarlanmış hata kullanıcı arayüzü oluşturun.
- Uygulamanın geri kalanını işlevsel tutarken hataları etkilenen segmentlere izole edin.
- Tam sayfa yeniden yükleme olmadan bir hatadan kurtulmayı denemek için işlevsellik ekleyin.

Bir rota segmentinin içine bir `error.js` dosyası ekleyerek ve bir React bileşenini dışa aktararak hata kullanıcı arayüzü oluşturun:

<img alt="error" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ferror-special-file.png&w=3840&q=75&dpl=dpl_G1mtmG8Eq9P8U8iiGPcqaT83bNbK" /><br/>

```ts
"use client"; // Error components must be Client Components

import { useEffect } from "react";

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  useEffect(() => {
    // Hatayı bir hata raporlama hizmetine kaydedin
    console.error(error);
  }, [error]);

  return (
    <div>
      <h2>Something went wrong!</h2>
      <button
        onClick={
          // Segmenti yeniden oluşturmayı deneyerek kurtarmaya çalışın
          () => reset()
        }
      >
        Try again
      </button>
    </div>
  );
}
```

## `error.js` Nasıl Çalışır?

<img alt="error-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ferror-overview.png&w=3840&q=75&dpl=dpl_G1mtmG8Eq9P8U8iiGPcqaT83bNbK" /><br/>

- `error.js` otomatik olarak iç içe geçmiş bir alt segmenti veya `page.js` bileşenini saran bir React Hata Sınırı oluşturur.
- `error.js` dosyasından dışa aktarılan React bileşeni, yedek bileşen olarak kullanılır.
- Hata sınırı içinde bir hata atılırsa, hata içerilir ve yedek bileşen render edilir.
- Yedek hata bileşeni etkin olduğunda, hata sınırının üzerindeki düzenler durumlarını korur ve etkileşimli kalır ve hata bileşeni hatadan kurtulmak için işlevsellik görüntüleyebilir.

## Hatalardan Kurtarma

Bir hatanın nedeni bazen geçici olabilir. Bu durumlarda, sadece tekrar denemek sorunu çözebilir.

Bir hata bileşeni `reset()` fonksiyonunu kullanarak kullanıcıdan hatadan kurtulmaya çalışmasını isteyebilir. İşlev çalıştırıldığında, Hata sınırının içeriğini yeniden render etmeye çalışır. Başarılı olursa, yedek hata bileşeni yeniden render etme işleminin sonucuyla değiştirilir.

```ts
"use client";

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

## İç İçe Rotalar (Nested Routes)

Özel dosyalar aracılığıyla oluşturulan React bileşenleri, belirli bir iç içe hiyerarşi içinde oluşturulur.

Örneğin, her ikisi de `layout.js` ve `error.js` dosyalarını içeren iki segmente sahip iç içe geçmiş bir rota aşağıdaki basitleştirilmiş bileşen hiyerarşisinde oluşturulur:

<img alt="error-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fnested-error-component-hierarchy.png&w=3840&q=75&dpl=dpl_G1mtmG8Eq9P8U8iiGPcqaT83bNbK" /><br/>

İç içe geçmiş bileşen hiyerarşisi, `error.js` dosyalarının iç içe geçmiş bir rota boyunca davranışı üzerinde etkilere sahiptir:

- Hatalar en yakın üst hata sınırına kadar kabarır. Bu, bir `error.js` dosyasının iç içe geçmiş tüm alt segmentleri için hataları işleyeceği anlamına gelir. Daha fazla veya daha az ayrıntılı hata kullanıcı arayüzü, `error.js` dosyalarını bir rotanın iç içe geçmiş klasörlerinde farklı seviyelere yerleştirerek elde edilebilir.
- Bir `error.js` sınırı, **aynı** segmentteki bir `layout.js` bileşeninde atılan hataları işlemez çünkü hata sınırı bu layout bileşeninin **içinde** yuvalanmıştır.

## Düzenlerde Hataları İşleme (Handling Errors in Layouts)

`error.js` sınırları, aynı segmentteki `layout.js` veya `template.js` bileşenlerinde atılan hataları yakalamaz. Bu kasıtlı hiyerarşi, bir hata oluştuğunda kardeş rotalar arasında paylaşılan önemli kullanıcı arayüzünü (navigasyon gibi) görünür ve işlevsel tutar.

Belirli bir düzen veya şablon içindeki hataları işlemek için, düzenlerin üst segmentine bir `error.js` dosyası yerleştirin.

Kök düzen veya şablon içindeki hataları işlemek için,`global-error.js` adı verilen `error.js`'nin bir varyasyonunu kullanın.

## Kök Düzenlerde Hataları İşleme (Handling Errors in Root Layouts)

Kök `app/error.js` sınırı, kök `app/layout.js` veya `app/template.js` bileşeninde atılan hataları yakalamaz.

Bu kök bileşenlerdeki hataları özel olarak ele almak için, kök uygulama dizininde bulunan `app/global-error.js` adlı `error.js` varyasyonunu kullanın.

Kök `error.js`'den farklı olarak, `global-error.js` hata sınırı tüm uygulamayı sarar ve yedek bileşeni etkin olduğunda kök düzeninin yerini alır. Bu nedenle, `global-error.js`'nin kendi `<html>` ve `<body>` etiketlerini tanımlaması gerektiğine dikkat etmek önemlidir.

`global-error.js` en az ayrıntılı hata kullanıcı arayüzüdür ve tüm uygulama için "catch-all" hata işleme olarak düşünülebilir. Kök bileşenler genellikle daha az dinamik olduğundan ve diğer `error.js` sınırları çoğu hatayı yakalayacağından sık sık tetiklenmesi pek olası değildir.

Bir `global-error.js` tanımlanmış olsa bile, geri dönüş bileşeni global olarak paylaşılan kullanıcı arayüzü ve markalamayı içeren kök düzen içinde oluşturulacak bir kök `error.js` tanımlanması önerilir.

```ts
"use client";

export default function GlobalError({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  return (
    <html>
      <body>
        <h2>Something went wrong!</h2>
        <button onClick={() => reset()}>Try again</button>
      </body>
    </html>
  );
}
```

## Sunucu Hatalarını İşleme (Handling Server Errors)

Veri getirme sırasında veya bir Sunucu Bileşeni içinde bir hata atılırsa, Next.js ortaya çıkan `Error` nesnesini hata prop'u olarak en yakın `error.js` dosyasına iletecektir.

`Next dev` çalıştırılırken `error` serileştirilir ve Sunucu Bileşeninden istemci `error.js`'ye iletilir. Üretimde `next start` çalıştırılırken güvenliği sağlamak için, hata mesajının bir özetini içeren bir `.digest` ile birlikte hataya genel bir `error` mesajı iletilir. Bu özet, sunucu günlüklerine karşılık gelmek için kullanılabilir.

# Paralel Rotalar (Parallel Routes)

Paralel Yönlendirme, bir veya daha fazla sayfayı aynı düzende eşzamanlı veya koşullu olarak render etmenize olanak tanır. Bir uygulamanın gösterge tabloları ve sosyal sitelerdeki beslemeler gibi son derece dinamik bölümleri için Paralel Yönlendirme, karmaşık yönlendirme modellerini uygulamak için kullanılabilir.

Örneğin, ekip ve analiz sayfalarını aynı anda oluşturabilirsiniz.

<img alt="paralel-rotalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Paralel Yönlendirme, her bir rota için bağımsız hata ve yükleme durumları tanımlamanıza olanak tanır.

<img alt="paralel-rotalar-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-cinematic-universe.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Paralel Yönlendirme, kimlik doğrulama durumu gibi belirli koşullara bağlı olarak bir yuvayı koşullu olarak render etmenize da olanak tanır. Bu, aynı URL üzerinde tamamen ayrılmış kod sağlar.

<img alt="paralel-rotalar-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

## Kongre (Convention)

Paralel rotalar adlandırılmış **yuvalar** kullanılarak oluşturulur. Yuvalar `@folder` konvansiyonu ile tanımlanır ve aynı seviyedeki düzene prop olarak aktarılır.

Yuvalar rota segmentleri değildir ve URL yapısını etkilemez. `/@team/members` dosya yoluna `/members` adresinden erişilebilir.

Örneğin, aşağıdaki dosya yapısı iki açık yuva tanımlar: `@analytics` ve `@team`.

<img alt="paralel-rotalar-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-file-system.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Yukarıdaki klasör yapısı, `app/layout.js`'deki bileşenin artık `@analytics` ve `@team` slots prop'larını kabul ettiği ve bunları `alt eleman` prop ile birlikte paralel olarak render edebileceği anlamına gelir:

```ts
export default function Layout(props: {
  children: React.ReactNode;
  analytics: React.ReactNode;
  team: React.ReactNode;
}) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  );
}
```

Bilmekte fayda var: `alt eleman` prop'u, bir klasörle eşleştirilmesi gerekmeyen örtük bir yuvadır. Bu, `app/page.js`'nin `app/@children/page.js` ile eşdeğer olduğu anlamına gelir.

## Eşleşmeyen Rotalar (Unmatched Routes)

Varsayılan olarak, bir yuva içinde oluşturulan içerik geçerli URL ile eşleşir.

Eşleşmeyen bir yuva olması durumunda, Next.js'nin işlediği içerik yönlendirme tekniğine ve klasör yapısına göre farklılık gösterir.

### `default.js`

Next.js geçerli URL'ye göre bir yuvanın etkin durumunu kurtaramadığında geri dönüş olarak render edilecek bir `default.js` dosyası tanımlayabilirsiniz.

Aşağıdaki klasör yapısını düşünün. `@team` yuvasının bir `settings` dizini var, ancak `@analytics`'in yok.

<img alt="paralel-rotalar-5" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Kök `/` dizininden `/settings` dizinine giderseniz, gezinme türüne ve `default.js` dosyasının kullanılabilirliğine bağlı olarak render edilen içerik farklı olur.

|                 | `@analytics/default.js` ile                         | `@analytics/default.js` olmadan                  |
| --------------- | --------------------------------------------------- | ------------------------------------------------ |
| Soft Navigation | `@team/settings/page.js` ve `@analytics/page.js`    | `@team/settings/page.js` ve `@analytics/page.js` |
| Hard Navigation | `@team/settings/page.js` ve `@analytics/default.js` | 404                                              |

### Yumuşak Navigasyon (Soft Navigation)

Yumuşak bir navigasyonda - Next.js, geçerli URL ile eşleşmese bile yuvanın daha önce etkin olan durumunu oluşturur.

### Sert Navigasyon (Hard Navigation)

Zor bir navigasyonda (bütün sayfanın yeniden yüklenmesini gerektiren bir navigasyon) Next.js önce eşleşmeyen yuvanın default.js dosyasını render etmeye çalışır. Eğer bu dosya mevcut değilse, bir 404 görüntülenir.

Eşleşmeyen rotalar için 404, paralel olarak render edilmemesi gereken bir rotayı yanlışlıkla render etmenizi sağlamaya yardımcı olur.

### `useSelectedLayoutSegment(s)`

Hem `useSelectedLayoutSegment` hem de `useSelectedLayoutSegments`, o yuvadaki etkin rota segmentini okumanızı sağlayan bir `parallelRoutesKey` kabul eder.

```ts
"use client";

import { useSelectedLayoutSegment } from "next/navigation";

export default async function Layout(props: {
  //...
  authModal: React.ReactNode;
}) {
  const loginSegments = useSelectedLayoutSegment("authModal");
  // ...
}
```

Bir kullanıcı URL çubuğunda `@authModal/login` veya `/login` adresine gittiğinde, `loginSegments` `"login"` dizesine eşit olacaktır.

## Örnekler

### Modaller (Modals)

Paralel Yönlendirme, modları render etmek için kullanılabilir.

<img alt="paralel-rotalar-6" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-auth-modal.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

`authModal` yuvası, örneğin `/login` gibi eşleşen bir rotaya gidilerek gösterilebilen bir `<Modal>` bileşeni oluşturur.

app/layout.tsx:

```ts
export default async function Layout(props: {
  // ...
  authModal: React.ReactNode;
}) {
  return (
    <>
      {/* ... */}
      {props.authModal}
    </>
  );
}
```

app/@authModal/login/page.tsx:

```ts
import { Modal } from "components/modal";

export default function Login() {
  return (
    <Modal>
      <h1>Login</h1>
      {/* ... */}
    </Modal>
  );
}
```

Modal etkin olmadığında içeriğinin işlenmemesini sağlamak için `null` döndüren bir `default.js` dosyası oluşturabilirsiniz.

app/@authModal/login/default.tsx:

```ts
export default function Default() {
  return null;
}
```

### Bir modalın kapatılması (Dismissing a modal)

İstemci gezintisi yoluyla, örneğin `<Link href="/login">` kullanılarak bir modal başlatılmışsa, `router.back()` öğesini çağırarak veya bir `Link` bileşeni kullanarak modalı kapatabilirsiniz.

app/@authModal/login/page.tsx:

```ts
"use client";
import { useRouter } from "next/navigation";
import { Modal } from "components/modal";

export default async function Login() {
  const router = useRouter();
  return (
    <Modal>
      <span onClick={() => router.back()}>Close modal</span>
      <h1>Login</h1>
      ...
    </Modal>
  );
}
```

Başka bir yere gitmek ve bir modalı kapatmak istiyorsanız, her şeyi kapsayan bir rota da kullanabilirsiniz.

<img alt="paralel-rotalar-7" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-catchall.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

app/@authModal/[...catchAll]/page.tsx:

```ts
export default function CatchAll() {
  return null;
}
```

Catch-all rotaları `default.js`'ye göre önceliklidir.

## Koşullu Rotalar (Conditional Routes)

Paralel Rotalar koşullu yönlendirme uygulamak için kullanılabilir. Örneğin, kimlik doğrulama durumuna bağlı olarak bir `@dashboard` veya `@login` rotası render edebilirsiniz.

```ts
import { getUser } from "@/lib/auth";

export default function Layout({ params, dashboard, login }) {
  const isLoggedIn = getUser();
  return isLoggedIn ? dashboard : login;
}
```

<img alt="paralel-rotalar-8" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

# Kesen Rotalar (Intercepting Routes)

Rotaları kesmek, geçerli sayfanın bağlamını korurken geçerli düzen içinde bir rota yüklemenize olanak tanır. Bu yönlendirme paradigması, farklı bir rota göstermek için belirli bir rotayı "kesmek" istediğinizde yararlı olabilir.

Örneğin, bir beslemenin içinden bir fotoğrafa tıklandığında, beslemeyi kaplayan bir modal fotoğrafla birlikte görünmelidir. Bu durumda Next.js, `/feed` yolunu keser ve bunun yerine `/photo/123` göstermek için bu URL'yi "maskeler".

<img alt="kesen-rotalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepting-routes-soft-navigate.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Ancak, örneğin paylaşılabilir bir URL'ye tıklayarak veya sayfayı yenileyerek doğrudan fotoğrafa gidildiğinde, modal yerine fotoğraf sayfasının tamamı render edilmelidir. Herhangi bir rota müdahalesi gerçekleşmemelidir.

<img alt="kesen-rotalar-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepting-routes-hard-navigate.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Convention

Kesişen rotalar, göreli yol kuralı `../`'ye benzeyen ancak segmentler için olan `(..)` kuralı ile tanımlanabilir.

Şu şekillerde Kullanabilirsiniz:

- `(.)` aynı seviyedeki segmentleri eşleştirmek için
- `(..)` bir üst seviyedeki segmentlerle eşleştirmek için
- `(..)(..)` iki seviye yukarıdaki segmentlerle eşleştirmek için
- `(...)` kök uygulama dizinindeki segmentleri eşleştirmek için

Örneğin, bir `(..)photo` dizini oluşturarak `fotoğraf` segmentini `besleme` segmenti içinden kesebilirsiniz.

<img alt="kesen-rotalar-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepted-routes-files.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

`(..)` kuralının dosya sistemini değil, yol segmentlerini temel aldığını unutmayın.

## Modaller (Modals)

Yakalama Rotaları, modaller oluşturmak için Paralel Rotalar ile birlikte kullanılabilir.

Bu kalıbı kullanarak modaller oluşturmak, modallerle çalışırken karşılaşılan bazı zorlukların üstesinden gelmenizi sağlar:

- Modal içeriği bir URL aracılığıyla paylaşılabilir hale getirin
- Sayfa yenilendiğinde, modalı kapatmak yerine bağlamı koruyun
- Önceki rotaya gitmek yerine geriye doğru gezinmede modalı kapatın
- İleriye doğru gezinme modalini yeniden açma

<img alt="kesen-rotalar-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepted-routes-modal-example.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Yukarıdaki örnekte, `@modal` bir segment değil bir slot olduğu için `photo` segmentine giden yol `(..)` eşleştiricisini kullanabilir. Bu, iki dosya sistemi seviyesi daha yüksek olmasına rağmen `photo` yolunun yalnızca bir segment seviyesi daha yüksek olduğu anlamına gelir.

Diğer örnekler arasında, özel bir `/login` sayfasına sahipken üst navbarda bir oturum açma modalı açmak veya bir yan modalda bir alışveriş sepeti açmak sayılabilir.

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

# Ara Yazılım (Middleware)

Ara yazılım, bir istek tamamlanmadan önce kod çalıştırmanıza olanak tanır. Ardından, gelen isteğe bağlı olarak, yeniden yazarak, yönlendirerek, istek veya yanıt başlıklarını değiştirerek veya doğrudan yanıt vererek yanıtı değiştirebilirsiniz.

Ara yazılım, önbelleğe alınan içerik ve yollar eşleştirilmeden önce çalışır.

## Convention

Middleware'i tanımlamak için projenizin kök dizinindeki `middleware.ts` (veya `.js`) dosyasını kullanın. Örneğin, `pages` veya `app` ile aynı seviyede veya varsa `src` içinde.

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

// İçinde `await` kullanılıyorsa bu işlev `async` olarak işaretlenebilir
export function middleware(request: NextRequest) {
  return NextResponse.redirect(new URL("/home", request.url));
}

// See "Matching Paths" below to learn more
export const config = {
  matcher: "/about/:path*",
};
```

## Eşleşen Yollar (Matching Paths)

Ara yazılım, projenizdeki **her rota için** çağrılacaktır. Çalıştırma sırası aşağıdaki gibidir:

1. `next.config.js`'den `headers`
2. `next.config.js`'den `redirects`
3. Ara yazılım (`rewrites`, `redirects`, vb.)
4. `next.config.js` dosyasından `beforeFiles` (`rewrites`)
5. Dosya sistemi rotaları (`public/`, `_next/static/`, `pages/`, `app/`, vb.)
6. `next.config.js` dosyasından `afterFiles` (`rewrites`)
7. Dinamik Rotalar (`/blog/[slug]`)
8. `next.config.js`'den `fallback` (`rewrites`)

## Eşleştirici (Matcher)

`matcher`, Orta Yazılımı (middleware) belirli yollarda çalışacak şekilde filtrelemenize olanak tanır.

```ts
export const config = {
  matcher: "/about/:path*",
};
```

Bir dizi sözdizimiyle tek bir yolu veya birden fazla yolu eşleştirebilirsiniz:

```ts
export const config = {
  matcher: ["/about/:path*", "/dashboard/:path*"],
};
```

`matcher` yapılandırması tam regex'e izin verir, böylece negatif lookahead'ler veya karakter eşleştirme gibi eşleştirmeler desteklenir. Belirli yollar hariç tümünü eşleştirmek için negatif lookahead örneği burada görülebilir:

```ts
export const config = {
  matcher: [
    /*
     * Match all request paths except for the ones starting with:
     * - api (API yolları)
     * - _next/static (static dosyalar)
     * - _next/image (görüntü optimizasyon dosyaları)
     * - favicon.ico (favicon dosyası)
     */
    "/((?!api|_next/static|_next/image|favicon.ico).*)",
  ],
};
```

Bilmekte fayda var: `matcher` değerlerinin sabit olması gerekir, böylece derleme zamanında statik olarak analiz edilebilirler. Değişkenler gibi dinamik değerler göz ardı edilecektir.

### Yapılandırılmış eşleştiriciler:

1. ile başlamalıdır `/`
2. Adlandırılmış parametreler içerebilir: `/about/:path`, `/about/a` ve `/about/b` ile eşleşir ancak `/about/a/c` ile eşleşmez
3. Adlandırılmış parametreler üzerinde değiştiricilere sahip olabilir (`:` ile başlayan): `/about/:path*` `/about/a/b/c` ile eşleşir çünkü `*` sıfır veya daha fazladır. `?` sıfır veya bir ve `+` bir veya daha fazla
4. Parantez içine alınmış düzenli ifade kullanabilir: `/about/(.x)`, `/about/:pathx` ile aynıdır

[Path-to-regexp](https://github.com/pillarjs/path-to-regexp#path-to-regexp-1) belgeleri hakkında daha fazla bilgi edinin.

Bilmekte fayda var: Geriye dönük uyumluluk için Next.js her zaman `/public` öğesini `/public/index` olarak kabul eder. Bu nedenle, `/public/:path` eşleştiricisi eşleşecektir.

### Koşullu İfadeler (Conditional Statements)

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  if (request.nextUrl.pathname.startsWith("/about")) {
    return NextResponse.rewrite(new URL("/about-2", request.url));
  }

  if (request.nextUrl.pathname.startsWith("/dashboard")) {
    return NextResponse.rewrite(new URL("/dashboard/user", request.url));
  }
}
```

## NextResponse

`NextResponse` API şunları yapmanıza olanak tanır:

- gelen isteği farklı bir URL'ye yönlendirir.
- belirli bir URL'yi görüntüleyerek yanıtı yeniden yazın
- API Routes, `getServerSideProps` ve `rewrite` hedefleri için istek üstbilgilerini ayarlama
- Yanıt çerezlerini ayarlama
- Yanıt başlıklarını ayarlama

Middleware'den bir yanıt üretmek için şunları yapabilirsiniz:

1. Yanıt üreten bir rotaya (Sayfa veya Edge API Rotası) yeniden yazma
2. Doğrudan bir NextResponse döndürür.

## Çerez Kullanımı (Using Cookies)

Çerezler normal başlıklardır. Bir İstekte, `Cookie` başlığında saklanırlar. Yanıtta ise `Set-Cookie` başlığında bulunurlar. Next.js, `NextRequest` ve `NextResponse` üzerindeki `cookies` uzantısı aracılığıyla bu çerezlere erişmek ve bunları değiştirmek için uygun bir yol sağlar.

1. Gelen istekler için çerezler şu yöntemlerle birlikte gelir: `get`, `getAll`, `set` ve `delete` çerezleri. `has` ile bir çerezin varlığını kontrol edebilir veya `clear` ile tüm çerezleri kaldırabilirsiniz.
2. Giden yanıtlar için, çerezler aşağıdaki `get`, `getAll`, `set` ve `delete` yöntemlerine sahiptir.

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  // Gelen istekte bir "Cookie:nextjs=fast" başlığının bulunduğunu varsayın
  // RequestCookies` API'sini kullanarak istekten çerezleri alma
  let cookie = request.cookies.get("nextjs");
  console.log(cookie); // => { name: 'nextjs', value: 'fast', Path: '/' }
  const allCookies = request.cookies.getAll();
  console.log(allCookies); // => [{ name: 'nextjs', value: 'fast' }]

  request.cookies.has("nextjs"); // => true
  request.cookies.delete("nextjs");
  request.cookies.has("nextjs"); // => false

  // ResponseCookies` API'sini kullanarak yanıt üzerinde çerezleri ayarlama
  const response = NextResponse.next();
  response.cookies.set("vercel", "fast");
  response.cookies.set({
    name: "vercel",
    value: "fast",
    path: "/",
  });
  cookie = response.cookies.get("vercel");
  console.log(cookie); // => { name: 'vercel', value: 'fast', Path: '/' }
  // Giden yanıt bir `Set-Cookie:vercel=fast;path=/test` başlığına sahip olacaktır.

  return response;
}
```

## Üstbilgileri Ayarlama (Setting Headers)

`NextResponse` API'sini kullanarak istek ve yanıt başlıklarını ayarlayabilirsiniz (istek başlıklarının ayarlanması Next.js v13.0.0'dan beri mevcuttur).

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(request: NextRequest) {
  // İstek başlıklarını klonlayın ve yeni bir `x-hello-from-middleware1` başlığı ayarlayın
  const requestHeaders = new Headers(request.headers);
  requestHeaders.set("x-hello-from-middleware1", "hello");

  // İstek başlıklarını NextResponse.rewrite içinde de ayarlayabilirsiniz
  const response = NextResponse.next({
    request: {
      // Yeni istek başlıkları
      headers: requestHeaders,
    },
  });

  // Yeni bir `x-hello-from-middleware2` yanıt başlığı ayarlayın
  response.headers.set("x-hello-from-middleware2", "hello");
  return response;
}
```

Bilmekte fayda var: Arka uç web sunucusu yapılandırmanıza bağlı olarak [431 Request Header Fields Too Large](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/431) hatasına neden olabileceğinden büyük başlıklar ayarlamaktan kaçının.

## Yanıt Üretme (Producing a Response)

Bir `Response` veya `NextResponse` örneği döndürerek Middleware'den doğrudan yanıt verebilirsiniz. (Bu Next.js v13.1.0'dan beri mevcuttur)

```ts
import { NextRequest, NextResponse } from "next/server";
import { isAuthenticated } from "@lib/auth";

// Ara yazılımı `/api/` ile başlayan yollarla sınırlayın
export const config = {
  matcher: "/api/:function*",
};

export function middleware(request: NextRequest) {
  // İsteği kontrol etmek için kimlik doğrulama işlevimizi çağırın
  if (!isAuthenticated(request)) {
    // Bir hata mesajı belirten JSON ile yanıt verin
    return new NextResponse(
      JSON.stringify({ success: false, message: "authentication failed" }),
      { status: 401, headers: { "content-type": "application/json" } }
    );
  }
}
```

## Gelişmiş Orta Yazılım Bayrakları (Advanced Middleware Flags)

Next.js'nin `v13.1` sürümünde, gelişmiş kullanım durumlarını ele almak için ara katman için `skipMiddlewareUrlNormalize` ve `skipTrailingSlashRedirect` olmak üzere iki ek bayrak tanıtıldı.

`skipTrailingSlashRedirect`, sondaki eğik çizgilerin eklenmesi veya kaldırılması için Next.js varsayılan yönlendirmelerinin devre dışı bırakılmasına olanak tanıyarak, bazı yollar için sondaki eğik çizginin korunmasına izin verebilen ancak diğerleri için izin vermeyen ara yazılım içinde özel işleme izin verir.

```ts
module.exports = {
  skipTrailingSlashRedirect: true,
};
```

```ts
const legacyPrefixes = ["/docs", "/blog"];

export default async function middleware(req) {
  const { pathname } = req.nextUrl;

  if (legacyPrefixes.some((prefix) => pathname.startsWith(prefix))) {
    return NextResponse.next();
  }

  // apply trailing slash handling
  if (
    !pathname.endsWith("/") &&
    !pathname.match(/((?!\.well-known(?:\/.*)?)(?:[^/]+\/)*[^/]+\.\w+)/)
  ) {
    req.nextUrl.pathname += "/";
    return NextResponse.redirect(req.nextUrl);
  }
}
```

`skipMiddlewareUrlNormalize`, Next.js'nin doğrudan ziyaretleri ve istemci geçişlerini aynı şekilde ele almak için yaptığı URL normalleştirmesini devre dışı bırakmaya olanak tanır. Bunun kilidini açtığı orijinal URL'yi kullanarak tam kontrole ihtiyaç duyduğunuz bazı gelişmiş durumlar vardır.

```ts
module.exports = {
  skipMiddlewareUrlNormalize: true,
};
```

```ts
export default async function middleware(req) {
  const { pathname } = req.nextUrl;

  // GET /_next/data/build-id/hello.json

  console.log(pathname);
  // bu bayrak ile /_next/data/build-id/hello.json
  //bayrak olmadan bu /hello olarak normalleştirilirdi
}
```

# Proje Organizasyonu ve Dosya Kolokasyonu (Project Organization and File Colocation)

Yönlendirme klasörü ve dosya kurallarının yanı sıra Next.js, proje dosyalarınızı nasıl düzenlediğiniz ve konumlandırdığınız konusunda görüş bildirmez.

## Varsayılan olarak güvenli ortak yerleşim (Safe colocation by default)

`app` dizininde, iç içe klasör hiyerarşisi rota yapısını tanımlar.

Her klasör, URL yolunda karşılık gelen bir segmentle eşlenen bir rota segmentini temsil eder.

Ancak, rota yapısı klasörler aracılığıyla tanımlansa da, bir rota segmentine bir `page.js` veya `route.js` dosyası eklenene kadar bir rota genel olarak erişilebilir değildir.

<img alt="proje-organizasyonu" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-not-routable.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

Ve bir rota genel erişime açık hale getirildiğinde bile, istemciye yalnızca `page.js` veya `route.js` tarafından döndürülen içerik gönderilir.

<img alt="proje-organizasyonu-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-routable.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

Bu, proje dosyalarının yanlışlıkla yönlendirilebilir olmadan `app` dizinindeki rota segmentlerinin içine güvenli bir şekilde yerleştirilebileceği anlamına gelir.

<img alt="proje-organizasyonu-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-colocation.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

Bilmekte fayda var:

- Bu, sayfalardaki herhangi bir dosyanın bir rota olarak kabul edildiği `pages` dizininden farklıdır.
- Proje dosyalarınızı `app` dizinine yerleştirebilirsiniz ancak bunu yapmak zorunda değilsiniz. Tercih ederseniz, bunları `app` dizininin dışında tutabilirsiniz.

## Proje organizasyon özellikleri (Project organization features)

Next.js, projenizi düzenlemenize yardımcı olacak çeşitli özellikler sunar.

### Özel Klasörler

Özel klasörler, bir klasörün önüne alt çizgi getirilerek oluşturulabilir: `_folderName`

Bu, klasörün özel bir uygulama ayrıntısı olduğunu ve yönlendirme sistemi tarafından dikkate alınmaması gerektiğini gösterir, böylece klasör ve tüm alt klasörleri yönlendirme dışında bırakılır.

<img alt="proje-organizasyonu-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-private-folders.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

`app` dizinindeki dosyalar varsayılan olarak güvenli bir şekilde ortak konumlandırılabildiğinden, özel klasörler ortak konumlandırma için gerekli değildir. Ancak, şunlar için yararlı olabilirler:

- UI mantığını yönlendirme mantığından ayırma.
- Dahili dosyaları bir proje ve Next.js ekosistemi genelinde tutarlı bir şekilde düzenleme.
- Kod düzenleyicilerde dosyaları sıralama ve gruplama.
- Gelecekteki Next.js dosya kurallarıyla olası adlandırma çakışmalarını önleme.

Bilmekte fayda var:

- Bir çatı kuralı olmamakla birlikte, özel klasörlerin dışındaki dosyaları da aynı alt çizgi kalıbını kullanarak "private" olarak işaretlemeyi düşünebilirsiniz.
- Klasör adının önüne `%5F` (alt çizginin URL ile kodlanmış biçimi) ekleyerek alt çizgi ile başlayan URL segmentleri oluşturabilirsiniz: `%5FfolderName`.
- Özel klasörler kullanmıyorsanız, beklenmedik adlandırma çakışmalarını önlemek için Next.js özel dosya kurallarını bilmek yararlı olacaktır.

## Rota Grupları (Route Groups)

Rota grupları bir klasör parantez içine alınarak oluşturulabilir: `(folderName)`

Bu, klasörün organizasyonel amaçlar için olduğunu ve rotanın URL yoluna dahil edilmemesi gerektiğini gösterir.

<img alt="proje-organizasyonu-5" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-route-groups.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

Rota grupları şunlar için kullanışlıdır:

- Rotaları gruplar halinde düzenleme, örneğin site bölümüne, amaca veya ekibe göre.
- Aynı rota segmenti düzeyinde iç içe düzenleri etkinleştirme:
  - Birden fazla kök düzen dahil olmak üzere aynı segmentte birden fazla iç içe düzen oluşturma
  - Ortak bir segmentteki rotaların alt kümesine bir düzen ekleme

## `src` Dizini

Next.js, uygulama kodunun (`app` dahil) isteğe bağlı bir `src` dizini içinde saklanmasını destekler. Bu, uygulama kodunu çoğunlukla bir projenin kök dizininde bulunan proje yapılandırma dosyalarından ayırır.

<img alt="proje-organizasyonu-6" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-src-directory.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

## Modül Yolu Takma Adları (Module Path Aliases)

Next.js, derinlemesine iç içe geçmiş proje dosyalarında içe aktarmaları okumayı ve sürdürmeyi kolaylaştıran Modül Yolu Takma Adlarını destekler.

```ts
// önce
import { Button } from "../../../components/button";

// sonra
import { Button } from "@/components/button";
```

## Proje organizasyon stratejileri (Project organization strategies)

Bir Next.js projesinde kendi dosyalarınızı ve klasörlerinizi düzenlemek söz konusu olduğunda "doğru" veya "yanlış" bir yol yoktur.

Aşağıdaki bölüm, yaygın stratejilerin çok üst düzey bir özetini listelemektedir. En basit çıkarım, sizin ve ekibiniz için işe yarayan bir strateji seçmek ve proje genelinde tutarlı olmaktır.

Bilmekte fayda var: Aşağıdaki örneklerimizde, `components` ve `lib` klasörlerini genelleştirilmiş yer tutucular olarak kullanıyoruz, bunların adlandırılmasının özel bir çerçeve önemi yoktur ve projeleriniz `ui`, `utils`, `hooks`, `styles` vb. gibi başka klasörler kullanabilir.

### Proje dosyalarını `app` dışında saklama

Bu strateji, tüm uygulama kodunu projenizin kök dizinindeki paylaşılan klasörlerde saklar ve `app` dizinini yalnızca yönlendirme amacıyla tutar.

<img alt="proje-organizasyonu-7" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-project-root.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

### Proje dosyalarını `app` içindeki üst düzey klasörlerde saklayın

Bu strateji, tüm uygulama kodunu `app` dizininin kök dizinindeki paylaşılan klasörlerde saklar.

<img alt="proje-organizasyonu-8" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-app-root.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9" /><br/>

### Proje dosyalarını özellik veya rotaya göre bölme

Bu strateji, genel olarak paylaşılan uygulama kodunu kök `app` dizininde depolar ve daha spesifik uygulama kodunu bunları kullanan rota segmentlerine böler.

<img alt="proje-organizasyonu-9" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-app-root-split.png&w=3840&q=75&dpl=dpl_GhJPXqxoPPM8iCyYvCDRicbiTqZ9"/><br/>

# Uluslararasılaştırma (Internationalization)

Next.js, birden fazla dili desteklemek için içeriğin yönlendirilmesini ve oluşturulmasını yapılandırmanıza olanak tanır. Sitenizi farklı yerel ayarlara uyumlu hale getirmek, çevrilmiş içerik (yerelleştirme) ve uluslararasılaştırılmış rotaları içerir.

## Terminoloji

- Yerel ayar: Bir dizi dil ve biçimlendirme tercihi için bir tanımlayıcı. Bu genellikle kullanıcının tercih ettiği dili ve muhtemelen coğrafi bölgesini içerir.
  - `en-US`: Amerika Birleşik Devletleri'nde konuşulan İngilizce
  - `nl-NL`: Hollanda'da konuşulduğu şekliyle Hollandaca
  - `nl`: Hollandaca, belirli bir bölge yok

## Yönlendirmeye Genel Bakış (Routing Overview)

Hangi yerel ayarın kullanılacağını seçmek için kullanıcının tarayıcıdaki dil tercihlerini kullanmanız önerilir. Tercih ettiğiniz dili değiştirmek, uygulamanıza gelen `Accept-Language` başlığını değiştirecektir.

Örneğin, aşağıdaki kütüphaneleri kullanarak, Üstbilgilere, desteklemeyi planladığınız yerel ayarlara ve varsayılan yerel ayara göre hangi yerel ayarı seçeceğinizi belirlemek için gelen bir İsteğe bakabilirsiniz.

```ts
import { match } from "@formatjs/intl-localematcher";
import Negotiator from "negotiator";

let headers = { "accept-language": "en-US,en;q=0.5" };
let languages = new Negotiator({ headers }).languages();
let locales = ["en-US", "nl-NL", "nl"];
let defaultLocale = "en-US";

match(languages, locales, defaultLocale); // -> 'en-US'
```

Yönlendirme, alt yol (`/fr/products`) veya etki alanı (`my-site.fr/products`) ile uluslararasılaştırılabilir. Bu bilgilerle artık kullanıcıyı Middleware içindeki yerel ayara göre yönlendirebilirsiniz.

```ts
import { NextResponse } from 'next/server'

let locales = ['en-US', 'nl-NL', 'nl']

// Yukarıdakine benzer şekilde veya bir kütüphane kullanarak tercih edilen yerel ayarı alın
function getLocale(request) { ... }

export function middleware(request) {
  // Yol adında desteklenen herhangi bir yerel ayar olup olmadığını kontrol edin
  const pathname = request.nextUrl.pathname
  const pathnameIsMissingLocale = locales.every(
    (locale) => !pathname.startsWith(`/${locale}/`) && pathname !== `/${locale}`
  )

  // Yerel ayar yoksa yönlendirme
  if (pathnameIsMissingLocale) {
    const locale = getLocale(request)

    // örneğin gelen istek /products
    // Yeni URL artık /en-US/products şeklindedir
    return NextResponse.redirect(
      new URL(`/${locale}/${pathname}`, request.url)
    )
  }
}

export const config = {
  matcher: [
    // Tüm dahili yolları atla (_next)
    '/((?!_next).*)',
    // İsteğe bağlı: yalnızca kök (/) URL'de çalıştır
    // '/'
  ],
}
```

Son olarak, `app/` içindeki tüm özel dosyaların `app/[lang]` altında yuvalandığından emin olun. Bu, Next.js yönlendiricisinin rotadaki farklı yerel ayarları dinamik olarak işlemesini ve `lang` parametresini her düzene ve sayfaya iletmesini sağlar. Örneğin:

```ts
// Artık geçerli yerel ayara erişiminiz var
// örneğin /en-US/products -> `lang` "en-US "dir
export default async function Page({ params: { lang } }) {
  return ...
}
```

Kök düzen de yeni klasörün içine yerleştirilebilir (örn. `app/[lang]/layout.js`).

## Yerelleştirme (Localization)

Görüntülenen içeriğin kullanıcının tercih ettiği yerel ayara veya yerelleştirmeye göre değiştirilmesi Next.js'ye özgü bir şey değildir. Aşağıda açıklanan modeller herhangi bir web uygulamasında aynı şekilde çalışacaktır.

Uygulamamız içinde hem İngilizce hem de Hollandaca içeriği desteklemek istediğimizi varsayalım. Bize bazı anahtarlardan yerelleştirilmiş bir dizeye eşleme sağlayan nesneler olan iki farklı "sözlük" tutabiliriz. Örneğin:

```ts
{
  "products": {
    "cart": "Add to Cart"
  }
}
```

```ts
{
  "products": {
    "cart": "Voeg toe aan winkelwagen"
  }
}
```

Ardından, istenen yerel ayar için çevirileri yüklemek üzere bir `getDictionary` işlevi oluşturabiliriz:

```ts
import "server-only";

const dictionaries = {
  en: () => import("./dictionaries/en.json").then((module) => module.default),
  nl: () => import("./dictionaries/nl.json").then((module) => module.default),
};

export const getDictionary = async (locale) => dictionaries[locale]();
```

O anda seçili olan dil göz önüne alındığında, bir düzen veya sayfanın içindeki sözlüğü getirebiliriz.

```ts
import { getDictionary } from "./dictionaries";

export default async function Page({ params: { lang } }) {
  const dict = await getDictionary(lang); // en
  return <button>{dict.products.cart}</button>; // Add to Cart
}
```

`app/` dizinindeki tüm düzenler ve sayfalar varsayılan olarak Sunucu Bileşenleri olduğundan, çeviri dosyalarının boyutunun istemci tarafı JavaScript paket boyutumuzu etkilemesi konusunda endişelenmemize gerek yoktur. Bu kod yalnızca sunucuda çalışacak ve tarayıcıya yalnızca ortaya çıkan HTML gönderilecektir.

## Statik Üretim (Static Generation)

Belirli bir yerel ayar kümesi için statik rotalar oluşturmak üzere `generateStaticParams`'ı herhangi bir sayfa veya düzenle birlikte kullanabiliriz. Bu, örneğin kök düzeninde global olabilir:

```ts
export async function generateStaticParams() {
  return [{ lang: "en-US" }, { lang: "de" }];
}

export default function Root({ children, params }) {
  return (
    <html lang={params.lang}>
      <body>{children}</body>
    </html>
  );
}
```

# Render Etme (Rendering)

Render etme, yazdığınız kodu kullanıcı arayüzlerine dönüştürür.

React 18 ve Next.js 13, uygulamanızı render etmenin yeni yollarını tanıttı. Bu sayfa, render ortamları, stratejileri, çalışma zamanları arasındaki farkları ve bunlara nasıl dahil olacağınızı anlamanıza yardımcı olacaktır.

## Render etme Ortamları

Uygulama kodunuzun işlenebileceği iki ortam vardır: istemci ve sunucu.

<img alt="render" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fclient-and-server-environments.png&w=3840&q=75&dpl=dpl_Fes67gTLa5ScjbSLtJLVo9u4FfQK"/><br/>

- İstemci, uygulama kodunuz için bir sunucuya istek gönderen bir kullanıcının cihazındaki tarayıcıyı ifade eder. Daha sonra sunucudan gelen yanıtı kullanıcının etkileşime girebileceği bir arayüze dönüştürür.
- Sunucu, bir veri merkezinde uygulama kodunuzu depolayan, istemciden gelen istekleri alan, bazı hesaplamalar yapan ve uygun bir yanıtı geri gönderen bilgisayarı ifade eder.

## Bileşen Düzeyinde İstemci ve Sunucu Render Etme

React 18'den önce, React kullanarak uygulamanızı oluşturmanın birincil yolu tamamen istemcideydi.

Next.js, uygulamanızı sayfalara ayırmak ve HTML oluşturup React tarafından [hidrasyon](https://react.dev/reference/react-dom/hydrate#hydrating-server-rendered-html) edilmek üzere istemciye göndererek sunucuda önceden render etmek için daha kolay bir yol sağladı. Ancak bu, ilk HTML'yi etkileşimli hale getirmek için istemcide ek JavaScript'e ihtiyaç duyulmasına neden oldu.

Şimdi, Sunucu ve İstemci Bileşenleri ile React, istemci ve sunucuda render edebilir, yani bileşen düzeyinde render etme ortamını seçebilirsiniz.

Varsayılan olarak, `app` yönlendiricisi Sunucu Bileşenlerini kullanır, bu da bileşenleri sunucuda kolayca render etmenize ve istemciye gönderilen JavaScript miktarını azaltmanıza olanak tanır.

## Sunucuda Statik ve Dinamik Render Etme

React bileşenleriyle istemci tarafı ve sunucu tarafı render etmeye ek olarak Next.js, Statik ve Dinamik render etme ile sunucuda render etmeyi optimize etme seçeneği sunar.

### Statik Render Etme

Static Render Etme ile hem Sunucu hem de İstemci Bileşenleri derleme zamanında sunucuda önceden render edilebilir. Çalışmanın sonucu önbelleğe alınır ve sonraki isteklerde yeniden kullanılır. Önbelleğe alınan sonuç da yeniden doğrulanabilir.

Bilmekte fayda var: Bu, Pages Router'daki Static Site Generation (SSG) ve Incremental Static Regeneration (ISR) ile eşdeğerdir.

Statik render etme sırasında Sunucu ve İstemci Bileşenleri farklı şekilde render edilir:

- İstemci Bileşenlerinin HTML ve JSON'ları önceden render edilir ve sunucuda önbelleğe alınır. Önbelleğe alınan sonuç daha sonra hidrasyon için istemciye gönderilir.
- Sunucu Bileşenleri React tarafından sunucuda render edilir ve yükleri HTML oluşturmak için kullanılır. Aynı işlenmiş yük, bileşenleri istemcide hidrasyon edilmek için de kullanılır ve istemcide JavaScript gerekmez.

### Dinamik Render Etme

Dinamik Render Etme ile hem Sunucu hem de İstemci Bileşenleri istek anında sunucu üzerinde render edilir. Çalışmanın sonucu önbelleğe alınmaz.

Bilmekte fayda var: Bu, Pages Router'daki Sunucu Tarafı Oluşturmaya (`getServerSideProps()`) eşdeğerdir.

## Edge ve Node.js Çalışma Zamanları

Sunucuda, sayfalarınızın render edilebileceği iki çalışma zamanı vardır:

- Node.js Çalışma Zamanı (varsayılan) tüm Node.js API'lerine ve ekosistemdeki uyumlu paketlere erişime sahiptir.
- Edge Çalışma Zamanı, Web API'lerini temel alır.

Her iki çalışma zamanı da dağıtım altyapınıza bağlı olarak sunucudan akışı destekler.

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

# Edge ve Node.js Çalışma Zamanları (Edge and Node.js Runtimes)

Next.js bağlamında "çalışma zamanı", yürütme sırasında kodunuz tarafından kullanılabilen kütüphaneler, API'ler ve genel işlevsellik kümesini ifade eder.

Next.js, uygulama kodunuzun bazı bölümlerini oluşturabileceğiniz iki sunucu çalışma zamanına sahiptir:

- Node.js Çalışma Zamanı
- Edge Çalışma Zamanı
- Her çalışma zamanının kendi API'leri vardır. Mevcut API'lerin tam listesi için lütfen [Node.js Docs](https://nodejs.org/docs/latest/api/) ve [Edge Docs](https://nextjs.org/docs/app/api-reference/edge)'a bakın. Her iki çalışma zamanı da dağıtım altyapınıza bağlı olarak akışı destekleyebilir.

Varsayılan olarak, `app` dizini Node.js çalışma zamanını kullanır. Ancak, rota bazında farklı çalışma zamanlarını (örn. Edge) seçebilirsiniz.

## Çalışma Zamanı Farklılıkları

Bir çalışma zamanı seçerken dikkat edilmesi gereken birçok husus vardır. Bu tablo bir bakışta önemli farklılıkları göstermektedir. Farklılıkların daha derinlemesine bir analizini istiyorsanız, aşağıdaki bölümlere göz atın.
| | Node | Serverless | Edge |
|---------|----------------|------------|----------|
| Cold Boot | / | ~250ms | Anında |
| HTTP Streaming | Evet | Evet | Evet |
| IO | Hepsi | Hepsi | `fetch` |
| Scalability | / | Yüksek | En Yüksek |
| Security | Normal | Yüksek | Yüksek |
| Latency | Normal | Düşük | En Düşük |
| npm Packages | Hepsi | Hepsi | Daha küçük bir alt küme |

## Edge Çalışma Zamanı

Next.js'de hafif Edge Runtime, mevcut Node.js API'lerinin bir alt kümesidir.

Küçük, basit işlevlerle düşük gecikme süresinde dinamik, kişiselleştirilmiş içerik sunmanız gerekiyorsa Edge Runtime idealdir. Edge Runtime'ın hızı minimum kaynak kullanımından gelir, ancak bu birçok senaryoda sınırlayıcı olabilir.

Örneğin, Vercel'de Edge Runtime'da yürütülen kod [1 MB ile 4 MB arasını geçemez](https://vercel.com/docs/concepts/limits/overview#edge-middleware-and-edge-functions-size), bu sınır içe aktarılan paketleri, yazı tiplerini ve dosyaları içerir ve dağıtım altyapınıza bağlı olarak değişir.

##  Node.js Çalışma Zamanı

Node.js çalışma zamanını kullanmak, tüm Node.js API'lerine ve bunlara dayanan tüm npm paketlerine erişmenizi sağlar. Ancak, başlatılması Edge çalışma zamanını kullanan rotalar kadar hızlı değildir.

Next.js uygulamanızı bir Node.js sunucusuna dağıtmak, altyapınızı yönetmeyi, ölçeklendirmeyi ve yapılandırmayı gerektirecektir. Alternatif olarak, Next.js uygulamanızı Vercel gibi sunucusuz bir platforma dağıtmayı düşünebilirsiniz; bu platform bunu sizin için halledecektir.

## Sunucusuz Node.js

Edge Runtime'dan daha karmaşık hesaplama yüklerini kaldırabilecek ölçeklenebilir bir çözüme ihtiyacınız varsa Sunucusuz idealdir. Örneğin Vercel'deki Sunucusuz İşlevler ile içe aktarılan paketler, yazı tipleri ve dosyalar dahil olmak üzere toplam kod boyutunuz [50 MB](https://vercel.com/docs/concepts/limits/overview#serverless-function-size)'tır.

Edge kullanan rotalara kıyasla dezavantajı, Sunucusuz İşlevlerin istekleri işlemeye başlamadan önce önyükleme yapmasının yüzlerce milisaniye sürebilmesidir. Sitenizin aldığı trafik miktarına bağlı olarak, işlevler sık sık "ısınmadığı" için bu sık karşılaşılan bir durum olabilir.

## Örnekler

### Segment Çalışma Zamanı Seçeneği

Next.js uygulamanızda tek tek rota segmentleri için bir çalışma zamanı belirleyebilirsiniz. Bunu yapmak için, runtime adında bir değişken tanımlayın ve dışa aktarın. Değişken bir dize olmalı ve `'nodejs'` ya da `'edge'` runtime değerine sahip olmalıdır.

Aşağıdaki örnekte, `'edge'` değerine sahip bir çalışma zamanını dışa aktaran bir sayfa rotası segmenti gösterilmektedir:

```ts
export const runtime = "edge"; // 'nodejs' (varsayılan) | 'edge'
```

Segment çalışma zamanı ayarlanmazsa, varsayılan `nodejs` çalışma zamanı kullanılacaktır. Node.js çalışma zamanından değiştirmeyi planlamıyorsanız çalışma zamanı seçeneğini kullanmanıza gerek yoktur.

# Veri Getirme (Data Fetching)

Next.js App Router, React ve Web platformu üzerine inşa edilmiş yeni, basitleştirilmiş bir veri getirme sistemi sunar.

## `fetch()` API

Yeni veri getirme sistemi, yerel [fetch() Web API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)'sinin üzerine inşa edilmiştir ve Sunucu Bileşenlerinde `async` ve `await`'i kullanır.

- React, otomatik istek tekilleştirme sağlamak için `fetch`'i genişletir.
- Next.js, her isteğin kendi önbelleğe alma ve yeniden doğrulama kurallarını belirlemesine izin vermek için `fetch` options nesnesini genişletir.

### Sunucudan Veri Getirme (Fetching Data on the Server)

Mümkün oldukça, Sunucu Bileşenlerinde veri getirmenizi öneririz. Sunucu Bileşenleri **her zaman sunucudan veri getirir**. Bu size şunları sağlar:

- Arka uç veri kaynaklarına (ör. veritabanları) doğrudan erişime sahip olun.
- Erişim belirteçleri ve API anahtarları gibi hassas bilgilerin istemciye ifşa edilmesini önleyerek uygulamanızı daha güvenli tutun.
- Verileri alın ve aynı ortamda işleyin. Bu, hem istemci ve sunucu arasındaki ileri geri iletişimi hem de istemcideki ana iş parçacığı üzerindeki çalışmayı azaltır.
- İstemcide birden fazla ayrı istek yerine tek bir gidiş-dönüş ile birden fazla veri getirme işlemi gerçekleştirin.
- İstemci-sunucu şelalelerini azaltın.
- Bulunduğunuz bölgeye bağlı olarak, veri getirme işlemi veri kaynağınıza daha yakın bir yerde de gerçekleşebilir, böylece gecikme süresi azalır ve performans artar.

**Bilmekte fayda var:** İstemci tarafında veri almak hala mümkündür. İstemci Bileşenleri ile [SWR](https://swr.vercel.app/) veya [React Query](https://tanstack.com/query/v4/) gibi üçüncü taraf bir kütüphane kullanmanızı öneririz. Gelecekte, React `use()` hook kullanarak İstemci Bileşenlerinde veri almak da mümkün olacak.

### Bileşen Düzeyinde Veri Getirme (Fetching Data at the Component Level)

App Router'da düzenlerin, sayfaların ve bileşenlerin içinden veri getirebilirsiniz. Veri getirme, Akış ve Askıya Alma ile de uyumludur.

**Bilmekte fayda var:** Düzenlerde, bir üst düzen ile onun alt bileşenleri arasında veri aktarmak mümkün değildir. Bir rotada aynı verileri birden çok kez talep ediyor olsanız bile, verileri doğrudan ihtiyaç duyan düzenin içinden almanızı öneririz. Sahne arkasında React ve Next.js, aynı verilerin birden fazla kez getirilmesini önlemek için istekleri önbelleğe alır ve tekilleştirir.

### Paralel ve Sıralı Veri Getirme (Parallel and Sequential Data Fetching)

Bileşenler içinde veri getirirken, iki veri getirme modelinin farkında olmanız gerekir: Paralel ve Sıralı.

<img alt="fetch" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fsequential-parallel-data-fetching.png&w=3840&q=75&dpl=dpl_BuM5KktxiCNXDgUUvBbDZYCUJ7hK"/>
<br>

- Paralel veri getirme ile, bir rotadaki istekler istekli olarak başlatılır ve aynı anda veri yüklenir. Bu, istemci-sunucu şelalelerini ve veri yüklemek için gereken toplam süreyi azaltır.
- Sıralı veri getirme ile, bir rotadaki istekler birbirine bağımlıdır ve şelaleler oluşturur. Bu modeli istediğiniz durumlar olabilir çünkü bir getirme işlemi diğerinin sonucuna bağlıdır veya kaynakları korumak için bir sonraki getirme işleminden önce bir koşulun yerine getirilmesini istersiniz. Ancak bu davranış kasıtsız da olabilir ve daha uzun yükleme sürelerine yol açabilir.

### Otomatik `fetch()` İsteği Tekilleştirme (Automatic fetch() Request Deduping)

Bir ağaçtaki birden fazla bileşende aynı verileri (örneğin mevcut kullanıcı) getirmeniz gerekiyorsa, Next.js aynı girdiye sahip `fetch` isteklerini `(GET)` otomatik olarak geçici bir önbellekte önbelleğe alacaktır. Bu optimizasyon, bir render etme geçişi sırasında aynı verilerin birden fazla kez getirilmesini önler.

<img alt="fetch-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fdeduplicated-fetch-requests.png&w=3840&q=75&dpl=dpl_BuM5KktxiCNXDgUUvBbDZYCUJ7hK"/>
<br>

- Sunucuda önbellek, render etme işlemi tamamlanana kadar bir sunucu isteğinin ömrü boyunca sürer.
  - Bu optimizasyon Düzenlerde, Sayfalarda, Sunucu Bileşenlerinde, `generateMetadata` ve `generateStaticParams`'da yapılan `fetch` istekleri için geçerlidir.
  - Bu optimizasyon statik oluşturma (static generation) sırasında da geçerlidir.
- İstemcide, önbellek, tam sayfa yeniden yüklenmeden önce bir oturum süresince (birden fazla istemci tarafı yeniden render etme içerebilir) sürer.

**Bilmekte fayda var:**

- `POST` istekleri otomatik olarak tekilleştirilmez.
- `Fetch`'i kullanamıyorsanız, React, istek süresince verileri manuel olarak önbelleğe almanıza olanak tanıyan bir `cache` işlevi sağlar.

### Statik ve Dinamik Veri Getirme (Static and Dynamic Data Fetching)

İki tür veri vardır: Statik ve Dinamik.

- Statik Veriler sık sık değişmeyen verilerdir. Örneğin, bir blog yazısı.
- Dinamik Veriler, sık sık değişen veya kullanıcılara özel olabilen verilerdir. Örneğin, bir alışveriş sepeti listesi.

<img alt="fetch-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fdynamic-and-static-data-fetching.png&w=3840&q=75&dpl=dpl_BuM5KktxiCNXDgUUvBbDZYCUJ7hK"/>
<br>

Next.js varsayılan olarak otomatik olarak statik getirmeler yapar. Bu, verilerin derleme zamanında getirileceği, önbelleğe alınacağı ve her istekte yeniden kullanılacağı anlamına gelir. Bir geliştirici olarak, statik verilerin nasıl önbelleğe alınacağı ve yeniden doğrulanacağı üzerinde kontrole sahipsiniz.

Statik veri kullanmanın iki faydası vardır:

1. Yapılan istek sayısını en aza indirerek veritabanınız üzerindeki yükü azaltır.
2. Daha iyi yükleme performansı için veriler otomatik olarak önbelleğe alınır.

Bununla birlikte, verileriniz kullanıcıya göre kişiselleştirilmişse veya her zaman en son verileri getirmek istiyorsanız, istekleri dinamik olarak işaretleyebilir ve önbelleğe almadan her istekte veri getirebilirsiniz.

## Veri Önbelleğe Alma (Caching Data)

Önbelleğe alma, verilerin bir konumda (örneğin [İçerik Dağıtım Ağı](https://vercel.com/docs/concepts/edge-network/overview)) depolanması işlemidir, böylece her istekte orijinal kaynaktan yeniden taranması gerekmez.

<img alt="cache" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fstatic-site-generation.png&w=3840&q=75&dpl=dpl_BuM5KktxiCNXDgUUvBbDZYCUJ7hK"/>
<br>

**Next.js Cache**, küresel olarak dağıtılabilen kalıcı bir [HTTP önbelleğidir](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching). Bu, önbelleğin otomatik olarak ölçeklenebileceği ve platformunuza bağlı olarak birden fazla bölgede paylaşılabileceği anlamına gelir (örn. Vercel).

Next.js, `fetch()` işlevinin [options nesnesini](https://developer.mozilla.org/en-US/docs/Web/API/fetch#:~:text=preflight%20requests.-,cache,-A%20string%20indicating), sunucudaki her isteğin kendi kalıcı önbellekleme davranışını ayarlamasına izin verecek şekilde genişletir. Bileşen düzeyinde veri getirme ile birlikte bu, uygulama kodunuzda önbelleğe almayı doğrudan verilerin kullanıldığı yerde yapılandırmanıza olanak tanır.

Sunucu render etme sırasında, Next.js bir getirme işlemiyle karşılaştığında, verilerin zaten mevcut olup olmadığını görmek için önbelleği kontrol edecektir. Eğer mevcutsa, önbelleğe alınan verileri döndürür. Değilse, gelecekteki istekler için verileri getirecek ve depolayacaktır.

**Bilmekte fayda var:** Eğer `fetch` kullanamıyorsanız, React istek süresince verileri manuel olarak önbelleğe almanızı sağlayan bir `cache` fonksiyonu sunar.

### Verileri Yeniden Doğrulama (Revalidating Data)

Yeniden doğrulama, önbelleğin temizlenmesi ve en son verilerin yeniden alınması işlemidir. Bu, verileriniz değiştiğinde ve tüm uygulamanızı yeniden oluşturmak zorunda kalmadan uygulamanızın en son sürümü gösterdiğinden emin olmak istediğinizde kullanışlıdır.

- Arka plan: Verileri belirli bir zaman aralığında yeniden doğrular.
- İsteğe bağlı: Bir güncelleme olduğunda verileri yeniden doğrular.

### Akış ve Gerilim (Streaming and Suspense)

Streaming ve Suspense, kullanıcı arayüzünün render edilmiş birimlerini aşamalı olarak render etmenize ve istemciye aşamalı olarak aktarmanıza olanak tanıyan yeni React özellikleridir.

Sunucu Bileşenleri ve iç içe düzenlerle, sayfanın özellikle veri gerektirmeyen kısımlarını anında render edebilir ve sayfanın veri getiren kısımları için bir yükleme durumu gösterebilirsiniz. Bu, kullanıcının sayfayla etkileşime geçmeden önce tüm sayfanın yüklenmesini beklemek zorunda olmadığı anlamına gelir.

<img alt="cache-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fserver-rendering-with-streaming.png&w=3840&q=75&dpl=dpl_BuM5KktxiCNXDgUUvBbDZYCUJ7hK"/>
<br>

## Eski Yöntemler

`getServerSideProps`, `getStaticProps` ve `getInitialProps` gibi önceki Next.js veri getirme yöntemleri yeni Uygulama Yönlendiricisinde desteklenmemektedir. Ancak, bunları Pages Router'da kullanmaya devam edebilirsiniz.

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

# Sunucu Eylemleri (Server Actions)

Sunucu Eylemleri, Next.js'de React Eylemleri üzerine inşa edilmiş bir **alfa** özelliğidir. Sunucu tarafı veri mutasyonlarını, azaltılmış istemci tarafı JavaScript'i ve aşamalı olarak geliştirilmiş formları etkinleştirirler. Sunucu Bileşenleri içinde tanımlanabilir ve/veya İstemci Bileşenlerinden çağrılabilirler:

Sunucu Bileşenleri ile:

```js
import { cookies } from "next/headers";

// Sunucu Bileşeni içinde tanımlanan sunucu eylemi
export default function AddToCart({ productId }) {
  async function addItem(data) {
    "use server";

    const cartId = cookies().get("cartId")?.value;
    await saveToDb({ cartId, data });
  }

  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

İstemci Bileşenleri ile:

```js
"use server";

export async function addItem(data) {
  const cartId = cookies().get("cartId")?.value;
  await saveToDb({ cartId, data });
}
```

```js
"use client";

import { addItem } from "./actions.js";

// İstemci Bileşeni içinde çağrılan Sunucu Eylemi
export default function AddToCart({ productId }) {
  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:**

- Sunucu Eylemlerini kullanmak, React `experimental` kanalını çalıştırmayı tercih edecektir.
- React Eylemleri, `useOptimistic` ve `useFormStatus`, Next.js veya React Sunucu Bileşenlerine özgü özellikler değildir.
- Next.js, `RevalidateTag` ve `RevalidatePath` gibi veri mutasyon API'lerinin eklenmesi de dahil olmak üzere React Actions'ı Next.js yönlendiricisine, paketleyicisine ve önbellekleme sistemine entegre eder.

## Convention

Deneysel `serverActions` bayrağını etkinleştirerek Next.js projenizde Sunucu Eylemlerini etkinleştirebilirsiniz.

```js
module.exports = {
  experimental: {
    serverActions: true,
  },
};
```

## Yaratılış (Creation)

Sunucu Eylemleri iki yerde tanımlanabilir:

- Onu kullanan bileşenin içinde (yalnızca Sunucu Bileşenleri)
- Yeniden kullanılabilirlik için ayrı bir dosyada (İstemci ve Sunucu Bileşenleri). Tek bir dosyada birden fazla Sunucu Eylemi tanımlayabilirsiniz.

### Sunucu Bileşenleri ile

Fonksiyon gövdesinin üst kısmında `"use server"` yönergesi ile asenkron bir fonksiyon tanımlayarak bir Sunucu Eylemi oluşturun. Bu fonksiyon, React Sunucu Bileşenleri protokolüne göre serileştirilebilir argümanlara ve serileştirilebilir bir dönüş değerine sahip olmalıdır.

```js
export default function ServerComponent() {
  async function myAction() {
    "use server";
    // ...
  }
}
```

### İstemci Bileşenleri ile

Bir İstemci Bileşeni içinde bir Sunucu Eylemi kullanıyorsanız, eyleminizi dosyanın üst kısmında "use server" yönergesi ile ayrı bir dosyada oluşturun. Ardından, Sunucu Eylemini İstemci Bileşeninize aktarın:

```js
"use server";

export async function myAction() {
  // ...
}
```

```js
"use client";

import { myAction } from "./actions";

export default function ClientComponent() {
  return (
    <form action={myAction}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:** Üst düzey bir `"use server"` yönergesi kullanıldığında, aşağıdaki tüm dışa aktarımlar Sunucu Eylemleri olarak kabul edilecektir. Tek bir dosyada birden fazla Sunucu Eyleminiz olabilir.

## Çağırma (Invocation)

Sunucu Eylemlerini aşağıdaki yöntemleri kullanarak çağırabilirsiniz:

- `action` kullanma: React'in `action` prop'u, bir `<form>` öğesi üzerinde bir Sunucu Eylemi çağırmaya izin verir.
- `formAction` kullanımı: React'in `formAction` özelliği, bir `<form>` öğesindeki `<button>`, `<input type="submit">` ve `<input type="image">` öğelerinin işlenmesini sağlar.
- `startTransition` ile Özel Çağırma: `startTransition` kullanarak `action` veya `formAction` kullanmadan Sunucu Eylemlerini çağırın. Bu yöntem Aşamalı Geliştirmeyi devre dışı bırakır.

### eylem (action)

Bir `form` öğesi üzerinde bir Sunucu Eylemi çağırmak için React'in `action` prop'unu kullanabilirsiniz. Action prop ile aktarılan Sunucu Eylemleri, kullanıcı etkileşimine yanıt olarak asenkron yan etkiler olarak hareket eder.

```js
export default function AddToCart({ productId }) {
  async function addItem(data) {
    "use server";

    const cartId = cookies().get("cartId")?.value;
    await saveToDb({ cartId, data });
  }

  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:** `action`, HTML'in ilkel [`action`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#action)'ına benzer

### `formAction`

Form Eylemlerini `button`, `input type="submit"` ve `input type="image"` gibi öğeler üzerinde işlemek için `formAction` prop'unu kullanabilirsiniz. `formAction` prop, formun eylemine göre önceliklidir.

```js
export default function Form() {
  async function handleSubmit() {
    "use server";
    // ...
  }

  async function submitImage() {
    "use server";
    // ...
  }

  return (
    <form action={handleSubmit}>
      <input type="text" name="name" />
      <input type="image" formAction={submitImage} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Bilmekte fayda var:** Bir `formAction`, HTML ilkel formaction'dır. React artık bu niteliğe fonksiyonlar aktarmanıza izin veriyor.

### `startTransition` kullanarak özel çağırma

Sunucu Eylemlerini `action` veya `formAction` kullanmadan da çağırabilirsiniz. Bunu, `useTransition` kancası tarafından sağlanan `startTransition`'ı kullanarak gerçekleştirebilirsiniz; bu, Sunucu Eylemlerini formların, düğmelerin veya girişlerin dışında kullanmak istiyorsanız yararlı olabilir.

**Bilmekte fayda var:** `startTransition`'ı kullanmak, kullanıma hazır Aşamalı Geliştirmeyi devre dışı bırakır.

```js
"use client";

import { useTransition } from "react";
import { addItem } from "../actions";

function ExampleClientComponent({ id }) {
  let [isPending, startTransition] = useTransition();

  return (
    <button onClick={() => startTransition(() => addItem(id))}>
      Add To Cart
    </button>
  );
}
```

```ts
"use server";

export async function addItem(id) {
  await addItemToDb(id);
  // Tüm ürün sayfalarını yeniden doğrulama için işaretler
  revalidatePath("/product/[id]");
}
```

### `StartTransition` olmadan özel çağırma

Sunucu Mutasyonları yapmıyorsanız, işlevi diğer işlevler gibi doğrudan bir prop olarak aktarabilirsiniz.

```js
import kv from "@vercel/kv";
import LikeButton from "./like-button";

export default function Page({ params }: { params: { id: string } }) {
  async function increment() {
    "use server";
    await kv.incr(`post:id:${params.id}`);
  }

  return <LikeButton increment={increment} />;
}
```

```js
"use client";

export default function LikeButton({
  increment,
}: {
  increment: () => Promise<void>,
}) {
  return (
    <button
      onClick={async () => {
        await increment();
      }}
    >
      Like
    </button>
  );
}
```

## Geliştirmeler

### Deneysel `useOptimistik`

Deneysel `useOptimistic` kancası, uygulamanızda iyimser güncellemeleri uygulamak için bir yol sağlar. İyimser güncellemeler, uygulamanın daha duyarlı görünmesini sağlayarak kullanıcı deneyimini geliştiren bir tekniktir.

Bir Sunucu Eylemi çağrıldığında, Sunucu Eyleminin yanıtını beklemek yerine, kullanıcı arayüzü beklenen sonucu yansıtacak şekilde hemen güncellenir.

```js
"use client";

import { experimental_useOptimistic as useOptimistic } from "react";
import { send } from "./actions.js";

export function Thread({ messages }) {
  const [optimisticMessages, addOptimisticMessage] = useOptimistic(
    messages,
    (state, newMessage) => [...state, { message: newMessage, sending: true }]
  );
  const formRef = useRef();

  return (
    <div>
      {optimisticMessages.map((m) => (
        <div>
          {m.message}
          {m.sending ? "Sending..." : ""}
        </div>
      ))}
      <form
        action={async (formData) => {
          const message = formData.get("message");
          formRef.current.reset();
          addOptimisticMessage(message);
          await send(message);
        }}
        ref={formRef}
      >
        <input type="text" name="message" />
      </form>
    </div>
  );
}
```

### Deneysel `useFormStatus`

Deneysel `useFormStatus` kancası Form Eylemleri içinde kullanılabilir ve `pending` özelliğini sağlar.

```js
"use client";

import { experimental_useFormStatus as useFormStatus } from "react-dom";

function Submit() {
  const { pending } = useFormStatus();

  return (
    <input
      type="submit"
      className={pending ? "button-pending" : "button-normal"}
      disabled={pending}
    >
      Submit
    </input>
  );
}
```

## Aşamalı İyileştirme

Aşamalı Geliştirme, bir `<form>`'un JavaScript olmadan veya JavaScript devre dışı bırakıldığında düzgün çalışmasını sağlar. Bu, form için JavaScript henüz yüklenmemiş olsa veya yüklenemese bile kullanıcıların formla etkileşime girmesine ve veri göndermesine olanak tanır.

Hem Sunucu Form Eylemleri hem de İstemci Form Eylemleri, iki stratejiden birini kullanarak Aşamalı Geliştirmeyi destekler:

- Bir Sunucu Eylemi doğrudan bir `<form>`'a aktarılırsa, JavaScript devre dışı bırakılsa bile form etkileşimlidir.
- Bir `<form>`'a bir İstemci Eylemi aktarılırsa, form hala etkileşimlidir, ancak eylem form hidratlanana kadar bir kuyruğa yerleştirilir. `<form>`, Seçici Hidrasyon ile önceliklendirilir, bu nedenle hızlı bir şekilde gerçekleşir.

```js
"use client";

import { useState } from "react";
import { handleSubmit } from "./actions.js";

export default function ExampleClientComponent({ myAction }) {
  const [input, setInput] = useState();

  return (
    <form action={handleSubmit} onChange={(e) => setInput(e.target.value)}>
      {/* ... */}
    </form>
  );
}
```

Her iki durumda da hidrasyon gerçekleşmeden önce form etkileşimlidir. Sunucu Eylemleri istemci JavaScript'ine dayanmama gibi ek bir avantaja sahip olsa da, etkileşimden ödün vermeden istediğiniz yerde İstemci Eylemleri ile ek davranışlar oluşturabilirsiniz.

## Boyut Sınırlaması

Varsayılan olarak, bir Sunucu Eylemine gönderilen istek gövdesinin maksimum boyutu 1 MB'dir. Bu, ayrıştırmak için çok fazla sunucu kaynağı tüketen büyük miktarda verinin sunucuya gönderilmesini önler.

Ancak, bu sınırı deneysel `serverActionsBodySizeLimit` seçeneğini kullanarak yapılandırabilirsiniz. Bayt sayısını veya baytlar tarafından desteklenen herhangi bir dize biçimini alabilir, örneğin `1000`, `'500kb'` veya `'3mb'`.

```js
module.exports = {
  experimental: {
    serverActions: true,
    serverActionsBodySizeLimit: "2mb",
  },
};
```

## Örnekler

### İstemci Bileşenleri ile Kullanım

#### İçe Aktarma

Sunucu Eylemleri İstemci Bileşenleri içinde tanımlanamaz, ancak içe aktarılabilirler. Sunucu Eylemlerini İstemci Bileşenlerinde kullanmak için, eylemi üst düzey bir "use server" yönergesi içeren bir dosyadan içe aktarabilirsiniz.

```js
"use server";

export async function addItem() {
  // ...
}
```

```js
"use client";

import { useTransition } from "react";
import { addItem } from "../actions";

function ExampleClientComponent({ id }) {
  let [isPending, startTransition] = useTransition();

  return (
    <button onClick={() => startTransition(() => addItem(id))}>
      Add To Cart
    </button>
  );
}
```

#### Proplar

Sunucu Eylemlerinin içe aktarılması tavsiye edilse de, bazı durumlarda bir Sunucu Eylemini bir İstemci Bileşenine prop olarak aktarmak isteyebilirsiniz.

Örneğin, eylem içinde dinamik olarak oluşturulan bir değer kullanmak isteyebilirsiniz. Bu durumda, bir Sunucu Eylemini prop olarak aktarmak uygun bir çözüm olabilir.

```js
import { ExampleClientComponent } from "./components/example-client-component.js";

function ExampleServerComponent({ id }) {
  async function updateItem(data) {
    "use server";
    modifyItem({ id, data });
  }

  return <ExampleClientComponent updateItem={updateItem} />;
}
```

```js
"use client";

function ExampleClientComponent({ updateItem }) {
  async function action(formData: FormData) {
    await updateItem(formData);
  }

  return (
    <form action={action}>
      <input type="text" name="name" />
      <button type="submit">Update Item</button>
    </form>
  );
}
```

### İsteğe Bağlı Yeniden Doğrulama

Sunucu Eylemleri, verileri isteğe bağlı olarak yola (`revalidatePath`) veya önbellek etiketine (`revalidateTag`) göre yeniden doğrulamak için kullanılabilir.

```js
import { revalidateTag } from "next/cache";

async function revalidate() {
  "sunucu kullan";
  revalidateTag("blog-posts");
}
```

### Doğrulama

Bir Sunucu Eylemine aktarılan veriler, eylem çağrılmadan önce doğrulanabilir veya temizlenebilir. Örneğin, eylemi bağımsız değişken olarak alan ve geçerli olması durumunda eylemi çağıran bir işlev döndüren bir sarmalayıcı işlev oluşturabilirsiniz.

```js
"use server";

import { withValidate } from "lib/form-validation";

export const action = withValidate((data) => {
  // ...
});
```

```js
export function withValidate(action) {
  return async (formData: FormData) => {
    "use server";

    const isValidData = verifyData(formData);

    if (!isValidData) {
      throw new Error("Invalid input.");
    }

    const data = process(formData);
    return action(data);
  };
}
```

### Başlıkları kullanma

Bir Sunucu Eylemi içinde `cookies` ve `headers` gibi gelen istek üstbilgilerini okuyabilirsiniz.

```js
import { cookies } from "next/headers";

async function addItem(data) {
  "use server";

  const cartId = cookies().get("cartId")?.value;

  await saveToDb({ cartId, data });
}
```

Ayrıca, bir Sunucu Eylemi içinde çerezleri değiştirebilirsiniz.

```js
import { cookies } from 'next/headers';

async function create(data) {
  'use server';

  const cart = await createCart():
  cookies().set('cartId', cart.id)
  // or
  cookies().set({
    name: 'cartId',
    value: cart.id,
    httpOnly: true,
    path: '/'
  })
}
```

## Glossary

### Eylemler (Actions)

Eylemler, React'te deneysel bir özelliktir ve bir kullanıcı etkileşimine yanıt olarak `asenkron` kod çalıştırmanıza olanak tanır.

Eylemler Next.js veya React Sunucu Bileşenlerine özgü değildir, ancak React'in kararlı sürümünde henüz mevcut değildir. Next.js aracılığıyla Eylemleri kullanırken, React `experimental` kanalını kullanmayı tercih etmiş olursunuz.

Eylemler, bir öğe üzerindeki `action` prop aracılığıyla tanımlanır. Genellikle HTML formları oluştururken, [action prop](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#action)'a bir URL iletirsiniz. Eylemler ile React artık doğrudan bir fonksiyon aktarmanıza izin veriyor.

React ayrıca Eylemler ile optimize güncellemeler için yerleşik çözümler sunar. Yeni modellerin hala geliştirilmekte olduğunu ve yeni API'lerin eklenebileceğini unutmamak önemlidir.

### Form Eylemleri

Web standardı `<form>` API'sine entegre edilmiş eylemler, kullanıma hazır aşamalı geliştirme ve yükleme durumlarını etkinleştirir. HTML ilkel [formaction](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#formaction)'a benzer.

### Sunucu İşlevleri

Sunucuda çalışan ancak istemcide çağrılabilen işlevler.

### Sunucu Eylemleri

Sunucu İşlevleri bir eylem olarak çağrılır.

Sunucu Eylemleri, bir `form` öğesinin `action` prop'una geçirilerek aşamalı olarak geliştirilebilir. Form, herhangi bir istemci tarafı JavaScript yüklenmeden önce etkileşimlidir. Bu, formun gönderilmesi için React hidrasyonunun gerekli olmadığı anlamına gelir.

### Sunucu Mutasyonları

Verilerinizi değiştiren ve `redirect`, `revalidatePath` veya `revalidateTag`'i çağıran Sunucu Eylemleri.

# Şekillendirme (Styling)

Next.js, uygulamanızı şekillendirmenin farklı yollarını destekler:

- **Global CSS:** Geleneksel CSS konusunda deneyimli olanlar için kullanımı basit ve tanıdıktır, ancak uygulama büyüdükçe daha büyük CSS paketlerine ve stilleri yönetmede zorluklara yol açabilir.
- **CSS Modülleri:** Adlandırma çakışmalarını önlemek ve sürdürülebilirliği artırmak için yerel olarak kapsamlandırılmış CSS sınıfları oluşturun.
- **Tailwind CSS:** Yardımcı sınıflar oluşturarak hızlı özel tasarımlara olanak tanıyan yardımcı program öncelikli bir CSS çerçevesi.
- **Sass:** CSS'yi değişkenler, iç içe kurallar ve mixinler gibi özelliklerle genişleten popüler bir CSS ön işlemcisi.
- **CSS-in-JS:** CSS'yi doğrudan JavaScript bileşenlerinize yerleştirerek dinamik ve kapsamı belirlenmiş stil oluşturma olanağı sağlar.

# CSS Modülleri (CSS Modules)

Next.js, `.module.css` uzantısını kullanan CSS Modülleri için yerleşik desteğe sahiptir.

CSS Modülleri, otomatik olarak benzersiz bir sınıf adı oluşturarak CSS'yi yerel olarak kapsar. Bu, çakışma endişesi olmadan farklı dosyalarda aynı sınıf adını kullanmanıza olanak tanır. Bu davranış CSS Modüllerini bileşen düzeyinde CSS eklemek için ideal bir yol haline getirir.

## Örnek

CSS Modülleri, `app` dizini içindeki herhangi bir dosyaya aktarılabilir:

```js
import styles from "./styles.module.css";

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return <section className={styles.dashboard}>{children}</section>;
}
```

```css
.dashboard {
  padding: 24px;
}
```

CSS Modülleri isteğe bağlı bir özelliktir ve yalnızca `.module.css` uzantılı dosyalar için etkinleştirilir. Normal `<link>` stil sayfaları ve global CSS dosyaları hala desteklenmektedir.

Üretimde, tüm CSS Modülü dosyaları otomatik olarak birçok küçültülmüş ve kod bölünmüş `.css` dosyasına birleştirilecektir. Bu `.css` dosyaları uygulamanızdaki sıcak yürütme yollarını temsil eder ve uygulamanızın boyaması için minimum miktarda CSS yüklenmesini sağlar.

## Küresel Stiller (Global Styles)

Global stiller, `app` dizini içindeki herhangi bir düzene, sayfaya veya bileşene aktarılabilir.

**Bilmekte fayda var:** Bu, yalnızca `_app.js` dosyasının içindeki global stilleri içe aktarabileceğiniz `pages` dizininden farklıdır.

Örneğin, `app/global.css` adında bir stil sayfası düşünün:

```css
body {
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

Kök düzen `(app/layout.js)` içinde, stilleri uygulamanızdaki her rotaya uygulamak için `global.css` stil sayfasını içe aktarın:

```js
// Bu stiller uygulamadaki her rota için geçerlidir
import "./global.css";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Harici Stil Sayfaları (External Stylesheets)

Harici paketler tarafından yayınlanan stil sayfaları, ortak konumlandırılmış bileşenler de dahil olmak üzere `app` dizininin herhangi bir yerine içe aktarılabilir:

```js
import "bootstrap/dist/css/bootstrap.css";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body className="container">{children}</body>
    </html>
  );
}
```

**Bilmekte fayda var:** Harici stil sayfaları doğrudan bir npm paketinden içe aktarılmalı veya indirilmeli ve kod tabanınızla birlikte yerleştirilmelidir. `<link rel="stylesheet" />` kullanamazsınız.

## Ek Özellikler

Next.js, stil ekleme yazma deneyimini iyileştirmek için ek özellikler içerir:

- `Next Dev` ile yerel olarak çalıştırılırken, yerel stil sayfaları (genel veya CSS modülleri), düzenlemeler kaydedildikçe değişiklikleri anında yansıtmak için Hızlı Yenileme özelliğinden yararlanacaktır.
- `Next build` ile üretim için oluştururken, stilleri almak için gereken ağ isteklerinin sayısını azaltmak için CSS dosyaları daha az sayıda küçültülmüş `.css` dosyasında bir araya getirilecektir.
- JavaScript'i devre dışı bırakırsanız stiller üretim derlemesinde (`next start`) yüklenmeye devam eder. Ancak, Hızlı Yenileme'yi etkinleştirmek için JavaScript'te `next dev` hala gereklidir.

# Tailwind CSS

[Tailwind CSS](https://tailwindcss.com/), Next.js ile son derece iyi çalışan bir yardımcı program öncelikli CSS çerçevesidir.

## Tailwind'i Yükleme

Tailwind CSS paketlerini yükleyin ve hem `tailwind.config.js` hem de `postcss.config.js` dosyalarını oluşturmak için `init` komutunu çalıştırın:

```terminal
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## Tailwind'i Yapılandırma

`tailwind.config.js` dosyasının içine Tailwind CSS sınıf adlarını kullanacak dosyaların yollarını ekleyin:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}", // App` dizininin eklendiğine dikkat edin.
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",

    // Veya `src` dizini kullanılıyorsa:
    "./src/**/*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

`postcss.config.js` dosyasını değiştirmenize gerek yoktur.

## Stilleri İçe Aktarma

Tailwind'in oluşturduğu stilleri uygulamanızdaki bir Global Stil Sayfasına enjekte etmek için kullanacağı [Tailwind CSS yönergelerini](https://tailwindcss.com/docs/functions-and-directives#directives) ekleyin:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Kök düzen `(app/layout.tsx`) içinde, stilleri uygulamanızdaki her rotaya uygulamak için `globals.css` stil sayfasını içe aktarın.

```js
import type { Metadata } from "next";

// These styles apply to every route in the application
import "./globals.css";

export const metadata: Metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## Sınıfları Kullanma

Tailwind CSS'yi yükledikten ve global stilleri ekledikten sonra, uygulamanızda Tailwind'in yardımcı sınıflarını kullanabilirsiniz.

```tsx
app / page.tsx;

export default function Page() {
  return <h1 className="text-3xl font-bold underline">Merhaba, Next.js!</h1>;
}
```

## Turbopack ile kullanım

Next.js 13.1'den itibaren Tailwind CSS ve PostCSS, [Turbopack](https://turbo.build/pack/docs/features/css#tailwind-css) ile desteklenmektedir.

# CSS-in-JS

**Uyarı:** Çalışma zamanı JavaScript gerektiren CSS-in-JS kütüphaneleri şu anda Sunucu Bileşenleri'nde desteklenmemektedir. CSS-in-JS'yi Sunucu Bileşenleri ve Akış gibi daha yeni React özellikleriyle kullanmak, kütüphane yazarlarının [eşzamanlı render etme](https://react.dev/blog/2022/03/29/react-v18#what-is-concurrent-react) dahil olmak üzere React'in en son sürümünü desteklemesini gerektirir.

React Sunucu Bileşenleri ve akış mimarisi desteğiyle CSS ve JavaScript varlıklarını işlemek için yukarı akış API'leri üzerinde React ekibiyle birlikte çalışıyoruz.

Aşağıdaki kütüphaneler `app` dizinindeki İstemci Bileşenlerinde desteklenmektedir (alfabetik olarak):

- [`kuma-ui`](https://kuma-ui.com/)
- [`@mui/material`](https://mui.com/material-ui/guides/next-js-app-router/)
- [`pandacss`](https://panda-css.com/)
- [`styled-jsx`](https://nextjs.org/docs/app/building-your-application/styling/css-in-js#styled-jsx)
- [`styled-components`](https://nextjs.org/docs/app/building-your-application/styling/css-in-js#styled-components)
- [`style9`](https://github.com/johanholmerin/style9)
- [`tamagui`](https://tamagui.dev/docs/guides/next-js#server-components)
- [`vanilya-extract`](https://github.com/vercel/next.js/tree/canary/examples/with-vanilla-extract)

Aşağıdakiler şu anda destek üzerinde çalışmaktadır:

- [`emotion`](https://github.com/emotion-js/emotion/issues/2928)

**Bilmekte fayda var:** Farklı CSS-in-JS kütüphanelerini test ediyoruz ve React 18 özelliklerini ve/veya `app` dizinini destekleyen kütüphaneler için daha fazla örnek ekleyeceğiz.

## Uygulamada CSS-in-JS'yi yapılandırma (Configuring CSS-in-JS in `app`)

CSS-in-JS'nin yapılandırılması üç adımlı bir katılım sürecidir:

- Bir render etme'deki tüm CSS kurallarını toplamak için bir stil kayıt defteri.
- Kuralları, onları kullanabilecek herhangi bir içerikten önce enjekte etmek için yeni `useServerInsertedHTML` kancası.
- İlk sunucu tarafı oluşturma sırasında uygulamanızı stil kayıt defteri ile saran bir İstemci Bileşeni.

### styled-jsx

İstemci Bileşenlerinde `styled-jsx` kullanmak için `v5.1.0` kullanılması gerekir. İlk olarak, yeni bir kayıt defteri oluşturun:

```js
app / registry.tsx;

("use client");

import React, { useState } from "react";
import { useServerInsertedHTML } from "next/navigation";
import { StyleRegistry, createStyleRegistry } from "styled-jsx";

export default function StyledJsxRegistry({
  children,
}: {
  children: React.ReactNode,
}) {
  // Only create stylesheet once with lazy initial state
  // x-ref: https://reactjs.org/docs/hooks-reference.html#lazy-initial-state
  const [jsxStyleRegistry] = useState(() => createStyleRegistry());

  useServerInsertedHTML(() => {
    const styles = jsxStyleRegistry.styles();
    jsxStyleRegistry.flush();
    return <>{styles}</>;
  });

  return <StyleRegistry registry={jsxStyleRegistry}>{children}</StyleRegistry>;
}
```

Ardından, kök düzeninizi kayıt defteri ile sarın:

```js
app / layout.tsx;

import StyledJsxRegistry from "./registry";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html>
      <body>
        <StyledJsxRegistry>{children}</StyledJsxRegistry>
      </body>
    </html>
  );
}
```

### Styled Components

Aşağıda `styled-components@v6.0.0-rc.1` veya daha büyük bir adresin nasıl yapılandırılacağına dair bir örnek verilmiştir:

İlk olarak, `styled-components` API'sini kullanarak render etme sırasında oluşturulan tüm CSS stil kurallarını toplayacak global bir kayıt bileşeni ve bu kuralları döndürecek bir fonksiyon oluşturun. Ardından, kayıt defterinde toplanan stilleri kök mizanpajdaki `<head>` HTML etiketine enjekte etmek için `useServerInsertedHTML` kancasını kullanın.

```js
lib / registry.tsx;

("use client");

import React, { useState } from "react";
import { useServerInsertedHTML } from "next/navigation";
import { ServerStyleSheet, StyleSheetManager } from "styled-components";

export default function StyledComponentsRegistry({
  children,
}: {
  children: React.ReactNode,
}) {
  // Only create stylesheet once with lazy initial state
  // x-ref: https://reactjs.org/docs/hooks-reference.html#lazy-initial-state
  const [styledComponentsStyleSheet] = useState(() => new ServerStyleSheet());

  useServerInsertedHTML(() => {
    const styles = styledComponentsStyleSheet.getStyleElement();
    styledComponentsStyleSheet.instance.clearTag();
    return <>{styles}</>;
  });

  if (typeof window !== "undefined") return <>{children}</>;

  return (
    <StyleSheetManager sheet={styledComponentsStyleSheet.instance}>
      {children}
    </StyleSheetManager>
  );
}
```

Kök düzenin `children` öğelerini stil kayıt defteri bileşeniyle sarın:

```js
app / layout.tsx;

import StyledComponentsRegistry from "./lib/registry";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html>
      <body>
        <StyledComponentsRegistry>{children}</StyledComponentsRegistry>
      </body>
    </html>
  );
}
```

**Bilmekte fayda var:**

- Sunucu render etme sırasında, stiller global bir kayıt defterine çıkarılır ve HTML'nizin `<head>` bölümüne aktarılır. Bu, stil kurallarının onları kullanabilecek tüm içeriklerden önce yerleştirilmesini sağlar. Gelecekte, stilleri nereye enjekte edeceğimizi belirlemek için yakında çıkacak bir React özelliğini kullanabiliriz.
- Akış sırasında, her bir yığından gelen stiller toplanacak ve mevcut stillere eklenecektir. İstemci tarafı hidrasyon tamamlandıktan sonra, `styled-components` her zamanki gibi devralacak ve başka dinamik stiller enjekte edecektir.
- Stil kaydı için özellikle ağacın en üst seviyesinde bir İstemci Bileşeni kullanıyoruz çünkü CSS kurallarını bu şekilde çıkarmak daha verimli. Bu, sonraki sunucu render etme'lerinde stillerin yeniden oluşturulmasını ve Sunucu Bileşeni yükünde gönderilmesini önler.

# Sass

Next.js, hem `.scss` hem de `.sass` uzantılarını kullanarak Sass için yerleşik desteğe sahiptir. `module.scss` veya `.module.sass` uzantısı aracılığıyla bileşen düzeyinde Sass kullanabilirsiniz.

İlk olarak, [`sass`](https://github.com/sass/sass) yükleyin:

```terminal
npm install --save-dev sass
```

**Bilmekte fayda var:**

Sass, her biri kendi uzantısına sahip [iki farklı sözdizimini](https://sass-lang.com/documentation/syntax) destekler. `.scss` uzantısı [SCSS sözdizimini](https://sass-lang.com/documentation/syntax#scss) kullanmanızı gerektirirken, `.sass` uzantısı [Girintili Sözdizimini ("Sass")](https://sass-lang.com/documentation/syntax#the-indented-syntax) kullanmanızı gerektirir.

Hangisini seçeceğinizden emin değilseniz, CSS'nin bir üst kümesi olan ve Girintili Sözdizimini ("Sass") öğrenmenizi gerektirmeyen `.scss` uzantısı ile başlayın.

## Sass Seçeneklerini Özelleştirme

Sass derleyicisini yapılandırmak istiyorsanız `next.config.js` dosyasında `sassOptions` seçeneğini kullanın.

```js
next.config.js;

const path = require("path");

module.exports = {
  sassOptions: {
    includePaths: [path.join(__dirname, "styles")],
  },
};
```

## Sass Değişkenleri

Next.js, CSS Modülü dosyalarından dışa aktarılan Sass değişkenlerini destekler.

Örneğin, dışa aktarılan `primaryColor` Sass değişkenini kullanarak:

```scss

app/variables.module.scss

$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

```js
app / page.js;

// maps to root `/` URL

import variables from "./variables.module.scss";

export default function Page() {
  return <h1 style={{ color: variables.primaryColor }}>Hello, Next.js!</h1>;
}
```

# Optimizasyonlar (Optimizations)

Next.js, uygulamanızın hızını ve [Core Web Vitals](https://web.dev/vitals/)'ı iyileştirmek için tasarlanmış çeşitli yerleşik optimizasyonlarla birlikte gelir. Bu kılavuz, kullanıcı deneyiminizi geliştirmek için yararlanabileceğiniz optimizasyonları kapsayacaktır.

## Yerleşik Bileşenler

Yerleşik bileşenler, yaygın UI optimizasyonlarını uygulamanın karmaşıklığını ortadan kaldırır. Bu bileşenler şunlardır:

- **Görüntüler:** Yerel `<img>` öğesi üzerine inşa edilmiştir. Görüntü Bileşeni, tembel yükleme ve görüntüleri cihaz boyutuna göre otomatik olarak yeniden boyutlandırma yoluyla görüntüleri performans için optimize eder.
- **Bağlantı:** Yerel `<a>` etiketleri üzerine inşa edilmiştir. Bağlantı Bileşeni, daha hızlı ve daha yumuşak sayfa geçişleri için sayfaları arka planda önceden hazırlar.
- **Komut Dosyaları:** Yerel `<script>` etiketleri üzerine inşa edilmiştir. Komut Dosyası Bileşeni, üçüncü taraf komut dosyalarının yüklenmesi ve yürütülmesi üzerinde kontrol sahibi olmanızı sağlar.

## Metadata

Meta veriler, arama motorlarının içeriğinizi daha iyi anlamasına yardımcı olur (bu da daha iyi SEO ile sonuçlanabilir) ve içeriğinizin sosyal medyada nasıl sunulduğunu özelleştirmenize olanak tanıyarak çeşitli platformlarda daha ilgi çekici ve tutarlı bir kullanıcı deneyimi oluşturmanıza yardımcı olur.

Next.js'deki Metadata API, bir sayfanın `<head>` öğesini değiştirmenize olanak tanır. Meta verileri iki şekilde yapılandırabilirsiniz:

- **Yapılandırma Tabanlı Meta Veriler:** Statik bir meta veri nesnesini veya dinamik bir generateMetadata işlevini bir `layout.js` veya `page.js` dosyasına aktarın.
- **Dosya Tabanlı Meta Veriler:** Rota segmentlerine statik veya dinamik olarak oluşturulan özel dosyalar ekleyin.

Ayrıca, imageResponse yapıcısı ile JSX ve CSS kullanarak dinamik Open Graph Görüntüleri oluşturabilirsiniz.

## Statik Varlıklar

Next.js `/public` klasörü resimler, yazı tipleri ve diğer dosyalar gibi statik varlıkları sunmak için kullanılabilir. `/public` içindeki dosyalar da CDN sağlayıcıları tarafından önbelleğe alınabilir, böylece verimli bir şekilde teslim edilirler.

## Analitik ve İzleme

Büyük uygulamalar için Next.js, uygulamanızın nasıl performans gösterdiğini anlamanıza yardımcı olmak için popüler analiz ve izleme araçlarıyla entegre olur.

# Görüntü Optimizasyonu (Image Optimization)

[Web Almanac](https://almanac.httparchive.org/)'a göre, görseller tipik bir web sitesinin sayfa ağırlığının büyük bir bölümünü oluşturur ve web sitenizin [LCP performansı](https://almanac.httparchive.org/en/2022/performance#lcp-image-optimization) üzerinde önemli bir etkiye sahip olabilir.

Next.js Image bileşeni, HTML `<img>` öğesini otomatik görüntü optimizasyonuna yönelik özelliklerle genişletir:

- **Boyut Optimizasyonu:** WebP ve AVIF gibi modern görüntü formatlarını kullanarak her cihaz için otomatik olarak doğru boyutta görüntüler sunun.
- **Görsel Kararlılık:** Görüntüler yüklenirken düzen kaymasını otomatik olarak önleyin.
- **Daha Hızlı Sayfa Yüklemeleri:** Görüntüler, isteğe bağlı bulanıklaştırma yer tutucuları ile yerel tarayıcıda lazy loading kullanılarak yalnızca görüntü alanına girdiklerinde yüklenir.
- **Varlık Esnekliği:** Uzak sunucularda depolanan görüntüler için bile isteğe bağlı görüntü yeniden boyutlandırma

**İzleyin:** [Youtube](https://youtu.be/IU_qq_c_lKA) → `next/image` nasıl kullanacağınız hakkında daha fazla bilgi edinin (9 dakika).

## Kullanım

```js
import Image from "next/image";
```

Daha sonra resminiz için `src` tanımlayabilirsiniz (yerel veya uzak).

### Yerel Görüntüler

Yerel bir görüntü kullanmak için `.jpg`, `.png` veya `.webp` görüntü dosyalarınızı içe aktarın.

Next.js, içe aktarılan dosyaya göre resminizin `width` ve `height` niteliklerini otomatik olarak belirleyecektir. Bu değerler, resminiz yüklenirken Kümülatif Düzen Kaymasını önlemek için kullanılır.

```js
import Image from "next/image";
import profilePic from "./me.png";

export default function Page() {
  return (
    <Image
      src={profilePic}
      alt="Picture of the author"
      // width={500} otomatik olarak sağlanır
      // height={500} otomatik olarak sağlanır
      // blurDataURL="data:..." otomatik olarak sağlanır
      // placeholder="blur" // Yükleme sırasında isteğe bağlı bulanıklaştırma
    />
  );
}
```

**Uyarı:** Dinamik `await import()` veya `require()` desteklenmez. Derleme zamanında analiz edilebilmesi için içe aktarma statik olmalıdır.

### Uzak Görüntüler

Uzak bir görüntü kullanmak için `src` özelliği bir URL dizesi olmalıdır.

Next.js'nin derleme işlemi sırasında uzak dosyalara erişimi olmadığından, `genişlik`, `yükseklik` ve isteğe bağlı `blurDataURL` desteklerini manuel olarak sağlamanız gerekir.

`width` ve `height` nitelikleri, görüntünün doğru en boy oranını çıkarmak ve görüntünün yüklenmesinden kaynaklanan düzen kaymasını önlemek için kullanılır. `width` ve `height`, görüntü dosyasının işlenen boyutunu belirlemez.

```js
import Image from "next/image";

export default function Page() {
  return (
    <Image
      src="https://s3.amazonaws.com/my-bucket/profile.png"
      alt="Picture of the author"
      width={500}
      height={500}
    />
  );
}
```

Görüntülerin optimize edilmesine güvenli bir şekilde izin vermek için `next.config.js` dosyasında desteklenen URL kalıplarının bir listesini tanımlayın. Kötü amaçlı kullanımı önlemek için mümkün olduğunca spesifik olun. Örneğin, aşağıdaki yapılandırma yalnızca belirli bir AWS S3 kovasından gelen görüntülere izin verecektir:

```js
// next.config.js
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "s3.amazonaws.com",
        port: "",
        pathname: "/my-bucket/**",
      },
    ],
  },
};
```

[`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns) yapılandırması hakkında daha fazla bilgi edinin. Resim `src` için göreli URL'ler kullanmak istiyorsanız, bir [`loader`](https://nextjs.org/docs/app/api-reference/components/image#loader) kullanın.

### Etki Alanları (Domains)

Bazen uzaktaki bir görüntüyü optimize etmek, ancak yine de yerleşik Next.js Görüntü Optimizasyon API'sini kullanmak isteyebilirsiniz. Bunu yapmak için, yükleyiciyi varsayılan ayarında bırakın ve Image `src` prop için mutlak bir URL girin.

Uygulamanızı kötü niyetli kullanıcılardan korumak için `next/image` bileşeniyle kullanmayı düşündüğünüz uzak ana bilgisayar adlarının bir listesini tanımlamanız gerekir.

### Yükleyiciler (Loaders)

Daha önceki örnekte, uzaktaki bir görüntü için kısmi bir URL (`"/me.png"`) sağlandığına dikkat edin. Bu, yükleyici mimarisi nedeniyle mümkündür.

Yükleyici, resminiz için URL'ler oluşturan bir işlevdir. Sağlanan `src`'yi değiştirir ve görüntüyü farklı boyutlarda istemek için birden çok URL oluşturur. Bu çoklu URL'ler otomatik [`srcset`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/srcset) oluşturmada kullanılır, böylece sitenize gelen ziyaretçilere görüntü alanları için doğru boyutta bir resim sunulur.

Next.js uygulamaları için varsayılan yükleyici, web üzerindeki herhangi bir yerden gelen görüntüleri optimize eden ve ardından bunları doğrudan Next.js web sunucusundan sunan yerleşik Görüntü Optimizasyon API'sini kullanır. Görüntülerinizi doğrudan bir CDN'den veya görüntü sunucusundan sunmak isterseniz, birkaç satır JavaScript ile kendi yükleyici işlevinizi yazabilirsiniz.

`Loader` prop ile görüntü başına veya `loaderFile` yapılandırması ile uygulama düzeyinde bir yükleyici tanımlayabilirsiniz.

## Öncelik

Her sayfa için [`En Büyük İçerik Boyası (LCP)`](https://web.dev/lcp/#what-elements-are-considered) öğesi olacak görüntüye `priority` özelliğini eklemelisiniz. Bunu yapmak Next.js'nin yükleme için görüntüye özel olarak öncelik vermesini sağlar (örneğin, ön yükleme etiketleri veya öncelik ipuçları aracılığıyla) ve LCP'de anlamlı bir artışa yol açar.

LCP öğesi genellikle sayfanın görüntü alanı içinde görünen en büyük resim veya metin bloğudur. `Next dev`'i çalıştırdığınızda, LCP öğesi `priority` özelliği olmayan bir `<Image>` ise bir konsol uyarısı görürsünüz.

LCP görüntüsünü belirledikten sonra, özelliği aşağıdaki gibi ekleyebilirsiniz:

```js
// app/page.js

import Image from "next/image";
import profilePic from "../public/me.png";

export default function Page() {
  return <Image src={profilePic} alt="Picture of the author" priority />;
}
```

[`next/image` bileşeni belgelerinde](https://nextjs.org/docs/app/api-reference/components/image#priority) `priority` hakkında daha fazla bilgi edinin.

## Görüntü Boyutlandırma (Image Sizing)

Görüntülerin performansa en çok zarar verdiği yollardan biri, görüntünün yüklenirken sayfadaki diğer öğeleri ittiği düzen kaymasıdır. Bu performans sorunu kullanıcılar için o kadar can sıkıcıdır ki [Kümülatif Düzen Kayması](https://web.dev/cls/) adı verilen kendi Core Web Vital'ine sahiptir. Görsel tabanlı düzen kaymalarını önlemenin yolu, [görsellerinizi her zaman boyutlandırmaktır](https://web.dev/optimize-cls/#images-without-dimensions). Bu, tarayıcının yüklemeden önce görüntü için tam olarak yeterli alan ayırmasını sağlar.

`next/image` iyi performans sonuçlarını garanti etmek için tasarlandığından, düzen kaymasına katkıda bulunacak şekilde kullanılamaz ve üç yoldan biriyle boyutlandırılmalıdır:

1. [Statik bir içe aktarma](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) kullanarak otomatik olarak
2. Açıkça, bir `width` ve `height` niteliği ekleyerek
3. Dolaylı olarak, görüntünün ana öğesini dolduracak şekilde genişlemesine neden olan [fill](https://nextjs.org/docs/app/api-reference/components/image#fill) kullanılarak.

**_Resimlerimin boyutunu bilmiyorsam ne yapmalıyım?_**

Görüntülerin boyutları hakkında bilgi sahibi olmadığınız bir kaynaktan görüntülere erişiyorsanız, yapabileceğiniz birkaç şey vardır:

**`fill` kullanın**

`fill` özelliği, resminizin ana öğesi tarafından boyutlandırılmasını sağlar. Herhangi bir medya sorgusu kesme noktasıyla eşleşecek şekilde boyutlar prop'u boyunca görüntünün üst öğesine sayfada alan vermek için CSS kullanmayı düşünün. Ayrıca görüntünün bu alanı nasıl kullanacağını tanımlamak için [`object-fit`](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit) ile `fill`, `contain` veya `cover` ve [`object-position`](https://developer.mozilla.org/en-US/docs/Web/CSS/object-position) kullanabilirsiniz.

**Görüntülerinizi normalleştirin**

Görüntüleri kontrol ettiğiniz bir kaynaktan sunuyorsanız, görüntüleri belirli bir boyuta normalleştirmek için görüntü işlem hattınızı değiştirmeyi düşünün.

**API çağrılarınızı değiştirin**

Uygulamanız bir API çağrısı kullanarak görüntü URL'lerini alıyorsa (örneğin bir CMS'ye), URL ile birlikte görüntü boyutlarını da döndürmek için API çağrısını değiştirebilirsiniz.

Resimlerinizi boyutlandırmak için önerilen yöntemlerden hiçbiri işe yaramazsa, `next/image` bileşeni standart `<img>` öğeleriyle birlikte bir sayfada iyi çalışacak şekilde tasarlanmıştır.

## Şekillendirme (Styling)

Image bileşenini şekillendirmek normal bir `<img>` öğesini şekillendirmeye benzer, ancak akılda tutulması gereken birkaç yönerge vardır:

- `className` veya `style` kullanın, `styled-jsx` değil.
  - Çoğu durumda `className` özelliğini kullanmanızı öneririz. Bu, içe aktarılmış bir CSS Modülü, global bir stil sayfası vb. olabilir.
  - Satır içi stilleri atamak için `style` özelliğini de kullanabilirsiniz.
  - styled-jsx'i kullanamazsınız çünkü geçerli bileşene kapsamlıdır (stili `global` olarak işaretlemediğiniz sürece).
- `fill` kullanırken, parent elementinin `position: relative` değerine sahip olması gerekir
  - Bu, görüntü öğesinin söz konusu düzen modunda düzgün bir şekilde oluşturulması için gereklidir.
- `fill` kullanıldığında, parent element `display: block` özelliğine sahip olmalıdır
  - Bu, `<div>` öğeleri için varsayılandır ancak aksi belirtilmelidir.

## Örnekler

### Duyarlı (Responsive)

<img alt="image" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fresponsive-image.png&w=3840&q=75&dpl=dpl_Ar23aifqMFJ8GSfuZKMSsarxXiuZ"/><br/>

```js
import Image from "next/image";
import mountains from "../public/mountains.jpg";

export default function Responsive() {
  return (
    <div style={{ display: "flex", flexDirection: "column" }}>
      <Image
        alt="Mountains"
        // Bir görüntünün içe aktarılması
        // genişlik ve yüksekliği otomatik olarak ayarlar
        src={mountains}
        sizes="100vw"
        // Görüntünün tam genişlikte görüntülenmesini sağlayın
        style={{
          width: "100%",
          height: "auto",
        }}
      />
    </div>
  );
}
```

### Konteyneri Doldurun (Fill Container)

<img alt="image" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ffill-container.png&w=3840&q=75&dpl=dpl_Ar23aifqMFJ8GSfuZKMSsarxXiuZ"/><br/>

```js
import Image from "next/image";
import mountains from "../public/mountains.jpg";

export default function Fill() {
  return (
    <div
      style={{
        display: "grid",
        gridGap: "8px",
        gridTemplateColumns: "repeat(auto-fit, minmax(400px, auto))",
      }}
    >
      <div style={{ position: "relative", height: "400px" }}>
        <Image
          alt="Mountains"
          src={mountains}
          fill
          sizes="(min-width: 808px) 50vw, 100vw"
          style={{
            objectFit: "cover", // cover, contain, none
          }}
        />
      </div>
      {/* Ve ızgarada daha fazla resim... */}
    </div>
  );
}
```

### Arka Plan Görüntüsü (Background Image)

<img alt="image" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Ffill-container.png&w=3840&q=75&dpl=dpl_Ar23aifqMFJ8GSfuZKMSsarxXiuZ"/><br/>

```js
import Image from "next/image";
import mountains from "../public/mountains.jpg";

export default function Background() {
  return (
    <Image
      alt="Mountains"
      src={mountains}
      placeholder="blur"
      quality={100}
      fill
      sizes="100vw"
      style={{
        objectFit: "cover",
      }}
    />
  );
}
```

Çeşitli stillerle kullanılan Görüntü bileşeni örnekleri için [Görüntü Bileşeni Demosu](https://image-component.nextjs.gallery/)'na bakın.

## Diğer Proplar (Other Properties)

[`next/image` bileşeni için kullanılabilir tüm özellikleri görüntüleyin.](https://nextjs.org/docs/app/api-reference/components/image)

## Konfigürasyon

`next/image` bileşeni ve Next.js Görüntü Optimizasyon API'si [`next.config.js` dosyasında](https://nextjs.org/docs/app/api-reference/next-config-js) yapılandırılabilir. Bu yapılandırmalar, [uzak görüntüleri etkinleştirmenize](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns), [özel görüntü kesme noktaları tanımlamanıza](https://nextjs.org/docs/app/api-reference/components/image#devicesizes), [önbelleğe alma davranışını değiştirmenize](https://nextjs.org/docs/app/api-reference/components/image#caching-behavior) ve daha fazlasına olanak tanır.

[Daha fazla bilgi için tam görüntü yapılandırma belgelerini okuyun.](https://nextjs.org/docs/app/api-reference/components/image#configuration-options)

# Yazı Tipi Optimizasyonu (Font Optimization)

`next/font` yazı tiplerinizi (özel yazı tipleri dahil) otomatik olarak optimize edecek ve gelişmiş gizlilik ve performans için harici ağ isteklerini kaldıracaktır.

🎥 **İzleyin:** next/font'un nasıl kullanılacağı hakkında daha fazla bilgi edinin → [YouTube (6 dakika)](https://www.youtube.com/watch?v=L8_98i_bMMA).

`next/font`, herhangi bir yazı tipi dosyası için yerleşik otomatik kendi kendine barındırma içerir. Bu, kullanılan temel CSS `size-adjust` özelliği sayesinde web fontlarını sıfır düzen kayması ile en iyi şekilde yükleyebileceğiniz anlamına gelir.

Bu yeni yazı tipi sistemi, performans ve gizliliği göz önünde bulundurarak tüm Google Yazı Tiplerini rahatça kullanmanıza da olanak tanır. CSS ve yazı tipi dosyaları derleme sırasında indirilir ve statik varlıklarınızın geri kalanıyla birlikte kendi kendine barındırılır. Tarayıcı tarafından Google'a hiçbir istek gönderilmez.

## Google Yazı Tipleri (Google Fonts)

Herhangi bir Google Yazı Tipini otomatik olarak kendi kendine barındırın. Yazı tipleri dağıtıma dahil edilir ve dağıtımınızla aynı etki alanından sunulur. Tarayıcı tarafından Google'a hiçbir istek gönderilmez.

Kullanmak istediğiniz yazı tipini next/font/google'dan bir işlev olarak içe aktararak başlayın. En iyi performans ve esneklik için [değişken yazı tipleri](https://fonts.google.com/variablefonts) kullanmanızı öneririz.

```js
// app/layout.tsx

import { Inter } from "next/font/google";

// Değişken bir yazı tipi yükleniyorsa, yazı tipi ağırlığını belirtmeniz gerekmez
const inter = Inter({
  subsets: ["latin"],
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={inter.className}>
      <body>{children}</body>
    </html>
  );
}
```

Değişken bir yazı tipi kullanamıyorsanız, bir ağırlık belirtmeniz gerekecektir:

```js
// app/layout.tsx

import { Roboto } from "next/font/google";

const roboto = Roboto({
  weight: "400",
  subsets: ["latin"],
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={roboto.className}>
      <body>{children}</body>
    </html>
  );
}
```

Bir dizi kullanarak birden fazla ağırlık ve/veya stil belirtebilirsiniz:

```js
// app/layout.tsx

const roboto = Roboto({
  weight: ["400", "700"],
  style: ["normal", "italic"],
  subsets: ["latin"],
  display: "swap",
});
```

**Bilmekte fayda var:** Birden fazla kelime içeren font adları için alt çizgi (\_) kullanın. Örneğin `Roboto Mono`, `Roboto_Mono` olarak içe aktarılmalıdır.

### Bir alt küme belirtme (Specifying a subset)

Google Yazı Tipleri otomatik olarak [alt kümelendirilir](https://fonts.google.com/knowledge/glossary/subsetting). Bu, yazı tipi dosyasının boyutunu azaltır ve performansı artırır. Bu alt kümelerden hangilerini önceden yüklemek istediğinizi tanımlamanız gerekir. `preload` doğruyken herhangi bir alt küme belirtilmemesi bir uyarı ile sonuçlanacaktır.

Bu, fonksiyon çağrısına eklenerek yapılabilir:

```js
const inter = Inter({ subsets: ["latin"] }); // latin alt kümesi
```

### Birden Fazla Yazı Tipi Kullanma (Using Multiple Fonts)

Uygulamanızda birden fazla yazı tipini içe aktarabilir ve kullanabilirsiniz. Kullanabileceğiniz iki yaklaşım vardır.

İlk yaklaşım, bir yazı tipini dışa aktaran, içe aktaran ve gerektiğinde `className`'ini uygulayan bir yardımcı program işlevi oluşturmaktır. Bu, yazı tipinin yalnızca işlendiğinde önceden yüklenmesini sağlar:

```js
// app/fonts.ts
import { Inter, Roboto_Mono } from "next/font/google";

export const inter = Inter({
  subsets: ["latin"],
  display: "swap",
});

export const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  display: "swap",
});
```

```js
// app/layout.tsx

import { inter } from "./fonts";

export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className={inter.className}>
      <body>
        <div>{children}</div>
      </body>
    </html>
  );
}
```

```js
// app/page.tsx

import { roboto_mono } from "./fonts";

export default function Page() {
  return (
    <>
      <h1 className={roboto_mono.className}>My page</h1>
    </>
  );
}
```

Yukarıdaki örnekte, `Inter` global olarak uygulanacak ve `Roboto Mono` gerektiğinde içe aktarılıp uygulanabilecektir.

Alternatif olarak, bir CSS değişkeni oluşturabilir ve bunu tercih ettiğiniz CSS çözümüyle kullanabilirsiniz:

```js
// app/layout.tsx

import { Inter, Roboto_Mono } from "next/font/google";
import styles from "./global.css";

const inter = Inter({
  subsets: ["latin"],
  variable: "--font-inter",
  display: "swap",
});

const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  variable: "--font-roboto-mono",
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={`${inter.variable} ${roboto_mono.variable}`}>
      <body>
        <h1>My App</h1>
        <div>{children}</div>
      </body>
    </html>
  );
}
```

```css
/* app/global.css */
html {
  font-family: var(--font-inter);
}

h1 {
  font-family: var(--font-roboto-mono);
}
```

Yukarıdaki örnekte, `Inter` global olarak uygulanacak ve tüm `<h1>` etiketleri `Roboto Mono` ile şekillendirilecektir.

**Öneri:** Her yeni yazı tipi kullanıcının indirmesi gereken ek bi kaynak olduğundan, birden fazla yazı tipini ihtiyatlı bir şekilde kullanın.

## Yerel Yazı Tipleri (Local Fonts)

`next/font/local` öğesini içe aktarın ve yerel yazı tipi dosyanızın `src`'sini belirtin. En iyi performans ve esneklik için [değişken fontlar](https://fonts.google.com/variablefonts) kullanmanızı öneririz.

```js
import localFont from "next/font/local";

// Yazı tipi dosyaları `app` içine yerleştirilebilir
const myFont = localFont({
  src: "./my-font.woff2",
  display: "swap",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={myFont.className}>
      <body>{children}</body>
    </html>
  );
}
```

Tek bir font ailesi için birden fazla dosya kullanmak istiyorsanız, `src` bir dizi olabilir:

```js
const roboto = localFont({
  src: [
    {
      path: "./Roboto-Regular.woff2",
      weight: "400",
      style: "normal",
    },
    {
      path: "./Roboto-Italic.woff2",
      weight: "400",
      style: "italic",
    },
    {
      path: "./Roboto-Bold.woff2",
      weight: "700",
      style: "normal",
    },
    {
      path: "./Roboto-BoldItalic.woff2",
      weight: "700",
      style: "italic",
    },
  ],
});
```

## Tailwind CSS ile

`next/font`, bir CSS değişkeni aracılığıyla Tailwind CSS ile kullanılabilir.

Aşağıdaki örnekte, `next/font/google`'dan Inter yazı tipini kullanıyoruz (Google veya Yerel Yazı Tiplerinden herhangi bir yazı tipini kullanabilirsiniz). CSS değişken adınızı tanımlamak için fontunuzu `variable` seçeneği ile yükleyin ve `inter`'e atayın. Ardından, CSS değişkenini HTML belgenize eklemek için `inter.variable` kullanın.

```js
// app/layout.tsx

import { Inter, Roboto_Mono } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
  display: "swap",
  variable: "--font-inter",
});

const roboto_mono = Roboto_Mono({
  subsets: ["latin"],
  display: "swap",
  variable: "--font-roboto-mono",
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en" className={`${inter.variable} ${roboto_mono.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

Son olarak, CSS değişkenini Tailwind CSS yapılandırmanıza ekleyin:

```js
// tailwind.config.js

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ["var(--font-inter)"],
        mono: ["var(--font-roboto-mono)"],
      },
    },
  },
  plugins: [],
};
```

Artık fontu öğelerinize uygulamak için `font-sans` ve `font-mono` yardımcı sınıflarını kullanabilirsiniz.

## Ön Yükleme

Sitenizin bir sayfasında bir yazı tipi işlevi çağrıldığında, bu işlev genel olarak kullanılamaz ve tüm rotalara önceden yüklenmez. Bunun yerine, yazı tipi yalnızca kullanıldığı dosya türüne bağlı olarak ilgili rotalara önceden yüklenir:

- Benzersiz bir sayfaysa, o sayfanın benzersiz rotasına önceden yüklenir.
- Bir düzen ise, düzen tarafından sarılan tüm rotalara önceden yüklenir.
- Kök düzen ise, tüm rotalara önceden yüklenir.

## Yazı tiplerini yeniden kullanma

`localFont` veya Google font işlevini her çağırdığınızda, bu font uygulamanızda bir örnek olarak barındırılır. Bu nedenle, aynı font işlevini birden fazla dosyaya yüklerseniz, aynı fontun birden fazla örneği barındırılır. Bu durumda aşağıdakileri yapmanız önerilir:

- Yazı tipi yükleyici işlevini tek bir paylaşılan dosyada çağırın
- Sabit olarak dışa aktarın
- Bu yazı tipini kullanmak istediğiniz her dosyadaki sabiti içe aktarın

# Komut Dosyası Optimizasyonu (Script Optimization)

## Düzen Komut Dosyaları (Layout Scripts)

Birden fazla rota için üçüncü taraf bir komut dosyası yüklemek için `next/script` dosyasını içe aktarın ve komut dosyasını doğrudan düzen bileşeninize ekleyin:

```js
// app/dashboard/layout.tsx

import Script from "next/script";

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <>
      <section>{children}</section>
      <Script src="https://example.com/script.js" />
    </>
  );
}
```

Üçüncü taraf komut dosyası, kullanıcı tarafından klasör rotasına (örn. `dashboard/page.js`) veya iç içe geçmiş herhangi bir rotaya (örn. `dashboard/settings/page.js`) erişildiğinde getirilir. Next.js, kullanıcı aynı düzende birden fazla rota arasında gezinse bile komut dosyasının yalnızca bir kez yüklenmesini sağlar.

## Uygulama Komut Dosyaları (Application Scripts)

Tüm rotalar için üçüncü taraf bir komut dosyası yüklemek için `next/script` dosyasını içe aktarın ve komut dosyasını doğrudan kök düzeninize ekleyin:

```js
// app/layout.tsx
import Script from "next/script";

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <Script src="https://example.com/script.js" />
    </html>
  );
}
```

Bu komut dosyası, uygulamanızdaki herhangi bir rotaya erişildiğinde yüklenir ve yürütülür. Next.js, kullanıcı birden fazla sayfa arasında gezinse bile betiğin yalnızca bir kez yüklenmesini sağlayacaktır.

**Öneri:** Performans üzerindeki gereksiz etkiyi en aza indirmek için üçüncü taraf komut dosyalarını yalnızca belirli sayfalara veya düzenlere eklemenizi öneririz.

## Strateji (Strategy)

`next/script`'in varsayılan davranışı herhangi bir sayfa veya düzende üçüncü taraf komut dosyalarını yüklemenize izin verse de, `strategy` özelliğini kullanarak yükleme davranışına ince ayar yapabilirsiniz:

- `beforeInteractive`: Kodu herhangi bir Next.js kodundan önce ve herhangi bir sayfa hidrasyonu gerçekleşmeden önce yükleyin.
- `afterInteractive`: (varsayılan) Kodu erken ancak sayfada bir miktar hidrasyon gerçekleştikten sonra yükleyin.
- `lazyOnload`: Tarayıcı boşta kaldığında kodu daha sonra yükleyin.
- `worker`: (deneysel) Komut dosyasını bir web çalışanına yükleyin.

## Komut Dosyalarını Bir Web İşçisine Boşaltma (Deneysel) (Offloading Scripts to a Web Worker (Experimental))

**Uyarı:** `worker` stratejisi henüz kararlı değildir ve henüz `app` dizini ile çalışmaz. Dikkatli kullanın.

`worker` stratejisini kullanan komut dosyaları [Partytown](https://partytown.builder.io/) ile bir web çalışanına yüklenir ve yürütülür. Bu, ana iş parçacığını uygulama kodunuzun geri kalanına ayırarak sitenizin performansını artırabilir.

Bu strateji hala deneyseldir ve yalnızca `next.config.js` dosyasında `nextScriptWorkers` bayrağı etkinleştirilirse kullanılabilir:

```js
// next.config.js

module.exports = {
  experimental: {
    nextScriptWorkers: true,
  },
};
```

Ardından, `next`'i çalıştırın (normalde `npm run dev` veya `yarn dev`) ve Next.js kurulumu tamamlamak için gerekli paketlerin kurulumunda size rehberlik edecektir:

```bash
npm run dev # or yarn dev
```

Bunun gibi talimatlar göreceksiniz: Lütfen `npm install @builder.io/partytown` komutunu çalıştırarak Partytown'ı yükleyin

Kurulum tamamlandığında, `strategy="worker"` tanımlaması uygulamanızda Partytown'ı otomatik olarak başlatacak ve komut dosyasını bir web worker'a yükleyecektir.

```js
// pages/home.tsx

import Script from "next/script";

export default function Home() {
  return (
    <>
      <Script src="https://example.com/script.js" strategy="worker" />
    </>
  );
}
```

Bir web çalışanına üçüncü taraf bir komut dosyası yüklerken dikkate alınması gereken bir dizi ödünleşme vardır. Daha fazla bilgi için lütfen Partytown'ın [tradeoffs](https://partytown.builder.io/trade-offs) belgelerine bakın.

## Satır İçi Komut Dosyaları (Inline Scripts)

Satır içi komut dosyaları veya harici bir dosyadan yüklenmeyen komut dosyaları da Komut Dosyası bileşeni tarafından desteklenir. JavaScript'i küme parantezleri içine yerleştirerek yazılabilirler:

```js
<Script id="show-banner">
  {`document.getElementById('banner').classList.remove('hidden')`}
</Script>
```

Ya da `dangerouslySetInnerHTML` özelliğini kullanarak:

```js
<Script
  id="show-banner"
  dangerouslySetInnerHTML={{
    __html: `document.getElementById('banner').classList.remove('hidden')`,
  }}
/>
```

**Uyarı:** Next.js'nin komut dosyasını izlemesi ve optimize etmesi için satır içi komut dosyaları için bir `id` özelliği atanmalıdır.

## Ek Kodun Yürütülmesi (Executing Additional Code)

Olay işleyicileri, belirli bir olay gerçekleştikten sonra ek kod çalıştırmak için Script bileşeniyle birlikte kullanılabilir:

- `onLoad`: Kodun yüklenmesi tamamlandıktan sonra kodu çalıştırın.
- `onReady`: Kodun yüklenmesi bittikten sonra ve bileşen her takıldığında kodu çalıştırın.
- `onError`: Kod yüklenemezse kodu çalıştırın.

Bu işleyiciler yalnızca `next/script` içe aktarıldığında ve kodun ilk satırı olarak `"use client"` tanımlanan bir İstemci Bileşeni içinde kullanıldığında çalışır:

```js
// app/page.tsx;

("use client");

import Script from "next/script";

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        onLoad={() => {
          console.log("Script has loaded");
        }}
      />
    </>
  );
}
```

## Ek Özellikler

Bir `<script>` öğesine atanabilecek, Kod bileşeni tarafından kullanılmayan, [nonce](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/nonce) veya [özel veri nitelikleri](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*) gibi birçok DOM niteliği vardır. Herhangi bir ek niteliğin eklenmesi, HTML'ye dahil edilen son, optimize edilmiş `<script>` öğesine otomatik olarak iletecektir.

```js
// app/page.tsx;

import Script from "next/script";

export default function Page() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        id="example-script"
        nonce="XUENAJFW"
        data-test="script"
      />
    </>
  );
}
```

# Metadata

Next.js, gelişmiş SEO ve web paylaşılabilirliği için uygulama meta verilerinizi (örneğin HTML head öğenizin içindeki `meta` ve `link` etiketleri) tanımlamak için kullanılabilecek bir Meta Veri API'sine sahiptir.

Uygulamanıza meta veri eklemenin iki yolu vardır:

- **Yapılandırma Tabanlı Meta Veriler:** Statik bir `meta` veri nesnesini veya dinamik bir `generateMetadata` işlevini bir `layout.js` veya `page.js` dosyasına aktarın
- **Dosya Tabanlı Meta Veriler:** Rota segmentlerine statik veya dinamik olarak oluşturulan özel dosyalar ekleyin.

Bu iki seçenekle de Next.js sayfalarınız için ilgili `<head>` öğelerini otomatik olarak oluşturacaktır. `ImageResponse` yapıcısını kullanarak dinamik OG görüntüleri de oluşturabilirsiniz

## Statik Meta Veriler

Statik meta verileri tanımlamak için bir `layout.js` veya static `page.js` dosyasından bir Meta Veri nesnesini dışa aktarın.

```js
// layout.tsx / page.tsx

import { Metadata } from "next";

export const metadata: Metadata = {
  title: "...",
  description: "...",
};

export default function Page() {}
```

## Dinamik Meta Veriler

Dinamik değerler gerektiren meta verileri `fetch` etmek için `generateMetadata` işlevini kullanabilirsiniz.

```js
// app/products/[id]/page.tsx

import { Metadata, ResolvingMetadata } from 'next'

type Props = {
  params: { id: string }
  searchParams: { [key: string]: string | string[] | undefined }
}

export async function generateMetadata(
  { params, searchParams }: Props,
  parent?: ResolvingMetadata
): Promise<Metadata> {
  // read route params
  const id = params.id

  // fetch data
  const product = await fetch(`https://.../${id}`).then((res) => res.json())

  // isteğe bağlı olarak ana meta verilere erişim ve genişletme (değiştirmek yerine)
  const previousImages = (await parent).openGraph?.images || []

  return {
    title: product.title,
    openGraph: {
      images: ['/some-specific-page-image.jpg', ...previousImages],
    },
  }
}

export default function Page({ params, searchParams }: Props) {}
```

**Bilmekte fayda var:**

- `generateMetadata` aracılığıyla hem statik hem de dinamik meta veriler yalnızca Sunucu Bileşenlerinde desteklenir.
- Next.js, bir rota render ederken `generateMetadata`, `generateStaticParam`, Layouts, Pages ve Sunucu Bileşenlerinde aynı veriler için getirme isteklerini otomatik olarak tekilleştirir. `fetch` kullanılamıyorsa React `cache` kullanılabilir
- Next.js, istemciye UI akışı yapmadan önce `generateMetadata` içindeki veri getirme işleminin tamamlanmasını bekler. Bu, akışlı bir yanıtın ilk bölümünün `<head>` etiketlerini içermesini garanti eder.

## Dosya tabanlı meta veriler

Bu özel dosyalar meta veriler için kullanılabilir:

- favicon.ico, apple-icon.jpg ve icon.jpg
- opengraph-image.jpg ve twitter-image.jpg
- robots.txt
- sitemap.xml

Bunları statik meta veriler için kullanabilir veya bu dosyaları kodla programlı olarak oluşturabilirsiniz.

## Davranış

Dosya tabanlı meta veriler daha yüksek önceliğe sahiptir ve yapılandırma tabanlı meta verileri geçersiz kılar.

### Varsayılan Alanlar

Bir rota meta veri tanımlamasa bile her zaman eklenen iki varsayılan `meta` etiket vardır:

- [Meta charset etiketi](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#attr-charset) web sitesi için karakter kodlamasını ayarlar.
- [Meta viewport etiketi](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag), web sitesinin farklı cihazlara göre ayarlanması için görüntü alanı genişliğini ve ölçeğini ayarlar.

```bash
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

**Bilmekte fayda var:** Varsayılan `viewport` meta etiketinin üzerine yazabilirsiniz.

### Sıralama (Ordering)

Meta veriler, kök segmentten başlayarak son page.js segmentine en yakın segmente kadar sırayla değerlendirilir. Örneğin:

1. `app/layout.tsx` (Kök Düzen)
2. `app/blog/layout.tsx` (İç İçe Blog Düzeni)
3. `app/blog/[slug]/page.tsx` (Blog Sayfası)

### Birleştirme

Değerlendirme sırasını takiben, aynı rotadaki birden fazla segmentten dışa aktarılan Meta Veri nesneleri, bir rotanın nihai meta veri çıktısını oluşturmak için yüzeysel olarak birleştirilir. Yinelenen anahtarlar sıralamalarına göre değiştirilir.

Bu, daha önceki bir segmentte tanımlanan `openGraph` ve `robotlar` gibi iç içe geçmiş alanlara sahip meta verilerin, bunları tanımlayan son segment tarafından üzerine yazıldığı anlamına gelir.

#### Alanların üzerine yazma (Overwriting Fields)

```js
// app/layout.js
export const metadata = {
  title: "Acme",
  openGraph: {
    title: "Acme",
    description: "Acme is a...",
  },
};
```

```js
// app/blog/page.js
export const metadata = {
  title: "Blog",
  openGraph: {
    title: "Blog",
  },
};

// Output:
// <title>Blog</title>
// <meta property="og:title" content="Blog" />
```

Yukarıdaki örnekte:

- `app/layout.js` dosyasındaki `title`, `app/blog/page.js` dosyasındaki title ile değiştirilir.
- `app/layout.js`'deki tüm `openGraph` alanları `app/blog/page.js`'de değiştirilir çünkü `app/blog/page.js` `openGraph` meta verilerini ayarlar. `openGraph.description`'ın olmadığına dikkat edin.

Bazı iç içe geçmiş alanları segmentler arasında paylaşırken diğerlerinin üzerine yazmak isterseniz, bunları ayrı bir değişkene çekebilirsiniz:

```js
// app/shared-metadata.js
export const openGraphImage = { images: ["http://..."] };
```

```js
// app/page.js

import { openGraphImage } from "./shared-metadata";

export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: "Home",
  },
};
```

```js
import { openGraphImage } from "../shared-metadata";

export const metadata = {
  openGraph: {
    ...openGraphImage,
    title: "About",
  },
};
```

Yukarıdaki örnekte, OG görüntüsü `app/layout.js` ve `app/about/page.js` arasında paylaşılırken başlıklar farklıdır.

#### Devralınan alanlar (Inheriting fields)

```js
// app/layout.js

export const metadata = {
  title: "Acme",
  openGraph: {
    title: "Acme",
    description: "Acme is a...",
  },
};
```

```js
// app/about/page.js

export const metadata = {
  title: "About",
};

// Output:
// <title>About</title>
// <meta property="og:title" content="Acme" />
// <meta property="og:description" content="Acme is a..." />
```

**Notlar:**

- `app/layout.js`'deki `title`, `app/about/page.js`'deki `title` ile değiştirilir.
- `app/about/page.js` `openGraph` meta verilerini ayarlamadığı için `app/layout.js`'deki tüm `openGraph` alanları `app/about/page.js`'de miras alınır.

## Dinamik Görüntü Oluşturma (Dynamic Image Generation)

`ImageResponse` yapıcısı, JSX ve CSS kullanarak dinamik görüntüler oluşturmanıza olanak tanır. Bu, Open Graph görüntüleri, Twitter kartları ve daha fazlası gibi sosyal medya görüntüleri oluşturmak için kullanışlıdır.

`ImageResponse`, Edge Runtime'ı kullanır ve Next.js, edge'de önbelleğe alınan görüntülere doğru başlıkları otomatik olarak ekleyerek performansı artırmaya ve yeniden hesaplamayı azaltmaya yardımcı olur.

`ImageResponse`'u kullanmak için `next/server`'dan içe aktarabilirsiniz:

```js
// app/about/route.js

import { ImageResponse } from "next/server";

export const runtime = "edge";

export async function GET() {
  return new ImageResponse(
    (
      <div
        style={{
          fontSize: 128,
          background: "white",
          width: "100%",
          height: "100%",
          display: "flex",
          textAlign: "center",
          alignItems: "center",
          justifyContent: "center",
        }}
      >
        Hello world!
      </div>
    ),
    {
      width: 1200,
      height: 600,
    }
  );
}
```

`ImageResponse`, Rota İşleyicileri ve dosya tabanlı Meta Veriler dahil olmak üzere diğer Next.js API'leri ile iyi bir şekilde entegre olur. Örneğin, derleme zamanında veya istek zamanında dinamik olarak Open Graph görüntüleri oluşturmak için `ImageResponse`'u bir `opengraph-image.tsx` dosyasında kullanabilirsiniz.

`ImageResponse`, flexbox ve mutlak konumlandırma, özel yazı tipleri, metin kaydırma, merkezleme ve iç içe görüntüler gibi yaygın CSS özelliklerini destekler.

**Bilmekte fayda var:**

- Örnekler [Vercel OG Playground](https://og-playground.vercel.app/)'da mevcuttur.
- `ImageResponse`, HTML ve CSS'yi PNG'ye dönüştürmek için [@vercel/og](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation), [Satori](https://github.com/vercel/satori) ve Resvg kullanır
- Yalnızca Edge Çalışma Zamanı desteklenir. Varsayılan Node.js çalışma zamanı çalışmayacaktır.
- Yalnızca flexbox ve CSS özelliklerinin bir alt kümesi desteklenir. Gelişmiş düzenler (örn. `display: grid`) çalışmayacaktır.
- Maksimum paket boyutu `500KB`. Paket boyutu JSX, CSS, yazı tipleri, resimler ve diğer tüm varlıkları içerir. Sınırı aşarsanız, varlıkların boyutunu küçültmeyi veya çalışma zamanında getirmeyi düşünün.
- Yalnızca `ttf`, `otf` ve `woff` yazı tipi biçimleri desteklenir. Font ayrıştırma hızını en üst düzeye çıkarmak için `woff` yerine `ttf` veya `otf` tercih edilir.

## JSON-LD

[JSON-LD](https://json-ld.org/), içeriğinizi anlamak için arama motorları tarafından kullanılabilen yapılandırılmış veriler için bir formattır. Örneğin, bir kişiyi, bir olayı, bir organizasyonu, bir filmi, bir kitabı, bir tarifi ve diğer birçok varlık türünü tanımlamak için kullanabilirsiniz.

JSON-LD için şu anki önerimiz, yapılandırılmış verileri `layout.js` veya `page.js` bileşenlerinizde bir `<script>` etiketi olarak işlemektir.

Örneğin:

```js
// app/products/[id]/page.tsx

export default async function Page({ params }) {
  const product = await getProduct(params.id);

  const jsonLd = {
    "@context": "https://schema.org",
    "@type": "Product",
    name: product.name,
    image: product.image,
    description: product.description,
  };

  return (
    <section>
      {/_ Add JSON-LD to your page _/}
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      {/_ ... _/}
    </section>
  );
}
```

Yapılandırılmış verilerinizi Google için [Zengin Sonuçlar Testi](https://search.google.com/test/rich-results) veya [genel Şema İşaretleme Doğrulayıcısı](https://validator.schema.org/) ile doğrulayabilir ve test edebilirsiniz.

JSON-LD'nizi, [schema-dts](https://www.npmjs.com/package/schema-dts) gibi topluluk paketlerini kullanarak TypeScript ile yazabilirsiniz:

```js
import { Product, WithContext } from "schema-dts";

const jsonLd: WithContext<Product> = {
  "@context": "https://schema.org",
  "@type": "Product",
  name: "Next.js Sticker",
  image: "https://nextjs.org/imgs/sticker.png",
  description: "Dynamic at the speed of static.",
};
```

# Statik Varlıklar (Static Assets)

Next.js, görüntüler gibi statik dosyaları kök dizinde `public` adlı bir klasör altında sunabilir. `public` içindeki dosyalara daha sonra kodunuz tarafından temel URL'den (`/`) başlayarak başvurulabilir.

Örneğin, `public` içine `me.png` eklerseniz, aşağıdaki kod görüntüye erişecektir:

```js
// Avatar.js

import Image from "next/image";

export function Avatar() {
  return <Image src="/me.png" alt="me" width="64" height="64" />;
}
```

`Robots.txt`, `favicon.ico` gibi statik meta veri dosyaları için `app` klasörünün içinde özel meta veri dosyaları kullanmalısınız.

**Bilmekte fayda var:**

- Dizin `public` olarak adlandırılmalıdır. Bu ad değiştirilemez ve statik varlıkları sunmak için kullanılan tek dizindir.
- Yalnızca derleme sırasında `public` dizininde bulunan varlıklar Next.js tarafından sunulacaktır. Çalışma zamanında eklenen dosyalar kullanılamayacaktır. Kalıcı dosya depolama için [AWS S3](https://aws.amazon.com/s3/) gibi üçüncü taraf bir hizmet kullanmanızı öneririz.

# Tembel Yükleme (Lazy Loading)

Next.js'deki [tembel yükleme](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading), bir rotayı oluşturmak için gereken JavaScript miktarını azaltarak bir uygulamanın ilk yükleme performansını artırmaya yardımcı olur.

İstemci Bileşenlerinin ve içe aktarılan kitaplıkların yüklenmesini ertelemenize ve bunları yalnızca gerektiğinde istemci paketine dahil etmenize olanak tanır. Örneğin, bir kullanıcı açmak için tıklayana kadar bir modalin yüklenmesini ertelemek isteyebilirsiniz.

Next.js'de tembel yüklemeyi uygulayabileceğiniz iki yol vardır:

1. `next/dynamic` ile Dinamik İçe Aktarımları Kullanma
2. [Suspense](https://react.dev/reference/react/Suspense) ile [`React.lazy()`](https://react.dev/reference/react/lazy) Kullanımı

Varsayılan olarak, Sunucu Bileşenleri otomatik olarak [code split](https://developer.mozilla.org/en-US/docs/Glossary/Code_splitting) edebilir ve kullanıcı arayüzü parçalarını sunucudan istemciye aşamalı olarak göndermek için akışı kullanabilirsiniz. Tembel yükleme İstemci Bileşenleri için geçerlidir.

## `next/dynamic`

`next/dynamic`, [`React.lazy()`](https://react.dev/reference/react/lazy) ve [Suspense](https://react.dev/reference/react/Suspense)'in bir bileşimidir. Artımlı geçişe izin vermek için `app` ve `pages` dizinlerinde aynı şekilde davranır.

## Örnekler

### İstemci Bileşenlerini İçe Aktarma (Importing Client Components)

```js
// app/page.js

"use client";

import { useState } from "react";
import dynamic from "next/dynamic";

// Client Components:
const ComponentA = dynamic(() => import("../components/A"));
const ComponentB = dynamic(() => import("../components/B"));
const ComponentC = dynamic(() => import("../components/C"), { ssr: false });

export default function ClientComponentExample() {
  const [showMore, setShowMore] = useState(false);

  return (
    <div>
      {/* Hemen yükleyin, ancak ayrı bir istemci paketinde */}
      <ComponentA />

      {/* Talep üzerine yükleyin, yalnızca koşul karşılandığında/karşılanırsa */}
      {showMore && <ComponentB />}
      <button onClick={() => setShowMore(!showMore)}>Toggle</button>

      {/* Yalnızca istemci tarafına yükleyin */}
      <ComponentC />
    </div>
  );
}
```

### SSR'yi Atlama (Skipping SSR)

`React.lazy()` ve [Suspense](https://react.dev/reference/react/Suspense) kullanıldığında, İstemci Bileşenleri varsayılan olarak önceden render edilecektir (SSR).

Bir İstemci Bileşeni için ön render etmeyi devre dışı bırakmak istiyorsanız, ssr seçeneğini false olarak ayarlayabilirsiniz:

```js
const ComponentC = dynamic(() => import("../components/C"), { ssr: false });
```

### Sunucu Bileşenlerini İçe Aktarma (Importing Server Components)

Bir Sunucu Bileşenini dinamik olarak içe aktarırsanız, Sunucu Bileşeninin kendisi değil, yalnızca Sunucu Bileşeninin alt bileşenleri olan İstemci Bileşenleri lazy-load edilecektir.

```js
// app/page.js

import dynamic from "next/dynamic";

// Server Component:
const ServerComponent = dynamic(() => import("../components/ServerComponent"));

export default function ServerComponentExample() {
  return (
    <div>
      <ServerComponent />
    </div>
  );
}
```

### Harici Kütüphaneleri Yükleme

Harici kütüphaneler [`import()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) fonksiyonu kullanılarak isteğe bağlı olarak yüklenebilir. Bu örnekte bulanık arama için `fuse.js` harici kütüphanesi kullanılmaktadır. Modül, yalnızca kullanıcı arama girdisini yazdıktan sonra istemciye yüklenir.

```js
// app/page.js

"use client";

import { useState } from "react";

const names = ["Tim", "Joe", "Bel", "Lee"];

export default function Page() {
  const [results, setResults] = useState();

  return (
    <div>
      <input
        type="text"
        placeholder="Search"
        onChange={async (e) => {
          const { value } = e.currentTarget;
          // Dynamically load fuse.js
          const Fuse = (await import("fuse.js")).default;
          const fuse = new Fuse(names);

          setResults(fuse.search(value));
        }}
      />
      <pre>Results: {JSON.stringify(results, null, 2)}</pre>
    </div>
  );
}
```

### Özel bir yükleme bileşeni ekleme (Adding a custom loading component)

```js
// app/page.js

import dynamic from "next/dynamic";

const WithCustomLoading = dynamic(
  () => import("../components/WithCustomLoading"),
  {
    loading: () => <p>Loading...</p>,
  }
);

export default function Page() {
  return (
    <div>
      {/* <WithCustomLoading/> yüklenirken yükleme bileşeni oluşturulacaktır */}
      <WithCustomLoading />
    </div>
  );
}
```

### Adlandırılmış Dışa Aktarmaları İçe Aktarma (Importing Named Exports)

Adlandırılmış bir dışa aktarımı dinamik olarak içe aktarmak için, [`import()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) işlevi tarafından döndürülen Promise'den geri döndürebilirsiniz:

```js
// components/hello.js

"use client";

export function Hello() {
  return <p>Hello!</p>;
}
```

```js
// app/page.js

import dynamic from "next/dynamic";

const ClientComponent = dynamic(() =>
  import("../components/hello").then((mod) => mod.Hello)
);
```

# Analitik (Analytics)

[Next.js Speed Insights](https://nextjs.org/analytics), farklı metrikler kullanarak sayfaların performansını analiz etmenize ve ölçmenize olanak tanır.

[Vercel dağıtımlarında](https://vercel.com/docs/concepts/speed-insights?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) sıfır yapılandırma ile [Gerçek Deneyim Puanınızı](https://vercel.com/docs/concepts/speed-insights#core-web-vitals-explained?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) toplamaya başlayabilirsiniz.

Bu belgenin geri kalanında Next.js Speed Insights'ın kullandığı yerleşik aktarıcı açıklanmaktadır.

## Web Vitals

[Web Vitals](https://web.dev/vitals/), bir web sayfasının kullanıcı deneyimini yakalamayı amaçlayan bir dizi yararlı metriktir. Aşağıdaki web hayati değerlerinin tümü dahildir:

- [Time to First Byte](https://developer.mozilla.org/en-US/docs/Glossary/Time_to_first_byte) (TTFB)
- [First Contentful Paint](https://developer.mozilla.org/en-US/docs/Glossary/First_contentful_paint) (FCP)
- [Largest Contentful Paint](https://web.dev/lcp/) (LCP)
- [First Input Delay](https://web.dev/fid/) (FID)
- [Cumulative Layout Shift](https://web.dev/cls/) (CLS)
- [Interaction to Next Paint](https://web.dev/inp/) (INP) (experimental)

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

# Enstrümantasyon

Projenizin kök dizinindeki (veya kullanıyorsanız `src` klasörünün içindeki) `instrumentation.ts` (veya `.js`) dosyasından `register` adlı bir işlevi dışa aktarırsanız, yeni bir Next.js sunucu örneği önyüklendiğinde bu işlevi çağırırız.

**Bilmekte fayda var:**

- Bu özellik deneyseldir. Kullanmak için, `next.config.js` dosyanızda `experimental.instrumentationHook = true;` tanımlayarak açıkça tercih etmelisiniz.
- `instrumentation` dosyası, `app` veya `pages` dizini içinde değil, projenizin kök dizininde olmalıdır. Eğer `src` klasörünü kullanıyorsanız, dosyayı `pages` ve `app` ile birlikte `src`'nin içine yerleştirin.
- Bir son ek eklemek için `pageExtensions` yapılandırma seçeneğini kullanırsanız, `instrumentation` dosya adını da eşleşecek şekilde güncellemeniz gerekecektir.
- Kullanabileceğiniz temel bir [with-opentelemetry](https://github.com/vercel/next.js/tree/canary/examples/with-opentelemetry) örneği oluşturduk.

`register` işleviniz deploy edildiğinde, her soğuk önyüklemede çağrılacaktır (ancak her ortamda tam olarak bir kez).

Bazen, neden olacağı yan etkiler nedeniyle kodunuzda bir dosyayı içe aktarmak yararlı olabilir. Örneğin, bir dizi global değişkeni tanımlayan bir dosyayı içe aktarabilir, ancak içe aktarılan dosyayı kodunuzda asla açıkça kullanmayabilirsiniz. Yine de paketin bildirdiği global değişkenlere erişiminiz olacaktır.

Aşağıdaki örnekte gösterildiği gibi, `register` işlevinizde kullanmak isteyebileceğiniz `instrumentation.ts` dosyasında yan etkileri olan dosyaları içe aktarabilirsiniz:

```ts
// your-project/instrumentation.ts;

import { init } from "package-init";

export function register() {
  init();
}
```

Ancak, yan etkileri olan dosyaları içe aktarmak için bunun yerine `register` işlevinizin içinden `import` etmeyi kullanmanızı öneririz. Aşağıdaki örnek, bir `register` fonksiyonunda `import`'un temel bir kullanımını göstermektedir:

```ts
// your-project/instrumentation.ts
export async function register() {
  await import("package-with-side-effect");
}
```

Bunu yaparak, tüm yan etkilerinizi kodunuzda tek bir yerde toplayabilir ve dosyaların içe aktarılmasından kaynaklanan istenmeyen sonuçlardan kaçınabilirsiniz.

Tüm ortamlarda `register` diyoruz, bu nedenle hem `edge` hem de `nodejs`'i desteklemeyen herhangi bir kodu koşullu olarak içe aktarmak gerekir. Geçerli ortamı almak için `NEXT_RUNTIME` ortam değişkenini kullanabilirsiniz. Ortama özgü bir kodu içe aktarmak şu şekilde görünecektir:

```ts
// your-project/instrumentation.ts

export async function register() {
  if (process.env.NEXT_RUNTIME === "nodejs") {
    await import("./instrumentation-node");
  }

  if (process.env.NEXT_RUNTIME === "edge") {
    await import("./instrumentation-edge");
  }
}
```

# Yapılandırma (Configuring)

Next.js, projenizi belirli gereksinimleri karşılayacak şekilde özelleştirmenize olanak tanır. Bu, TypeScript, ESlint ve daha fazlası ile entegrasyonların yanı sıra Mutlak İçe Aktarmalar ve Ortam Değişkenleri gibi dahili yapılandırma seçeneklerini de içerir.

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

# ESLint

Next.js, kutudan çıkar çıkmaz entegre bir [ESLint](https://eslint.org/) deneyimi sağlar. `next lint`'i `package.json` dosyasına bir betik olarak ekleyin:

```json
{
  "scripts": {
    "lint": "next lint"
  }
}
```

Ardından `npm run lint` veya `yarn lint` komutunu çalıştırın:

```bash
yarn lint
```

Uygulamanızda henüz ESLint yapılandırılmadıysa, kurulum ve yapılandırma süreci boyunca size rehberlik edilecektir.

```bash
yarn lint
```

Bunun gibi bir komut istemi göreceksiniz:

? How would you like to configure ESLint?

❯ Strict (recommended)
Base
Cancel

Aşağıdaki üç seçenekten biri seçilebilir:

- **Strict:** Next.js'nin temel ESLint yapılandırması ile birlikte daha katı bir [Core Web Vitals kural kümesi](https://nextjs.org/docs/app/building-your-application/configuring/eslint#core-web-vitals) içerir. Bu, ESLint'i ilk kez kuran geliştiriciler için önerilen yapılandırmadır.

```bash
// .eslintrc.json

{
"extends": "next/core-web-vitals"
}
```

- **Base:** Next.js'nin temel ESLint yapılandırmasını içerir.

```bash
// .eslintrc.json

{
  "extends": "next"
}
```

- **Cancel:** Herhangi bir ESLint yapılandırması içermez. Bu seçeneği yalnızca kendi özel ESLint yapılandırmanızı kurmayı planlıyorsanız seçin.

İki yapılandırma seçeneğinden biri seçilirse Next.js, uygulamanızda geliştirme bağımlılıkları olarak `eslint` ve `eslint-config-next`'i otomatik olarak yükleyecek ve projenizin kök dizininde seçtiğiniz yapılandırmayı içeren bir `.eslintrc.json` dosyası oluşturacaktır.

Artık hataları yakalamak için ESLint'i her çalıştırmak istediğinizde `next lint`'i çalıştırabilirsiniz. ESLint kurulduktan sonra, her derleme sırasında otomatik olarak çalışacaktır (`next build`). Hatalar derlemeyi başarısız kılarken, uyarılar başarısız olmayacaktır.

`next build` sırasında ESLint'in çalışmasını istemiyorsanız, [ESLint'i Yoksayma](https://nextjs.org/docs/app/api-reference/next-config-js/eslint) belgesine bakın.

Geliştirme sırasında uyarıları ve hataları doğrudan kod düzenleyicinizde görüntülemek için uygun bir [entegrasyon](https://eslint.org/docs/user-guide/integrations#editors) kullanmanızı öneririz.

## ESLint Yapılandırması

Varsayılan yapılandırma (`eslint-config-next`) Next.js'de en iyi kullanıma hazır lintleme deneyimine sahip olmak için ihtiyacınız olan her şeyi içerir. Uygulamanızda ESLint zaten yapılandırılmadıysa, bu yapılandırmayla birlikte ESLint'i kurmak için `next lint`'i kullanmanızı öneririz.

`eslint-config-next`'i diğer ESLint yapılandırmalarıyla birlikte kullanmak isterseniz, herhangi bir çakışmaya neden olmadan bunu nasıl yapacağınızı öğrenmek için [Ek Yapılandırmalar](https://nextjs.org/docs/app/building-your-application/configuring/eslint#additional-configurations) bölümüne bakın.

Aşağıdaki ESLint eklentilerinden önerilen kural kümelerinin tümü `eslint-config-next` içinde kullanılır:

- [`eslint-plugin-react`](https://www.npmjs.com/package/eslint-plugin-react)
- [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks)
- [`eslint-plugin-next`](https://www.npmjs.com/package/@next/eslint-plugin-next)

Bu, `next.config.js` dosyasındaki yapılandırmaya göre öncelikli olacaktır.

## ESLint Eklentisi (ESlint Plugin)

Next.js, bir Next.js uygulamasındaki yaygın sorunları ve problemleri yakalamayı mümkün kılan temel yapılandırma içinde zaten paketlenmiş olan bir ESLint eklentisi, [eslint-plugin-next](https://www.npmjs.com/package/@next/eslint-plugin-next) sağlar. Kuralların tamamı aşağıdaki gibidir:

| Kural                                                    | Açıklama                                                                                              |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| @next/next/google-font-display                           | Google Fonts ile font-display davranışını zorlar.                                                     |
| @next/next/google-font-preconnect                        | Google Fonts ile `preconnect` kullanımını sağlar.                                                     |
| @next/next/inline-script-id                              | Satır içi içeriğe sahip `next/script` bileşenlerinde `id` niteliğini zorunlu kılın.                   |
| @next/next/next-script-for-ga                            | Google Analytics için satır içi script kullanırken `next/script` bileşenini tercih eder.              |
| @next/next/no-assign-module-variable                     | `module` değişkenine atama yapılmasını önler.                                                         |
| @next/next/no-async-client-component                     | İstemci bileşenlerinin async fonksiyonlar olmasını önler.                                             |
| @next/next/no-before-interactive-script-outside-document | `next/script`'in `beforeInteractive` stratejisinin `pages/_document.js` dışında kullanılmasını önler. |
| @next/next/no-css-tags                                   | Manuel stil sayfası etiketlerini önler.                                                               |
| @next/next/no-document-import-in-page                    | `next/document`'ın ` dışında içe aktarılmasını önler.                                                 |
| @next/next/no-duplicate-head                             | `pages/_document.js`'de `<Head>` kullanımının çoğaltılmasını önler.                                   |
| @next/next/no-head-element                               | `<head>` elementinin kullanımını önler.                                                               |
| @next/next/no-head-import-in-document                    | `pages/_document.js`'de `next/head` kullanımını önler.                                                |
| @next/next/no-html-link-for-pages                        | Dahili Next.js sayfalarına gitmek için `<a>` elementlerinin kullanılmasını önler.                     |
| @next/next/no-img-element                                | Daha yavaş LCP ve daha yüksek bant genişliği nedeniyle `<img>` elementinin kullanılmasını önler.      |
| @next/next/no-page-custom-font                           | Sadece sayfa özel fontlarını önler.                                                                   |
| @next/next/no-script-component-in-head                   | `next/head` bileşeninde `next/script` kullanımını önler.                                              |
| @next/next/no-styled-jsx-in-document                     | `pages/_document.js`'de `styled-jsx` kullanımını önler.                                               |
| @next/next/no-sync-scripts                               | Senkronize scriptleri önler.                                                                          |
| @next/next/no-title-in-document-head                     | `next/document`'tan Head bileşeni ile `<title>` kullanımını önler.                                    |
| @next/next/no-typos                                      | Next.js'in veri getirme fonksiyonlarında yaygın yazım hatalarını önler                                |
| @next/next/no-unwanted-polyfillio                        | Polyfill.io'dan çoğaltılmış polyfill'leri önler.                                                      |

Uygulamanızda zaten ESLint yapılandırılmışsa, birkaç koşul karşılanmadığı sürece `eslint-config-next`'i dahil etmek yerine doğrudan bu eklentiden genişletmenizi öneririz. Daha fazla bilgi için [Önerilen Eklenti Kural Seti](https://nextjs.org/docs/app/building-your-application/configuring/eslint#recommended-plugin-ruleset)'ne bakın.

### Özel Ayarlar

#### `rootDir`

Next.js'nin kök dizininizde yüklü olmadığı bir projede (monorepo gibi) `eslint-plugin-next` kullanıyorsanız, `eslint-plugin-next`'e `.eslintrc` dosyanızdaki `settings` özelliğini kullanarak Next.js uygulamanızı nerede bulacağını söyleyebilirsiniz:

```json
// .eslintrc.json

{
  "extends": "next",
  "settings": {
    "next": {
      "rootDir": "packages/my-app/"
    }
  }
}
```

`rootDir` bir yol (göreli veya mutlak), bir glob (örn. `"packages/\*/"`) veya bir yol ve/veya glob dizisi olabilir.

## Özel Dizinleri ve Dosyaları Lintleme

Next.js varsayılan olarak `pages/`, `app/`, `components/`, `lib/` ve `src/` dizinlerindeki tüm dosyalar için ESLint'i çalıştıracaktır. Ancak, üretim derlemeleri için `next.config.js` dosyasındaki `eslint` yapılandırmasında `dirs` seçeneğini kullanarak hangi dizinleri kullanacağınızı belirtebilirsiniz:

```js
// next.config.js

module.exports = {
  eslint: {
    dirs: ["pages", "utils"], // Üretim derlemeleri sırasında ESLint'i yalnızca 'pages' ve 'utils' dizinlerinde çalıştırın (next build)
  },
};
```

Benzer şekilde, `--dir` ve `--file` bayrakları `next lint` için belirli dizinleri ve dosyaları lintlemek için kullanılabilir:

```bash
next lint --dir pages --dir utils --file bar.js
```

## Önbellekleme (Caching)

Performansı artırmak için, ESLint tarafından işlenen dosyaların bilgileri varsayılan olarak önbelleğe alınır. Bu bilgiler `.next/cache` dosyasında veya tanımladığınız derleme dizininde saklanır. Tek bir kaynak dosyanın içeriğinden daha fazlasına bağlı olan herhangi bir ESLint kuralı ekliyorsanız ve önbelleği devre dışı bırakmanız gerekiyorsa, `next lint` ile `--no-cache` bayrağını kullanın.

```bash
next lint --no-cache
```

## Kuralları Devre Dışı Bırakma (Disabling Rules)

Desteklenen eklentiler (`react`, `react-hooks`, `next`) tarafından sağlanan herhangi bir kuralı değiştirmek veya devre dışı bırakmak isterseniz, `.eslintrc` dosyanızdaki rules özelliğini kullanarak bunları doğrudan değiştirebilirsiniz:

```json
// .eslintrc.json

{
  "extends": "next",
  "rules": {
    "react/no-unescaped-entities": "off",
    "@next/next/no-page-custom-font": "off"
  }
}
```

### Core Web Vitals

`next/core-web-vitals` kural kümesi, `next lint` ilk kez çalıştırıldığında ve strict seçeneği seçildiğinde etkinleştirilir.

```bash
{
  "extends": "next/core-web-vitals"
}
```

`next/core-web-vitals`, `eslint-plugin-next`'i [Core Web Vitals](https://web.dev/vitals/)'ı etkiliyorsa varsayılan olarak uyarı olan bir dizi kuralda hata verecek şekilde günceller.

`Next/core-web-vitals` giriş noktası, Create Next App ile oluşturulan yeni uygulamalar için otomatik olarak dahil edilir.

## Diğer Araçlarla Kullanım (Using with Other Tools)

### Prettier

ESLint ayrıca mevcut [Prettier](https://prettier.io/) kurulumunuzla çakışabilecek kod biçimlendirme kuralları da içerir. ESLint ve Prettier'in birlikte çalışmasını sağlamak için ESLint yapılandırmanıza [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)'i eklemenizi öneririz.

İlk olarak, bağımlılığı yükleyin:

```bash
npm install --save-dev eslint-config-prettier

yarn add --dev eslint-config-prettier
```

Ardından, mevcut ESLint yapılandırmanıza `prettier` ekleyin:

```json
// .eslintrc.json
{
  "extends": ["next", "prettier"]
}
```

### lint-staged

Aşamalı git dosyalarında linter çalıştırmak için [lint-staged](https://github.com/okonet/lint-staged) ile `next lint` kullanmak isterseniz, `--file` bayrağının kullanımını belirtmek için projenizin kök dizinindeki `.lintstagedrc.js` dosyasına aşağıdakileri eklemeniz gerekir.

```js
// .lintstagedrc.js

const path = require("path");

const buildEslintCommand = (filenames) =>
  `next lint --fix --file ${filenames
    .map((f) => path.relative(process.cwd(), f))
    .join(" --file ")}`;

module.exports = {
  "*.{js,jsx,ts,tsx}": [buildEslintCommand],
};
```

## Mevcut Yapılandırmayı Taşıma (Migrating Existing Configuration)

### Önerilen Eklenti Kural Seti (Recommended Plugin Rule Set)

Uygulamanızda zaten ESLint yapılandırılmışsa ve aşağıdaki koşullardan herhangi biri doğruysa:

- Aşağıdaki eklentilerden bir veya daha fazlasını zaten yüklediniz (ayrı olarak veya `airbnb` veya `react-app` gibi farklı bir yapılandırma aracılığıyla):
  - `react`
  - `react-hooks`
  - `jsx-a11y`
  - `import`
- Babel'in Next.js içinde yapılandırılma şeklinden farklı olan belirli `parserOptions` tanımladınız (Babel yapılandırmanızı özelleştirmediğiniz sürece bu önerilmez)
- İçe aktarmaları işlemek için tanımlanmış Node.js ve/veya TypeScript [çözümleyicileriyle](https://github.com/benmosher/eslint-plugin-import#resolvers) birlikte `eslint-plugin-import` yüklü

Ardından, bu özelliklerin [`eslint-config-next`](https://github.com/vercel/next.js/blob/canary/packages/eslint-config-next/index.js) içinde nasıl yapılandırıldığını tercih ediyorsanız bu ayarları kaldırmanızı veya bunun yerine doğrudan Next.js ESLint eklentisinden genişletmenizi öneririz:

```json
module.exports = {
  extends: [
    //...
    'plugin:@next/next/recommended',
  ],
};
```

Eklenti, `next lint`'i çalıştırmaya gerek kalmadan projenize normal şekilde kurulabilir:

```bash
npm install --save-dev @next/eslint-plugin-next

yarn add --dev @next/eslint-plugin-next
```

### Ek Konfigürasyonlar

Zaten ayrı bir ESLint yapılandırması kullanıyorsanız ve `eslint-config-next`'i dahil etmek istiyorsanız, diğer yapılandırmalardan sonra en son genişletildiğinden emin olun. Örneğin:

```json
// .eslintrc.json

{
  "extends": ["eslint:recommended", "next"]
}
```

`next` yapılandırma, `parser`, `plugins` ve `settings` özellikleri için varsayılan değerlerin ayarlanmasını zaten ele alır. Kullanım durumunuz için farklı bir yapılandırmaya ihtiyaç duymadığınız sürece bu özelliklerden herhangi birini manuel olarak yeniden beyan etmenize gerek yoktur.

Başka paylaşılabilir yapılandırmalar eklerseniz, bu özelliklerin üzerine yazılmadığından veya değiştirilmediğinden emin olmanız gerekir. Aksi takdirde, `next` yapılandırmayla davranış paylaşan tüm yapılandırmaları kaldırmanızı veya yukarıda belirtildiği gibi doğrudan Next.js ESLint eklentisinden genişletmenizi öneririz.

# Ortam Değişkenleri (Environment Variables)

Next.js, aşağıdakileri yapmanıza olanak tanıyan ortam değişkenleri için yerleşik destekle birlikte gelir:

- Ortam değişkenlerini yüklemek için `.env.local` kullanın
- `NEXT_PUBLIC_` ile önekleyerek tarayıcı için ortam değişkenlerini paketleyin

## Ortam Değişkenlerini Yükleme

Next.js, ortam değişkenlerini `.env.local`'den `process.env`'ye yüklemek için yerleşik desteğe sahiptir.

```bash
// .env.local


DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

Bu, `process.env.DB_HOST`, `process.env.DB_USER` ve `process.env.DB_PASS` dosyalarını otomatik olarak Node.js ortamına yükler ve bunları Rota İşleyicilerinde kullanmanıza olanak tanır.

Örneğin:

```js
// app/api/route.js

export async function GET() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  });
  // ...
}
```

### Diğer Değişkenlere Referans Verme

Next.js, `.env*` dosyalarınızın içindeki `$VARIABLE` gibi diğer değişkenlere referans vermek için `$` kullanan değişkenleri otomatik olarak genişletecektir. Bu, diğer gizliliklere referans vermenizi sağlar. Örneğin:

```bash
// .env
TWITTER_USER=nextjs
TWITTER_URL=https://twitter.com/$TWITTER_USER
```

Yukarıdaki örnekte, `process.env.TWITTER_URL` `https://twitter.com/nextjs` olarak ayarlanacaktır.

**Bilmekte fayda var:** Gerçek değerinde `$` olan bir değişken kullanmanız gerekiyorsa, bunun öncelenmesi gerekir, örneğin `\$`.

## Tarayıcı için Ortam Değişkenlerinin Paketlenmesi

Non-`NEXT_PUBLIC_` ortam değişkenleri yalnızca Node.js ortamında kullanılabilir, yani tarayıcı tarafından erişilemezler (istemci farklı bir ortamda çalışır).

Bir ortam değişkeninin değerini tarayıcıda erişilebilir kılmak için Next.js, derleme sırasında istemciye teslim edilen js paketine bir değer "satır içi" ekleyebilir ve `process.env.[variable]`'a yapılan tüm referansları sabit kodlanmış bir değerle değiştirebilir. Bunu yapmasını söylemek için değişkenin önüne `NEXT_PUBLIC_` eklemeniz yeterlidir. Örneğin:

```terminal
NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk
```

Bu, Next.js'ye Node.js ortamındaki `process.env.NEXT_PUBLIC_ANALYTICS_ID`'ye yapılan tüm referansları `next build`'i çalıştırdığınız ortamdaki değerle değiştirmesini söyleyecek ve kodunuzun herhangi bir yerinde kullanmanıza izin verecektir. Tarayıcıya gönderilen tüm JavaScript'lerde satır içi olarak yer alacaktır.

**Not:** Oluşturulduktan sonra, uygulamanız artık bu ortam değişkenlerindeki değişikliklere yanıt vermeyecektir. Örneğin, bir ortamda oluşturulan slug'ları başka bir ortama tanıtmak için bir Heroku pipeline kullanıyorsanız veya tek bir Docker görüntüsü oluşturup birden fazla ortama dağıtıyorsanız, tüm `NEXT_PUBLIC_` değişkenleri derleme zamanında değerlendirilen değerle dondurulacaktır, bu nedenle proje oluşturulduğunda bu değerlerin uygun şekilde ayarlanması gerekir. Çalışma zamanı ortam değerlerine erişmeniz gerekiyorsa, bunları istemciye sağlamak için kendi API'nizi kurmanız gerekir (talep üzerine veya başlatma sırasında).

```js
import setupAnalyticsService from "../lib/my-analytics-service";

// 'NEXT_PUBLIC_ANALYTICS_ID', 'NEXT_PUBLIC_' ile ön ekli olduğu için burada kullanılabilir.
// Derleme sırasında `setupAnalyticsService('abcdefghijk')` olarak dönüştürülecektir.

setupAnalyticsService(process.env.NEXT_PUBLIC_ANALYTICS_ID);

function HomePage() {
  return <h1>Hello World</h1>;
}

export default HomePage;
```

Aşağıdaki gibi dinamik aramaların satır içi yapılmayacağını unutmayın:

```js
// Bu bir değişken kullandığı için satır içi yapılmayacaktır
const varName = "NEXT_PUBLIC_ANALYTICS_ID";
setupAnalyticsService(process.env[varName]);

// Bu bir değişken kullandığı için satır içi yapılmayacaktır
const env = process.env;
setupAnalyticsService(env.NEXT_PUBLIC_ANALYTICS_ID);
```

## Varsayılan Ortam Değişkenleri

Genel olarak yalnızca bir `.env.local` dosyası gereklidir. Ancak, bazen geliştirme (`next dev`) veya production (`next start`) ortamı için bazı varsayılanlar eklemek isteyebilirsiniz.

Next.js, `.env` (tüm ortamlar), `.env.development` (geliştirme ortamı) ve `.env.production` (production ortamı) içinde varsayılanları ayarlamanıza olanak tanır.

`.env.local` her zaman ayarlanan varsayılanları geçersiz kılar.

**Bilmenizde fayda var:** `.env`, `.env.development` ve `.env.production` dosyaları varsayılanları tanımladıkları için deponuza dahil edilmelidir. `.env*.local` dosyaları `.gitignore`'a eklenmelidir, çünkü bu dosyaların göz ardı edilmesi amaçlanmıştır. `.env.local` gizli dosyaların saklanabileceği yerdir.

## Vercel'de Ortam Değişkenleri

Next.js uygulamanızı [Vercel](https://vercel.com/)'e deploy ederken, Ortam Değişkenleri [Proje Ayarları](https://vercel.com/docs/concepts/projects/environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website)'nda yapılandırılabilir.

Her tür Ortam Değişkeni burada yapılandırılmalıdır. Geliştirmede kullanılan Ortam Değişkenleri bile - ki bunlar daha sonra [yerel cihazınıza indirilebilir](https://vercel.com/docs/concepts/projects/environment-variables#development-environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website).

[Geliştirme Ortam Değişkenlerini yapılandırdıysanız](https://vercel.com/docs/concepts/projects/environment-variables#development-environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website), aşağıdaki komutu kullanarak bunları yerel makinenizde kullanmak üzere bir `.env.local` içine çekebilirsiniz:

```Terminal
vercel env pull .env.local
```

## Test Ortamı Değişkenleri

`development` ve `production` ortamlarının yanı sıra 3. bir seçenek daha mevcuttur: `test`. Geliştirme veya production ortamları için varsayılanları ayarlayabileceğiniz gibi, aynı şeyi test ortamı için bir `.env.test` dosyası ile de yapabilirsiniz (ancak bu önceki ikisi kadar yaygın değildir). Next.js, `testing` ortamında `.env.development` veya `.env.production` dosyalarındaki ortam değişkenlerini yüklemeyecektir.

Bu, yalnızca test amacıyla belirli ortam değişkenlerini ayarlamanız gereken `jest` veya `cypress` gibi araçlarla testler çalıştırırken kullanışlıdır. `NODE_ENV` `test` olarak ayarlanırsa test varsayılan değerleri yüklenecektir, ancak test araçları bunu sizin için ele alacağından genellikle bunu manuel olarak yapmanız gerekmez.

`test` ortamı ile hem `development` hem de `production` arasında aklınızda bulundurmanız gereken küçük bir fark vardır: Testlerin herkes için aynı sonuçları üretmesini beklediğiniz için `.env.local` yüklenmeyecektir. Bu şekilde her test yürütmesi, `.env.local` (varsayılan seti geçersiz kılmak için tasarlanmıştır) dosyanızı yok sayarak farklı yürütmelerde aynı env varsayılanlarını kullanacaktır.

**Bilmenizde fayda var:** Varsayılan Ortam Değişkenlerine benzer şekilde, `.env.test` dosyası deponuza dahil edilmelidir, ancak `.env.test.local` dosyası dahil edilmemelidir, çünkü `.env*.local` dosyasının `.gitignore` aracılığıyla göz ardı edilmesi amaçlanmıştır.

Birim testlerini çalıştırırken, `@next/env` paketindeki `loadEnvConfig` işlevinden yararlanarak ortam değişkenlerinizi Next.js'nin yaptığı gibi yüklediğinizden emin olabilirsiniz.

```js
// // Aşağıdakiler, test kurulumunuz için bir Jest global kurulum dosyasında veya benzerinde kullanılabilir
import { loadEnvConfig } from "@next/env";

export default async () => {
  const projectDir = process.cwd();
  loadEnvConfig(projectDir);
};
```

## Ortam Değişkeni Yük Sırası

Ortam değişkenleri sırasıyla aşağıdaki yerlerde aranır ve değişken bulunduğunda durdurulur.

1. `process.env`
2. `.env.$(NODE_ENV).local`
3. `.env.local` (`NODE_ENV` `test` olduğunda kontrol edilmez.)
4. `.env.$(NODE_ENV)`
5. `.env`

Örneğin, `NODE_ENV` `development` ise ve hem `.env.development.local` hem de `.env`'de bir değişken tanımlarsanız, `.env.development.local`'deki değer kullanılır.

**Bilmekte fayda var:** `NODE_ENV` için izin verilen değerler `development`, `production` ve `test`tir.

## Bilmekte fayda var

- Eğer bir `/src` dizini kullanıyorsanız, `.env.*` dosyaları projenizin kök dizininde kalmalıdır.
- `NODE_ENV` ortam değişkeni atanmamışsa Next.js, `next dev` komutunu çalıştırırken otomatik olarak `development` veya diğer tüm komutlar için `production` ataması yapar.

# Mutlak İçe Aktarmalar ve Modül Yolu Takma Adları (Absolute Imports and Module Path Aliases)

Next.js, `tsconfig.json` ve `jsconfig.json` dosyalarının `"paths"` ve `"baseUrl"` seçenekleri için yerleşik destek sunar.

Bu seçenekler, proje dizinlerini mutlak yollara takma ad olarak eklemenize olanak tanıyarak modülleri içe aktarmayı kolaylaştırır. Örneğin:

```ts
// önce
import { Button } from "../../../components/button";

// sonra
import { Button } from "@/components/button";
```

**bilmekte fayda var:** `create-next-app`, bu seçenekleri sizin için yapılandırmayı önerir.

## Mutlak İçe Aktarmalar (Absolute Imports)

`baseUrl` yapılandırma seçeneği, projenin kökünden doğrudan içe aktarmanıza olanak tanır.

Bu yapılandırmanın bir örneği:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": "."
  }
}
```

```typescript
// components/button.tsx;

export default function Button() {
  return <button>Click me</button>;
}
```

```js
// app / page.tsx;

import Button from "components/button";

export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  );
}
```

### Modül Takma Adları (Module Aliases)

`baseUrl` yolu yapılandırmasına ek olarak, `"paths"` seçeneğini kullanarak modül yollarını "alias" olarak kullanabilirsiniz.

Örneğin, aşağıdaki yapılandırma, `@/components/*`'ı `components/*`'a eşler:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/components/_": ["components/_"]
    }
  }
}
```

```ts
// components/button.tsx

export default function Button() {
  return <button>Click me</button>;
}
```

```ts
/// app/page.tsx

import Button from "@/components/button";

export default function HomePage() {
  return (
    <>
      <h1>Hello World</h1>
      <Button />
    </>
  );
}
```

`"paths"` her biri `baseUrl` konumuna görelidir. Örneğin:

```json
// tsconfig.json veya jsconfig.json

{
  "compilerOptions": {
    "baseUrl": "src/",
    "paths": {
      "@/styles/_": ["styles/_"],
      "@/components/_": ["components/_"]
    }
  }
}
```

```js
// pages/index.js

import Button from "@/components/button";
import "@/styles/styles.css";
import Helper from "utils/helper";

export default function HomePage() {
  return (
    <Helper>
      <h1>Hello World</h1>
      <Button />
    </Helper>
  );
}
```

# MDX

[Markdown](https://daringfireball.net/projects/markdown/syntax), metni biçimlendirmek için kullanılan hafif bir biçimlendirme dilidir. Düz metin sözdizimi kullanarak yazmanıza ve yapısal olarak geçerli HTML'ye dönüştürmenize olanak tanır. Genellikle web sitelerinde ve bloglarda içerik yazmak için kullanılır.

Siz aşağıdakini yazdığınızda...

```md
I **love** using [Next.js](https://nextjs.org/)
```

Çıktı:

```md
<p> <a href="https://nextjs.org/">Next.js</a></p> kullanmayı <strong>seviyorum</strong>
```

[MDX](https://mdxjs.com/), [JSX](https://react.dev/learn/writing-markup-with-jsx)'i doğrudan markdown dosyalarınıza yazmanıza olanak tanıyan bir markdown üst kümesidir. Dinamik etkileşim eklemenin ve içeriğinize React bileşenleri yerleştirmenin güçlü bir yoludur.

Next.js, hem uygulamanızın içindeki yerel MDX içeriğini hem de sunucudan dinamik olarak getirilen uzak MDX dosyalarını destekleyebilir. Next.js eklentisi, Sunucu Bileşenlerinde (`app`'de varsayılan) kullanım desteği de dahil olmak üzere Markdown ve React bileşenlerini HTML'ye dönüştürmeyi yönetir.

## `@next/mdx`

`@next/mdx` paketi, projelerinizin kök dizinindeki `next.config.js` dosyasında yapılandırılır. Yerel dosyalardan veri alır ve doğrudan `/pages` veya `/app` dizininizde `.mdx` uzantılı sayfalar oluşturmanıza olanak tanır.

## Başlarken

`@next/mdx` paketini yükleyin:

```bash
npm install @next/mdx @mdx-js/loader @mdx-js/react @types/mdx
```

Uygulamanızın kök dizininde (`app/` veya `src/` klasörünün üst dizini) `mdx-components.tsx` dosyasını oluşturun:

```tsx
///mdx-components.tsx

import type { MDXComponents } from "mdx/types";

// Bu dosya, MDX dosyalarında kullanılmak üzere
// özel React bileşenleri sağlamanıza olanak tanır.
// Diğer kütüphanelerdeki bileşenler de dahil olmak üzere
// istediğiniz herhangi bir react bileşenini
// içe aktarabilir ve kullanabilirsiniz.

// Bu dosya MDX'i `app` dizininde kullanmak için gereklidir.
export function useMDXComponents(components: MDXComponents): MDXComponents {
  return {
    // Yerleşik bileşenlerin özelleştirilmesine, örneğin stil eklenmesine izin verir.
    // h1: ({ children }) => <h1 style={{ fontSize: "100px" }}>{children}</h1>,
    ...components,
  };
}
```

`next.config.js` dosyasını `mdxRs` kullanacak şekilde güncelleyin:

```js
///next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    mdxRs: true,
  },
};

const withMDX = require("@next/mdx")();
module.exports = withMDX(nextConfig);
```

`app` dizininize MDX içerikli yeni bir dosya ekleyin:

```mdx
// app/hello.mdx

Merhaba, Next.js!

MDX dosyalarındaki React bileşenlerini içe aktarabilir ve kullanabilirsiniz.
```

İçeriği görüntülemek için `MDX` dosyasını bir `pages` içine aktarın:

```tsx
// app/page.tsx

import HelloWorld from "./hello.mdx";

export default function Page() {
  return <HelloWorld />;
}
```

## Uzaktan MDX (Remote MDX)

Markdown veya MDX dosyalarınız uygulamanızın içinde yaşamıyorsa, bunları sunucudan dinamik olarak getirebilirsiniz. Bu, bir CMS'den veya başka bir veri kaynağından içerik almak için kullanışlıdır.

MDX içeriğini almak için iki popüler topluluk paketi vardır: [`next-mdx-remote`](https://github.com/hashicorp/next-mdx-remote#react-server-components-rsc--nextjs-app-directory-support) ve [`contentlayer`](https://www.contentlayer.dev/). Örneğin, aşağıdaki örnek `next-mdx-remote` kullanmaktadır:

**Bilmekte fayda var:** Lütfen dikkatli olun. MDX, JavaScript olarak derlenir ve sunucuda yürütülür. MDX içeriğini yalnızca güvenilir bir kaynaktan almalısınız, aksi takdirde bu durum uzaktan kod yürütülmesine (RCE) yol açabilir.

```ts
// app/page.tsx

import { MDXRemote } from "next-mdx-remote/rsc";

export default async function Home() {
  const res = await fetch("https://...");
  const markdown = await res.text();
  return <MDXRemote source={markdown} />;
}
```

## Düzenlemeler (Layouts)

MDX içeriği etrafında bir düzen paylaşmak için Uygulama Yönlendiricisi ile [yerleşik düzen desteği](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#layouts)ni kullanabilirsiniz.

## Remark ve Rehype Eklentileri

MDX içeriğini dönüştürmek için isteğe bağlı olarak `remark` ve `rehype` eklentileri sağlayabilirsiniz. Örneğin, GitHub Flavored Markdown'ı desteklemek için `remark-gfm` kullanabilirsiniz.

`remark` ve `rehype` ekosistemi yalnızca ESM olduğundan, yapılandırma dosyası olarak `next.config.mjs` dosyasını kullanmanız gerekir.

```js
//next.config.mjs

import remarkGfm from "remark-gfm";
import createMDX from "@next/mdx";

/** @type {import('next').NextConfig} */
const nextConfig = {};

const withMDX = createMDX({
  options: {
    extension: /\.mdx?$/,
    remarkPlugins: [remarkGfm],
    rehypePlugins: [],
    // Eğer `MDXProvider` kullanıyorsanız, aşağıdaki satırı kaldırın.
    // providerImportSource: "@mdx-js/react",
  },
});
export default withMDX(nextConfig);
```

## Frontmatter

Frontmatter, bir sayfa hakkındaki verileri depolamak için kullanılabilen YAML benzeri bir anahtar/değer eşleştirmesidir. Öntanımlı olarak `@next/mdx` frontmatter'ı desteklemez, ancak MDX içeriğinize frontmatter eklemek için [gray-matter](https://github.com/jonschlinkert/gray-matter) gibi birçok çözüm vardır.

Sayfa meta verilerine `@next/mdx` ile erişmek için `.mdx` dosyası içinden bir meta nesnesini dışa aktarabilirsiniz:

```mdx
export const meta = {
  author: 'Rich Haines',
}
 
# My MDX pag

e
```

## Özel Unsurlar

Markdown kullanmanın hoş yönlerinden biri, yerel `HTML` öğeleriyle eşleşerek yazmayı hızlı ve sezgisel hale getirmesidir:

```md
Bu markdown'da bir listedir:

- Bir
- İki
- Üç
```

Yukarıdaki işlem aşağıdaki `HTML`'yi oluşturur:

```html
<p>Bu markdown'da bir listedir:</p>

<ul>
  <li>Bir</li>
  <li>İki</li>
  <li>Üç</li>
</ul>
```

Web sitenize veya uygulamanıza özel bir his vermek için kendi öğelerinizi şekillendirmek istediğinizde, kısa kodları aktarabilirsiniz. Bunlar, `HTML` öğelerine eşlenen kendi özel bileşenlerinizdir. Bunu yapmak için `MDXProvider`'ı kullanır ve bir components nesnesini prop olarak geçirirsiniz. Components nesnesindeki her nesne anahtarı bir `HTML` öğesi adıyla eşleşir.

Etkinleştirmek için `next.config.js` içinde `providerImportSource: "@mdx-js/react"` belirtmeniz gerekir:

```js
//next.config.js

const withMDX = require("@next/mdx")({
  // ...
  options: {
    providerImportSource: "@mdx-js/react",
  },
});
```

Ardından sağlayıcıyı sayfanızda ayarlayın

```js
//pages/index.js

import { MDXProvider } from "@mdx-js/react";
import Image from "next/image";
import { Heading, InlineCode, Pre, Table, Text } from "my-components";

const ResponsiveImage = (props) => (
  <Görüntü
    alt={props.alt}
    sizes="100vw"
    style={{ width: "100%", height: "auto" }}
    {...props}
  />
);

const bileşenler = {
  img: ResponsiveImage,
  h1: Heading.H1,
  h2: Heading.H2,
  p: Metin,
  Öncesi: Öncesi,
  kod: InlineCode,
};

export default function Post(props) {
  dönüş(
    <MDXProvider components={components}>
      <main {...props} />
    </MDXProvider>
  );
}
```

Site genelinde kullanıyorsanız, sağlayıcıyı `_app.js`'ye eklemek isteyebilirsiniz, böylece tüm MDX sayfaları özel öğe yapılandırmasını alır.

## Derin Anlatım: Markdown'ı HTML'e nasıl dönüştürürsünüz?

React, Markdown'ı yerel olarak anlamaz. Markdown düz metninin önce HTML'ye dönüştürülmesi gerekir. Bu, `remark` ve `rehype` ile gerçekleştirilebilir.

`remark`, markdown etrafında bir araç ekosistemidir. `rehype` da aynıdır, ancak HTML içindir. Örneğin, aşağıdaki kod parçacığı markdown'u HTML'ye dönüştürür:

```js
import { unified } from "unified";
import remarkParse from "remark-parse";
import remarkRehype from "remark-rehype";
import rehypeSanitize from "rehype-sanitize";
import rehypeStringify from "rehype-stringify";

main();

async function main() {
  const file = await unified()
    .use(remarkParse) // Markdown AST'ye dönüştürme
    .use(remarkRehype) // HTML AST'ye Dönüştürme
    .use(rehypeSanitize) // HTML girdisini sterilize edin
    .use(rehypeStringify) // AST'yi serileştirilmiş HTML'ye dönüştürme
    .process("Hello, Next.js!");

  console.log(String(file)); // <p>Hello, Next.js!</p>
}
```

`remark` ve `rehype` ekosistemi, [sözdizimi vurgulama](https://github.com/atomiks/rehype-pretty-code), [başlıkları bağlama](https://github.com/rehypejs/rehype-autolink-headings), [içindekiler tablosu oluşturma](https://github.com/remarkjs/remark-toc) ve daha fazlası için eklentiler içerir.

Aşağıda gösterildiği gibi `@next/mdx` kullanırken, sizin için halledildiğinden doğrudan `remark` ve `rehype` kullanmanıza gerek yoktur.

## Rust tabanlı MDX derleyicisini kullanma (Deneysel)

Next.js, Rust dilinde yazılmış yeni bir MDX derleyicisini desteklemektedir. Bu derleyici hala deneyseldir ve üretim kullanımı için önerilmez. Yeni derleyiciyi kullanmak için `next.config.js` dosyasını `withMDX`'e aktarırken yapılandırmanız gerekir:

```js
// next.config.js
module.exports = withMDX({
  experimental: {
    mdxRs: true,
  },
});
```

## Yararlı Bağlantılar

- [MDX](https://mdxjs.com/)
- [`@next/mdx`](https://www.npmjs.com/package/@next/mdx)
- [remark](https://github.com/remarkjs/remark)
- [rehype](https://github.com/rehypejs/rehype)

# src Dizini

Projenizin kök dizininde özel Next.js `app` veya `pages` dizinlerine sahip olmaya alternatif olarak Next.js, uygulama kodunu `src` dizininin altına yerleştirmenin yaygın modelini de destekler.

Bu, uygulama kodunu, bazı bireyler ve ekipler tarafından tercih edilen, çoğunlukla bir projenin kök dizininde bulunan proje yapılandırma dosyalarından ayırır.

`src` dizinini kullanmak için, `app` Router klasörünü veya `pages` Router klasörünü sırasıyla `src/app` veya `src/pages` dizinine taşıyın.

<img alt="src-dizini" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-src-directory.png&w=1920&q=75&dpl=dpl_FgqPZgpvfTdBpYwq43qhnaRUcyXh"/>
<br>

**Bilmekte Fayda Var:**

- `/public` dizini projenizin kök dizininde kalmalıdır.
- `package.json`, `next.config.js` ve `tsconfig.json` gibi yapılandırma dosyaları projenizin kök dizininde kalmalıdır.
- `.env.*` dosyaları projenizin kök dizininde kalmalıdır.
- Kök dizinde `app` veya `pages` varsa `src/app` veya `src/pages` göz ardı edilecektir.
- Eğer `src` kullanıyorsanız, muhtemelen `/components` veya `/lib` gibi diğer uygulama klasörlerini de taşıyacaksınız.
- Tailwind CSS kullanıyorsanız, [içerik bölümündeki](https://tailwindcss.com/docs/content-configuration) `tailwind.config.js` dosyasına `/src` önekini eklemeniz gerekir.

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
