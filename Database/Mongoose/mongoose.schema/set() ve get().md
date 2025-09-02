
Mongoose’da her şema alanı (path), **setter** ve **getter** fonksiyonlarıyla özelleştirilebilir:

- **Setter (`set`)**: Bir alana değer atanırken o değeri değiştirmek veya işlemek için kullanılır.
- **Getter (`get`)**: Bir alandan değer okunurken, değeri değiştirmek veya işlemek için kullanılır.

---

## 🧠 Nerede Kullanılır?

- Veriyi veritabanına yazmadan önce (setter) formatlamak,
- Veriyi veritabanından okuduktan sonra (getter) biçimlendirmek,
- Özel dönüşümler yapmak.

---

## 🧪 Örnek 1 – Basit Setter Kullanımı

```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    set: v => v.trim()  // boşlukları otomatik sil
  }
});

const User = mongoose.model('User', userSchema);

const user = new User({ name: '  Ahmet  ' });
console.log(user.name); // 'Ahmet' (boşluklar otomatik silindi)
```

---

## 🧪 Örnek 2 – Getter ile Okunan Veriyi Formatlama

```js
const productSchema = new mongoose.Schema({
  price: {
    type: Number,
    get: v => v.toFixed(2)  // ondalık iki basamak göster
  }
});

const Product = mongoose.model('Product', productSchema);

const product = new Product({ price: 12.3456 });
console.log(product.price); // '12.35' (string olarak)
```

---

## 📌 Detaylı Kullanım

Setter ve getter fonksiyonları şema tanımlanırken `path` nesnesine şöyle atanır:

```js
schema.path('fieldName').set(function(value) {
  // işleme
  return yeniDeğer;
});

schema.path('fieldName').get(function(value) {
  // işleme
  return yeniDeğer;
});
```

---

## 🧪 Örnek 3 – `path()` ile Setter ve Getter Eklemek

```js
const userSchema = new mongoose.Schema({
  email: String
});

userSchema.path('email').set(function(value) {
  return value.toLowerCase();
});

userSchema.path('email').get(function(value) {
  return value.toUpperCase();
});

const User = mongoose.model('User', userSchema);

const user = new User({ email: 'TeSt@Example.Com' });
console.log(user.email); // 'TEST@EXAMPLE.COM' (okunurken büyük harf)
```

---

## 🧩 Setter ve Getter Arasındaki Fark

|İşlem|Ne Zaman Çalışır|Amaç|
|---|---|---|
|**Setter** (`set()`)|Model örneğine değer atanırken|Veriyi veritabanına kaydetmeden önce değiştirmek|
|**Getter** (`get()`)|Model örneğinden değer okunurken|Veriyi okunurken biçimlendirmek veya değiştirmek|

---

## ❗ Notlar

- Getter fonksiyonları genellikle **sadece model örneği üzerinde** çalışır, veritabanındaki gerçek veri etkilenmez.
- Setter fonksiyonları, veri veritabanına gitmeden önce işlenir.
- Getter’lar, JSON’a dönüştürme sırasında veya direkt alan okunurken devreye girer.

---

## ✅ Özet

|Metod|Kullanım|
|---|---|
|`schema.path('field').set(fn)`|Değer atanırken veriyi işler|
|`schema.path('field').get(fn)`|Değer okunurken veriyi işler|
