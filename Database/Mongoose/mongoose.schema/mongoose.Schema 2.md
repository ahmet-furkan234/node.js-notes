
### 1. **`mongoose.Schema`**

Veri modelinin iskeletini tanımlar.

**Metotları ve özellikleri:**

| Method / Özellik   | Açıklama                                    |
| ------------------ | ------------------------------------------- |
| `add()`            | Schema'ya sonradan alan ekler               |
| `path()`           | Bir alanı tanımlar veya döner               |
| `pre()` / `post()` | Middleware (öncesi/sonrası işlemler)        |
| `index()`          | Manuel index oluşturur                      |
| `virtual()`        | Sanal (veritabanında olmayan) alan tanımlar |
| `set()` / `get()`  | Özel setter/getter tanımlar                 |
| `plugin()`         | Eklenti tanımlar                            |
| `methods`          | Belge (instance) fonksiyonu ekler           |
| `statics`          | Model (class) fonksiyonu ekler              |

**Örnek:**

```js
schema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});
```

---

### 3. **`mongoose.connect()`**

MongoDB'ye bağlanmak için kullanılır.

```js
mongoose.connect('mongodb://localhost:27017/mydb');
```

---

### 4. **`mongoose.Types.ObjectId`**

Manuel olarak `ObjectId` oluşturmak veya karşılaştırmak için kullanılır.

```js
const id = new mongoose.Types.ObjectId();
```

---

### 5. **`mongoose.Schema.Types`**

Özel türler:

- `String`
- `Number`
- `Boolean`
- `Date`
- `Buffer`
- `ObjectId`
- `Array`
- `Decimal128`
- `Map`
- `Mixed` (her türden veri tutar)

