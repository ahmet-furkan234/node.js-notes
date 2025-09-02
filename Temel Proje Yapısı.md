
Node.js'de controller yapısı, genellikle **MVC (Model-View-Controller)** mimarisine dayanır. Özellikle Express.js ile çalışırken controller yapısı, kodun modüler, okunabilir ve bakımı kolay bir şekilde organize edilmesini sağlar.

---

### 🔹 Controller Yapısı Nedir?

Controller’lar, gelen istekleri işler ve modele ya da servislere yönlendirir. İlgili veriyi alır, işleme tabi tutar ve cevabı döner.

---

### 📁 Temel Proje Yapısı

```bash
project/
├── controllers/
│   └── user.controller.js
├── models/
│   └── user.model.js
├── routes/
│   └── user.routes.js
├── services/
│   └── user.service.js (opsiyonel)
├── app.js
```

---

### 1️⃣ `controllers/user.controller.js`

```js
import * as userService from '../services/user.service.js';

export const getAllUsers = async (req, res) => {
  try {
    const users = await userService.getUsers();
    res.json(users);
  } catch (err) {
    res.status(500).json({ error: 'Kullanıcılar alınamadı.' });
  }
};

export const getUserById = async (req, res) => {
  try {
    const user = await userService.getUserById(req.params.id);
    if (!user) return res.status(404).json({ error: 'Kullanıcı bulunamadı.' });
    res.json(user);
  } catch (err) {
    res.status(500).json({ error: 'Bir hata oluştu.' });
  }
};
```

---

### 2️⃣ `models/user.model.js` (Mongoose örneği)

```js
import mongoose from 'mongoose';

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
});

export default mongoose.model('User', userSchema);
```

---

### 3️⃣ `services/user.service.js` (opsiyonel ama önerilir)

```js
import User from '../models/user.model.js';

export const getUsers = () => User.find();

export const getUserById = (id) => User.findById(id);
```

---

### 4️⃣ `routes/user.routes.js`

```js
import express from 'express';
import * as userController from '../controllers/user.controller.js';

const router = express.Router();

router.get('/', userController.getAllUsers);
router.get('/:id', userController.getUserById);

export default router;
```

---

### 5️⃣ `app.js` (Uygulama başlatıcı)

```js
import express from 'express';
import mongoose from 'mongoose';
import userRoutes from './routes/user.routes.js';

const app = express();

app.use(express.json());
app.use('/api/users', userRoutes);

mongoose.connect('mongodb://localhost:27017/mydb')
  .then(() => {
    app.listen(3000, () => {
      console.log('Sunucu 3000 portunda çalışıyor...');
    });
  })
  .catch(err => console.error('MongoDB bağlantı hatası:', err));
```

---

### ✅ Özet:

|Katman|Görev|
|---|---|
|Controller|İstekleri alır, service’e yönlendirir ve cevap döner.|
|Service|İş mantığını içerir, modelle çalışır.|
|Model|Veritabanı şeması ve işlemleri.|
|Route|URL yol haritası.|
 