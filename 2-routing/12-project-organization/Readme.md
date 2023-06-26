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
