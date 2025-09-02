
## ✅ 1. **Model Methodları (Statik CRUD İşlemleri)**

Bunlar doğrudan `Model` (örneğin `User`) üzerinden çağrılır. Bu methodlar MongoDB'ye sorgu atar.

|Statik Method|Açıklama|
|---|---|
|`Model.create()`|Yeni belge ekler|
|`Model.find()`|Belgeleri listeler|
|`Model.findById()`|ID ile belge bulur|
|`Model.findOne()`|Tek bir belge bulur|
|`Model.updateOne()`|İlk eşleşen belgeyi günceller|
|`Model.updateMany()`|Tüm eşleşenleri günceller|
|`Model.findByIdAndUpdate()`|ID ile bulup günceller|
|`Model.deleteOne()`|İlk eşleşen belgeyi siler|
|`Model.deleteMany()`|Tüm eşleşen belgeleri siler|
|`Model.findByIdAndDelete()`|ID ile bulup siler|
|`Model.exists()`|Varlık kontrolü yapar|
|`Model.countDocuments()`|Belge sayar|
|`Model.aggregate()`|Aggregation pipeline başlatır|
|`Model.insertMany()`|Toplu belge ekler|

> Bunların hepsi `await User.method()` şeklinde çalışır ve MongoDB ile doğrudan iletişime geçer.

---

## ✅ 2. **Document (Instance) Methodları**

Bu işlemler bir modelin örneği (belge) üzerinde yapılır. Örnek:

```js
const user = new User({ name: "TkMatE", email: "tkmate@example.com" });
await user.save();  // -> MongoDB'ye kaydeder
```

|Instance Method|Açıklama|
|---|---|
|`doc.save()`|Belgeyi kaydeder|
|`doc.remove()`|Belgeyi siler|
|`doc.validate()`|Belgeyi doğrular|
|`doc.toObject()`|JS objesine çevirir|
|`doc.toJSON()`|JSON formatına çevirir|

---

## ✅ 3. Diğer Mongoose Özellikleri

### 🔧 Gelişmiş Özellikler

|Konu|Açıklama|
|---|---|
|`query helpers`|Özelleştirilmiş query zincirleri|
|`populate()`|Referanslı verileri çeker (join benzeri)|
|`lean()`|Performans için düz obje döner|
|`mongoose.connection`|Bağlantı olaylarını yönetir|
|`mongoose.Schema.Types`|Özel türler (`ObjectId`, `Decimal128`, vb.)|

---

## 🔚 Sonuç: `mongoose.model()`'den Sonra...

| Sonraki Konular                                       |
| ----------------------------------------------------- |
| CRUD işlemleri (`create`, `find`, vs.)                |
| Belge işlemleri (`save`, `remove`, vs.)               |
| `populate()`, `lean()`, `select()` kullanımı          |
| `model.hooks`, `model.plugins`, `model.discriminator` |
| Bağlantı kontrolü (`mongoose.connection`)             |
