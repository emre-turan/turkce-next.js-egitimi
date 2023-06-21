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
