
Mongoose modellerinde bir belgeyi **JavaScript nesnesine** (`toObject`) veya **JSON formatına** (`toJSON`) dönüştürmek için kullanılan **ayarlardır**.

- `toObject()` metodu: Bir Mongoose belgesini (document) sade bir JS nesnesine çevirir.
- `toJSON()` metodu: JSON.stringify gibi işlemler için JSON formatına çevirir.

Bu metotlar dönüşüm sırasında bazı **özel ayarları** dikkate alır.

---

## 🧠 Amaçları

- Veritabanında saklanan tüm alanları **görünür yapmak** veya **gizlemek**
- Sanal (`virtual`) alanların dönüşüme dahil edilmesi
- Belge nesnesinden belirli alanları **çıkarma** veya **dönüştürme**
- Örneğin şifre gibi hassas alanların JSON çıktısında gösterilmemesi

---

## 🧪 Kullanımı

### Örnek: Sanal alanları JSON ve Object dönüşümüne dahil etmek

```js
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

// Sanal alanların toJSON ve toObject çıktısında görünmesi için:
userSchema.set('toJSON', { virtuals: true });
userSchema.set('toObject', { virtuals: true });
```

---

## 🧩 Diğer Yaygın Kullanımlar

|Ayar|Açıklama|
|---|---|
|`virtuals: true`|Sanal alanları dönüşüme dahil eder|
|`versionKey: false`|`__v` alanını dönüşümde gizler|
|`transform`|Dönüşüm sırasında özelleştirilmiş işlem yapmaya yarar|

---

### `transform` Örneği

Belge JSON’a çevrilirken `password` gibi hassas alanları kaldırmak için:

```js
userSchema.set('toJSON', {
  virtuals: true,
  transform: (doc, ret) => {
    delete ret.password;
    return ret;
  }
});
```

---

## 📌 Özet

|Metod|Kullanım Amacı|
|---|---|
|`toObject()`|Modelden saf JS nesnesi almak için|
|`toJSON()`|JSON.stringify çağrıldığında dönen nesneyi kontrol etmek için|
|`set('toJSON')` ve `set('toObject')`|Bu dönüşümlerde özel ayarlar yapmak için|

---

## 🔎 Neden önemli?

- API’de istemciye gönderilen JSON’da fazladan veya hassas veriler görünmesin diye kontrol sağlar.
- Sanal alanlar ve özel formatlama bu sayede API çıktılarına eklenebilir.
- Dönüşüm sürecini istediğin gibi manipüle etmene olanak verir.
