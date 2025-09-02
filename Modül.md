
Node.js'te bir dosya (ör. `app.js`, `math.js`) aslında bir modüldür.  
✅ **Modül = Kendi başına çalışan bağımsız bir kod parçası.**

➡ Node.js modül sistemi şunu sağlar:

- Kodları **parçalara ayırarak yönetilebilir hale getirme**
- Tekrar kullanılabilirlik (aynı modülü farklı dosyalarda kullanabilirsin)
- Değişkenlerin ve fonksiyonların **global kapsamda kirlenmesini önleme**

---

# 🌟 **2️⃣ Node.js’te Modül Türleri**

|Modül Türü|Açıklama|
|---|---|
|**Yerleşik (Built-in) Modüller**|Node.js ile birlikte gelir. Ör: `fs`, `http`, `path`, `os`|
|**Kullanıcı Tanımlı Modüller**|Senin yazdığın dosyalar. Ör: `math.js`, `logger.js`|
|**Üçüncü Parti Modüller**|NPM’den yüklenenler. Ör: `express`, `lodash`|

---

# 🌟 **3️⃣ Modül Nasıl Oluşturulur ve Kullanılır?**

## 📌 **Modül Oluşturmak**

Bir dosya oluştur ve içine fonksiyon, nesne, sınıf veya değişken tanımla.

▶ **math.js**

```js
function topla(a, b) {
    return a + b;
}

function carp(a, b) {
    return a * b;
}

// Dışa aktar (export)
module.exports = {
    topla,
    carp
};
```

## 📌 **Modülü Kullanmak**

▶ **app.js** 

```js
const math = require('./math');

console.log(math.topla(5, 3));  // 8
console.log(math.carp(4, 2));   // 8
```

💡 `require('./math')` derken **./** ile dosya yolunu belirtiyoruz.

---

# 🌟 **4️⃣ `module.exports` ve `exports` Farkı**

Node.js her modülü şöyle sarar:

```js
(function(exports, require, module, __filename, __dirname) {
    // senin dosyan
});
```

Yani dosyanın içi bir fonksiyon gibi çalışır.  
✅ **exports** ve **module.exports** ikisi de başlangıçta aynı nesneyi işaret eder.

### 📝 Örnek

```js
// Geçerli:
exports.selam = () => console.log("Merhaba!");

// Geçerli:
module.exports = {
    selam: () => console.log("Merhaba!")
};

// ⚠️ Dikkat! Şunu yaparsan exports kopar:
exports = () => console.log("Bu export edilmez!");
```

👉 **Kural:**  
Eğer bir obje veya fonksiyonu doğrudan dışa vereceksen `module.exports = ...` kullan.  
`exports.something = ...` ile obje özellikleri ekle.

---

# 🌟 **5️⃣ Her Modülün Özel Değişkenleri**

Node.js her modüle bazı özel değişkenler sağlar:

| Değişken     | Açıklama                         |
| ------------ | -------------------------------- |
| `module`     | Modülün bilgilerini içerir       |
| `exports`    | Dışa aktarılan nesne             |
| `__filename` | Dosyanın tam yolu                |
| `__dirname`  | Dosyanın bulunduğu klasörün yolu |

---

# 🌟 **6️⃣ Yerleşik (Built-in) Modüller Örneği**

## 📂 **fs (dosya sistemi)**

```js
const fs = require('fs');

fs.writeFileSync('dosya.txt', 'Merhaba Dosya');
const veri = fs.readFileSync('dosya.txt', 'utf8');
console.log(veri);  // Merhaba Dosya
```

## 📂 **path**

```js
const path = require('path');

console.log(path.basename(__filename));  // app.js (örnek)
console.log(path.join(__dirname, 'data', 'test.txt'));  
```

---

# 🌟 **7️⃣ NPM Modülleri (Üçüncü Parti Modüller)**

```bash
npm install lodash
```

▶ **app.js**

```js
const _ = require('lodash');

console.log(_.capitalize('merhaba dünya'));  // Merhaba dünya
```

---

# 🌟 **8️⃣ Modüller Nasıl Cache'lenir?**

Bir modül bir kez `require` edildiğinde:
- Node.js onu belleğe alır (cache)
- Sonraki `require` çağrıları aynı nesneyi döner

▶ Örnek:

```js
// bir.js
console.log("Bir.js yüklendi");

// app.js
require('./bir');
require('./bir');  // sadece bir kez "Bir.js yüklendi" yazılır
```

---

# 🌟 **9️⃣ Döngüsel Modül Bağımlılığı (Circular Dependency)**

Modüller birbirini require ederse **döngü** oluşur.  
▶ Örnek:

```js
A -> B -> A
```

Node.js bunu tolere eder ama incomplete (eksik) export dönebilir.

---

# 🌟 1️⃣0️⃣ Modüller ve Kapsam**

- Modülde tanımlanan her şey kendi dosyasına özeldir.
- Dışarı export edilmedikçe başka dosyadan erişilemez.

▶ Örnek:

```js
// a.js
const gizli = 123;
module.exports.goster = () => console.log(gizli);

// b.js
const a = require('./a');
a.goster();   // 123
console.log(a.gizli);  // undefined
```

# 🌟 1️⃣1️⃣ ES6 Modül Desteği (import/export)**

Node.js artık `.mjs` uzantısı veya `package.json` içine `"type": "module"` ile ES6 modül sistemini destekler.

▶ ES6 export:

```js
export function topla(a, b) {
    return a + b;
}
```

▶ ES6 import:

```js
import { topla } from './math.mjs';
console.log(topla(2, 3));  // 5
```

---

# 🌟 1️⃣2️⃣ Modül Yol Çözümleme**

Node.js `require` sırasıyla şuralara bakar:  
1️⃣ Core modüller (ör: `fs`)  
2️⃣ Verilen dosya/dizin (ör: `./modul`)  
3️⃣ `node_modules` klasörü  
4️⃣ Ana dizindeki `node_modules`’a kadar çıkar

▶ Örnek arama sırası:

```js
require('lodash')
-> node_modules/lodash/index.js
```

---

# 🌟 1️⃣3️⃣ module nesnesinin içeriği**

```js
console.log(module);
```

➡ Örnek çıktı:

```js
{
  "id": ".",
  "path": "/dosya/yolu",
  "exports": {},
  "filename": "/dosya/yolu/app.js",
  "loaded": false,
  ...
}
```

---

# 🌟 1️⃣4️⃣ Tüm Modül Sistemi Özet Diyagramı**

```lua
+-----------------------------+
|    Node.js Çalışma Ortamı    |
+-----------------------------+
          |
          v
+----------------+     +----------------+     +-----------------+
| Yerleşik Modül | --> | Kullanıcı Modül | --> | 3. Parti Modül  |
|   (fs, http)   |     |  (./math.js)    |     |  (express)      |
+----------------+     +----------------+     +-----------------+

--> require() modülü bulur, cache'ler ve döner
--> module.exports ne ise onu döner
```

---

# 🌟 1️⃣5️⃣ Modüllerde En İyi Pratikler**

✅ Gereksiz global değişken tanımlama.  
✅ Küçük, anlamlı modüller yaz.  
✅ `module.exports` kullan, `exports` yerine.  
✅ Döngüsel bağımlılıktan kaçın.  
✅ Yalnızca gerekli modülleri yükle.

---

# 🎁 **Sana mini örnek bir yapı**

```lua
proje/
 ├── app.js
 ├── math.js
 ├── utils/
 │    └── logger.js
 └── node_modules/
```

▶ **math.js**

```js
function topla(a, b) { return a + b; }
module.exports = { topla };
```

▶ **utils/logger.js**

```js
module.exports = (msg) => console.log("LOG:", msg);
```

▶ **app.js**

```js
const math = require('./math');
const logger = require('./utils/logger');

const sonuc = math.topla(10, 5);
logger(`Sonuç: ${sonuc}`);
```

---

# 🏁 **Sonuç**

Node.js modül sistemi:  
✅ Kodun bölünmesini ve düzenlenmesini sağlar.  
✅ Kapsamı yönetir.  
✅ Tekrar kullanılabilir modüller oluşturmanı sağlar.  
✅ NPM ile kolay genişletilir.