
👉 `path` modülü **dosya ve dizin yolları üzerinde çalışmak** için kullanılan yerleşik (built-in) bir Node.js modülüdür.  
👉 Platformlar arası (Windows, Linux, macOS) uyumlu yollar oluşturur.

💡 Örneğin:

- Windows: `C:\projem\app.js`
- Linux/macOS: `/home/user/projem/app.js`  
    `path` sayesinde bu farklarla uğraşmazsın, otomatik işler!

---

## 💻 **`path` modülünü kullanmak**

```js
const path = require('path');
```

---

## ⚡ **En çok kullanılan `path` fonksiyonları**

---

### 1️⃣ `path.join([...paths])`

👉 Parçaları birleştirip düzgün bir yol oluşturur.  
👉 Gereksiz `//` veya `\` karakterlerini düzeltir.

```js
const dosyaYolu = path.join(__dirname, 'data', 'veri.json');
console.log(dosyaYolu);
```

✅ Çıktı (örnek):

```js
/Users/tkmate/projem/data/veri.json
```

✅ Windows’ta:


```js
C:\Users\tkmate\projem\data\veri.json
```

---

### 2️⃣ `path.resolve([...paths])`

👉 Verilen yolları tam dosya yoluna (absolute path) dönüştürür.

```js
const tamYol = path.resolve('data', 'veri.json');
console.log(tamYol);
```

✅ Çıktı:

```js
/Users/tkmate/projem/data/veri.json  (bulunduğun dizine göre tam yol)
```

---

### 3️⃣ `path.basename(path)`

👉 Dosya adını döner.

```js
const dosyaAdi = path.basename('/Users/tkmate/projem/app.js');
console.log(dosyaAdi);  // app.js
```

---

### 4️⃣ `path.dirname(path)`

👉 Yolun klasör kısmını döner.

```js
const klasor = path.dirname('/Users/tkmate/projem/app.js');
console.log(klasor);  // /Users/tkmate/projem
```

---

### 5️⃣ `path.extname(path)`

👉 Dosya uzantısını döner.

```js
const uzanti = path.extname('/Users/tkmate/projem/app.js');
console.log(uzanti);  // .js
```

---

### 6️⃣ `path.parse(path)`

👉 Dosya yolunu parçalara ayırır (objeye).

```js
const detay = path.parse('/Users/tkmate/projem/app.js');
console.log(detay);
```

✅ Çıktı:

```js
{
  root: '/',
  dir: '/Users/tkmate/projem',
  base: 'app.js',
  ext: '.js',
  name: 'app'
}
```

---

### 7️⃣ `path.normalize(path)`

👉 Yoldaki fazlalıkları temizler (ör. çift `//`, `..`, `.` gibi).

```js
console.log(path.normalize('/Users//tkmate/../tkmate/projem//app.js'));
// /Users/tkmate/projem/app.js
```

---

## 📝 **Örnek: Dosya okurken path kullanımı**

```js
const fs = require('fs');
const path = require('path');

const dosyaYolu = path.join(__dirname, 'data', 'veri.txt');

fs.readFile(dosyaYolu, 'utf-8', (err, data) => {
    if (err) {
        console.error("Dosya okunamadı:", err);
        return;
    }
    console.log("Dosya içeriği:", data);
});
```

✅ Dosya yolu düzgün oluşturulur, her sistemde sorunsuz çalışır.

---

## 💡 **Özet tablo**

|Yöntem|Açıklama|
|---|---|
|`join`|Parçaları birleştirir, yolu düzeltir|
|`resolve`|Tam yol oluşturur|
|`basename`|Dosya adını döner|
|`dirname`|Klasör yolunu döner|
|`extname`|Dosya uzantısını döner|
|`parse`|Yolu obje şeklinde parçalar|
|`normalize`|Yolu temizler|

---

## 🎁 **Sonuç**

✅ `path` modülü dosya/dizin yollarında karmaşa yaşamamanı sağlar.  
✅ Platformlar arası uyumluluk için şarttır.  
✅ `join` ve `resolve` günlük kullanımda en sık kullanılan yöntemlerdir.