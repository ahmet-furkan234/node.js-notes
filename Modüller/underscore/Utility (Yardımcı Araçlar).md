
## 🔧 1. `_.identity(value)`

Aldığı değeri aynen geri döner. Genellikle varsayılan işlev olarak kullanılır.

```js
console.log(_.identity(42)); // 42
console.log(_.identity("TkMatE")); // "TkMatE"
```

---

## 🔧 2. `_.constant(value)`

Verilen değeri her çağrıldığında dönen bir fonksiyon üretir.

```js
const alwaysTrue = _.constant(true);
console.log(alwaysTrue()); // true
```

---

## 🔧 3. `_.noop()`

Hiçbir şey yapmayan boş bir fonksiyon döner (callback yerine kullanılabilir).

```js
const useless = _.noop;
useless(); // hiçbir şey yapmaz
```

---

## 🔧 4. `_.times(n, iteratee)`

Belirli sayıda fonksiyonu çalıştırır ve döndürür.

```js
_.times(3, i => console.log("Merhaba #" + i));
// Merhaba #0
// Merhaba #1
// Merhaba #2
```

---

## 🔧 5. `_.random(min, max, [floating])`

Belirtilen aralıkta rastgele sayı üretir. `floating: true` olursa ondalıklı döner.

```js
console.log(_.random(1, 5)); // örn: 4
console.log(_.random(0, 1, true)); // örn: 0.384
```

---

## 🔧 6. `_.now()`

Geçerli zaman damgasını (timestamp) döner (milisaniye cinsinden).

```js
console.log(_.now()); // örn: 1721572514580
```

---

## 🔧 7. `_.escape(string)`

HTML özel karakterlerini kaçar (XSS koruması için faydalı).

```js
console.log(_.escape("TkMatE <script>alert('XSS')</script>"));
// "TkMatE &lt;script&gt;alert(&#x27;XSS&#x27;)&lt;/script&gt;"
```

---

## 🔧 8. `_.unescape(string)`

Kaçırılmış HTML karakterlerini normale çevirir.

```js
console.log(_.unescape("TkMatE &lt;b&gt;bold&lt;/b&gt;"));
// "TkMatE <b>bold</b>"
```

---

## 🔧 9. `_.result(object, property, [defaultValue])`

Eğer property bir fonksiyonsa çalıştırır, değilse direk döner. Yoksa default verir.

```js
const obj = {
  name: "TkMatE",
  greeting() { return "Hello!"; }
};

console.log(_.result(obj, "name"));       // "TkMatE"
console.log(_.result(obj, "greeting"));   // "Hello!"
console.log(_.result(obj, "age", 25));    // 25
```

---

## 🔧 10. `_.uniqueId([prefix])`

Benzersiz bir ID oluşturur. İsteğe bağlı prefix eklenebilir.

```js
console.log(_.uniqueId("btn_")); // örn: "btn_1"
console.log(_.uniqueId("btn_")); // "btn_2"
```

---

## 🔧 11. `_.template(templateString, [settings])`

Lodash ile de benzer olan gelişmiş şablon oluşturucudur.

```js
const compiled = _.template("Merhaba <%= user %>!");
console.log(compiled({ user: "Ersin" })); // "Merhaba Ersin!"
```

---

## 🔧 12. `_.property(path)`

Belirtilen yol üzerinden bir nesneden değer dönen fonksiyon döner.

```js
const getName = _.property("name");
console.log(getName({ name: "TkMatE" })); // "TkMatE"
```

---

## 🔧 13. `_.propertyOf(object)`

Belirtilen nesneye göre property erişimi yapan fonksiyon döner.

```js
const user = { id: 1, name: "Ersin" };
const getFromUser = _.propertyOf(user);

console.log(getFromUser("name")); // "Ersin"
```

---

## 🔧 14. `_.matcher(attrs)`

Verilen özelliklere uyan nesneleri eşleştiren bir predicate döner.

```js
const isAdmin = _.matcher({ role: "admin" });

console.log(isAdmin({ name: "Ali", role: "admin" })); // true
console.log(isAdmin({ name: "Ayşe", role: "user" })); // false
```

---

## 🔧 15. `_.iteratee(value, [context])`

Verilen değere göre uygun iteratee fonksiyonu döner. (callback alternatifi)

```js
const users = [{ name: "Ali" }, { name: "Ayşe" }];
const names = _.map(users, _.iteratee("name"));
console.log(names); // ["Ali", "Ayşe"]
```

---

## 🔧 16. `_.toPath(path)`

Dizeyi veya dize dizisini, iç içe property yollarına dönüştürür.

```js
console.log(_.toPath("user.address.city")); // ["user", "address", "city"]
```

---

### ✅ Sonuç:

Underscore.js’in **Utility (yardımcı araçlar)** bölümü de tamamlandı.  
İstersen şimdi son kategori olan **"Chaining (Zincirleme İşlemler)"** ile devam edebiliriz. Zincirleme metodlar, underscore fonksiyonlarını art arda kullanmak için büyük kolaylık sağlar.

Devam edelim mi?