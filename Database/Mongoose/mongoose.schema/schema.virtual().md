
`virtual` alanlar, veritabanında fiziksel olarak kayıtlı olmayan, ama şema üzerinde **hesaplanan** veya **geçici olarak** tutulan alanlardır.  
Yani, bir belgeye ait olan ancak doğrudan veritabanında yer almayan **sanal alanlar**dır.

---

## 🧠 Söz Dizimi

```js
schema.virtual('fieldName')
  .get(function() {
    // Getter fonksiyonu: alan okunduğunda çalışır
  })
  .set(function(value) {
    // (Opsiyonel) Setter fonksiyonu: alan yazıldığında çalışır
  });
```

---

## 🧪 Örnek 1 – Full Name Sanal Alanı

```js
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

// fullName alanı, firstName + lastName olarak hesaplanıyor
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

const User = mongoose.model('User', userSchema);

(async () => {
  const user = new User({ firstName: 'Ahmet', lastName: 'Yılmaz' });
  console.log(user.fullName); // "Ahmet Yılmaz"
})();
```

---

## 🧪 Örnek 2 – Sanal Alana Değer Atama

```js
userSchema.virtual('fullName')
  .get(function() {
    return `${this.firstName} ${this.lastName}`;
  })
  .set(function(name) {
    const split = name.split(' ');
    this.firstName = split[0];
    this.lastName = split[1];
  });

const user = new User();
user.fullName = 'Mehmet Demir';

console.log(user.firstName); // Mehmet
console.log(user.lastName);  // Demir
```

---

## 🔥 Sanal Alanların Özellikleri

| Özellik                      | Açıklama                                        |
| ---------------------------- | ----------------------------------------------- |
| Veritabanına yazılmaz        | Sadece uygulama içi hesaplama ve kullanım       |
| `get` fonksiyonu             | Sanal alanın değeri hesaplanır                  |
| `set` fonksiyonu (opsiyonel) | Sanal alana yazma işlemi yapabilir              |
| JSON çıktısına dahil etmek   | `.toJSON()` ve `.toObject()` ile kontrol edilir |

---

## 📋 JSON/Objeye Sanal Alanları Dahil Etmek

Varsayılan olarak, sanal alanlar `toJSON()` veya `toObject()` çıktısına dahil edilmez. Dahil etmek için şema ayarı yapılmalı:

```js
userSchema.set('toJSON', { virtuals: true });
userSchema.set('toObject', { virtuals: true });
```

---

## 🧩 Sanal Alanların Kullanım Alanları

- Hesaplanan değerler (ad soyad, tam adres, yaş hesaplama vb.)
- Karmaşık formatlama işlemleri
- Veritabanında tutulmayan geçici veriler
- İlişkisel verilerden (populate ile) kolayca türetilen alanlar

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`schema.virtual()`|Fiziksel olmayan, hesaplanan alan oluşturur|
|`get/set`|Değer okuma/yazma mantığını belirler|
|Veritabanına yazılmaz|Yalnızca uygulama seviyesinde tutulur|
|JSON/Objeye dahil etme|`toJSON`/`toObject` ayarı ile sağlanır|
