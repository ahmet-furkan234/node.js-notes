
`post` middleware, Mongoose modelinde belirli bir işlem **sonrasında** otomatik olarak çalışan fonksiyonları tanımlamak için kullanılır.

Bu fonksiyonlar, veritabanı işlemi tamamlandıktan sonra tetiklenir.  
Genellikle **loglama**, **temizlik**, **bildirim gönderme** gibi işlemler için kullanılır.

---

## 🧠 Söz Dizimi

```js
schema.post(hook, function(doc, next) {
  // yapılacak işlem
  next();
});
```

- `hook`: Middleware’in tetikleneceği işlem adı (örn: `'save'`, `'remove'`, `'updateOne'`, `'findOneAndUpdate'`, vb.)
- `doc`: İşlem sonucu dönen belge (örneğin save sonrası kaydedilen belge)
- `next`: Middleware tamamlandığında çağrılan fonksiyon

---

## 🧪 Örnek 1 – Kayıt Sonrası Loglama

```js
userSchema.post('save', function(doc, next) {
  console.log(`${doc.name} başarıyla kaydedildi.`);
  next();
});
```

---

## 🧪 Örnek 2 – Silme Sonrası İşlem

```js
userSchema.post('remove', function(doc, next) {
  console.log(`${doc._id} ID'li kullanıcı silindi.`);
  next();
});
```

---

## 🔥 Desteklenen Hook’lar

|Hook İsmi|Açıklama|
|---|---|
|`save`|`save()` sonrası|
|`remove`|`remove()` sonrası|
|`updateOne`|`updateOne()` sonrası|
|`findOneAndUpdate`|`findOneAndUpdate()` sonrası|
|`insertMany`|`insertMany()` sonrası|

---

## 🧩 `post` Middleware Özellikleri

- `pre` middleware’in tam tersidir, işlem **tamamlandıktan sonra** çalışır.
- Genellikle yan etki (side effect) işlemleri için uygundur.
- `post` fonksiyonunda `next` parametresi zorunlu değildir ama callback pattern’ine uyum için tavsiye edilir.
- Eğer işlem sırasında hata yakalanacaksa, `pre` middleware tercih edilir.

---

## 🛠️ Asenkron `post` Middleware

```js
userSchema.post('save', async function(doc) {
  await sendNotification(doc.email);
});
```

---

## ❗ Özet

|Özellik|Açıklama|
|---|---|
|`schema.post()`|İşlem tamamlandıktan sonra çalışan middleware|
|Kullanım alanı|Loglama, bildirim, temizlik, diğer yan etkiler|
|`doc` parametresi|İşlem sonucunda dönen belge|
|Asenkron destek|Async/await ile kolayca kullanılabilir|
