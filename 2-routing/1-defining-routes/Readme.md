# Rotaların Tanımlanması

Devam etmeden önce [Yönlendirme Temelleri](#yönlendirme-temelleri-routing-fundamentals) bölümünün okunması önerilir.

Bu bölüm, Next.js uygulamanızda rotaları nasıl tanımlayacağınız ve düzenleyeceğiniz konusunda size rehberlik edecektir.

## Rotalar Oluşturma

Next.js, rotaları tanımlamak için **klasörlerin** kullanıldığı dosya sistemi tabanlı bir yönlendirici kullanır.

Her klasör, bir **URL** segmentiyle eşleşen bir [rota segmentini](#rota-segmentleri) temsil eder. [İç içe bir rota](#i̇ç-i̇çe-rotalar) oluşturmak için, klasörleri birbirinin içine yerleştirebilirsiniz.

<img alt="rotalar oluşturma" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Froute-segments-to-path-segments.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Rota segmentlerini genel erişime açmak için özel bir [`page.js` dosyası](#sayfalar) kullanılır.

<img alt="rotalar oluşturma-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fdefining-routes.png&w=3840&q=75&dpl=dpl_C2pSAYXZnY6DPcYmVfUv54azW3BJ" /><br/>

Bu örnekte, `/dashboard/analytics` URL yolu, karşılık gelen bir `page.js` dosyasına sahip olmadığı için _genel erişime_ açık değildir. Bu klasör bileşenleri, stil sayfalarını, görüntüleri veya diğer ortak dosyaları depolamak için kullanılabilir.

## Kullanıcı Arayüzü Oluşturma

Her bir rota segmenti için kullanıcı arayüzü oluşturmak üzere [özel dosya kuralları](#dosya-kuralları) kullanılır. En yaygın olanları, bir rotaya özgü kullanıcı arayüzünü gösteren [sayfalar](#sayfalar) ve birden fazla rotada paylaşılan kullanıcı arayüzünü gösteren [düzenlerdir](#düzenler).

Örneğin, ilk sayfanızı oluşturmak için `app` dizininin içine bir `page.js` dosyası ekleyin ve bir React bileşenini dışa aktarın:

```tsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
```
