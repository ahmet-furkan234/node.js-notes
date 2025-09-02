
`glob`, dosya yollarını **kısa tanımlarla** eşlemeni sağlayan bir **pattern-matching (şablon eşleştirme)** aracıdır.

**Kullanım Alanları:**

- Belirli uzantıya sahip dosyaları bulmak
- Klasör yapısı içinde recursive (iç içe) dosya aramak
- Örneğin: `src/**/*.js` → tüm `.js` dosyalarını iç içe klasörlerde bulur

---

## 🔧 2. Kurulum

```bash
npm install glob
```

---

## 📁 Örnek Dosya Yapısı

```
project/
├── src/
│   ├── app.js
│   ├── utils/
│   │   └── helper.js
│   └── data.json
├── logs/
│   └── app.log
└── findFiles.mjs
```

---

## 📄 3. ECMAScript Modül Örneği (`findFiles.mjs`)

```js
import { glob } from 'glob';

const jsFiles = await glob('src/**/*.js');  // tüm .js dosyalarını bulur
console.log('JavaScript dosyaları:', jsFiles);

const allFiles = await glob('**/*.*');  // tüm dosyaları bul
console.log('Tüm dosyalar:', allFiles);
```

> Not: `glob` artık Promise destekli çalışır, `await` ile kullanabilirsin.

---

## 🔍 4. Pattern (Desen) Anlamları

|Pattern|Anlamı|
|---|---|
|`*.js`|Geçerli klasördeki `.js` dosyaları|
|`**/*.js`|Tüm klasörlerdeki `.js` dosyaları|
|`src/**/*.json`|`src` altında tüm `.json` dosyaları|
|`**/helper.*`|İsmi `helper` olan ve uzantısı ne olursa olsun dosyalar|
|`!**/*.test.js`|`.test.js` ile biten dosyaları dışla|
|`{*.js,*.json}`|`.js` veya `.json` olan dosyalar|

---

## ⚙️ 5. Opsiyonel Ayarlar

```js
const files = await glob('**/*.js', {
  ignore: ['node_modules/**'], // bu klasörü atla
  cwd: 'src',                  // aramayı bu klasörde başlat
  absolute: true              // tam yol döndür
});
```

---

## 🔄 6. Sync Kullanımı (Eğer istersek)

```js
import { globSync } from 'glob';

const files = globSync('src/**/*.js');
console.log(files);
```

---

## 📚 7. `glob` Nerelerde Kullanılır?

- Webpack gibi build sistemlerinde
- Test dosyası bulmada (`**/*.test.js`)
- Linter, preloader, backup araçları
- Script'lerde (örneğin `.env.*` dosyalarını bulmak için)
