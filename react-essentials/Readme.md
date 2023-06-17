# React Temelleri

Next.js ile uygulama geliştirmek için React'in Sunucu Bileşenleri gibi yeni özelliklerine aşina olmak bize yardımcı olacaktır. Bu bölümde, Sunucu ve İstemci Bileşenleri arasındaki farkları, ne zaman kullanılacaklarını ve önerilen kalıpları inceleyeceğiz.

## Sunucu (Server) Bileşenleri

Sunucu (Server) ve İstemci (Client) Bileşenleri, geliştiricilerin sunucu ve istemciyi kapsayan uygulamalar oluşturmasına olanak tanıyarak istemci tarafı uygulamaların zengin etkileşimini geleneksel sunucu görüntülemenin gelişmiş performansıyla birleştirir.

## Sunucu Bileşenleri ile Düşünme

React'in kullanıcı arayüzü oluşturma konusundaki düşüncelerimizi değiştirmesine benzer şekilde, React Sunucu Bileşenleri de sunucu ve istemciden yararlanan hibrit uygulamalar oluşturmak için yeni bir zihinsel model sunuyor.

React, tüm uygulamanızı istemci tarafında işlemek yerine (Tek Sayfalı Uygulamalarda olduğu gibi), artık size bileşenlerinizi amaçlarına göre nerede işleyeceğinizi seçme esnekliği sunuyor.

<img alt="sunucu bileşenleri" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fthinking-in-server-components.png&w=3840&q=75&dpl=dpl_sqd2P3Qu1LJeq8Pn8V3cFynj578V" /><br/>

Sayfayı daha küçük bileşenlere ayıracak olursak, bileşenlerin çoğunun etkileşimli olmadığını ve sunucuda Sunucu Bileşenleri olarak işlenebileceğini fark edeceksiniz. Daha küçük etkileşimli kullanıcı arayüzü parçaları için İstemci Bileşenlerini serpiştirebiliriz. Bu, Next.js'nin **sunucu öncelikli** yaklaşımıyla uyumludur.

## Neden Sunucu Bileşenleri?

Peki, neden Sunucu Bileşenleri diye düşünüyor olabilirsiniz. İstemci Bileşenleri yerine bunları kullanmanın avantajları nelerdir?

Sunucu Bileşenleri, geliştiricilerin sunucu altyapısından daha iyi yararlanmasını sağlar. Örneğin, veri getirmeyi sunucuya, veritabanınıza daha yakın bir yere taşıyabilir ve daha önce istemci JavaScript paketinin boyutunu etkileyecek büyük bağımlılıkları sunucuda tutarak performansı artırabilirsiniz. Sunucu Bileşenleri, bir React uygulaması yazmayı PHP veya Ruby on Rails'e benzer hale getirir, ancak bunu React'in gücü ve esnekliği ve kullanıcı arayüzünü şablonlamak için bileşenler modeli ile yapar.

Sunucu Bileşenleri ile ilk sayfa yüklemesi daha hızlıdır ve istemci tarafı JavaScript paketinin boyutu küçülür. Temel istemci tarafı çalışma zamanı önbelleğe alınabilir ve tahmin edilebilir boyuttadır ve uygulamanız büyüdükçe artmaz. Ek JavaScript yalnızca uygulamanızda İstemci Bileşenleri aracılığıyla istemci tarafı etkileşimi kullanıldıkça eklenir.

Next.js ile bir rota yüklendiğinde, ilk HTML sunucuda oluşturulur. Bu HTML daha sonra tarayıcıda aşamalı olarak geliştirilir ve istemcinin Next.js ve React istemci tarafı çalışma zamanını eşzamansız olarak yükleyerek uygulamayı devralmasına ve etkileşim eklemesine olanak tanır.

Sunucu Bileşenlerine geçişi kolaylaştırmak için, özel dosyalar ve ortak konumlandırılmış bileşenler de dahil olmak üzere, Uygulama Yönlendiricisi içindeki tüm bileşenler varsayılan olarak Sunucu Bileşenleridir. Bu, ekstra bir çalışma yapmadan bunları otomatik olarak benimsemenize ve hali hazırda mükemmel bir performans elde etmenize olanak tanır. İsteğe bağlı olarak 'use client' yönergesini kullanarak İstemci Bileşenleri de tercih edebilirsiniz.

## İstemci Bileşenleri

İstemci Bileşenleri, uygulamanıza istemci tarafı etkileşim eklemenizi sağlar. Next.js'te, bunlar sunucuda önceden oluşturulur (Pre-Render) ve istemci tarafında canlandırılır (hydration). İstemci Bileşenlerini, Sayfalar Yönlendiricisindeki bileşenlerin her zaman çalıştığı şekilde olduğunu düşünebilirsiniz.

### "use client" yönergesi

`"use client"` yönergesi, Sunucu ve İstemci Bileşen modül grafiği arasında bir sınır bildirmek için kullanılan bir kuraldır.

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

Uygulamanızın performansını artırmak için, İstemci Bileşenlerini mümkün olduğunca bileşen ağacınızın yapraklarına taşımanız önerilir.

Örneğin, statik öğelere sahip bir Yerleşim (Layout) (ör. logo, linkler, vb.) ve durum kullanabilen etkileşimli bir arama çubuğunuz olabilir.

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

1. **Sunucuda React**, sonucu istemciye göndermeden önce tüm Sunucu Bileşenlerini işler.

- Buna İstemci Bileşenleri içinde yer alan Sunucu Bileşenleri de dahildir.
- Bu aşamada karşılaşılan İstemci Bileşenleri atlanır.

2. **İstemcide**, React İstemci Bileşenlerini işler ve Sunucu Bileşenlerinin işlenmiş sonucundaki yuvaları, sunucuda ve istemcide yapılan işi birleştirir.

- Herhangi bir Sunucu Bileşeni bir İstemci Bileşeninin içine yerleştirilmişse, işlenen içerikler İstemci Bileşeninin içine doğru şekilde yerleştirilecektir.

Bilmekte fayda var:

Next.js'de, ilk sayfa yüklemesi sırasında, hem yukarıdaki adımdaki Sunucu Bileşenlerinin işlenmiş sonucu hem de İstemci Bileşenleri, daha hızlı bir ilk sayfa yüklemesi üretmek için sunucuda HTML olarak önceden işlenir.

## Sunucu Bileşenlerini İstemci Bileşenlerinin İçine Yerleştirme

Yukarıda özetlenen işleme akışı göz önüne alındığında, bir Sunucu Bileşeninin bir İstemci Bileşenine aktarılmasıyla ilgili bir kısıtlama vardır, çünkü bu yaklaşım ek bir sunucu gidiş gelişi gerektirecektir.

### Desteklenmeyen Model: Sunucu Bileşenlerini İstemci Bileşenlerinin İçine Aktarma

Aşağıdaki model desteklenmez. Bir Sunucu Bileşenini bir İstemci Bileşeninin içine aktaramazsınız:

```typescript
"use client";

// Bu düzen çalışmaz!!!!
// Bir Sunucu Bileşenini bir İstemci Bileşeninin içine aktaramazsınız.
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
// Bu düzen çalışır!!!!:
// Bir Sunucu Bileşenini, bir İstemci Bileşeninin alt öğesi veya prop'u olarak iletebilirsiniz.
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

1. Bu model, `children` prop ile [düzenlerde ve sayfalarda](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) zaten uygulanmaktadır, bu nedenle ek bir sarmalayıcı bileşen oluşturmanız gerekmez.
2. React bileşenlerini (JSX) diğer bileşenlere aktarmak yeni bir kavram değildir ve her zaman React kompozisyon modelinin bir parçası olmuştur.
3. Bu kompozisyon stratejisi, Sunucu ve İstemci Bileşenleri arasında çalışır çünkü prop'u alan bileşenin prop'un ne olduğu hakkında hiçbir bilgisi yoktur. Yalnızca kendisine aktarılan şeyin nereye yerleştirilmesi gerektiğinden sorumludur.

- Bu da aktarılan prop'un bağımsız olarak, bu durumda sunucuda, İstemci Bileşeni istemcide render edilmeden çok önce render edilmesini sağlar.
- Aynı "içeriği yukarı kaldırma" stratejisi, içe aktarılan iç içe geçmiş bir alt bileşeni yeniden işleyen bir üst bileşendeki durum değişikliklerini önlemek için kullanılmıştır.

4. Sadece `children` prop ile sınırlı değilsiniz. JSX iletmek için herhangi bir prop kullanabilirsiniz.

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

### "server-only" paketi

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
