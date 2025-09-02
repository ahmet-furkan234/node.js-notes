
`schema.path()` metodu, bir Mongoose şemasında **belirli bir alanın (path’in) tanımına erişmek** veya **yeni bir path tanımlamak** için kullanılır.

- En çok **alanın özelliklerine erişmek veya değiştirmek** için kullanılır.
- Ayrıca, alanın doğrulama, tür ve diğer ayarlarını programatik olarak inceleyebilirsin.

---

## 🧠 Söz Dizimi

```js
schema.path(pathName);
```

- `pathName`: Şema içindeki alanın adı (string olarak).
- Dönen değer: O alana ait **SchemaType** nesnesi (örneğin `SchemaString`, `SchemaNumber` vb.)

---

## 🧪 Örnek 1 – Alan Bilgilerini Okuma

```js
import mongoose from 'mongoose';

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, unique: true },
});

const namePath = userSchema.path('name');

console.log(namePath instanceof mongoose.Schema.Types.String); // true
console.log(namePath.options.required); // true
console.log(namePath.options.unique);   // undefined (unique email’de var)
```

---

## 🧪 Örnek 2 – Alan Üzerinde Değişiklik Yapma

```js
const emailPath = userSchema.path('email');

// unique değil ama biz dinamik olarak ekleyebiliriz:
emailPath.options.unique = true;
```

---

## 📌 Daha Fazla Kullanım

| Amaç                            | Açıklama                                                      |
| ------------------------------- | ------------------------------------------------------------- |
| Alan türüne erişmek             | `schema.path('fieldName').instance` (örn: 'String', 'Number') |
| Alan validasyonlarını görmek    | `schema.path('fieldName').validators`                         |
| Alanın default değerine erişmek | `schema.path('fieldName').defaultValue` (varsa)               |
| Custom getter/setter kontrolü   | `schema.path('fieldName').getters`, `.setters`                |

---

## 🧩 `SchemaType` Önemli Özellikleri

`schema.path()` ile dönen nesne, Mongoose’un farklı `SchemaType` türlerinden biridir (örn: `SchemaString`, `SchemaNumber`).

Önemli özellikler:

- `.instance` → Veri tipi ismi (örn: `"String"`, `"Number"`)
- `.options` → Şemada tanımlanmış tüm seçenekler (type, required, unique, default vb.)
- `.validators` → Bu alan için tanımlı validator fonksiyonları listesi
- `.getters` / `.setters` → Tanımlanmış getter/setter fonksiyonları

---

## 🎯 Özet

- `schema.path('alanAdi')` → O alana ait şema tanımını getirir
- Alan özelliklerini okumak ve gerekirse değiştirmek için kullanılır
- Özellikle dinamik schema işlemleri için faydalıdır
