
### 📦 Kurulum

```bash
npm install dotenv-flow dotenv-expand
```

---

### 📁 Örnek `.env` Dosyaları

**`.env`**

```env
HOST=localhost
PORT=3000
BASE_URL=http://${HOST}:${PORT}
```

**`.env.development`**

```env
API_PATH=/api/dev
FULL_API_URL=${BASE_URL}${API_PATH}
```

**`.env.production`**

```env
API_PATH=/api/prod
FULL_API_URL=${BASE_URL}${API_PATH}
```

---

### 📄 `config/env.js`

```js
import dotenvFlow from 'dotenv-flow';
import dotenvExpand from 'dotenv-expand';

const myEnv = dotenvFlow.config();
dotenvExpand.expand(myEnv);

export const env = {
  nodeEnv: process.env.NODE_ENV || 'development',
  fullApiUrl: process.env.FULL_API_URL,
  port: parseInt(process.env.PORT, 10) || 3000,
};
```

---

### 📄 `src/index.js`

```js
import { env } from '../config/env.js';

console.log('Ortam:', env.nodeEnv);
console.log('Tam API URL:', env.fullApiUrl);
console.log('Port:', env.port);
```

---

### 📋 Çalıştırma

```bash
NODE_ENV=development node src/index.js
# Tam API URL: http://localhost:3000/api/dev

NODE_ENV=production node src/index.js
# Tam API URL: http://localhost:3000/api/prod
```

---

## 🎯 Özet

- `dotenv-flow` çoklu `.env` dosyalarını ortam bazlı otomatik yüklüyor.
    
- `dotenv-expand` ise `.env` içindeki `${VAR}` referanslarını çözüyor.
    
- Birlikte kullanıldığında ortam bağımlı ve referanslı çevresel değişkenleri kolayca yönetebilirsin.
    

---

İstersen şimdi bu yapı için **hata yönetimi**, **eksik değişken kontrolü** veya **`cross-env` ile platform bağımsız ortam ayarı** gibi konulara geçebiliriz. Ya da başka bir konuda devam etmek istersen söyle!