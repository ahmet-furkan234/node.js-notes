
- Mongoose’da **Model**, belirli bir koleksiyona (`collection`) karşılık gelen ve veritabanı işlemlerini yapmamızı sağlayan bir sınıftır.
- `mongoose.model()` metodu ise yeni bir model oluşturmak ya da var olan modeli almak için kullanılır.

---

## 🧠 Kullanım Amacı

- Bir şemaya (`Schema`) dayalı olarak model oluşturmak,
- Oluşturulan modelle veritabanında CRUD işlemleri gerçekleştirmek.

---

## 🧪 Söz Dizimi

```js
mongoose.model(modelName, schema, collectionName);
```

- `modelName` (string): Modelin ismi, genellikle tekil ve büyük harfle başlar.
- `schema` (mongoose.Schema): Modelin dayandığı şema.
- `collectionName` (string, opsiyonel): Modelin ilişkilendirileceği koleksiyon adı. Belirtilmezse `modelName` küçük harfe çevrilip çoğul hali kullanılır.

---

## 🧪 Örnek 1 – Basit Model Oluşturma

```js
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
});

const User = mongoose.model('User', userSchema);

// Kullanım
const newUser = new User({ name: 'Ahmet', email: 'ahmet@example.com' });
await newUser.save();
```

Burada:

- Model adı: `User`
- Şema: `userSchema`
- Koleksiyon adı: otomatik olarak `users` (küçük harf ve çoğul) olur.

---

## 🧪 Örnek 2 – Koleksiyon Adını Belirtme

```js
const Cat = mongoose.model('Cat', catSchema, 'myCatsCollection');
```

Bu durumda veriler `myCatsCollection` adlı koleksiyonda saklanır.

---

## 🧩 Model Kullanımı

- `Model.find()`, `Model.findOne()`, `Model.create()` gibi CRUD metodları
- `new Model()` ile belge (document) oluşturma ve `save()` ile kaydetme
- `Model.updateOne()`, `Model.deleteMany()` vb.

---

## 🔥 Özet

|Parametre|Açıklama|
|---|---|
|`modelName`|Model ismi (genellikle tekil)|
|`schema`|Modelin şeması|
|`collectionName`|Koleksiyon adı (opsiyonel)|
