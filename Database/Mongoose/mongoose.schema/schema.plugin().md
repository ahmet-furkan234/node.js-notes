
`schema.plugin()` metodu, Mongoose şemasına **harici veya kendi yazdığın eklentileri (pluginleri)** uygulamak için kullanılır.  
Pluginler, şemaya **tekrar kullanılabilir özellikler, fonksiyonlar, middlewareler** eklemeye olanak sağlar.

---

## 🧠 Neden Kullanılır?

- Ortak işlevselliği birden fazla şemada kullanmak için (örneğin tarih damgası, soft delete, versiyonlama vb.)
- Kod tekrarı azaltmak için
- Şemaya özel davranışlar eklemek için

---

## 🧪 Söz Dizimi

```js
schema.plugin(pluginFunction, options);
```

- `pluginFunction`: Fonksiyon tipi plugin. İlk parametre olarak şemayı, ikinci parametre olarak opsiyonları alır.
- `options` (opsiyonel): Plugin'e özel ayarlar.

---

## 🧪 Örnek 1 – Basit Plugin Tanımlama

```js
function createdAtPlugin(schema, options) {
  schema.add({ createdAt: Date });

  schema.pre('save', function(next) {
    if (!this.createdAt) {
      this.createdAt = new Date();
    }
    next();
  });
}

const userSchema = new mongoose.Schema({ name: String });
userSchema.plugin(createdAtPlugin);

const User = mongoose.model('User', userSchema);
```

---

## 🧪 Örnek 2 – Hazır Plugin Kullanımı (mongoose-paginate-v2)

```js
import mongoosePaginate from 'mongoose-paginate-v2';

const articleSchema = new mongoose.Schema({
  title: String,
  content: String
});

// Paginate plugin’i ekledik
articleSchema.plugin(mongoosePaginate);

const Article = mongoose.model('Article', articleSchema);

// Artık Article.paginate() fonksiyonunu kullanabilirsin
```

---

## 🧩 Plugin Fonksiyonunun Yapısı

```js
function pluginFunction(schema, options) {
  // Şemaya alanlar ekleyebilir
  // Middleware tanımlayabilir
  // Metotlar ve statik fonksiyonlar ekleyebilir
}
```

---

## 🔥 Plugin Avantajları

- Kodunuzu modüler yapar,
- Proje çapında tekrar eden işlevleri kolayca yönetmeyi sağlar,
- Yeni özellikleri merkezi ve temiz şekilde ekler.

---

## ❗ Özet

|Özellik|Açıklama|
|---|---|
|`schema.plugin()`|Şemaya eklenti (plugin) ekler|
|Kod tekrarı önler|Ortak fonksiyonları paylaşır|
|Hazır pluginler|Çok sayıda açık kaynak plugin var|
