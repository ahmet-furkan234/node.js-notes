
`schema.index()` metodu, Mongoose şemasına **MongoDB indeksleri** eklemek için kullanılır.  
İndeksler, sorgu performansını artırmak için veritabanındaki belirli alanlar üzerinde oluşturulan veri yapılarıdır.

---

## 🧠 Söz Dizimi

```js
schema.index(fields, options);
```

- **fields**: İndeks oluşturulacak alan veya alanlar. Örnek `{ field1: 1, field2: -1 }`
    - `1` → Artan sıra (Ascending)
    - `-1` → Azalan sıra (Descending)   
- **options**: İndeks için ek ayarlar (örneğin `unique`, `sparse`, `background`, `expireAfterSeconds` vb.)

---

## 🧪 Örnek 1 – Basit İndeks Oluşturma

```js
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
});

// email alanına artan sırada indeks ekledik
userSchema.index({ email: 1 });
```

---

## 🧪 Örnek 2 – Benzersiz (Unique) İndeks

```js
userSchema.index({ email: 1 }, { unique: true });
```

Bu indeks sayesinde aynı email ile birden fazla kayıt yapılamaz.

---

## 🧪 Örnek 3 – Çoklu Alan (Compound) İndeks

```js
userSchema.index({ lastName: 1, firstName: 1 });
```

Bu, `lastName` ve `firstName` alanlarının kombinasyonuna göre indeks oluşturur.  
Sorgular bu iki alana göre optimize edilir.

---

## 🧪 Örnek 4 – TTL (Time To Live) İndeksi

Belirli bir süre sonunda otomatik silinen veriler için kullanılır.

```js
const sessionSchema = new mongoose.Schema({
  createdAt: { type: Date, default: Date.now, expires: 3600 } // 1 saat sonra sil
});
```

Alternatif olarak:

```js
sessionSchema.index({ createdAt: 1 }, { expireAfterSeconds: 3600 });
```

---

## 🔥 Önemli İndeks Opsiyonları

|Opsiyon|Açıklama|
|---|---|
|`unique: true`|Alanın eşsiz olmasını sağlar|
|`sparse: true`|Sadece değer atanmış belgelerde indeks oluşturur|
|`background: true`|İndeks arka planda oluşturulur (sunucu yavaşlamaz)|
|`expireAfterSeconds`|TTL indeks süresi (saniye cinsinden)|

---

## ⚠️ Notlar

- `schema.index()` sadece Mongoose tarafında indeks oluşturur, ancak indeks MongoDB’de fiziksel olarak yaratılır.
    
- Büyük veri tabanlarında arka planda (`background: true`) indeks oluşturmak önerilir.
    
- İndekslerin doğru tasarımı sorgu performansı için kritik önemdedir.
    

---

## 🧩 İndeksleri Listelemek

MongoDB shell veya MongoDB Compass ile koleksiyon indekslerini görebilirsin:

```js
db.collection.getIndexes();
```

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`schema.index()`|Şemaya indeks ekler|
|Performans|Sorgu hızlandırmak için kullanılır|
|Opsiyonlar|`unique`, `sparse`, `background`, `expireAfterSeconds` gibi ayarlar yapılabilir|

---

İstersen `plugin()` ya da `methods/statics` gibi diğer Mongoose schema metodlarına geçebiliriz.  
Hangisiyle devam edelim TkMatE?