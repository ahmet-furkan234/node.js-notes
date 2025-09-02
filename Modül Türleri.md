
Modül = Node.js’te **kodları parçalara bölmek** ve bu parçaları **içe/dışa aktarmak** için kullanılan birimlerdir.  
Her Node dosyası aslında bir modüldür.

---

## 🧩 **Node.js Modül Türleri**

Node.js’te modüller 3 ana kategoriye ayrılır:

|Modül Türü|Açıklama|
|---|---|
|**Yerleşik (Built-in)**|Node.js’in kendi sağladığı hazır modüller.|
|**Kullanıcı Tanımlı**|Kendi yazdığın dosyalar (ör. `math.js`, `app.js`).|
|**Üçüncü Parti (3rd Party)**|NPM’den yüklediğin modüller (ör. `express`, `axios`).|

---

## 1️⃣ **Yerleşik (Built-in) Modüller**

Node.js ile birlikte gelir, kurulum gerekmez.

🔹 Örnekler:

- `fs` (file system) → Dosya işlemleri
- `http` → Sunucu kurmak
- `path` → Dosya ve dizin yollarını işlemek
- `os` → İşletim sistemi bilgisi almak

🔹 Örnek:

```js
const fs = require('fs');

fs.writeFileSync('deneme.txt', 'Merhaba Node.js');
```

---

## 2️⃣ **Kullanıcı Tanımlı Modüller**

Kendi oluşturduğun `.js` dosyalarıdır.  
Bu dosyaları `require` veya `import` ile içe aktarabilirsin.

🔹 Örnek:  
`math.js`

```js
function topla(a, b) {
  return a + b;
}
module.exports = { topla };
```

`app.js`

```js
const math = require('./math');
console.log(math.topla(3, 5));  // 8
```

> **Not:** `./` yazmayı unutma, kendi dosyan olduğunda şart!

---

## 3️⃣ **Üçüncü Parti (NPM Modülleri)**

Node.js topluluğu tarafından yazılmış modüller.  
NPM (Node Package Manager) üzerinden yüklenir.

🔹 Örnek:

```bash
npm install axios
```

`app.js`

```js
const axios = require('axios');

axios.get('https://api.quotable.io/random')
  .then(res => console.log(res.data))
  .catch(err => console.error(err));
```

---

## ⚡ **Modül Sistemleri Türleri (Ekstra Bilgi)**

Node.js’te modüller iki farklı sistemle yazılabilir:

|Sistem|Açıklama|Dosya uzantısı|
|---|---|---|
|**CommonJS**|`require`, `module.exports` kullanır.|`.js`|
|**ES6 Module (ESM)**|`import`, `export` kullanır.|`.mjs` (veya `type: module`)|

🔹 CommonJS:

```js
const fs = require('fs');
module.exports = { topla };
```

🔹 ES6 Module:

```js
import fs from 'fs';
export function topla(a, b) { return a + b; }
```

> **Not:** ES6 modül için dosya uzantısı `.mjs` olmalı ya da `package.json` içinde:

```json
{ "type": "module" }
```

---

## 📝 **Özet Tablo**

|Modül Türü|Nereden Gelir?|Nasıl Kullanılır?|
|---|---|---|
|Yerleşik|Node.js’in içinde hazır gelir|`const fs = require('fs');`|
|Kullanıcı Tanımlı|Kendi yazdığın dosyalar|`const m = require('./modul.js');`|
|Üçüncü Parti|NPM’den kurarsın|`const axios = require('axios');`|

---

## 🎁 **Sonuç**

✅ Node.js modüllerle kodu parçalar ve yönetilebilir hale getirir.  
✅ Üç tür modül vardır: Yerleşik, kullanıcı tanımlı, üçüncü parti.  
✅ Modül sistemleri: **CommonJS** (require), **ES6 module** (import).