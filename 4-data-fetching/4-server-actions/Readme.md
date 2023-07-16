# Sunucu Eylemleri (Server Actions)

Sunucu Eylemleri, Next.js'de React Eylemleri üzerine inşa edilmiş bir **alfa** özelliğidir. Sunucu tarafı veri mutasyonlarını, azaltılmış istemci tarafı JavaScript'i ve aşamalı olarak geliştirilmiş formları etkinleştirirler. Sunucu Bileşenleri içinde tanımlanabilir ve/veya İstemci Bileşenlerinden çağrılabilirler:

Sunucu Bileşenleri ile:

```js
import { cookies } from "next/headers";

// Sunucu Bileşeni içinde tanımlanan sunucu eylemi
export default function AddToCart({ productId }) {
  async function addItem(data) {
    "use server";

    const cartId = cookies().get("cartId")?.value;
    await saveToDb({ cartId, data });
  }

  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

İstemci Bileşenleri ile:

```js
"use server";

export async function addItem(data) {
  const cartId = cookies().get("cartId")?.value;
  await saveToDb({ cartId, data });
}
```

```js
"use client";

import { addItem } from "./actions.js";

// İstemci Bileşeni içinde çağrılan Sunucu Eylemi
export default function AddToCart({ productId }) {
  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:**

- Sunucu Eylemlerini kullanmak, React `experimental` kanalını çalıştırmayı tercih edecektir.
- React Eylemleri, `useOptimistic` ve `useFormStatus`, Next.js veya React Sunucu Bileşenlerine özgü özellikler değildir.
- Next.js, `RevalidateTag` ve `RevalidatePath` gibi veri mutasyon API'lerinin eklenmesi de dahil olmak üzere React Actions'ı Next.js yönlendiricisine, paketleyicisine ve önbellekleme sistemine entegre eder.

## Convention

Deneysel `serverActions` bayrağını etkinleştirerek Next.js projenizde Sunucu Eylemlerini etkinleştirebilirsiniz.

```js
module.exports = {
  experimental: {
    serverActions: true,
  },
};
```

## Yaratılış (Creation)

Sunucu Eylemleri iki yerde tanımlanabilir:

- Onu kullanan bileşenin içinde (yalnızca Sunucu Bileşenleri)
- Yeniden kullanılabilirlik için ayrı bir dosyada (İstemci ve Sunucu Bileşenleri). Tek bir dosyada birden fazla Sunucu Eylemi tanımlayabilirsiniz.

### Sunucu Bileşenleri ile

Fonksiyon gövdesinin üst kısmında `"use server"` yönergesi ile asenkron bir fonksiyon tanımlayarak bir Sunucu Eylemi oluşturun. Bu fonksiyon, React Sunucu Bileşenleri protokolüne göre serileştirilebilir argümanlara ve serileştirilebilir bir dönüş değerine sahip olmalıdır.

```js
export default function ServerComponent() {
  async function myAction() {
    "use server";
    // ...
  }
}
```

### İstemci Bileşenleri ile

Bir İstemci Bileşeni içinde bir Sunucu Eylemi kullanıyorsanız, eyleminizi dosyanın üst kısmında "use server" yönergesi ile ayrı bir dosyada oluşturun. Ardından, Sunucu Eylemini İstemci Bileşeninize aktarın:

```js
"use server";

export async function myAction() {
  // ...
}
```

```js
"use client";

import { myAction } from "./actions";

export default function ClientComponent() {
  return (
    <form action={myAction}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:** Üst düzey bir `"use server"` yönergesi kullanıldığında, aşağıdaki tüm dışa aktarımlar Sunucu Eylemleri olarak kabul edilecektir. Tek bir dosyada birden fazla Sunucu Eyleminiz olabilir.

## Çağırma (Invocation)

Sunucu Eylemlerini aşağıdaki yöntemleri kullanarak çağırabilirsiniz:

- `action` kullanma: React'in `action` prop'u, bir `<form>` öğesi üzerinde bir Sunucu Eylemi çağırmaya izin verir.
- `formAction` kullanımı: React'in `formAction` özelliği, bir `<form>` öğesindeki `<button>`, `<input type="submit">` ve `<input type="image">` öğelerinin işlenmesini sağlar.
- `startTransition` ile Özel Çağırma: `startTransition` kullanarak `action` veya `formAction` kullanmadan Sunucu Eylemlerini çağırın. Bu yöntem Aşamalı Geliştirmeyi devre dışı bırakır.

### eylem (action)

Bir `form` öğesi üzerinde bir Sunucu Eylemi çağırmak için React'in `action` prop'unu kullanabilirsiniz. Action prop ile aktarılan Sunucu Eylemleri, kullanıcı etkileşimine yanıt olarak asenkron yan etkiler olarak hareket eder.

```js
export default function AddToCart({ productId }) {
  async function addItem(data) {
    "use server";

    const cartId = cookies().get("cartId")?.value;
    await saveToDb({ cartId, data });
  }

  return (
    <form action={addItem}>
      <button type="submit">Add to Cart</button>
    </form>
  );
}
```

**Bilmekte fayda var:** `action`, HTML'in ilkel [`action`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#action)'ına benzer

### `formAction`

Form Eylemlerini `button`, `input type="submit"` ve `input type="image"` gibi öğeler üzerinde işlemek için `formAction` prop'unu kullanabilirsiniz. `formAction` prop, formun eylemine göre önceliklidir.

```js
export default function Form() {
  async function handleSubmit() {
    "use server";
    // ...
  }

  async function submitImage() {
    "use server";
    // ...
  }

  return (
    <form action={handleSubmit}>
      <input type="text" name="name" />
      <input type="image" formAction={submitImage} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Bilmekte fayda var:** Bir `formAction`, HTML ilkel formaction'dır. React artık bu niteliğe fonksiyonlar aktarmanıza izin veriyor.

### `startTransition` kullanarak özel çağırma

Sunucu Eylemlerini `action` veya `formAction` kullanmadan da çağırabilirsiniz. Bunu, `useTransition` kancası tarafından sağlanan `startTransition`'ı kullanarak gerçekleştirebilirsiniz; bu, Sunucu Eylemlerini formların, düğmelerin veya girişlerin dışında kullanmak istiyorsanız yararlı olabilir.

**Bilmekte fayda var:** `startTransition`'ı kullanmak, kullanıma hazır Aşamalı Geliştirmeyi devre dışı bırakır.

```js
"use client";

import { useTransition } from "react";
import { addItem } from "../actions";

function ExampleClientComponent({ id }) {
  let [isPending, startTransition] = useTransition();

  return (
    <button onClick={() => startTransition(() => addItem(id))}>
      Add To Cart
    </button>
  );
}
```

```ts
"use server";

export async function addItem(id) {
  await addItemToDb(id);
  // Tüm ürün sayfalarını yeniden doğrulama için işaretler
  revalidatePath("/product/[id]");
}
```

### `StartTransition` olmadan özel çağırma

Sunucu Mutasyonları yapmıyorsanız, işlevi diğer işlevler gibi doğrudan bir prop olarak aktarabilirsiniz.

```js
import kv from "@vercel/kv";
import LikeButton from "./like-button";

export default function Page({ params }: { params: { id: string } }) {
  async function increment() {
    "use server";
    await kv.incr(`post:id:${params.id}`);
  }

  return <LikeButton increment={increment} />;
}
```

```js
"use client";

export default function LikeButton({
  increment,
}: {
  increment: () => Promise<void>,
}) {
  return (
    <button
      onClick={async () => {
        await increment();
      }}
    >
      Like
    </button>
  );
}
```

## Geliştirmeler

### Deneysel `useOptimistik`

Deneysel `useOptimistic` kancası, uygulamanızda iyimser güncellemeleri uygulamak için bir yol sağlar. İyimser güncellemeler, uygulamanın daha duyarlı görünmesini sağlayarak kullanıcı deneyimini geliştiren bir tekniktir.

Bir Sunucu Eylemi çağrıldığında, Sunucu Eyleminin yanıtını beklemek yerine, kullanıcı arayüzü beklenen sonucu yansıtacak şekilde hemen güncellenir.

```js
"use client";

import { experimental_useOptimistic as useOptimistic } from "react";
import { send } from "./actions.js";

export function Thread({ messages }) {
  const [optimisticMessages, addOptimisticMessage] = useOptimistic(
    messages,
    (state, newMessage) => [...state, { message: newMessage, sending: true }]
  );
  const formRef = useRef();

  return (
    <div>
      {optimisticMessages.map((m) => (
        <div>
          {m.message}
          {m.sending ? "Sending..." : ""}
        </div>
      ))}
      <form
        action={async (formData) => {
          const message = formData.get("message");
          formRef.current.reset();
          addOptimisticMessage(message);
          await send(message);
        }}
        ref={formRef}
      >
        <input type="text" name="message" />
      </form>
    </div>
  );
}
```

### Deneysel `useFormStatus`

Deneysel `useFormStatus` kancası Form Eylemleri içinde kullanılabilir ve `pending` özelliğini sağlar.

```js
"use client";

import { experimental_useFormStatus as useFormStatus } from "react-dom";

function Submit() {
  const { pending } = useFormStatus();

  return (
    <input
      type="submit"
      className={pending ? "button-pending" : "button-normal"}
      disabled={pending}
    >
      Submit
    </input>
  );
}
```

## Aşamalı İyileştirme

Aşamalı Geliştirme, bir `<form>`'un JavaScript olmadan veya JavaScript devre dışı bırakıldığında düzgün çalışmasını sağlar. Bu, form için JavaScript henüz yüklenmemiş olsa veya yüklenemese bile kullanıcıların formla etkileşime girmesine ve veri göndermesine olanak tanır.

Hem Sunucu Form Eylemleri hem de İstemci Form Eylemleri, iki stratejiden birini kullanarak Aşamalı Geliştirmeyi destekler:

- Bir Sunucu Eylemi doğrudan bir `<form>`'a aktarılırsa, JavaScript devre dışı bırakılsa bile form etkileşimlidir.
- Bir `<form>`'a bir İstemci Eylemi aktarılırsa, form hala etkileşimlidir, ancak eylem form hidratlanana kadar bir kuyruğa yerleştirilir. `<form>`, Seçici Hidrasyon ile önceliklendirilir, bu nedenle hızlı bir şekilde gerçekleşir.

```js
"use client";

import { useState } from "react";
import { handleSubmit } from "./actions.js";

export default function ExampleClientComponent({ myAction }) {
  const [input, setInput] = useState();

  return (
    <form action={handleSubmit} onChange={(e) => setInput(e.target.value)}>
      {/* ... */}
    </form>
  );
}
```

Her iki durumda da hidrasyon gerçekleşmeden önce form etkileşimlidir. Sunucu Eylemleri istemci JavaScript'ine dayanmama gibi ek bir avantaja sahip olsa da, etkileşimden ödün vermeden istediğiniz yerde İstemci Eylemleri ile ek davranışlar oluşturabilirsiniz.

## Boyut Sınırlaması

Varsayılan olarak, bir Sunucu Eylemine gönderilen istek gövdesinin maksimum boyutu 1 MB'dir. Bu, ayrıştırmak için çok fazla sunucu kaynağı tüketen büyük miktarda verinin sunucuya gönderilmesini önler.

Ancak, bu sınırı deneysel `serverActionsBodySizeLimit` seçeneğini kullanarak yapılandırabilirsiniz. Bayt sayısını veya baytlar tarafından desteklenen herhangi bir dize biçimini alabilir, örneğin `1000`, `'500kb'` veya `'3mb'`.

```js
module.exports = {
  experimental: {
    serverActions: true,
    serverActionsBodySizeLimit: "2mb",
  },
};
```

## Örnekler

### İstemci Bileşenleri ile Kullanım

#### İçe Aktarma

Sunucu Eylemleri İstemci Bileşenleri içinde tanımlanamaz, ancak içe aktarılabilirler. Sunucu Eylemlerini İstemci Bileşenlerinde kullanmak için, eylemi üst düzey bir "use server" yönergesi içeren bir dosyadan içe aktarabilirsiniz.

```js
"use server";

export async function addItem() {
  // ...
}
```

```js
"use client";

import { useTransition } from "react";
import { addItem } from "../actions";

function ExampleClientComponent({ id }) {
  let [isPending, startTransition] = useTransition();

  return (
    <button onClick={() => startTransition(() => addItem(id))}>
      Add To Cart
    </button>
  );
}
```

#### Proplar

Sunucu Eylemlerinin içe aktarılması tavsiye edilse de, bazı durumlarda bir Sunucu Eylemini bir İstemci Bileşenine prop olarak aktarmak isteyebilirsiniz.

Örneğin, eylem içinde dinamik olarak oluşturulan bir değer kullanmak isteyebilirsiniz. Bu durumda, bir Sunucu Eylemini prop olarak aktarmak uygun bir çözüm olabilir.

```js
import { ExampleClientComponent } from "./components/example-client-component.js";

function ExampleServerComponent({ id }) {
  async function updateItem(data) {
    "use server";
    modifyItem({ id, data });
  }

  return <ExampleClientComponent updateItem={updateItem} />;
}
```

```js
"use client";

function ExampleClientComponent({ updateItem }) {
  async function action(formData: FormData) {
    await updateItem(formData);
  }

  return (
    <form action={action}>
      <input type="text" name="name" />
      <button type="submit">Update Item</button>
    </form>
  );
}
```

### İsteğe Bağlı Yeniden Doğrulama

Sunucu Eylemleri, verileri isteğe bağlı olarak yola (`revalidatePath`) veya önbellek etiketine (`revalidateTag`) göre yeniden doğrulamak için kullanılabilir.

```js
import { revalidateTag } from "next/cache";

async function revalidate() {
  "sunucu kullan";
  revalidateTag("blog-posts");
}
```

### Doğrulama

Bir Sunucu Eylemine aktarılan veriler, eylem çağrılmadan önce doğrulanabilir veya temizlenebilir. Örneğin, eylemi bağımsız değişken olarak alan ve geçerli olması durumunda eylemi çağıran bir işlev döndüren bir sarmalayıcı işlev oluşturabilirsiniz.

```js
"use server";

import { withValidate } from "lib/form-validation";

export const action = withValidate((data) => {
  // ...
});
```

```js
export function withValidate(action) {
  return async (formData: FormData) => {
    "use server";

    const isValidData = verifyData(formData);

    if (!isValidData) {
      throw new Error("Invalid input.");
    }

    const data = process(formData);
    return action(data);
  };
}
```

### Başlıkları kullanma

Bir Sunucu Eylemi içinde `cookies` ve `headers` gibi gelen istek üstbilgilerini okuyabilirsiniz.

```js
import { cookies } from "next/headers";

async function addItem(data) {
  "use server";

  const cartId = cookies().get("cartId")?.value;

  await saveToDb({ cartId, data });
}
```

Ayrıca, bir Sunucu Eylemi içinde çerezleri değiştirebilirsiniz.

```js
import { cookies } from 'next/headers';

async function create(data) {
  'use server';

  const cart = await createCart():
  cookies().set('cartId', cart.id)
  // or
  cookies().set({
    name: 'cartId',
    value: cart.id,
    httpOnly: true,
    path: '/'
  })
}
```

## Glossary

### Eylemler (Actions)

Eylemler, React'te deneysel bir özelliktir ve bir kullanıcı etkileşimine yanıt olarak `asenkron` kod çalıştırmanıza olanak tanır.

Eylemler Next.js veya React Sunucu Bileşenlerine özgü değildir, ancak React'in kararlı sürümünde henüz mevcut değildir. Next.js aracılığıyla Eylemleri kullanırken, React `experimental` kanalını kullanmayı tercih etmiş olursunuz.

Eylemler, bir öğe üzerindeki `action` prop aracılığıyla tanımlanır. Genellikle HTML formları oluştururken, [action prop](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#action)'a bir URL iletirsiniz. Eylemler ile React artık doğrudan bir fonksiyon aktarmanıza izin veriyor.

React ayrıca Eylemler ile optimize güncellemeler için yerleşik çözümler sunar. Yeni modellerin hala geliştirilmekte olduğunu ve yeni API'lerin eklenebileceğini unutmamak önemlidir.

### Form Eylemleri

Web standardı `<form>` API'sine entegre edilmiş eylemler, kullanıma hazır aşamalı geliştirme ve yükleme durumlarını etkinleştirir. HTML ilkel [formaction](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#formaction)'a benzer.

### Sunucu İşlevleri

Sunucuda çalışan ancak istemcide çağrılabilen işlevler.

### Sunucu Eylemleri

Sunucu İşlevleri bir eylem olarak çağrılır.

Sunucu Eylemleri, bir `form` öğesinin `action` prop'una geçirilerek aşamalı olarak geliştirilebilir. Form, herhangi bir istemci tarafı JavaScript yüklenmeden önce etkileşimlidir. Bu, formun gönderilmesi için React hidrasyonunun gerekli olmadığı anlamına gelir.

### Sunucu Mutasyonları

Verilerinizi değiştiren ve `redirect`, `revalidatePath` veya `revalidateTag`'i çağıran Sunucu Eylemleri.
