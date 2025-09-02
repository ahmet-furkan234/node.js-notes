
> `multipart/form-data` kullanan formlarda, **hiç dosya gönderilmediğinde** kullanılır.  
> Amaç: Multer'ın form verisini **parse edebilmesi** ve `req.body`'ye alabilmesi.

---

## 📌 Kullanımı

```js
upload.none()
```

---

## 🧪 Örnek Senaryo

### 📝 HTML (Frontend):

```html
<form action="/submit" method="POST" enctype="multipart/form-data">
  <input type="text" name="username" />
  <input type="email" name="email" />
  <button type="submit">Gönder</button>
</form>
```

### 📝 Express (Backend):

```js
import express from 'express';
import multer from 'multer';

const app = express();
const upload = multer(); // diskStorage yok, çünkü dosya yok

app.post('/submit', upload.none(), (req, res) => {
  console.log(req.body); // { username: 'TkMatE', email: 'tkmate@example.com' }
  res.send('Form verisi alındı');
});
```

---

## ❓ Neden `upload.none()`?

Çünkü `enctype="multipart/form-data"` kullanıldığında, `body-parser` ya da `express.urlencoded()` gibi middleware’ler form verisini **parse edemez**.  
İşte bu yüzden `upload.none()` devreye girer ve sadece metin verilerini yakalar.

---

## ⚠️ Uyarılar

|Durum|Açıklama|
|---|---|
|`enctype` boşsa|`upload.none()` gerekmez (çünkü veri zaten `application/x-www-form-urlencoded` olur)|
|Dosya gelirse|Hata verir: `"Unexpected file"`|
|`upload.none()` varsa|Formda **sadece metin alanları** olmalı|

---

## 🔐 Doğru Kullanım Örnekleri

|Amaç|Kullanım|
|---|---|
|Sadece kullanıcı adı/alınan bilgi|✅ `upload.none()`|
|Dosyasız form + `multipart/form-data`|✅ `upload.none()`|
|Dosya da gönderilecek|❌ `upload.none()` kullanma (yerine `upload.single`, `upload.array` vs.)|
