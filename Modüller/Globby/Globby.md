
- `globby`, Node.js için gelişmiş dosya arama ve filtreleme kütüphanesidir.
- `glob` fonksiyonlarını daha kolay ve modern bir API ile sunar.
- Promise desteklidir, async/await ile mükemmel uyum sağlar.
- Gelişmiş **ignore**, **brace expansion**, **multiple pattern** gibi özellikler var.
- ES Modül ve CommonJS desteği mevcut.

---

## 🔧 Kurulum

```bash
npm install globby
```

---

## 📄 Basit Kullanım Örneği (ESM)

```js
import globby from 'globby';

async function findFiles() {
  const paths = await globby(['src/**/*.js', '!src/**/*.test.js']);
  console.log('Bulunan dosyalar:', paths);
}

findFiles();
```

---

## 🔍 Globby Özellikleri

|Özellik|Açıklama|
|---|---|
|Çoklu pattern|`['src/**/*.js', '!src/**/*.test.js']`|
|Ignore ayarı|`ignore: ['node_modules']`|
|Brace Expansion|`{js,ts,json}` destekler|
|Absolute yol|`absolute: true` ile tam yol döner|
|`cwd` ayarı|Başlangıç klasörü belirlenebilir|
|Promise ve Sync sürüm|`globby.sync()` ile senkron kullanım|

---

## 📚 Detaylı Örnekler

### 1. Çoklu Pattern ile Dosya Bulma

```js
import globby from 'globby';

const patterns = ['src/**/*.{js,ts}', '!src/**/*.test.ts'];
const files = await globby(patterns);
console.log(files);
```

---

### 2. Ignore Ayarı

```js
const files = await globby('**/*.js', {
  ignore: ['node_modules/**', 'dist/**']
});
console.log(files);
```

---

### 3. Absolute Yol ile Dosya Listesi

```js
const files = await globby('src/**/*.js', { absolute: true });
console.log(files);
```

---

### 4. Senkron Kullanım

```js
import globby from 'globby';

const files = globby.sync('src/**/*.js');
console.log(files);
```

---

### 5. `cwd` Ayarı ile Başlangıç Dizini Belirleme

```js
const files = await globby('*.js', { cwd: 'src/utils' });
console.log(files);
```

---

## ⚙️ Nerelerde Kullanılır?

- Modern build araçları ve scriptlerde
    
- Dosya filtreleme işlemlerinde
    
- Test dosyalarını veya belirli tipte dosyaları bulmada
    
- Büyük projelerde hızlı dosya arama ihtiyaçlarında
    

---

İstersen `globby` ile dosya bulma ve işleme içeren küçük bir script yazalım veya `glob` ile farklarını karşılaştıralım. Ne dersin?