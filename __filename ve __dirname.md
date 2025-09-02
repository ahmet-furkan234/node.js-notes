
Node.js'de her dosya bir **modül** olarak çalıştırılır. Node, bu modül için bazı özel değişkenler sağlar. İşte bunlardan ikisi:

|Değişken|Ne işe yarar?|
|---|---|
|`__filename`|Şu anda çalışmakta olan dosyanın tam dosya yolunu verir.|
|`__dirname`|Şu anda çalışmakta olan dosyanın bulunduğu klasörün tam yolunu verir.|

---

## 📝 **Örnek Kullanım**

Diyelim projenin dizin yapısı şöyle:

```bash
/projem
 └── app.js
```

Ve `app.js` içinde şunu yazalım:

```js
console.log("__filename:", __filename);
console.log("__dirname :", __dirname);
```

Eğer bu dosyayı şöyle çalıştırırsan:

```js
node app.js
```

Mesela çıktın şöyle olabilir:

```js
__filename: /Users/tkmate/projem/app.js
__dirname : /Users/tkmate/projem
```

---

## ⚡ **Ne Zaman Kullanılır?**

👉 **Dosya veya klasör yollarını bulmak için:**  
Örneğin başka bir dosyayı açarken ya da bir dosya yolu oluştururken:

```js
const path = require('path');
const dosyaYolu = path.join(__dirname, 'data', 'veri.json');
console.log(dosyaYolu);
```

> Bu: `/Users/tkmate/projem/data/veri.json` gibi bir tam yol oluşturur.

👉 **Hangi dosyada çalıştığını bilmek için:**  
Debug sırasında dosyanın yerini öğrenmek isteyebilirsin.

---

## ⚠️ **Dikkat Edilecek Noktalar**

✅ `__filename` ve `__dirname` sadece **Node.js** içinde çalışır.  
✅ Tarayıcıda (`browser`) çalışmaz, çünkü tarayıcıda dosya sistemi yoktur.  
✅ Modül sisteminin bir parçasıdır ve her dosyada kendi değerini alır.

---

## 💡 **Basit Diyagram**

```js
/Users/tkmate/projem/
 ├── app.js
```

```js
// app.js içindeyiz
console.log(__dirname);  // /Users/tkmate/projem
console.log(__filename); // /Users/tkmate/projem/app.js
```

---
## 🔑 **Özet**

|Değişken|Açıklama|
|---|---|
|`__filename`|Çalışan dosyanın tam yolu|
|`__dirname`|Çalışan dosyanın bulunduğu klasörün tam yolu|