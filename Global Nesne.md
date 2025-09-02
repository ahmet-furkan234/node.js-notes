
Node.js'te `global` adlı bir nesne bulunur. Bu nesne, Node.js çalışma ortamında **her dosyada ve her fonksiyonda doğrudan erişilebilen değerleri ve fonksiyonları** içerir. Bu, tarayıcı ortamındaki `window` veya `self` nesnesine benzer bir yapıdadır.

✅ **Özellik:**  
Global nesnedeki bir değişken veya fonksiyon **require etmeye ya da import etmeye gerek kalmadan** her yerde kullanılabilir.

---

## 🚀 **Global Nesnenin Temel Özellikleri**

- Her Node.js modülü kendi kapsama alanında çalışır, ama `global` nesneye yazılanlar tüm modüllerden erişilebilir.
- `global` ile tanımlanan şeyler, dosya bazında değil, süreç (process) bazında global olur.
- Kapsam yönetimi açısından dikkatli kullanılmalıdır; gereksiz global değişkenler **çakışma ve hata** yaratabilir.

---

## 🌟 **Global Nesneye Dahil Olan Başlıca Üyeler**

### 1️⃣ **console**

`console.log`, `console.error`, `console.warn` gibi metodlar aslında global nesnededir.

```js
console.log("Merhaba Node.js!");
```

✅ `console` nesnesini herhangi bir yerde `require` etmeden doğrudan kullanabilirsin.

---

### 2️⃣ **setTimeout, setInterval, setImmediate**

Bu fonksiyonlar global nesneye dahildir:

```js
setTimeout(() => {
    console.log("1 saniye geçti");
}, 1000);

setInterval(() => {
    console.log("Her 2 saniyede bir çalışır");
}, 2000);

setImmediate(() => {
    console.log("Event loop'un sonraki aşamasında çalışır");
});
```

---

### 3️⃣ **process**

Node.js’in çalışma sürecini temsil eder.

```js
console.log(process.pid);  // Çalışan Node sürecinin ID'si
console.log(process.version);  // Node.js sürümü
```

✅ Tüm Node dosyalarından erişilebilen global bir nesnedir.

---

### 4️⃣ **__dirname ve __filename**

Her modülün kendi bulunduğu dizini ve dosya adını verir:

```js
console.log(__dirname);   // Dosyanın bulunduğu klasörün tam yolu
console.log(__filename);  // Dosyanın tam yolu
```

📝 Not: Bunlar `global` nesnesinin doğrudan bir üyesi değil ama global kapsamda tanımlıdır, her dosyada otomatik olarak bulunur.

---

### 5️⃣ **Buffer**

Node.js’in binary veriyle çalışmasını sağlayan sınıftır:

```js
const buf = Buffer.from("Merhaba");
console.log(buf);  // <Buffer 4d 65 72 68 61 62 61>
```

✅ Binary dosyalarla, veri akışıyla uğraşırken sıkça kullanılır.

---

### 6️⃣ **global**

Global nesneye kendisini temsil eden isimdir:

```js
global.a = 42;
console.log(global.a);  // 42
console.log(a);         // 42 (ama kullanımı önerilmez)
```

---

## 🌈 **Global Nesneye Yeni Değer Eklemek**

```js
global.customValue = "Bu bir global değişkendir";
console.log(customValue);  // "Bu bir global değişkendir"
```

💡 **Neden tavsiye edilmez?**  
Çünkü uygulaman büyüdükçe hangi dosyada hangi global değişken tanımlandı, hangisi üzerine yazıldı takibi zorlaşır ve hata yapma riski artar.

---

## 📝 **Global Nesne İle window Farkı**

| Özellik             | Tarayıcı (window) | Node.js (global)                                           |
| ------------------- | ----------------- | ---------------------------------------------------------- |
| Çalışma ortamı      | Tarayıcı          | Sunucu (Node.js)                                           |
| DOM erişimi         | Evet              | Hayır                                                      |
| Modül kapsama alanı | Tek global alan   | Her dosya modül, ama global nesne tüm modüllerden erişilir |
| Global nesne adı    | `window`          | `global`                                                   |

---

## 🔑 **Örnek: global değişken tanımlama ve erişim**

```js
// dosya1.js
global.sharedVar = "Ben tüm dosyalardan erişilebilirim";

// dosya2.js
console.log(global.sharedVar);  // "Ben tüm dosyalardan erişilebilirim"
```

