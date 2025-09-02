
`upload.single('file')`, Multer'ın **tek bir dosya** yüklemek için kullandığı middleware fonksiyonudur.

```js
upload.single(fieldname)
```

### 📌 Parametre: `fieldname`

- Bu, HTML formundaki `<input type="file" name="file" />` kısmındaki `name` özelliğidir.
- Yani `upload.single('file')` demek, `name="file"` olan bir dosya alanını kabul et demektir.

---

## 🧪 Basit Örnek

### 📝 Frontend (HTML Form):

```html
<form action="/upload" method="POST" enctype="multipart/form-data">
  <input type="file" name="file" />
  <button type="submit">Yükle</button>
</form>
```

### 📝 Backend (Node.js + Express):

```js
import express from 'express';
import multer from 'multer';

const app = express();
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
  console.log(req.file); // Tek dosya objesi
  res.send('Dosya yüklendi!');
});
```

---

## 🎯 `req.file` Objesi Ne İçerir?

`upload.single()` kullandığında dosya bilgisi `req.file` içine yerleştirilir. Örneğin:

```json
{
  "fieldname": "file",
  "originalname": "ornek.png",
  "encoding": "7bit",
  "mimetype": "image/png",
  "destination": "uploads/",
  "filename": "1691081900000-ornek.png",
  "path": "uploads/1691081900000-ornek.png",
  "size": 20345
}
```

---

## 💡 Notlar

|Özellik|Açıklama|
|---|---|
|`fieldname`|Formdaki `name` değeri|
|`originalname`|Kullanıcının yüklediği orijinal dosya ismi|
|`mimetype`|`image/png`, `application/pdf` gibi dosya türü|
|`destination`|Yükleneceği klasör|
|`filename`|Sunucuda saklanan dosya adı (genellikle random)|
|`path`|Dosyanın tam yolu|
|`size`|Byte cinsinden boyut|

---

## ✅ Ne Zaman Kullanılır?

- Profil fotoğrafı gibi **tek bir dosya** yüklenecekse.
- Basit ve hızlı bir dosya upload işlemi gerekiyorsa.
