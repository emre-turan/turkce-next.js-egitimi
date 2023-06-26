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
