# Bağlama ve Gezinme (Linking and Navigating)

Next.js yönlendiricisi, istemci tarafında gezinme ile sunucu merkezli yönlendirme kullanır. Anlık yükleme durumlarını ve eş zamanlı görüntülemeyi destekler.

Rotalar arasında gezinmenin iki yolu vardır:

- `<Link>` Bileşeni
- `useRouter` Kancası

## `<Link>` Bileşeni

`<Link>`, rotalar arasında ön getirme ve istemci tarafında gezinme sağlamak için HTML `<a>` öğesini genişleten bir React bileşenidir. Next.js'de rotalar arasında gezinmenin birincil yoludur.

`<Link>`'i kullanmak için next/link'ten içe aktarın ve bileşene bir href prop iletin:

```tsx
import Link from "next/link";

export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>;
}
```

## Örnekler

### Dinamik Segmentlere Bağlantı

Dinamik segmentlere bağlantı verirken, bir bağlantı listesi oluşturmak için [şablon değişmezlerini ve enterpolasyonu](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) kullanabilirsiniz. Örneğin, blog gönderilerinin bir listesini oluşturmak için:

```tsx
import Link from "next/link";

export default function PostList({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${post.slug}`}>{post.title}</Link>
        </li>
      ))}
    </ul>
  );
}
```

### Aktif Bağlantıları Kontrol Etme

Bir bağlantının etkin olup olmadığını belirlemek için `usePathname()` işlevini kullanabilirsiniz. Örneğin, etkin bağlantıya bir sınıf eklemek için, geçerli yol adının bağlantının `href`'iyle eşleşip eşleşmediğini kontrol edebilirsiniz:

```tsx
"use client";

import { usePathname } from "next/navigation";
import { Link } from "next/link";

export function Navigation({ navLinks }) {
  const pathname = usePathname();

  return (
    <>
      {navLinks.map((link) => {
        const isActive = pathname.startsWith(link.href);

        return (
          <Link
            className={isActive ? "text-blue" : "text-black"}
            href={link.href}
            key={link.name}
          >
            {link.name}
          </Link>
        );
      })}
    </>
  );
}
```

### Bir kimliğe kaydırma (Scrolling to an `id`)

`<Link>`'in varsayılan davranışı, değişen rota segmentinin en üstüne kaydırmaktır. `href` içinde tanımlanmış bir `id` olduğunda, normal bir `<a>` etiketine benzer şekilde belirli id'ye kaydırılır.

Rota segmentinin en üstüne kaydırmayı önlemek için `scroll={false}` olarak ayarlayın ve `href` öğesine karma bir `id` ekleyin:

```tsx
<Link href="/#hashid" scroll={false}>
  Scroll to specific id.
</Link>
```

## `useRouter()` Hook

`useRouter` kancası, İstemci Bileşenleri içindeki rotaları programlı olarak değiştirmenize olanak tanır.

`useRouter`'ı kullanmak için `next/navigation`'dan içe aktarın ve İstemci Bileşeninizin içindeki kancayı çağırın:

```tsx
"use client";

import { useRouter } from "next/navigation";

export default function Page() {
  const router = useRouter();

  return (
    <button type="button" onClick={() => router.push("/dashboard")}>
      Dashboard
    </button>
  );
}
```

Öneri: `useRouter` kullanmak için özel bir gereksiniminiz olmadığı sürece rotalar arasında gezinmek için `<Link>` bileşenini kullanın.

## Navigasyon Nasıl Çalışır?

- `<Link>`kullanılarak veya `router.push()` çağrısı yapılarak bir rota geçişi başlatılır.
- Yönlendirici, tarayıcının adres çubuğundaki URL'yi günceller.
- Yönlendirici, istemci tarafı önbelleğindeki değişmeyen bölümleri (ör. paylaşılan düzenler) yeniden kullanarak gereksiz çalışmayı önler. Bu aynı zamanda kısmi işleme olarak da adlandırılır.
- Yumuşak gezinme koşulları karşılanırsa, yönlendirici yeni segmenti sunucu yerine önbellekten alır. Değilse, yönlendirici sert bir gezinme gerçekleştirir ve Sunucu Bileşeni yükünü sunucudan alır.
- Oluşturulursa, yük getirilirken sunucudan yükleme kullanıcı arayüzü gösterilir.
- Yönlendirici, yeni segmentleri istemcide işlemek için önbelleğe alınan veya yeni yükü kullanır.

### Oluşturulan Sunucu Bileşenlerinin İstemci Tarafında Önbelleğe Alınması

Yeni yönlendirici, Sunucu Bileşenlerinin (yük) işlenmiş sonucunu depolayan bir bellek içi istemci tarafı önbelleğine sahiptir. Önbellek, herhangi bir düzeyde geçersiz kılmaya izin veren ve eşzamanlı render işlemlerinde tutarlılık sağlayan rota segmentlerine bölünmüştür.

Kullanıcılar uygulamada gezinirken, yönlendirici daha önce getirilen segmentlerin ve önceden getirilen segmentlerin yükünü önbellekte depolayacaktır.

Bu, belirli durumlarda yönlendiricinin sunucuya yeni bir istekte bulunmak yerine önbelleği yeniden kullanabileceği anlamına gelir. Bu, verilerin yeniden alınmasını ve bileşenlerin gereksiz yere yeniden oluşturulmasını önleyerek performansı artırır.

### Önbelleğin Geçersiz Kılınması

Sunucu Eylemleri, verileri yola (`revalidatePath`) veya önbellek etiketine (`revalidateTag`) göre isteğe bağlı olarak yeniden doğrulamak için kullanılabilir.

### Prefetching

Prefetching, bir rotayı ziyaret edilmeden önce arka planda önceden yüklemenin bir yoludur. Önceden yüklenen rotaların işlenmiş sonucu yönlendiricinin istemci tarafı önbelleğine eklenir. Bu, önceden yüklenmiş bir rotaya gitmeyi neredeyse anlık hale getirir.

Varsayılan olarak, bileşeni kullanırken görünüm alanında görünür hale geldiklerinde rotalar önceden taranır. Bu, sayfa ilk yüklendiğinde veya kaydırma yoluyla gerçekleşebilir. Rotalar, `useRouter()` kancasının prefetch yöntemi kullanılarak programlı olarak da önceden alınabilir.

#### Statik ve Dinamik Rotalar:

- Rota statikse, rota segmentleri için tüm Sunucu Bileşeni yükleri önceden taranacaktır.
- Rota dinamikse, ilk paylaşılan düzenden ilk `loading.js` dosyasına kadar olan yük önceden taranır. Bu, tüm rotayı dinamik olarak önceden getirmenin maliyetini azaltır ve dinamik rotalar için anlık yükleme durumlarına izin verir.

### Yumuşak Navigasyon (Soft Navigation)

Gezinme sırasında, değiştirilen segmentler için önbellek yeniden kullanılır (varsa) ve veri için sunucuya yeni bir istek yapılmaz.

#### Yumuşak Navigasyon için Koşullar

Navigasyonda Next.js, navigasyon yaptığınız rota önceden taranmışsa ve dinamik segmentler içermiyorsa ya da mevcut rota ile aynı dinamik parametrelere sahipse yumuşak navigasyon kullanacaktır.

Örneğin, dinamik bir `[team]` segmenti içeren aşağıdaki rotayı düşünün: `/dashboard/[team]/*`. `dashboard/[team]/*` altındaki önbelleğe alınmış segmentler yalnızca `[team]` parametresi değiştiğinde geçersiz kılınacaktır.

- `/dashboard/team-red/*` adresinden `/dashboard/team-red/*` adresine gitmek yumuşak bir navigasyon olacaktır.
- `/dashboard/team-red/*` adresinden `/dashboard/team-blue/*` adresine gitmek zor bir navigasyon olacaktır.

### Sert Navigasyon (Hard Navigation)

Gezinme sırasında önbellek geçersiz kılınır ve sunucu verileri yeniden alır ve değiştirilen segmentleri yeniden işler.

### Geri/İleri Navigasyon

Geri ve ileri gezinme (popstate olayı) yumuşak bir gezinme davranışına sahiptir. Bu, istemci tarafı önbelleğinin yeniden kullanıldığı ve gezinmenin neredeyse anlık olduğu anlamına gelir.

### Odaklanma ve Kaydırma Yönetimi

Varsayılan olarak, Next.js odağı ayarlar ve gezinme sırasında değiştirilen segmenti görünüme kaydırır.