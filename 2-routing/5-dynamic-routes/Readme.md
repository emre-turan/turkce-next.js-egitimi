# Dinamik Rotalar (Dynamic Routes)

Segment adlarını önceden tam olarak bilmediğinizde ve dinamik verilerden rotalar oluşturmak istediğinizde, istek zamanında doldurulan veya derleme zamanında önceden oluşturulan Dinamik Segmentleri kullanabilirsiniz.

Bir Dinamik Segment, bir klasörün adını köşeli parantezler içine alarak oluşturulabilir: `[folderName]`. Örneğin, `[id]` veya `[slug]`.

Dinamik Segmentler `layout`, `page`, `route` ve `generateMetadata` fonksiyonlarına `params` prop olarak aktarılır.

Örneğin, bir blog aşağıdaki `app/blog/[slug]/page.js` rotasını içerebilir; burada `[slug]` blog gönderileri için Dinamik Segmenttir.

```ts
export default function Page({ params }: { params: { slug: string } }) {
  return <div>My Post: {params.slug}</div>;
}
```

| Rota                         | Örnek URL     | `Params`                   |
| ---------------------------- | ------------- | -------------------------- |
| `app/shop/[...slug]/page.js` | `/shop/a`     | `{ slug: ['a'] }`          |
| `app/shop/[...slug]/page.js` | `/shop/a/b`   | `{ slug: ['a', 'b'] }`     |
| `app/shop/[...slug]/page.js` | `/shop/a/b/c` | `{ slug: ['a', 'b', 'c']}` |

## İsteğe Bağlı Her Şeyi Yakalayan Segmentler (Optional Catch-all Segments)

Catch-all Segmentleri, parametreyi çift köşeli parantez içine alarak isteğe bağlı hale getirilebilir: `[[...folderName]]`.

Örneğin, `app/shop/[[...slug]]/page.js`, `/shop/clothes`, `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`'e ek olarak `/shop` ile de eşleşecektir.

`Tümünü yakala` ve `isteğe bağlı tümünü yakala` segmentleri arasındaki fark, isteğe bağlı olduğunda parametre içermeyen rotanın da eşleştirilmesidir (yukarıdaki örnekte `/shop`).

| Route                          | Example URL   | `Params`                   |
| ------------------------------ | ------------- | -------------------------- |
| `app/shop/[[...slug]]/page.js` | `/shop`       | `{}`                       |
| `app/shop/[[...slug]]/page.js` | `/shop/a`     | `{ slug: ['a'] }`          |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b`   | `{ slug: ['a', 'b'] }`     |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b/c` | `{ slug: ['a', 'b', 'c']}` |

### TypeScript

TypeScript kullanırken, yapılandırılmış rota segmentinize bağlı olarak `params` için türler ekleyebilirsiniz.

```ts
export default function Page({ params }: { params: { slug: string } }) {
  return <h1>My Page</h1>;
}
```

| Route                               | `Params` Type Definition                 |
| ----------------------------------- | ---------------------------------------- | ------------ |
| `app/blog/[slug]/page.js`           | `{ slug: string }`                       | slug: string |
| `app/shop/[...slug]/page.js`        | `{ slug: string[] }`                     |
| `app/[categoryId]/[itemId]/page.js` | `{ categoryId: string, itemId: string }` |
