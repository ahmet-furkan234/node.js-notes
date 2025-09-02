
Environment variable, işletim sisteminin veya uygulamanın çalışırken okuyabileceği dışsal bir ayardır. Kodda sabit olarak yazmak yerine dışarıdan alınır.

### 📌 Örnekler:

```bash
PORT=3000
NODE_ENV=production
DB_PASSWORD=sifre123
```

---

## 🟩 Node.js Projesinde Environment Variable Kullanımı

### 1. `.env` Dosyası Oluştur

Proje dizinine bir `.env` dosyası koy:

```
.env
```

```env
PORT=4000
API_KEY=my-secret-api-key
NODE_ENV=development
```

> Bu dosya hiçbir zaman `git` ile paylaşılmaz! `.gitignore` içine eklenmeli:

```
.env
```

---

### 2. `dotenv` Paketi ile Okuma

#### 🔸 Kurulum:

```bash
npm install dotenv
```

#### 🔸 Kullanım (`.mjs` veya `"type": "module"` kullanarak):

```js
// config.mjs
import dotenv from 'dotenv';
dotenv.config();

console.log('Port:', process.env.PORT);
console.log('API Key:', process.env.API_KEY);
```

> `dotenv.config()` çağrısı `.env` dosyasını okuyup `process.env` içine değerleri yerleştirir.

---

## 🧠 `process.env` Nedir?

Node.js'in global değişkenlerinden biridir. `.env` olmasa da işletim sisteminden gelen değişkenleri tutar.

```js
console.log(process.env.USER);      // işletim sistemi kullanıcı adı
console.log(process.env.NODE_ENV); // development, production vs.
```

---

## 🧪 Gelişmiş Kullanım Örneği

```js
// server.mjs
import dotenv from 'dotenv';
dotenv.config();

import http from 'http';

const PORT = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
  res.end(`Sunucu ${PORT} portunda çalışıyor`);
});

server.listen(PORT, () => {
  console.log(`Server ${PORT} portunda başlatıldı`);
});
```

---

## ⚠️ Güvenlik Notu

- `.env` dosyasını `GitHub`, `Docker` gibi sistemlere göndermemelisin.
- `.env.example` adında bir şablon dosya oluşturabilirsin:

```env
# .env.example
PORT=YOUR_PORT
API_KEY=YOUR_API_KEY
```

---

## 🧰 Bonus: Ortama Göre Ayar (development vs production)

```js
if (process.env.NODE_ENV === 'development') {
  console.log('Geliştirme modundayız');
} else {
  console.log('Canlı moddayız');
}
```

---

Hazırsan sıradaki konu olarak `dotenv-expand`, `.env.production`, `cross-env`, veya `config` yapıları gibi ileri düzey `.env` kullanımına geçebiliriz. Devam edelim mi?