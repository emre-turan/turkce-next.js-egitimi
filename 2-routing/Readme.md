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
