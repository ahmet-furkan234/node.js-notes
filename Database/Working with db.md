Node.js'te **veritabanı (database)** kullanımı, genellikle bir veritabanı sürücüsü veya ORM (Object Relational Mapping) kütüphanesi aracılığıyla gerçekleştirilir. Aşağıda en yaygın kullanılan veritabanları ve Node.js ile nasıl entegre edildiğine dair temel bilgiler veriyorum. Sonrasında senin seçimine göre detaylara geçebiliriz.

---

## 🔧 1. Hangi Veritabanı ile Kullanmak İstiyorsun?

### 📌 SQL Tabanlılar:

|Veritabanı|Kullanılan Kütüphane|Açıklama|
|---|---|---|
|MySQL / MariaDB|`mysql2`, `sequelize`|En yaygın kullanılan SQL veritabanları|
|PostgreSQL|`pg`, `sequelize`, `knex`|Güçlü ve açık kaynaklı SQL veritabanı|
|SQLite|`sqlite3`, `sequelize`|Dosya tabanlı küçük projeler için|

### 📌 NoSQL Tabanlılar:

|Veritabanı|Kullanılan Kütüphane|
|---|---|
|MongoDB|`mongoose`, `mongodb`|
|Redis|`ioredis`, `redis`|

---

## 🚀 En Yaygın Kullanım: MongoDB (NoSQL)

### MongoDB'yi Node.js ile Kullanma Adımları:

#### 1. Kurulum

```bash
npm install mongoose
```

#### 2. Bağlantı Kurma

```js
// db.js
import mongoose from "mongoose";

const connectDB = async () => {
  try {
    await mongoose.connect("mongodb://localhost:27017/your_database_name");
    console.log("MongoDB'ye bağlanıldı.");
  } catch (error) {
    console.error("Veritabanı bağlantı hatası:", error);
  }
};

export default connectDB;
```

#### 3. Model Tanımlama

```js
// models/User.js
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  createdAt: {
    type: Date,
    default: Date.now,
  },
});

const User = mongoose.model("User", userSchema);
export default User;
```

#### 4. CRUD Örneği

```js
// userController.js
import User from "./models/User.js";

// Yeni kullanıcı oluştur
export const createUser = async (req, res) => {
  const user = new User({ name: "Ali", email: "ali@example.com" });
  await user.save();
  res.send("Kullanıcı oluşturuldu");
};
```

---

## 💡 Alternatif: MySQL ile Sequelize Kullanımı (SQL)

```bash
npm install mysql2 sequelize
```

```js
// db.js
import { Sequelize } from "sequelize";

const sequelize = new Sequelize("db_adi", "kullanici", "sifre", {
  host: "localhost",
  dialect: "mysql",
});

export default sequelize;
```

Model, CRUD işlemleri ve ilişkiler de mümkündür.

---

## ⚙️ Uygulama Akışı Örneği

```bash
app.js → Veritabanına bağlan
       → Route'ları yükle
       → CRUD işlemleri yap
```
