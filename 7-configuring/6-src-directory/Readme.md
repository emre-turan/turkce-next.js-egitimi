# src Dizini

Projenizin kök dizininde özel Next.js `app` veya `pages` dizinlerine sahip olmaya alternatif olarak Next.js, uygulama kodunu `src` dizininin altına yerleştirmenin yaygın modelini de destekler.

Bu, uygulama kodunu, bazı bireyler ve ekipler tarafından tercih edilen, çoğunlukla bir projenin kök dizininde bulunan proje yapılandırma dosyalarından ayırır.

`src` dizinini kullanmak için, `app` Router klasörünü veya `pages` Router klasörünü sırasıyla `src/app` veya `src/pages` dizinine taşıyın.

<img alt="src-dizini" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-src-directory.png&w=1920&q=75&dpl=dpl_FgqPZgpvfTdBpYwq43qhnaRUcyXh"/>
<br>

**Bilmekte Fayda Var:**

- `/public` dizini projenizin kök dizininde kalmalıdır.
- `package.json`, `next.config.js` ve `tsconfig.json` gibi yapılandırma dosyaları projenizin kök dizininde kalmalıdır.
- `.env.*` dosyaları projenizin kök dizininde kalmalıdır.
- Kök dizinde `app` veya `pages` varsa `src/app` veya `src/pages` göz ardı edilecektir.
- Eğer `src` kullanıyorsanız, muhtemelen `/components` veya `/lib` gibi diğer uygulama klasörlerini de taşıyacaksınız.
- Tailwind CSS kullanıyorsanız, [içerik bölümündeki](https://tailwindcss.com/docs/content-configuration) `tailwind.config.js` dosyasına `/src` önekini eklemeniz gerekir.
