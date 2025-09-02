
## 📁 Örnek Proje Dosya Yapısı

```
my-env-demo/
├── index.js
├── .env
├── .env.development
├── .env.production
├── .env.development.local
├── .env.production.local
├── package.json
```

---

## 🟩 1. Dotenv ile Yapılandırma

### 📄 `.env.development`

```
API_URL=http://localhost:3000
```

### 📄 `.env.production`

```
API_URL=https://api.production.com
```

### 📄 index.js

```js
import dotenv from 'dotenv';

const envFile = `.env.${process.env.NODE_ENV || 'development'}`;
dotenv.config({ path: envFile });

console.log('API_URL:', process.env.API_URL);
```

> ### Çalıştırma

```bash
NODE_ENV=development node index.js
# Çıktı: API_URL: http://localhost:3000

NODE_ENV=production node index.js
# Çıktı: API_URL: https://api.production.com
```

> `.env.local`, `.env.production.local` gibi dosyaları desteklemez. Yüklemek istersen ayrıca `.config({ path: '...' })` yazman gerekir.

---

## 🟦 2. Dotenv-Flow ile Yapılandırma

### 📄 `.env` (ortak değer)

```
SHARED_KEY=abc123
```

### 📄 `.env.development`

```
API_URL=http://localhost:3000
```

### 📄 `.env.production`

```
API_URL=https://api.production.com
```

### 📄 `.env.production.local`

```
API_URL=https://api.production-override.com
```

### 📄 index.js

```js
import dotenvFlow from 'dotenv-flow';

dotenvFlow.config();

console.log('API_URL:', process.env.API_URL);
console.log('SHARED_KEY:', process.env.SHARED_KEY);
```

> ### Çalıştırma

```bash
NODE_ENV=development node index.js
# API_URL: http://localhost:3000
# SHARED_KEY: abc123

NODE_ENV=production node index.js
# API_URL: https://api.production-override.com
# SHARED_KEY: abc123
```

✅ `.env`, `.env.production`, `.env.production.local` **otomatik sıralı yüklenir**  
⛔ `config({ path: ... })` gerekmez

---

## 🔍 Karşılaştırmalı Avantajlar

|Özellik|`dotenv`|`dotenv-flow`|
|---|---|---|
|Ortam dosyası seçimi|Manuel (`path: ...`)|Otomatik `NODE_ENV` üzerinden|
|Yerel override desteği|Yok|Var (`.env.*.local`)|
|Ortak `.env` ile birleşim|Yok|Var|
|Kurulum|`dotenv`|`dotenv-flow`|
|Karmaşıklık|Basit|Bir tık daha gelişmiş|

---

## 📦 Kurulum Komutları

```bash
npm install dotenv        # Sadece dotenv
npm install dotenv-flow   # dotenv-flow ile gelişmiş destek
```

---

## Devam Edelim mi?

İstersen bu yapıların gerçek bir proje içinde **config.js**, **env.service.js** gibi ayrı modüllere nasıl taşındığını da gösterebilirim.  
Özellikle katmanlı projelerde `env` yapılandırmasını soyutlamak çok işine yarar.

Devam edelim mi? Yoksa sıradaki başka bir konuya geçelim mi?