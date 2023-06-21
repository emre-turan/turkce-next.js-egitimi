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
