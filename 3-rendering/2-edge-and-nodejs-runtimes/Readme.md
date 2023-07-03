# Edge ve Node.js Çalışma Zamanları (Edge and Node.js Runtimes)

Next.js bağlamında "çalışma zamanı", yürütme sırasında kodunuz tarafından kullanılabilen kütüphaneler, API'ler ve genel işlevsellik kümesini ifade eder.

Next.js, uygulama kodunuzun bazı bölümlerini oluşturabileceğiniz iki sunucu çalışma zamanına sahiptir:

- Node.js Çalışma Zamanı
- Edge Çalışma Zamanı
- Her çalışma zamanının kendi API'leri vardır. Mevcut API'lerin tam listesi için lütfen [Node.js Docs](https://nodejs.org/docs/latest/api/) ve [Edge Docs](https://nextjs.org/docs/app/api-reference/edge)'a bakın. Her iki çalışma zamanı da dağıtım altyapınıza bağlı olarak akışı destekleyebilir.

Varsayılan olarak, `app` dizini Node.js çalışma zamanını kullanır. Ancak, rota bazında farklı çalışma zamanlarını (örn. Edge) seçebilirsiniz.

## Çalışma Zamanı Farklılıkları

Bir çalışma zamanı seçerken dikkat edilmesi gereken birçok husus vardır. Bu tablo bir bakışta önemli farklılıkları göstermektedir. Farklılıkların daha derinlemesine bir analizini istiyorsanız, aşağıdaki bölümlere göz atın.
| | Node | Serverless | Edge |
|---------|----------------|------------|----------|
| Cold Boot | / | ~250ms | Anında |
| HTTP Streaming | Evet | Evet | Evet |
| IO | Hepsi | Hepsi | `fetch` |
| Scalability | / | Yüksek | En Yüksek |
| Security | Normal | Yüksek | Yüksek |
| Latency | Normal | Düşük | En Düşük |
| npm Packages | Hepsi | Hepsi | Daha küçük bir alt küme |

## Edge Çalışma Zamanı

Next.js'de hafif Edge Runtime, mevcut Node.js API'lerinin bir alt kümesidir.

Küçük, basit işlevlerle düşük gecikme süresinde dinamik, kişiselleştirilmiş içerik sunmanız gerekiyorsa Edge Runtime idealdir. Edge Runtime'ın hızı minimum kaynak kullanımından gelir, ancak bu birçok senaryoda sınırlayıcı olabilir.

Örneğin, Vercel'de Edge Runtime'da yürütülen kod [1 MB ile 4 MB arasını geçemez](https://vercel.com/docs/concepts/limits/overview#edge-middleware-and-edge-functions-size), bu sınır içe aktarılan paketleri, yazı tiplerini ve dosyaları içerir ve dağıtım altyapınıza bağlı olarak değişir.

##  Node.js Çalışma Zamanı

Node.js çalışma zamanını kullanmak, tüm Node.js API'lerine ve bunlara dayanan tüm npm paketlerine erişmenizi sağlar. Ancak, başlatılması Edge çalışma zamanını kullanan rotalar kadar hızlı değildir.

Next.js uygulamanızı bir Node.js sunucusuna dağıtmak, altyapınızı yönetmeyi, ölçeklendirmeyi ve yapılandırmayı gerektirecektir. Alternatif olarak, Next.js uygulamanızı Vercel gibi sunucusuz bir platforma dağıtmayı düşünebilirsiniz; bu platform bunu sizin için halledecektir.

## Sunucusuz Node.js

Edge Runtime'dan daha karmaşık hesaplama yüklerini kaldırabilecek ölçeklenebilir bir çözüme ihtiyacınız varsa Sunucusuz idealdir. Örneğin Vercel'deki Sunucusuz İşlevler ile içe aktarılan paketler, yazı tipleri ve dosyalar dahil olmak üzere toplam kod boyutunuz [50 MB](https://vercel.com/docs/concepts/limits/overview#serverless-function-size)'tır.

Edge kullanan rotalara kıyasla dezavantajı, Sunucusuz İşlevlerin istekleri işlemeye başlamadan önce önyükleme yapmasının yüzlerce milisaniye sürebilmesidir. Sitenizin aldığı trafik miktarına bağlı olarak, işlevler sık sık "ısınmadığı" için bu sık karşılaşılan bir durum olabilir.

## Örnekler

### Segment Çalışma Zamanı Seçeneği

Next.js uygulamanızda tek tek rota segmentleri için bir çalışma zamanı belirleyebilirsiniz. Bunu yapmak için, runtime adında bir değişken tanımlayın ve dışa aktarın. Değişken bir dize olmalı ve `'nodejs'` ya da `'edge'` runtime değerine sahip olmalıdır.

Aşağıdaki örnekte, `'edge'` değerine sahip bir çalışma zamanını dışa aktaran bir sayfa rotası segmenti gösterilmektedir:

```ts
export const runtime = "edge"; // 'nodejs' (varsayılan) | 'edge'
```

Segment çalışma zamanı ayarlanmazsa, varsayılan `nodejs` çalışma zamanı kullanılacaktır. Node.js çalışma zamanından değiştirmeyi planlamıyorsanız çalışma zamanı seçeneğini kullanmanıza gerek yoktur.
