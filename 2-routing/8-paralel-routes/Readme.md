# Paralel Rotalar (Parallel Routes)

Paralel Yönlendirme, bir veya daha fazla sayfayı aynı düzende eşzamanlı veya koşullu olarak render etmenize olanak tanır. Bir uygulamanın gösterge tabloları ve sosyal sitelerdeki beslemeler gibi son derece dinamik bölümleri için Paralel Yönlendirme, karmaşık yönlendirme modellerini uygulamak için kullanılabilir.

Örneğin, ekip ve analiz sayfalarını aynı anda oluşturabilirsiniz.

<img alt="paralel-rotalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Paralel Yönlendirme, her bir rota için bağımsız hata ve yükleme durumları tanımlamanıza olanak tanır.

<img alt="paralel-rotalar-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-cinematic-universe.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Paralel Yönlendirme, kimlik doğrulama durumu gibi belirli koşullara bağlı olarak bir yuvayı koşullu olarak render etmenize da olanak tanır. Bu, aynı URL üzerinde tamamen ayrılmış kod sağlar.

<img alt="paralel-rotalar-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

## Kongre (Convention)

Paralel rotalar adlandırılmış **yuvalar** kullanılarak oluşturulur. Yuvalar `@folder` konvansiyonu ile tanımlanır ve aynı seviyedeki düzene prop olarak aktarılır.

Yuvalar rota segmentleri değildir ve URL yapısını etkilemez. `/@team/members` dosya yoluna `/members` adresinden erişilebilir.

Örneğin, aşağıdaki dosya yapısı iki açık yuva tanımlar: `@analytics` ve `@team`.

<img alt="paralel-rotalar-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-file-system.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Yukarıdaki klasör yapısı, `app/layout.js`'deki bileşenin artık `@analytics` ve `@team` slots prop'larını kabul ettiği ve bunları `alt eleman` prop ile birlikte paralel olarak render edebileceği anlamına gelir:

```ts
export default function Layout(props: {
  children: React.ReactNode;
  analytics: React.ReactNode;
  team: React.ReactNode;
}) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  );
}
```

Bilmekte fayda var: `alt eleman` prop'u, bir klasörle eşleştirilmesi gerekmeyen örtük bir yuvadır. Bu, `app/page.js`'nin `app/@children/page.js` ile eşdeğer olduğu anlamına gelir.

## Eşleşmeyen Rotalar (Unmatched Routes)

Varsayılan olarak, bir yuva içinde oluşturulan içerik geçerli URL ile eşleşir.

Eşleşmeyen bir yuva olması durumunda, Next.js'nin işlediği içerik yönlendirme tekniğine ve klasör yapısına göre farklılık gösterir.

### `default.js`

Next.js geçerli URL'ye göre bir yuvanın etkin durumunu kurtaramadığında geri dönüş olarak render edilecek bir `default.js` dosyası tanımlayabilirsiniz.

Aşağıdaki klasör yapısını düşünün. `@team` yuvasının bir `settings` dizini var, ancak `@analytics`'in yok.

<img alt="paralel-rotalar-5" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Kök `/` dizininden `/settings` dizinine giderseniz, gezinme türüne ve `default.js` dosyasının kullanılabilirliğine bağlı olarak render edilen içerik farklı olur.

|                 | `@analytics/default.js` ile                         | `@analytics/default.js` olmadan                  |
| --------------- | --------------------------------------------------- | ------------------------------------------------ |
| Soft Navigation | `@team/settings/page.js` ve `@analytics/page.js`    | `@team/settings/page.js` ve `@analytics/page.js` |
| Hard Navigation | `@team/settings/page.js` ve `@analytics/default.js` | 404                                              |

### Yumuşak Navigasyon (Soft Navigation)

Yumuşak bir navigasyonda - Next.js, geçerli URL ile eşleşmese bile yuvanın daha önce etkin olan durumunu oluşturur.

### Sert Navigasyon (Hard Navigation)

Zor bir navigasyonda (bütün sayfanın yeniden yüklenmesini gerektiren bir navigasyon) Next.js önce eşleşmeyen yuvanın default.js dosyasını render etmeye çalışır. Eğer bu dosya mevcut değilse, bir 404 görüntülenir.

Eşleşmeyen rotalar için 404, paralel olarak render edilmemesi gereken bir rotayı yanlışlıkla render etmenizi sağlamaya yardımcı olur.

### `useSelectedLayoutSegment(s)`

Hem `useSelectedLayoutSegment` hem de `useSelectedLayoutSegments`, o yuvadaki etkin rota segmentini okumanızı sağlayan bir `parallelRoutesKey` kabul eder.

```ts
"use client";

import { useSelectedLayoutSegment } from "next/navigation";

export default async function Layout(props: {
  //...
  authModal: React.ReactNode;
}) {
  const loginSegments = useSelectedLayoutSegment("authModal");
  // ...
}
```

Bir kullanıcı URL çubuğunda `@authModal/login` veya `/login` adresine gittiğinde, `loginSegments` `"login"` dizesine eşit olacaktır.

## Örnekler

### Modaller (Modals)

Paralel Yönlendirme, modları render etmek için kullanılabilir.

<img alt="paralel-rotalar-6" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-auth-modal.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

`authModal` yuvası, örneğin `/login` gibi eşleşen bir rotaya gidilerek gösterilebilen bir `<Modal>` bileşeni oluşturur.

app/layout.tsx:

```ts
export default async function Layout(props: {
  // ...
  authModal: React.ReactNode;
}) {
  return (
    <>
      {/* ... */}
      {props.authModal}
    </>
  );
}
```

app/@authModal/login/page.tsx:

```ts
import { Modal } from "components/modal";

export default function Login() {
  return (
    <Modal>
      <h1>Login</h1>
      {/* ... */}
    </Modal>
  );
}
```

Modal etkin olmadığında içeriğinin işlenmemesini sağlamak için `null` döndüren bir `default.js` dosyası oluşturabilirsiniz.

app/@authModal/login/default.tsx:

```ts
export default function Default() {
  return null;
}
```

### Bir modalın kapatılması (Dismissing a modal)

İstemci gezintisi yoluyla, örneğin `<Link href="/login">` kullanılarak bir modal başlatılmışsa, `router.back()` öğesini çağırarak veya bir `Link` bileşeni kullanarak modalı kapatabilirsiniz.

app/@authModal/login/page.tsx:

```ts
"use client";
import { useRouter } from "next/navigation";
import { Modal } from "components/modal";

export default async function Login() {
  const router = useRouter();
  return (
    <Modal>
      <span onClick={() => router.back()}>Close modal</span>
      <h1>Login</h1>
      ...
    </Modal>
  );
}
```

Başka bir yere gitmek ve bir modalı kapatmak istiyorsanız, her şeyi kapsayan bir rota da kullanabilirsiniz.

<img alt="paralel-rotalar-7" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fparallel-routes-catchall.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

app/@authModal/[...catchAll]/page.tsx:

```ts
export default function CatchAll() {
  return null;
}
```

Catch-all rotaları `default.js`'ye göre önceliklidir.

## Koşullu Rotalar (Conditional Routes)

Paralel Rotalar koşullu yönlendirme uygulamak için kullanılabilir. Örneğin, kimlik doğrulama durumuna bağlı olarak bir `@dashboard` veya `@login` rotası render edebilirsiniz.

```ts
import { getUser } from "@/lib/auth";

export default function Layout({ params, dashboard, login }) {
  const isLoggedIn = getUser();
  return isLoggedIn ? dashboard : login;
}
```

<img alt="paralel-rotalar-8" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fconditional-routes-ui.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>
