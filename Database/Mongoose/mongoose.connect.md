
## 🔌 Mongoose Connection – Temel Bilgi

MongoDB ile Mongoose üzerinden bağlantı kurmak için şu komutu kullanırız:

```js
import mongoose from 'mongoose';

mongoose.connect('mongodb://localhost:27017/mydatabase')
  .then(() => console.log('MongoDB bağlantısı başarılı'))
  .catch(err => console.error('Bağlantı hatası:', err));
```

---

## 📚 `mongoose.connect()` Ayarları

### Temel Parametreler:

```js
mongoose.connect(uri, options)
```

- **`uri`**: MongoDB bağlantı URI’si. Örnek:  
    `mongodb://localhost:27017/mydb`  
    veya bulutta:  
    `mongodb+srv://username:password@cluster.mongodb.net/mydb`
- **`options`**: İsteğe bağlı yapılandırmalar.

### Örnek:

```js
mongoose.connect('mongodb://localhost:27017/myapp', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

---

## ⚙️ Sık Kullanılan `connect` Seçenekleri

|Seçenek|Açıklama|
|---|---|
|`useNewUrlParser`|Yeni URL parçalayıcıyı kullanır. (Zorunlu hale geldi)|
|`useUnifiedTopology`|Yeni bağlantı izleyiciyi kullanır (soket, replica vs. için).|
|`dbName`|URL'den farklı bir veritabanı adı belirtmek için|
|`authSource`|Kimlik doğrulama yapılacak DB adı|
|`user`, `pass`|Kullanıcı adı ve şifre ayrı verilirse|

---

## 🧠 Bağlantı Olayları (Events)

Mongoose bağlantı nesnesi üzerinden olaylar (events) dinlenebilir:

```js
const db = mongoose.connection;

db.on('connected', () => console.log('✅ Mongoose bağlandı'));
db.on('error', (err) => console.log('❌ Hata:', err));
db.on('disconnected', () => console.log('⚠️ Mongoose bağlantısı koptu'));
```

---

## 🛠️ Otomatik Yeniden Bağlanma (Reconnection)

Mongoose, bağlantı koparsa **otomatik yeniden bağlanmaya çalışır.**  
Ancak istersen kendin özel işlem tanımlayabilirsin:

```js
mongoose.connection.on('disconnected', () => {
  setTimeout(() => {
    mongoose.connect(DB_URI, options);
  }, 5000); // 5 saniye sonra tekrar dene
});
```

---

## 🚫 Bağlantıyı Kapatmak

```js
await mongoose.disconnect();
```

---

## 📦 `.env` ile URI Kullanımı (Tavsiye Edilen)

```js
import mongoose from 'mongoose';
import dotenv from 'dotenv';

dotenv.config();

mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log('✅ DB bağlantısı başarılı'))
  .catch((err) => console.log('❌ DB bağlantı hatası:', err));
```

`.env` dosyası örneği:

```
MONGO_URI=mongodb://localhost:27017/mydatabase
```
