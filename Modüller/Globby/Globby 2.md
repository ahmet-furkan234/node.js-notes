
# 🔴 `glob` ile Dosya Arama Örneği (Promise + Async)

```js
import { glob } from 'glob';

async function findJSWithGlob() {
  // Tek pattern, ignore ile basit filtre
  const files = await glob('src/**/*.js', {
    ignore: ['**/*.test.js']
  });
  console.log('glob ile bulunan dosyalar:', files);
}

findJSWithGlob();
```

---

# 🟢 `globby` ile Aynı İş (Çoklu pattern, daha temiz)

```js
import globby from 'globby';

async function findJSWithGlobby() {
  // Çoklu pattern kolayca kullanılıyor, ignore pattern olarak '!' ile
  const files = await globby(['src/**/*.js', '!**/*.test.js']);
  console.log('globby ile bulunan dosyalar:', files);
}

findJSWithGlobby();
```

---

# 🔍 Farklar

|Kriter|glob|globby|
|---|---|---|
|**Çoklu pattern**|Zor veya ayrı ayrı çağrı yapman gerekir|Tek çağrıda array ile çoklu pattern kullanılır|
|**Ignore ayarı**|Opsiyonel, objeyle belirtilir|`!` işaretiyle pattern listesinde kolayca yapılır|
|**API**|`glob(pattern, options, callback)` veya Promise|Promise tabanlı, async/await ile kolay|
|**Kod sadeliği**|Daha uzun, callback veya opsiyonlar ile|Daha kısa, temiz, modern|
|**Performans**|Küçük projelerde yeterli|Büyük ve karmaşık projelerde daha optimize|
