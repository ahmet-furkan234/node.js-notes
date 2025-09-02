

## 1. Belirli Uzantılı Dosyaları Bulma (Promise / Async)

```js
import { glob } from 'glob';

async function findJSFiles() {
  const jsFiles = await glob('src/**/*.js');
  console.log('Tüm JS dosyaları:', jsFiles);
}

findJSFiles();
```

---

## 2. `ignore` ile İstenmeyen Klasörleri Atlamak

```js
const files = await glob('**/*.js', {
  ignore: ['node_modules/**', 'dist/**']
});
console.log('Node_modules ve dist dışındaki js dosyaları:', files);
```

---

## 3. Dosya Adlarına Göre Filtreleme (Örnek: sadece `test` ile biten dosyalar)

```js
const testFiles = await glob('**/*test.js');
console.log('Test dosyaları:', testFiles);
```

---

## 4. `cwd` ile Arama Klasörünü Değiştirme

```js
const files = await glob('*.js', { cwd: 'src/utils' });
console.log('src/utils içindeki js dosyaları:', files);
```

---

## 5. `absolute` ile Tam Yol Alma

```js
const files = await glob('src/**/*.js', { absolute: true });
console.log('Tam yol ile dosyalar:', files);
```

---

## 6. Birden Fazla Desen (Brace Expansion)

```js
const files = await glob('src/**/*.{js,json}');
console.log('JS ve JSON dosyaları:', files);
```

---

## 7. Sync Örnek

```js
import { globSync } from 'glob';

const files = globSync('src/**/*.js');
console.log('Sync js dosyaları:', files);
```

---

## 8. Örnek: Belirli Dosyaları Silme (fs-extra ile birlikte)

```js
import { glob } from 'glob';
import fs from 'fs-extra';

async function cleanDist() {
  const files = await glob('dist/**/*.map');  // .map dosyalarını bul
  for (const file of files) {
    await fs.remove(file);
    console.log(`${file} silindi`);
  }
}

cleanDist();
```
