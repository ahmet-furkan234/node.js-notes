
`schema.methods`, Mongoose modellerinin **örneklerine (document instance)** özel, **örnek metotları (instance methods)** tanımlamak için kullanılır.

- Bu metotlar, modelden oluşturulan her belge (document) üzerinde çağrılabilir.
- Belgeye özgü işlemler yapmak için uygundur.

---

## 🧠 Nasıl Çalışır?

- `schema.methods` nesnesine istediğin metotları ekleyebilirsin.
- Daha sonra o şemadan oluşturulan modelin her örneğinde bu metotlar kullanılabilir.

---

## 🧪 Örnek 1 – Basit Metot Tanımlama

```js
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
});

// fullName adında örnek metot
userSchema.methods.fullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

const User = mongoose.model('User', userSchema);

(async () => {
  const user = new User({ firstName: 'Ahmet', lastName: 'Yılmaz' });
  console.log(user.fullName()); // "Ahmet Yılmaz"
})();
```

---

## 🧪 Örnek 2 – Şifre Kontrol Metodu (Örnek Metot)

```js
import bcrypt from 'bcryptjs';

userSchema.methods.comparePassword = async function(candidatePassword) {
  return await bcrypt.compare(candidatePassword, this.password);
};
```

Bu metodu, `user` örneği üzerinden çağırıp şifre doğrulaması yapabilirsin.

---

## 🧩 `methods` ile Neler Yapılır?

- Belgeye özel hesaplamalar (örneğin `fullName()`)
- Belge üzerinde doğrulama ve karşılaştırma işlemleri
- Belgeyi başka biçime dönüştürme işlemleri

---

## 🔥 Kullanımın Avantajları

- Metotlar doğrudan belge örnekleriyle ilişkilidir, kullanım kolaylığı sağlar.
- Kod tekrarı azaltır, fonksiyonları organize eder.
- Özelleştirilmiş belge davranışları için idealdir.

---

## ❗ Notlar

- `methods` sadece belge (document) örneklerinde çalışır, model sınıfında değil.
- Async/await veya Promise döndürebilir.

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`schema.methods`|Model örneklerine özel metotlar tanımlar|
|`this`|Metot içinde o belgeyi (document) ifade eder|
|Kullanım|`const user = new User(); user.methodName()`|
