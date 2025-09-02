
Multer’da `upload.fields()` fonksiyonu, **birden fazla dosya alanı** (field) içeren formlar için kullanılır. Yani formda birden fazla `input[type="file"]` varsa ve her biri farklı `name` alanına sahipse bu yöntem kullanılır.

---

## 📌 Kullanımı

```js
upload.fields([
  { name: 'avatar', maxCount: 1 },
  { name: 'gallery', maxCount: 3 }
])
```

Bu örnekte:

- `avatar` alanına **en fazla 1** dosya yüklenebilir.
- `gallery` alanına **en fazla 3** dosya yüklenebilir.

---

## 🧪 Örnek Kullanım

### 📝 HTML (Frontend):

```html
<form action="/upload" method="POST" enctype="multipart/form-data">
  <input type="file" name="avatar" />
  <input type="file" name="gallery" multiple />
  <button type="submit">Yükle</button>
</form>
```

### 📝 Express (Backend):

```js
import express from 'express';
import multer from 'multer';

const app = express();
const upload = multer({ dest: 'uploads/' });

app.post(
  '/upload',
  upload.fields([
    { name: 'avatar', maxCount: 1 },
    { name: 'gallery', maxCount: 3 }
  ]),
  (req, res) => {
    console.log(req.files);

    res.send('Dosyalar yüklendi');
  }
);
```

---

## 🧾 `req.files` Nasıl Görünür?

```js
{
  avatar: [
    {
      fieldname: 'avatar',
      originalname: 'avatar.jpg',
      encoding: '7bit',
      mimetype: 'image/jpeg',
      destination: 'uploads/',
      filename: '1691081900000-avatar.jpg',
      path: 'uploads/1691081900000-avatar.jpg',
      size: 12345
    }
  ],
  gallery: [
    {
      fieldname: 'gallery',
      originalname: 'photo1.jpg',
      ...
    },
    {
      fieldname: 'gallery',
      originalname: 'photo2.jpg',
      ...
    }
  ]
}
```

### Yani:

- `req.files.avatar` → tek bir dosya içeren dizi
- `req.files.gallery` → birden fazla dosya içeren dizi

---

## 💡 Ne Zaman Kullanılır?

|Senaryo|Kullanım|
|---|---|
|Farklı dosya alanları varsa|✅ `upload.fields()`|
|Tek bir alan, çoklu dosya|➡️ `upload.array()`|
|Tek bir alan, tek dosya|➡️ `upload.single()`|
