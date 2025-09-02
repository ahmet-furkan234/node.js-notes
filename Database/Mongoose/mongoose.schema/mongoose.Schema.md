
## 📦 Mongoose Schema Açıklamaları

```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,       // ⬅️ Zorunlu alan
  },
  email: {
    type: String,
    required: true,       // ⬅️ Zorunlu alan
    unique: true,         // ⬅️ Aynı değerden sadece bir tane olabilir
  },
  createdAt: {
    type: Date,
    default: Date.now,    // ⬅️ Varsayılan değer: şu anki zaman
  },
});
```

---

### 🔍 Alanlar Tek Tek Açıklaması

|Alan Adı|Açıklama|
|---|---|
|**name**|Kullanıcının ismini tutar|
|**email**|Kullanıcının email adresi, eşsiz ve zorunlu olmalı|
|**createdAt**|Kullanıcı kaydının oluşturulma zamanı (otomatik verilir)|

---

### 🧱 Şema Özellikleri

#### 1. `type`

Alan veri tipini belirtir.  
Mongoose desteklediği türler:

```js
type: String
type: Number
type: Boolean
type: Date
type: Buffer
type: mongoose.Schema.Types.ObjectId
type: [String] // dizi
```

---

#### 2. `required`

Alan doldurulmak **zorunda** mı?

```js
required: true
// veya özel mesaj:
required: [true, 'İsim boş bırakılamaz']
```

---

#### 3. `unique`

Bu alanın veritabanında **eşsiz** olması gerektiğini belirtir.

> ⚠️ Not: Bu Mongoose'da doğrulama yapmaz, **MongoDB'de benzersiz bir index oluşturur**. Aynı email'le kayıt yapılmaya çalışılırsa hata alırsın.

```js
unique: true
```

---

#### 4. `default`

Varsayılan değer atar. Alan gönderilmezse bu değer atanır.

```js
default: Date.now     // kayıt tarihi
default: "Aktif"      // string sabit
default: false        // boolean
```

---

## 🔧 Bonus: Gelişmiş Ayarlar Örnekleri

```js
age: {
  type: Number,
  min: 18,                  // minimum yaş
  max: 120,                 // maksimum yaş
  required: true
},

status: {
  type: String,
  enum: ['active', 'passive', 'banned'],  // sadece bu değerler olabilir
  default: 'active',
},

phone: {
  type: String,
  validate: {
    validator: function(v) {
      return /^[0-9]{10}$/.test(v); // 10 haneli sayı kontrolü
    },
    message: props => `${props.value} geçerli bir telefon değil!`
  }
}
```

---

## 🎯 Özet

|Özellik|Açıklama|
|---|---|
|`type`|Alanın veri tipi|
|`required`|Zorunlu olup olmadığı|
|`unique`|Eşsiz olup olmadığı|
|`default`|Varsayılan değeri|
|`enum`|Sadece belirli değerleri kabul eder|
|`validate`|Özel doğrulama fonksiyonu|
|`min`/`max`|Sayısal ve tarihsel minimum–maksimum değerler|
