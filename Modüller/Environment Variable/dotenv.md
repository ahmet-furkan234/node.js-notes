
`.env` dosyasında tanımladığın değişkenleri, Node.js içindeki `process.env` nesnesine **otomatik aktarmaya yarar**.

```bash
npm install dotenv
```

---

## 🧪 Basit Kullanım

### 1. `.env` dosyası oluştur:

```
PORT=3000
API_KEY=xyz123
```

### 2. `dotenv` modülünü projenin en başında çağır:

```js
// app.mjs (veya app.js)
import dotenv from 'dotenv';
dotenv.config(); // .env dosyasını yükle

console.log(process.env.PORT);     // 3000
console.log(process.env.API_KEY);  // xyz123
```

> `dotenv.config()` çağrısı yapılmazsa `process.env.PORT` **undefined** olur.

---

## 🧩 `.env` Dosyası Formatı

```env
# Yorum satırı
PORT=3000
DEBUG=true
API_KEY="abc xyz"
FULL_NAME=TkMatE
```

- Boşluk varsa `"çift tırnak"` kullanmalısın.
- `#` ile yorum yazılabilir.
- Satır başı ve sonu boşluklar yok sayılır.

---

## 📁 Dosya Konumu

`.env` genelde `root` klasörde olur:

```
my-project/
│
├─ .env
├─ app.mjs
```

Ama istersen özel bir dosya da belirtebilirsin:

```js
dotenv.config({ path: './config/.env.prod' });
```

---

## 📦 Dotenv ile Uygulama Ortamını Yönetme (NODE_ENV)

```env
NODE_ENV=development
```

```js
if (process.env.NODE_ENV === 'production') {
  console.log("Canlı ortamdayız");
} else {
  console.log("Geliştirme ortamı");
}
```

---

## 🧠 Gelişmiş Yapı: Merkezi Config

### `config.mjs`

```js
import dotenv from 'dotenv';
dotenv.config();

export const config = {
  port: parseInt(process.env.PORT, 10) || 3000,
  apiKey: process.env.API_KEY,
  dbPassword: process.env.DB_PASSWORD
};
```

### `server.mjs`

```js
import { config } from './config.mjs';

console.log(`Sunucu ${config.port} portunda çalışıyor`);
```

---

## ❗ Güvenlik ve `.gitignore`

`.env` dosyası asla Git'e gönderilmemeli. `.gitignore` dosyana ekle:

```
.env
```

---

## 🔁 Çoklu Ortamlar İçin Kullanım

Projende farklı `.env` dosyaları olabilir:

```
.env.development
.env.production
.env.test
```

Ve `dotenv`'i ortam değişkenine göre yönlendirebilirsin:

```js
import dotenv from 'dotenv';

const envFile = `.env.${process.env.NODE_ENV || 'development'}`;
dotenv.config({ path: envFile });
```

---

## ⏭️ İleri Seviye: `dotenv-expand`, `dotenv-flow`

İstersen bu araçlarla `.env` içinde başka değişkenleri referans alabilir, `.env.defaults` gibi yapılar kurabilirsin.
