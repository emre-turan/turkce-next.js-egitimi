# Statik Varlıklar (Static Assets)

Next.js, görüntüler gibi statik dosyaları kök dizinde `public` adlı bir klasör altında sunabilir. `public` içindeki dosyalara daha sonra kodunuz tarafından temel URL'den (`/`) başlayarak başvurulabilir.

Örneğin, `public` içine `me.png` eklerseniz, aşağıdaki kod görüntüye erişecektir:

```js
// Avatar.js

import Image from "next/image";

export function Avatar() {
  return <Image src="/me.png" alt="me" width="64" height="64" />;
}
```

`Robots.txt`, `favicon.ico` gibi statik meta veri dosyaları için `app` klasörünün içinde özel meta veri dosyaları kullanmalısınız.

**Bilmekte fayda var:**

- Dizin `public` olarak adlandırılmalıdır. Bu ad değiştirilemez ve statik varlıkları sunmak için kullanılan tek dizindir.
- Yalnızca derleme sırasında `public` dizininde bulunan varlıklar Next.js tarafından sunulacaktır. Çalışma zamanında eklenen dosyalar kullanılamayacaktır. Kalıcı dosya depolama için [AWS S3](https://aws.amazon.com/s3/) gibi üçüncü taraf bir hizmet kullanmanızı öneririz.
