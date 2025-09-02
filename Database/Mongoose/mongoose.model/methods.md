
### 1. **`Model.create(doc, [callback])`**

- Yeni bir veya birden fazla belge oluşturup kaydeder.
- Promise döner.

```js
await User.create({ name: 'Ahmet', email: 'ahmet@example.com' });
```

---

### 2. **`Model.find(conditions, [projection], [options], [callback])`**

- Şarta uyan belgeleri getirir.
- Boş koşul tüm koleksiyonu döner.

```js
const users = await User.find({ isActive: true });
```

---

### 3. **`Model.findOne(conditions, [projection], [options], [callback])`**

- Şarta uyan ilk belgeyi getirir.

```js
const user = await User.findOne({ email: 'ahmet@example.com' });
```

---

### 4. **`Model.findById(id, [projection], [options], [callback])`**

- ID’ye göre belge getirir.

```js
const user = await User.findById('60a6f9a8f2d3f82b1c123456');
```

---

### 5. **`Model.updateOne(filter, update, [options], [callback])`**

- Şarta uyan ilk belgeyi günceller.

```js
await User.updateOne({ email: 'ahmet@example.com' }, { isActive: false });
```

---

### 6. **`Model.updateMany(filter, update, [options], [callback])`**

- Şarta uyan tüm belgeleri günceller.

```js
await User.updateMany({ isActive: false }, { isActive: true });
```

---

### 7. **`Model.deleteOne(filter, [callback])`**

- Şarta uyan ilk belgeyi siler.

```js
await User.deleteOne({ email: 'ahmet@example.com' });
```

---

### 8. **`Model.deleteMany(filter, [callback])`**

- Şarta uyan tüm belgeleri siler.

```js
await User.deleteMany({ isActive: false });
```

---

### 9. **`Model.countDocuments(filter, [callback])`**

- Şarta uyan belge sayısını döner.

```js
const count = await User.countDocuments({ isActive: true });
```

---

### 10. **`Model.distinct(field, [filter], [callback])`**

- Belirtilen alandaki benzersiz değerleri döner.

```js
const emails = await User.distinct('email');
```

---

### 11. **`Model.aggregate(pipeline, [options], [callback])`**

- Aggregation pipeline ile gelişmiş sorgular yapar.

```js
const results = await User.aggregate([
  { $match: { isActive: true } },
  { $group: { _id: "$role", count: { $sum: 1 } } }
]);
```

---

### 12. **`Model.findOneAndUpdate(filter, update, [options], [callback])`**

- Şarta uyan ilk belgeyi güncelleyip güncellenmiş belgeyi döner.

```js
const updatedUser = await User.findOneAndUpdate(
  { email: 'ahmet@example.com' },
  { isActive: false },
  { new: true }
);
```

---

### 13. **`Model.findOneAndDelete(filter, [options], [callback])`**

- Şarta uyan ilk belgeyi silip silinen belgeyi döner.

```js
const deletedUser = await User.findOneAndDelete({ email: 'ahmet@example.com' });
```

---

### 14. **`Model.watch(pipeline, [options])`**

- MongoDB change stream dinleyicisi açar.

```js
const changeStream = User.watch();
changeStream.on('change', (change) => {
  console.log('Değişiklik:', change);
});
```

---

## Özet Tablo

| Method               | Açıklama                         |
| -------------------- | -------------------------------- |
| `create()`           | Yeni belge oluşturur ve kaydeder |
| `find()`             | Çoklu belge sorgular             |
| `findOne()`          | Tek belge getirir                |
| `findById()`         | ID’ye göre belge getirir         |
| `updateOne()`        | Tek belge günceller              |
| `updateMany()`       | Çoklu belge günceller            |
| `deleteOne()`        | Tek belge siler                  |
| `deleteMany()`       | Çoklu belge siler                |
| `countDocuments()`   | Belge sayısını döner             |
| `distinct()`         | Benzersiz değerleri getirir      |
| `aggregate()`        | Aggregation pipeline kullanır    |
| `findOneAndUpdate()` | Tek belgeyi günceller ve döner   |
| `findOneAndDelete()` | Tek belgeyi siler ve döner       |
| `watch()`            | Change stream açar               |
