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
