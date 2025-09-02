
Mongoose’un `toJSON` veya `toObject` ayarlarında kullanılan `transform` fonksiyonu, dönüşüm sırasında **belge (document) ve onun JS objesi halini** kontrol etmek için çağrılır.

### Parametreler

|Parametre|Açıklama|
|---|---|
|`doc`|Orijinal Mongoose **Document** nesnesi (yani Mongoose modeli). İçerisinde tüm Mongoose fonksiyonları, sanal alanlar vb. bulunur.|
|`ret`|`doc`’un saf JavaScript nesnesine dönüştürülmüş hali (yani sonuç olarak dönecek obje). Bu nesne JSON.stringify veya `toObject()` çıktısıdır.|

---

## 🧠 Nasıl Kullanılır?

`transform` fonksiyonu içinde `ret` nesnesi üzerinde istediğin değişiklikleri yapabilir, gereksiz alanları silebilir, alan isimlerini değiştirebilir veya yeni alanlar ekleyebilirsin.

---

## 🧪 Örnek: `password` alanını JSON’dan kaldırmak

```js
userSchema.set('toJSON', {
  transform: (doc, ret) => {
    delete ret.password;  // JSON çıktısından şifreyi kaldır
    ret.id = ret._id;     // _id yerine id alanı ekle
    delete ret._id;       // _id’yi kaldır
    delete ret.__v;       // version key’i kaldır
    return ret;
  }
});
```

---

## 📌 Özet

- `doc` = Tam Mongoose belge nesnesi (model)
- `ret` = `doc`’un saf JS nesnesine dönüştürülmüş hali (çıktı için kullanılacak)

`transform` ile `ret` üzerinde istediğin değişiklikleri yap, `doc` ise gerektiğinde tam model verisiyle erişim için elinde.
