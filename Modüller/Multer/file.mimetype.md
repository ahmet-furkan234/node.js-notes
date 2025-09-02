
### 🖼️ **Görsel Dosyalar (Images)**

|Dosya Türü|MIME Type|
|---|---|
|JPEG|`image/jpeg`|
|PNG|`image/png`|
|GIF|`image/gif`|
|SVG|`image/svg+xml`|
|BMP|`image/bmp`|
|WEBP|`image/webp`|
|ICO|`image/x-icon`|

---

### 📄 **Doküman Dosyaları (Documents)**

|Dosya Türü|MIME Type|
|---|---|
|PDF|`application/pdf`|
|Word (.doc)|`application/msword`|
|Word (.docx)|`application/vnd.openxmlformats-officedocument.wordprocessingml.document`|
|Excel (.xls)|`application/vnd.ms-excel`|
|Excel (.xlsx)|`application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`|
|PowerPoint|`application/vnd.ms-powerpoint` veya `application/vnd.openxmlformats-officedocument.presentationml.presentation`|
|TXT|`text/plain`|
|CSV|`text/csv`|
|JSON|`application/json`|
|XML|`application/xml` veya `text/xml`|

---

### 🎵 **Ses Dosyaları (Audio)**

|Dosya Türü|MIME Type|
|---|---|
|MP3|`audio/mpeg`|
|WAV|`audio/wav`|
|OGG|`audio/ogg`|
|AAC|`audio/aac`|

---

### 🎬 **Video Dosyaları (Video)**

|Dosya Türü|MIME Type|
|---|---|
|MP4|`video/mp4`|
|AVI|`video/x-msvideo`|
|WebM|`video/webm`|
|MOV|`video/quicktime`|
|MKV|`video/x-matroska`|

---

### 📦 **Sıkıştırılmış Dosyalar (Archives)**

|Dosya Türü|MIME Type|
|---|---|
|ZIP|`application/zip`|
|RAR|`application/x-rar-compressed`|
|7Z|`application/x-7z-compressed`|
|TAR|`application/x-tar`|
|GZ|`application/gzip`|

---

## 🔍 Örnek Kullanım (`fileFilter` içinde)

```js
fileFilter: (req, file, cb) => {
  const allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
  if (allowedTypes.includes(file.mimetype)) {
    cb(null, true);
  } else {
    cb(new Error('Yalnızca JPEG, PNG veya PDF dosyalarına izin verilir.'));
  }
}
```

---

## 🎯 Notlar:

- `file.mimetype` her zaman güvenilir değildir. Dosya içerik kontrolü yapılmadan sadece uzantıya bakar.
- Gerçek güvenlik için dosya imzası (magic number) kontrolü gerekir. Örneğin `file-type` kütüphanesi kullanılabilir.
- İstemci tarafından gönderilen `Content-Type` header'ına bağlıdır, bu yüzden manuel olarak da değiştirilebilir.
