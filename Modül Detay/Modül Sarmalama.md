# 🚀 **Bu yapı nedir?**

```js
(function (exports, require, module, __filename, __dirname) {
  // senin dosyan
});
```

👉 **Node.js’in her dosyayı sarmaladığı (wrap ettiği) bir fonksiyondur.**

Node.js bir dosyayı okuduğunda, onu bir modül haline getirirken şöyle bir fonksiyon içine alır.  
Bu sayede:  
✅ Dosya kendi kapsama alanına (scope) sahip olur.  
✅ Global değişkenler tanımlanmadan dosya içindeki değişkenler korunur.  
✅ Modül sistemini (`exports`, `module.exports`, `require`) sağlar. 

---

# 🌟 **Aslında Node.js şu işlemi yapar:**

Sen dosyaya şunu yazmış olsan:

```js
console.log("Merhaba");
```

Node.js bunu şöyle işler:

```js
(function (exports, require, module, __filename, __dirname) {
  console.log("Merhaba");
});
```

Ve bunu çağırır:

```js
(function (exports, require, module, __filename, __dirname) {
  console.log("Merhaba");
})(exportsObj, requireFunction, moduleObj, "/tam/yol/dosya.js", "/tam/yol");
```

---

# 🌟 **Bu sayede Node.js sana şunları sağlar:**

|Parametre|Görev|
|---|---|
|`exports`|Modülden dışarı verilecek özellikleri tanımlaman için boş bir nesne|
|`require`|Başka modülleri çağırmanı sağlayan fonksiyon|
|`module`|Modülün kendisini ve `module.exports`'u temsil eder|
|`__filename`|O anki dosyanın tam yolu|
|`__dirname`|O anki dosyanın bulunduğu dizin yolu|

---

# 🔑 **Neden böyle bir sarmalama yapılıyor?**

✅ Her dosyanın kendi kapsamı olur, değişkenler global scope’u kirletmez.  
✅ Modül sistemi (require, exports) otomatik olarak her dosyada hazır olur.  
✅ Dosya konumu bilgileri (__dirname, __filename) hazır olur.

---

# 🎨 **Basit görselleştirme**

Senin dosyan:

```
const fs = require('fs');
console.log("Merhaba");
```

Node.js aslında şöyle yapıyor:

```js
(function(exports, require, module, __filename, __dirname) {
    const fs = require('fs');
    console.log("Merhaba");
})(...değerler...)
```

---

# 📌 **Bunun sonucu olarak**

- Dosyanın içi bir **modül kapsama alanında** çalışır.
- `var`, `let`, `const` ile tanımladığın değişkenler **global değil, dosya içi değişkenlerdir**.
- Sen aslında modülünün içini bir fonksiyonun içindeymiş gibi yazıyorsun.

---

# 💡 **Avantajları**

✅ Güvenli bir kapsama alanı sağlar.  
✅ Modül sistemi otomatik gelir.  
✅ Aynı isimde değişkenler farklı dosyalarda çakışmaz.

---

# ⚠ **Sen bunu göremezsin**

Node.js bunu perde arkasında yapar.  
Sen dosyana `function(...)` yazmazsın, ama Node.js bunu senin için hazırlar.

---

# 📝 **Sonuç olarak**

👉 **Bu yapı, modül sisteminin temelidir.**  
👉 **Her dosyanın izole edilmesini ve modüler olmasını sağlar.**  
👉 **`require`, `exports`, `module.exports`, `__filename`, `__dirname` gibi şeylerin otomatik kullanılabilmesini sağlar.**