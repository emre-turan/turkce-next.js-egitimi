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
