
Underscore.js, fonksiyonları art arda zincirleme yaparak, okunabilir ve etkili kod yazmayı kolaylaştırır.  
Bir zincirleme başlatmak için `_.chain()` kullanılır. Sonunda `.value()` çağrılarak sonuç alınır.

---

## 1. `_.chain(obj)`

Bir nesne veya dizi üzerinde zincirleme başlatır.

```js
const result = _.chain([1, 2, 3, 4])
  .map(n => n * 2)
  .filter(n => n > 4)
  .value();

console.log(result); // [6, 8]
```

---

## 2. `.value()`

Zincirleme sonunda, işlenmiş sonucu elde etmek için çağrılır.

---

### Örnek Tam Zincirleme:

```js
const data = [
  { name: "Ali", age: 23 },
  { name: "Ayşe", age: 21 },
  { name: "Ahmet", age: 25 },
];

const names = _.chain(data)
  .filter(person => person.age > 22)
  .map(person => person.name)
  .value();

console.log(names); // ["Ali", "Ahmet"]
```

---

## 3. Zincirlemede kullanılan metotların tamamı:

Underscore zincirleme sırasında tüm fonksiyonları destekler. Örneğin:

- Koleksiyon metodları: `map`, `filter`, `reduce`, `find`, ...
- Array metodları: `first`, `last`, `uniq`, `flatten`, ...
- Object metodları: `keys`, `values`, `pick`, `omit`, ...
- Function metodları: `bind`, `partial`, `memoize`, ...

---

## 4. Zincirleme örneği — karmaşık işlem:

```js
const result = _.chain([1, 2, 3, 4, 5, 6])
  .filter(n => n % 2 === 0)   // [2, 4, 6]
  .map(n => n * n)            // [4, 16, 36]
  .reduce((sum, n) => sum + n, 0)  // 56
  .value();

console.log(result);  // 56
```

---

## 5. `_.tap(object, interceptor)`

Zincirde ara adımda yan etki için kullanılır (örneğin debug).

```js
const result = _.chain([1, 2, 3, 4])
  .map(n => n * 2)
  .tap(arr => console.log("Ara:", arr)) // Ara: [2,4,6,8]
  .filter(n => n > 5)
  .value();

console.log(result); // [6,8]
```

---

# Özet

- Zincirleme, birçok Underscore metodunu ardışık kullanmanı sağlar.
- `_.chain()` ile başlatılır, `.value()` ile sonlandırılır.
- Kodun okunabilirliği artar ve karmaşık işlemler basitleşir.
