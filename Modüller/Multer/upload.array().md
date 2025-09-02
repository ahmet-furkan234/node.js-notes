
Bir formda yalnızca **bir dosya alanı (örneğin `images`)** varsa ve bu alandan **birden fazla dosya** yüklenebiliyorsa, `upload.array()` kullanılır.

---

## 📌 Kullanımı

```js
upload.array(fieldname, maxCount)
```

- `fieldname`: `<input type="file" name="images" multiple>` içindeki `name` değeri
- `maxCount`: Maksimum kaç dosya kabul edileceği

---

## 🧪 Örnek Kullanım

### 📝 HTML (Frontend):

```html
<form action="/upload" method="POST" enctype="multipart/form-data">
  <input type="file" name="photos" multiple />
  <button type="submit">Yükle</button>
</form>
```

### 📝 Express (Backend):

```js
import express from 'express';
import multer from 'multer';

const app = express();
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.array('photos', 5), (req, res) => {
  console.log(req.files); // Tüm dosyalar burada dizide
  res.send('Dosyalar yüklendi');
});
```

---

## 🔍 `req.files` Nasıl Görünür?

`upload.array()` kullandığında `req.files` doğrudan **dizi (array)** olur:

```js
[
  {
    fieldname: 'photos',
    originalname: 'pic1.jpg',
    mimetype: 'image/jpeg',
    destination: 'uploads/',
    filename: '1691081900000-pic1.jpg',
    path: 'uploads/1691081900000-pic1.jpg',
    size: 20000
  },
  {
    fieldname: 'photos',
    originalname: 'pic2.jpg',
    ...
  }
]
```

---

## ⚠️ Notlar

- Formda `<input name="photos" multiple>` olmalı
- Maksimum sayıda dosya sınırını `upload.array('photos', 5)` ile belirleyebilirsin
- Dosya uzantısı ve boyut sınırlama gibi kontrolleri ayrıca ayarlarsın (istersen birazdan onları da gösteririm)

---

## 🤔 Ne Zaman `upload.array()` Kullanılır?

|Senaryo|Yöntem|
|---|---|
|Tek input, çoklu dosya|✅ `upload.array()`|
|Birden fazla input, her biri farklı adla|➡️ `upload.fields()`|
|Tek dosya yüklenecek|➡️ `upload.single()`|
