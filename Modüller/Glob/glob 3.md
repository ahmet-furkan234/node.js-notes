
## 1. Belirli Uzantılı Dosyaları Bulma (Promise / Async)

```js
import { glob } from 'glob';

async function findJSFiles() {
  const jsFiles = await glob('src/**/*.js');
  console.log('Tüm JS dosyaları:', jsFiles);
}

findJSFiles();
```

**Açıklama:**  
`src` klasörü ve onun içindeki tüm alt klasörlerdeki `.js` uzantılı dosyaları arar.  
`**` ifadesi iç içe tüm klasörleri, `*.js` ise `.js` uzantılı dosyaları ifade eder.  
Sonuç bir dizi (array) olarak döner ve içinde bulunan tüm dosyaların yolları listelenir.

---

## 2. `ignore` ile İstenmeyen Klasörleri Atlamak

```js
const files = await glob('**/*.js', {
  ignore: ['node_modules/**', 'dist/**']
});
console.log('Node_modules ve dist dışındaki js dosyaları:', files);
```

**Açıklama:**  
Projede genel olarak tüm klasörlerde `.js` dosyalarını arar ama `node_modules` ve `dist` klasörlerinin içini **arama dışında bırakır**.  
Bu sayede sadece bizim yazdığımız dosyalar veya ilgilendiğimiz dosyalar listelenir. Bu klasörler genellikle büyük ve çok dosyalıdır, bu yüzden genelde hariç tutulur.

---

## 3. Dosya Adlarına Göre Filtreleme (Örnek: sadece `test` ile biten dosyalar)

```js
const testFiles = await glob('**/*test.js');
console.log('Test dosyaları:', testFiles);
```

**Açıklama:**  
İç içe tüm klasörlerde ismi `test.js` ile biten dosyaları arar.  
Örneğin: `example.test.js` veya `userTest.js` gibi dosyalar yakalanır.  
Test dosyalarını bulmak için sıklıkla kullanılır.

---

## 4. `cwd` ile Arama Klasörünü Değiştirme

```js
const files = await glob('*.js', { cwd: 'src/utils' });
console.log('src/utils içindeki js dosyaları:', files);
```

**Açıklama:**  
`cwd` (current working directory) parametresi ile aramanın hangi klasörden başlatılacağını belirtiriz.  
Bu örnekte sadece `src/utils` klasöründeki `.js` dosyaları aranır, alt klasörler dahil değil.  
Yani proje kökünden değil, `src/utils` klasöründen bakar.

---

## 5. `absolute` ile Tam Yol Alma

```js
const files = await glob('src/**/*.js', { absolute: true });
console.log('Tam yol ile dosyalar:', files);
```

**Açıklama:**  
Normalde `glob` dosya yollarını **göreli (relative)** olarak döner.  
`absolute: true` dersek, dosyaların tam (mutlak) yollarını verir.  
Özellikle dosyalarla başka modüllerde işlem yaparken tam yol gerekebilir.

---

## 6. Birden Fazla Desen (Brace Expansion)

```js
const files = await glob('src/**/*.{js,json}');
console.log('JS ve JSON dosyaları:', files);
```

**Açıklama:**  
`{js,json}` ifadesi, `src` altındaki tüm klasörlerde hem `.js` hem de `.json` uzantılı dosyaları bulmamızı sağlar.  
Yani iki ayrı desen yazmak yerine tek bir pattern ile arama yapmış oluruz.  
Bu, esneklik ve kısalık sağlar.

---

## 7. Sync Örnek

```js
import { globSync } from 'glob';

const files = globSync('src/**/*.js');
console.log('Sync js dosyaları:', files);
```

**Açıklama:**  
Aynı `.js` dosyalarını arama işlemini **senkron (bloklayıcı)** şekilde yapar.  
İşlem bitene kadar başka kod çalışmaz.  
Genellikle küçük scriptlerde veya startup sırasında tercih edilir.

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

**Açıklama:**  
`dist` klasörü altındaki tüm `.map` uzantılı dosyaları bulur (genelde source map dosyalarıdır).  
Sonra tek tek siler.  
Böylece gereksiz veya deploy sonrası tutulmaması gereken dosyalar temizlenmiş olur.  
`fs-extra`'nın `remove` metodu, dosya veya klasörleri güvenli şekilde silmeye yarar.
