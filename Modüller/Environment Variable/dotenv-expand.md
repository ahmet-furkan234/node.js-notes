
`dotenv-expand`, `.env` dosyası içinde **bir değişkeni başka bir değişkenin değeriyle referans almanı** sağlar. Yani `.env` içindeki değişkenlerin birbirini kullanmasına olanak verir.

---

# ⚙️ Nasıl Çalışır?

`dotenv` tek başına sadece düz key=value şeklinde okur.  
`dotenv-expand` ise `${VAR_NAME}` gibi ifadeleri genişletir.

---

# 📦 Kurulum

```bash
npm install dotenv dotenv-expand
```

---

# 🧪 Kullanım Örneği

### .env dosyası:

```env
BASE_URL=http://localhost:3000
API_ENDPOINT=${BASE_URL}/api
```

---

### index.js:

```js
import dotenv from 'dotenv';
import dotenvExpand from 'dotenv-expand';

const myEnv = dotenv.config();
dotenvExpand.expand(myEnv);

console.log(process.env.BASE_URL);       // http://localhost:3000
console.log(process.env.API_ENDPOINT);   // http://localhost:3000/api
```

---

# 📌 Açıklama:

- `dotenv.config()` `.env` dosyasını okur.
- `dotenvExpand.expand()` değişkenlerin içindeki `${...}` ifadelerini açar ve gerçek değerlerle değiştirir.
- `API_ENDPOINT` değişkeni artık `${BASE_URL}/api` ifadesi yerine gerçek URL olur.

---

# 🧠 Neden Kullanılır?

- Tekrar eden değerleri `.env` içinde kolayca kullanmak için.
- Daha temiz ve bakımı kolay `.env` dosyaları yazmak için.

---

# 🔍 Örnek Daha Karmaşık

```env
HOST=localhost
PORT=3000
BASE_URL=http://${HOST}:${PORT}
API_PATH=/api/v1
FULL_API_URL=${BASE_URL}${API_PATH}
```

Çıktı:

```js
console.log(process.env.FULL_API_URL);  
// http://localhost:3000/api/v1
```
