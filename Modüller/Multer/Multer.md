
Multer, `multipart/form-data` türündeki formlardan gelen **dosya verilerini** işler. Yani HTML formlarından veya Postman'dan resim, PDF, video gibi dosyalar gönderildiğinde bunları alır, işler ve sunucuda belirtilen dizine kaydeder.

---

## 🔧 1. Kurulum

```bash
npm install multer
```

---

## 🧠 2. Temel Kullanım (tek dosya)

```js
import express from 'express';
import multer from 'multer';

const app = express();

// Depolama ayarı
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, 'uploads/'); // klasör yoksa önceden oluşturmalısın
  },
  filename: (req, file, cb) => {
    cb(null, Date.now() + '-' + file.originalname);
  }
});

// Middleware oluştur
const upload = multer({ storage });

app.post('/upload', upload.single('image'), (req, res) => {
  res.json({ message: 'Dosya yüklendi', file: req.file });
});

app.listen(3000, () => console.log('Server çalışıyor'));
```

📌 `upload.single('image')`: formdaki input name="image" olan tek bir dosyayı işler.

---

## 🔁 3. Birden Çok Dosya (aynı alan adıyla)

```js
app.post('/upload-many', upload.array('photos', 5), (req, res) => {
  res.json({ files: req.files });
});
```

---

## 🧩 4. Farklı Alan Adlarıyla Çoklu Dosya

```js
app.post('/upload-mixed', upload.fields([
  { name: 'avatar', maxCount: 1 },
  { name: 'gallery', maxCount: 8 }
]), (req, res) => {
  res.json({ files: req.files });
});
```

---

## 🔒 5. Dosya Türü Kontrolü (`fileFilter`)

```js
const upload = multer({
  storage,
  fileFilter: (req, file, cb) => {
    if (file.mimetype === 'image/png' || file.mimetype === 'image/jpeg') {
      cb(null, true);
    } else {
      cb(new Error('Sadece JPEG ve PNG!'), false);
    }
  }
});
```

---

## 📏 6. Dosya Boyutu Sınırı

```js
const upload = multer({
  storage,
  limits: { fileSize: 1024 * 1024 * 2 } // Maks 2MB
});
```

---

## 📂 7. `req.file` ve `req.files` İçeriği

```json
{
  "fieldname": "image",
  "originalname": "logo.png",
  "encoding": "7bit",
  "mimetype": "image/png",
  "destination": "uploads/",
  "filename": "16910121123-logo.png",
  "path": "uploads/16910121123-logo.png",
  "size": 89283
}
```

---

## ❓ `cb` Nedir?

`cb` yani callback, Multer içinde:

- `cb(null, value)` → hata yoksa değer döndürür.
- `cb(err)` → hata varsa ilk argüman hata olmalı.

Örn:

```js
cb(null, 'uploads/') // başarılı dizin
cb(new Error('Geçersiz tip')) // hata fırlat
```

---

## 🧪 Test Etmek İçin

- Postman’da `POST /upload` isteği aç
- Body → form-data seç
- `Key = image`, `Type = File`, dosya seç
