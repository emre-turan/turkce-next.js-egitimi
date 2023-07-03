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

