
`schema.statics`, Mongoose modellerinin **sınıf (class) metotları** olarak, yani **model seviyesinde** tanımlanan metotları ifade eder.

- Bu metotlar, model üzerinde doğrudan çağrılır (örneğin `User.findByEmail()` gibi).
- Model genelinde kullanılan yardımcı fonksiyonlar için uygundur.

---

## 🧠 Nasıl Çalışır?

- `schema.statics` nesnesine metotlar eklenir.
- Bu metotlar model (class) üzerinde çağrılır, bir belge örneği (document) değil.

---

## 🧪 Örnek 1 – Statik Metot Tanımlama

```js
const userSchema = new mongoose.Schema({
  email: String,
  name: String,
});

// Email ile kullanıcı bulmak için statik metot
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email });
};

const User = mongoose.model('User', userSchema);

(async () => {
  const user = await User.findByEmail('test@example.com');
  console.log(user);
})();
```

---

## 🧪 Örnek 2 – Karmaşık Statik Metot

```js
userSchema.statics.findActiveUsers = function() {
  return this.find({ isActive: true });
};
```

---

## 🧩 `statics` ile Neler Yapılır?

- Model genelinde kullanılacak sorgu metotları,
- Özel filtreleme, toplu işlemler,
- Yardımcı fonksiyonlar, fabrika metotları

---

## 🔥 Avantajları

- Modelin doğrudan kendisine metot ekler,
- Kod organizasyonu sağlar,
- Tekrar eden sorgular ve işlemler için kolaylık.

---

## ❗ Notlar

- `statics` metotları **model üzerinde**, `methods` ise **document üzerinde** çalışır.
- Statik metotlar async/await destekler.

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`schema.statics`|Model seviyesinde (class metotları) tanımlar|
|`this`|Metot içinde modeli ifade eder|
|Kullanım|`User.staticMethodName()` şeklinde çağrılır|
