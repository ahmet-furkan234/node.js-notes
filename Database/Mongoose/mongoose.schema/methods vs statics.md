
|Özellik|`methods`|`statics`|
|---|---|---|
|**Neye ait?**|Modelin **örneklerine (document)** ait|Modelin **kendisine (class/model)** ait|
|**Nasıl çağrılır?**|`const doc = new Model(); doc.methodName()`|`Model.staticMethodName()`|
|**Kapsam**|Belge bazında (tek tek kayıtlara özgü)|Genel model bazında (tüm koleksiyona hitap)|
|**`this` bağlamı**|O anki belgeyi (`document`) gösterir|Modeli (`Model`) gösterir|
|**Kullanım amacı**|Belgeye özel davranışlar, hesaplamalar, doğrulamalar|Toplu işlemler, özel sorgular, yardımcı fonksiyonlar|
|**Örnek kullanım**|`user.fullName()` — kullanıcı adı döndürür|`User.findByEmail()` — eposta ile kullanıcı arar|
|**Async/await desteği**|Evet|Evet|
|**Performans farkı**|Belgeye bağlı çalışır, hafıza kullanımı belge sayısına göre artar|Modele bağlı, genelde performans daha sabit|

---

## 🧪 Örneklerle Karşılaştırma

### `methods` örneği (örnek metot)

```js
userSchema.methods.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

const user = new User({ firstName: 'Ahmet', lastName: 'Yılmaz' });
console.log(user.getFullName()); // "Ahmet Yılmaz"
```

### `statics` örneği (statik metot)

```js
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email });
};

const user = await User.findByEmail('ahmet@example.com');
```

---

## 🔍 Özet

|Özellik|`methods`|`statics`|
|---|---|---|
|Bağlam|Document (tek belge)|Model (tüm koleksiyon)|
|Kullanım amacı|Belgeye özgü işlemler|Koleksiyon bazlı sorgular|
|Çağrı şekli|`doc.methodName()`|`Model.staticMethodName()`|
|Örnek|Hesaplama, doğrulama, dönüştürme|Bulma, toplu güncelleme, özel sorgular|

---

### İpuçları

- Belgeye özgü bir işlem yapacaksan `methods` kullan.
- Koleksiyon çapında (örneğin tüm kullanıcılar üzerinde) bir sorgu veya işlemse `statics` kullan.
- Kod düzeni ve okunabilirlik için bu ayrımı net yapmak önemli.
