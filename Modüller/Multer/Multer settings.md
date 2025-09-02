
## Multer `{}` İçindeki Ayarlar (Options)

### 1. **storage**

- Dosyaların nerede ve nasıl saklanacağını belirler.
- Varsayılan: `MemoryStorage` (RAM’de tutar, dosya oluşturmaz).
- En çok kullanılan: `diskStorage`

```js
const storage = multer.diskStorage({
  destination: (req, file, cb) => cb(null, 'uploads/'),
  filename: (req, file, cb) => cb(null, Date.now() + '-' + file.originalname)
});
```

Kullanımı:

```js
const upload = multer({ storage });
```

---

### 2. **limits**

- Yüklenen dosyalar için sınırlar koyar (boyut, dosya sayısı vs.)

|Özellik|Açıklama|Örnek|
|---|---|---|
|`fileSize`|Maksimum dosya boyutu (byte)|`1024 * 1024 * 5` (5MB)|
|`files`|Maksimum dosya sayısı|`5`|
|`fields`|Maksimum alan sayısı|`10`|
|`parts`|Maksimum toplam form parçası|`15`|
|`headerPairs`|Maks header sayısı|`2000`|

Örnek:

```js
const upload = multer({
  limits: { fileSize: 1024 * 1024 * 2 } // 2MB
});
```

---

### 3. **fileFilter**

- Dosya türünü kontrol eder ve kabul/reddeder.
- Fonksiyon: `(req, file, cb) => { ... }`

```js
const upload = multer({
  fileFilter: (req, file, cb) => {
    if (file.mimetype === 'image/png') cb(null, true);
    else cb(new Error('Yalnızca PNG yüklenebilir!'), false);
  }
});
```

---

### 4. **preservePath**

- Dosyanın orijinal yolunu (path) korur.
- Özellikle çoklu dosya yükleme esnasında klasör yapısı varsa kullanılır.
- Boolean, default `false`

```js
const upload = multer({ preservePath: true });
```

---

### 5. **limits.fileSize** (Tekrar vurgulama)

- Dosya boyutu sınırı, sunucuya aşırı yüklenmeyi önler.

---

### 6. **onFileUploadStart** (Eski sürümlerde)

- Yükleme başlamadan önce tetiklenir (artık resmi desteklenmiyor, middleware ile yapılır).

---

## Örnek Komple Multer Konfigürasyonu

```js
import multer from 'multer';

const storage = multer.diskStorage({
  destination: (req, file, cb) => cb(null, './uploads'),
  filename: (req, file, cb) => cb(null, Date.now() + '-' + file.originalname)
});

const upload = multer({
  storage,
  limits: { fileSize: 1024 * 1024 * 2, files: 5 },
  fileFilter: (req, file, cb) => {
    if (file.mimetype === 'image/jpeg' || file.mimetype === 'image/png') cb(null, true);
    else cb(new Error('Sadece JPEG ve PNG yüklenebilir'), false);
  }
});
```
