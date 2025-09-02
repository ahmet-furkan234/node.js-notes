
`add()` metodu, **önceden tanımlanmış bir şemaya sonradan alanlar (paths)** eklemeni sağlar.

Bu, özellikle şemayı **modüler yapılarla bölmek**, **ortak alanları dış dosyalarda tanımlamak** ya da **dinamik alan eklemek** istediğinde çok işe yarar.

---

## 🧠 Söz Dizimi

```js
schema.add(schemaDefinitionObject);
```

---

## 🧪 Örnek 1 – Şemaya Sonradan Alan Ekleme

```js
import mongoose from 'mongoose';

const userSchema = new mongoose.Schema({
  name: String
});

// Sonradan email ve createdAt alanlarını ekledik
userSchema.add({
  email: {
    type: String,
    required: true,
    unique: true
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

const User = mongoose.model('User', userSchema);
```

---

## 🧪 Örnek 2 – Ortak Alanları Harici Dosyada Tanımlayıp Eklemek

### 🔹 `commonFields.js`

```js
// Ortak alanları tanımlıyoruz
export default {
  createdAt: {
    type: Date,
    default: Date.now
  },
  updatedAt: {
    type: Date,
    default: Date.now
  }
};
```

### 🔹 `userModel.js`

```js
import mongoose from 'mongoose';
import commonFields from './commonFields.js';

const userSchema = new mongoose.Schema({
  name: String,
  email: String
});

userSchema.add(commonFields); // ortak alanları ekledik

export default mongoose.model('User', userSchema);
```

---

## 🎯 Ne Zaman Kullanılır?

|Kullanım Durumu|Açıklama|
|---|---|
|Ortak alanları tekrar yazmamak için|Tüm modellerde `createdAt`, `updatedAt`, `status`, vs. gibi alanlar varsa|
|Şemayı dinamik olarak genişletmek için|Özellikle modüler veya plugin destekli sistemlerde|
|Kalıtım benzeri yapı kurmak için|Temel şemaya ek alanlar dahil etmek için|

---

## ❗ Notlar

- `add()` metodu **schema oluşturulduktan sonra çağrılır**.
- Eğer aynı ada sahip bir alan varsa, `add()` ile üzerine yazılır (bu dikkat edilmesi gereken bir noktadır).
- Derin (`nested`) alanlar da eklenebilir:

```js
schema.add({
  address: {
    city: String,
    country: String
  }
});
```

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`schema.add({})`|Şemaya sonradan alan ekler|
|Ortak alanlar|Harici bir dosyadan eklenebilir|
|Dinamik kullanım|Plugin/kalıtım sistemlerinde işe yarar|
