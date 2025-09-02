
✅ **ES6 modül sistemi**, JavaScript’in tarayıcı ve Node.js ortamında modüler kod yazmamızı sağlayan modern standart modül sistemidir.

💡 **Amaç:**

- Kodun parçalanmasını sağlamak
- Her dosyayı bağımsız bir modül olarak çalıştırmak
- Yalnızca ihtiyaç olan kısımları dışa aktarmak ve kullanmak

---

# 🌟 **2️⃣ ES6 Modül Sözdizimi**

## 📌 **Dışa Aktarma (export)**

### Bireysel export

```js
// math.js
export function topla(a, b) {
  return a + b;
}

export const PI = 3.14;
```

### Toplu export

```js
// math.js
function carp(a, b) { return a * b; }
function bol(a, b) { return a / b; }

export { carp, bol };
```

### Varsayılan export (default)

```js
// math.js
export default function(a, b) {
  return a - b;
}
```

---

## 📌 **İçe Aktarma (import)**

### Bireysel import

```js
import { topla, PI } from './math.js';

console.log(topla(2,3));  // 5
console.log(PI);         // 3.14
```

### Tümü bir isim altında

```js
import * as math from './math.js';

console.log(math.topla(2,3));  // 5
console.log(math.PI);         // 3.14
```

### Varsayılan import

```js
import cikar from './math.js';

console.log(cikar(5,2));  // 3
```

---

# 🌟 **3️⃣ ES6 Modül Özellikleri**

|Özellik|Açıklama|
|---|---|
|**Static structure**|import/export en üst seviyede (top-level) tanımlanmalı. Dinamik olmaz.|
|**Asenkron yükleme**|import'lar tarayıcı ve Node.js'te asenkron şekilde çalışır.|
|**Tarayıcı uyumlu**|Doğrudan `<script type="module">` ile kullanılabilir.|
|**Top-level await**|ES2022’den itibaren doğrudan modül dosyalarında await yazabilirsin.|
|**Tek bir default export**|Bir modülde sadece bir tane `export default` olabilir.|

---

# 🌟 **4️⃣ Node.js’te ES6 Modül Kullanımı**

Node.js’te ES6 modül kullanmak için:  
✅ `.mjs` uzantılı dosya yaz  
✅ **veya** `.js` uzantılı dosyada `package.json` içine `"type": "module"` koy

▶ **package.json**

json

```json
{
  "type": "module"
}
```

---

# 🌟 **5️⃣ ES6 Modül Örneği**

📂 Dizinin:

```lua
proje/
 ├── package.json  (type: module içerir)
 ├── math.js
 └── app.js
```

▶ **math.js**

```js
export function topla(a, b) {
  return a + b;
}

export default function(a, b) {
  return a - b;
}
```

▶ **app.js**

```js
import { topla } from './math.js';
import cikar from './math.js';

console.log(topla(5,3));  // 8
console.log(cikar(5,3));  // 2
```

---

# 🌟 **6️⃣ CommonJS ile ES6 Modül Farkları**

|Özellik|CommonJS (require/module.exports)|ES6 Modül (import/export)|
|---|---|---|
|**Yükleme tipi**|Senkron (require hemen döner)|Asenkron (import çalıştırılmadan önce yüklenir)|
|**Sözdizimi**|`const mod = require('...')`  <br>`module.exports = ...`|`import ... from ...`  <br>`export ...`|
|**Dosya tipi (Node.js)**|.js (varsayılan)|.mjs  <br>veya .js + `"type": "module"`|
|**Tarayıcı desteği**|Doğrudan desteklenmez|Tarayıcı ve Node.js uyumlu|
|**Top-level await**|Desteklemez|Destekler (ES2022+)|
|**Dinamik import**|require ile yapılabilir|`import()` ile yapılır (asenkron promise döner)|
|**Export yapısı**|module.exports her şeyi tanımlar|export/export default ayrı ayrı yazılır|
|**Analiz kolaylığı**|Daha az static analiz dostu|Static analiz ve ağaç sarsıntısı (tree-shaking) için mükemmel|

---

## 🎨 **Farkları Diyagramla Gösterelim**

```lua
CommonJS (Node.js özel):
+---------------------+
| module.exports = {}  |
| const mod = require()|
+---------------------+

ES6 Modül (JS standart):
+---------------------+
| export ...           |
| import ... from ...  |
+---------------------+
```

---

# 🌟 **7️⃣ Dinamik Import Farkı**

▶ **CommonJS**

```js
const fs = require('fs');
```

✅ Senkron, hemen döner.

▶ **ES6**

```js
const fs = await import('fs');
```

✅ Asenkron, promise döner.

---

# 🌟 **8️⃣ En iyi ne zaman hangisini kullanmalı?**

✅ **CommonJS kullan:**

- Sadece Node.js çalıştırıyorsan ve eski projelerle uyum istiyorsan
- Hızlı prototip ve eski paketlerle çalışıyorsan

✅ **ES6 Modül kullan:**

- Modern uygulamalar yazıyorsan
- Hem tarayıcı hem Node uyumlu bir yapı istiyorsan
- Tree-shaking (gereksiz kodları atma) istiyorsan
- Top-level await gibi modern özellikler istiyorsan

---

# 🌟 **9️⃣ Özet**

|                  | CommonJS         | ES6 Modül                      |
|:-----------------|:-----------------|:-------------------------------|
| Kullanım         | Node.js özel     | JS standardı (Node + tarayıcı) |
| Yükleme          | require, senkron | import, asenkron               |
| Tarayıcı desteği | ❌                | ✅                              |
| Static analiz    | Zor              | Kolay                          |
| Dosya tipi       | .js              | .mjs ya da .js + `type:module` |  

---

# 📝 **Sonuç**

💡 **CommonJS**: Node.js’in geleneksel modül sistemi. Hızlı, basit ama modern özelliklere uyumsuz.  
💡 **ES6 Modül**: Modern JS standardı, tarayıcı + Node uyumlu, future-proof.