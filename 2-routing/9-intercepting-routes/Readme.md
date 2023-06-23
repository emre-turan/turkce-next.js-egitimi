# Kesen Rotalar (Intercepting Routes)

Rotaları kesmek, geçerli sayfanın bağlamını korurken geçerli düzen içinde bir rota yüklemenize olanak tanır. Bu yönlendirme paradigması, farklı bir rota göstermek için belirli bir rotayı "kesmek" istediğinizde yararlı olabilir.

Örneğin, bir beslemenin içinden bir fotoğrafa tıklandığında, beslemeyi kaplayan bir modal fotoğrafla birlikte görünmelidir. Bu durumda Next.js, `/feed` yolunu keser ve bunun yerine `/photo/123` göstermek için bu URL'yi "maskeler".

<img alt="kesen-rotalar" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepting-routes-soft-navigate.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Ancak, örneğin paylaşılabilir bir URL'ye tıklayarak veya sayfayı yenileyerek doğrudan fotoğrafa gidildiğinde, modal yerine fotoğraf sayfasının tamamı render edilmelidir. Herhangi bir rota müdahalesi gerçekleşmemelidir.

<img alt="kesen-rotalar-2" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepting-routes-hard-navigate.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

## Convention

Kesişen rotalar, göreli yol kuralı `../`'ye benzeyen ancak segmentler için olan `(..)` kuralı ile tanımlanabilir.

Şu şekillerde Kullanabilirsiniz:

- `(.)` aynı seviyedeki segmentleri eşleştirmek için
- `(..)` bir üst seviyedeki segmentlerle eşleştirmek için
- `(..)(..)` iki seviye yukarıdaki segmentlerle eşleştirmek için
- `(...)` kök uygulama dizinindeki segmentleri eşleştirmek için

Örneğin, bir `(..)photo` dizini oluşturarak `fotoğraf` segmentini `besleme` segmenti içinden kesebilirsiniz.

<img alt="kesen-rotalar-3" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepted-routes-files.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

`(..)` kuralının dosya sistemini değil, yol segmentlerini temel aldığını unutmayın.

## Modaller (Modals)

Yakalama Rotaları, modaller oluşturmak için Paralel Rotalar ile birlikte kullanılabilir.

Bu kalıbı kullanarak modaller oluşturmak, modallerle çalışırken karşılaşılan bazı zorlukların üstesinden gelmenizi sağlar:

- Modal içeriği bir URL aracılığıyla paylaşılabilir hale getirin
- Sayfa yenilendiğinde, modalı kapatmak yerine bağlamı koruyun
- Önceki rotaya gitmek yerine geriye doğru gezinmede modalı kapatın
- İleriye doğru gezinme modalini yeniden açma

<img alt="kesen-rotalar-4" src="https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fintercepted-routes-modal-example.png&w=3840&q=75&dpl=dpl_8fzWiojXNexXAYQSWwEEmzPxZwZN" /><br/>

Yukarıdaki örnekte, `@modal` bir segment değil bir slot olduğu için `photo` segmentine giden yol `(..)` eşleştiricisini kullanabilir. Bu, iki dosya sistemi seviyesi daha yüksek olmasına rağmen `photo` yolunun yalnızca bir segment seviyesi daha yüksek olduğu anlamına gelir.

Diğer örnekler arasında, özel bir `/login` sayfasına sahipken üst navbarda bir oturum açma modalı açmak veya bir yan modalda bir alışveriş sepeti açmak sayılabilir.
