
`pre` middleware, Mongoose modelinde belirli bir işlem **öncesinde** otomatik olarak çalışan fonksiyonları tanımlamak için kullanılır.

Bu fonksiyonlar, veritabanına veri kaydetmeden önce, güncellemeden önce veya başka işlemlerden önce tetiklenir.  
Genellikle **doğrulama**, **hashleme**, **loglama** gibi işlemler için kullanılır.

---

## 🧠 Söz Dizimi

```js
schema.pre(hook, function(next) {
  // yapılacak işlem
  next();
});
```

- `hook`: Middleware’in tetikleneceği işlem adı (örn: `'save'`, `'updateOne'`, `'remove'`, `'validate'` vb.)
    
- `next`: Middleware tamamlandığında çağrılan fonksiyon
    

---

## 🧪 En Yaygın Kullanım – `save` Öncesi Hashleme

```js
import mongoose from 'mongoose';
import bcrypt from 'bcryptjs';

const userSchema = new mongoose.Schema({
  username: String,
  password: String,
});

// save işlemi öncesi password hashle
userSchema.pre('save', async function(next) {
  if (!this.isModified('password')) return next();

  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);

  next();
});

const User = mongoose.model('User', userSchema);
```

---

## 🔥 Diğer Yaygın `pre` Hook’ları

|Hook İsmi|Açıklama|
|---|---|
|`save`|`save()` çağrılmadan önce|
|`validate`|Validasyon öncesinde|
|`remove`|`remove()` öncesinde|
|`updateOne`|`updateOne()` öncesinde|
|`findOneAndUpdate`|`findOneAndUpdate()` öncesinde|
|`insertMany`|Çoklu ekleme işlemi öncesinde|

---

## 🧪 Örnek – Güncelleme Öncesi Middleware

```js
userSchema.pre('findOneAndUpdate', function(next) {
  this.set({ updatedAt: new Date() }); // updatedAt alanını güncelle
  next();
});
```

---

## 🧩 Middleware Fonksiyonunun `this` Bağlamı

- `pre('save')` içinde `this`, o an kaydedilen belgeyi gösterir.
    
- `pre('updateOne')` veya `pre('findOneAndUpdate')` içinde `this`, query objesidir.
    

Bu yüzden kullanım şekilleri farklıdır.

---

## 🛠️ Asenkron Middleware

`pre` fonksiyonları, ya callback (`next`) ile ya da async/await ile yazılabilir:

```js
schema.pre('save', async function() {
  await someAsyncOperation();
});
```

---

## ❗ Özet

|Özellik|Açıklama|
|---|---|
|`schema.pre()`|Belirli işlemlerden önce çalışan middleware tanımlar|
|Yaygın kullanım|Hashleme, validasyon, loglama, tarih güncelleme|
|`this` bağlamı|Hook türüne göre değişir (document ya da query)|
|Asenkron destek|Callback veya async/await ile yazılabilir|

---

İstersen `post` middleware, `virtual` alanlar veya başka schema metodlarına da geçebiliriz.  
Hangi konu ile devam etmek istersin?