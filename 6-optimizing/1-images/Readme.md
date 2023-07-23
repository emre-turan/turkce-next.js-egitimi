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
