
`process.env`, Node.js'te bulunan **global bir nesnedir** ve uygulamanın çalıştığı **ortam değişkenlerini** (environment variables) tutar.

Bu nesne sayesinde `.env` dosyasından veya sistemden gelen tüm değerleri **okuyabilir**, bu değerlere göre uygulamanı **dinamik** hale getirebilirsin.

---

### 🔍 Basit Örnek

`.env` dosyası:

```env
PORT=3000
DB_PASSWORD=sifrem123
```

```js
// app.mjs
import dotenv from 'dotenv';
dotenv.config();

console.log(process.env.PORT);         // 3000
console.log(process.env.DB_PASSWORD);  // sifrem123
```

> `dotenv.config()` çağrısı ile `.env` dosyası yüklenmezse `process.env.PORT` `undefined` olur.

---

## 📌 Özellikler

| Özellik                        | Açıklama                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------- |
| `process.env`                  | Sadece string değerler tutar (sayısal veya boolean veriler bile string olur) |
| Globaldir                      | Her yerden erişilebilir                                                      |
| Değiştirilebilir               | `process.env.X = 'yeni değer'` yapılabilir ama önerilmez                     |
| Sadece okuma için kullanılmalı | `readonly` gibi davranılmalı                                                 |

---

### 🚫 Sayısal veya Boolean Değerler

```js
console.log(typeof process.env.PORT); // "string"
console.log(process.env.PORT + 1);    // "30001" çünkü string olarak işlem yapılır
```

Bu nedenle sayı olarak kullanmak için **parse etmelisin**:

```js
const port = parseInt(process.env.PORT, 10);
```

---

## 🔐 Gizli Bilgilerde Kullanımı

- API anahtarları, şifreler gibi değerleri kod içine yazmak yerine `.env` içine koy:

```env
DB_PASSWORD=mysecret
JWT_SECRET=abc123xyz
```

```js
const jwt = process.env.JWT_SECRET;
```

---

## 🧪 Sistem Ortam Değişkenleri (Terminal üzerinden)

`.env` kullanmadan da tanımlanabilir:

**Windows:**

```bash
set API_KEY=test123 && node app.js
```

**Linux/macOS:**

```bash
API_KEY=test123 node app.js
```

```js
console.log(process.env.API_KEY); // test123
```

---

## 🧰 Ortama Göre Davranış

```js
if (process.env.NODE_ENV === 'production') {
  console.log("Canlı ortamda çalışıyorum");
} else {
  console.log("Geliştirme ortamı");
}
```

`.env`:

```env
NODE_ENV=development
```

---

## ✅ Uygulama: config.js dosyası ile merkezi yapı

```js
// config.mjs
export const config = {
  port: parseInt(process.env.PORT) || 3000,
  env: process.env.NODE_ENV || 'development',
  dbPassword: process.env.DB_PASSWORD,
};
```

---

## 🔐 Güvenlik Uyarısı

- `.env` değerleri uygulama içinde asla **açık şekilde konsola yazılmamalı** (özellikle üretim ortamında).
- `.env` dosyası **hiçbir zaman sürüm kontrolüne dahil edilmemeli**.
