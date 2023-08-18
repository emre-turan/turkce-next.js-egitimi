# Dağıtım (Deploying)

Tebrikler! Next.js uygulamanızı dağıtmaya hazır olduğunuz için buradasınız. Bu sayfa, Next.js Build API'sini kullanarak yönetilen veya kendi kendine barındırılan dağıtımın nasıl yapılacağını gösterecektir.

## Next.js Yapı API'si

`next build`, uygulamanızın üretim için optimize edilmiş bir sürümünü oluşturur. Bu standart çıktı şunları içerir:

- `getStaticProps` veya Otomatik Statik Optimizasyon kullanan sayfalar için HTML dosyaları
- Genel stiller veya ayrı ayrı kapsamlandırılmış stiller için CSS dosyaları
- Next.js sunucusundan dinamik içeriği önceden render etmek için JavaScript
- React aracılığıyla istemci tarafında etkileşim için JavaScript

Bu çıktı `.next` klasörünün içinde oluşturulur:

- `.next/static/chunks/pages` - Bu klasördeki her JavaScript dosyası aynı isimli rota ile ilgilidir. Örneğin, `.next/static/chunks/pages/about.js`, uygulamanızda `/about` rotası görüntülendiğinde yüklenen JavaScript dosyası olacaktır
- `.next/static/media` - `next/image` adresinden statik olarak içe aktarılan görüntüler hashlenir ve buraya kopyalanır
- `.next/static/css` - Uygulamanızdaki tüm sayfalar için global CSS dosyaları
- `.next/server/pages` - Sunucudan önceden işlenen HTML ve JavaScript giriş noktaları. `.nft.json` dosyaları, Çıktı Dosyası İzleme etkinleştirildiğinde oluşturulur ve belirli bir sayfaya bağlı olan tüm dosya yollarını içerir.
- `.next/server/chunks` - Uygulamanızda birden fazla yerde kullanılan paylaşılan JavaScript parçaları
- `.next/cache` - Next.js sunucusundan derleme önbelleği ve önbelleğe alınmış görüntüler, yanıtlar ve sayfalar için çıktı. Önbellek kullanmak, derleme sürelerini azaltmaya ve görüntü yükleme performansını artırmaya yardımcı olur

`.next` içindeki tüm JavaScript kodu derlenmiş ve tarayıcı paketleri en iyi performansı elde etmeye ve tüm modern tarayıcıları desteklemeye yardımcı olmak için küçültülmüştür.

## Vercel ile Yönetilen Next.js

[Vercel](https://vercel.com/?utm_source=next-site&utm_medium=docs&utm_campaign=next-website), Next.js uygulamanızı sıfır yapılandırma ile dağıtmanın en hızlı yoludur.

Vercel'e dağıtım yaparken, platform [Next.js'yi otomatik olarak algılar](https://vercel.com/solutions/nextjs?utm_source=next-site&utm_medium=docs&utm_campaign=next-website), `next build` çalıştırır ve derleme çıktısını sizin için optimize eder:

- Değişmemişse önbelleğe alınan varlıkların dağıtımlar arasında sürdürülmesi
- Her işlem için benzersiz bir URL ile [değişmez dağıtımlar](https://vercel.com/features/previews?utm_source=next-site&utm_medium=docs&utm_campaign=next-website)
- [Sayfalar](https://nextjs.org/docs/pages/building-your-application/rendering/automatic-static-optimization) mümkünse otomatik olarak statik olarak optimize edilir
- Varlıklar (JavaScript, CSS, görüntüler, yazı tipleri) sıkıştırılır ve bir [Global Edge Ağından](https://vercel.com/features/infrastructure?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) sunulur
- API Rotaları otomatik olarak sonsuz ölçeklendirilebilen yalıtılmış [Sunucusuz İşlevler](https://vercel.com/features/infrastructure?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) olarak optimize edilir
- Middleware, sıfır soğuk başlatma ve anında önyükleme yapan Edge İşlevleri olarak otomatik olarak optimize edilir

Buna ek olarak, Vercel aşağıdaki gibi özellikler sağlar:

- [Next.js Speed Insights](https://vercel.com/analytics?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) ile otomatik performans izleme
- Otomatik HTTPS ve SSL sertifikaları
- Otomatik CI/CD (GitHub, GitLab, Bitbucket vb. aracılığıyla)
- [Ortam Değişkenleri](https://vercel.com/docs/environment-variables?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) için Destek
- [Özel Domainler](https://vercel.com/docs/custom-domains?utm_source=next-site&utm_medium=docs&utm_campaign=next-website) için Destek
- `next/image` ile Görüntü Optimizasyonu Desteği
- `git push` aracılığıyla anında küresel dağıtımlar

Denemek için bir Next.js uygulamasını [Vercel'e ücretsiz olarak dağıtın](https://vercel.com/new/git/external?repository-url=https://github.com/vercel/next.js/tree/canary/examples/hello-world&project-name=hello-world&repository-name=hello-world&utm_source=next-site&utm_medium=docs&utm_campaign=next-website).
