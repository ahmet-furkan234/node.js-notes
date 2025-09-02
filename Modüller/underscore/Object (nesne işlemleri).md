
## 🔸 1. `_.keys(object)`

Belirtilen nesnenin kendi enumerable (sayılabilir) anahtarlarını döner.

```js
_.keys({ ad: "TkMatE", yas: 25 });  
// ["ad", "yas"]
```

---

## 🔸 2. `_.allKeys(object)`

Nesnenin hem kendi hem de prototip zincirindeki tüm özelliklerini döner.

```js
function Person() { this.ad = "TkMatE"; }
Person.prototype.yas = 25;

_.allKeys(new Person());  
// ["ad", "yas"]
```

---

## 🔸 3. `_.values(object)`

Bir nesnenin değerlerini dizi olarak döner.

```js
_.values({ ad: "TkMatE", yas: 25 });  
// ["TkMatE", 25]
```

---

## 🔸 4. `_.mapObject(object, iteratee)`

Bir nesnenin her özelliğine `iteratee` fonksiyonu uygular, yeni nesne döner.

```js
_.mapObject({ a: 1, b: 2 }, v => v * 2);  
// { a: 2, b: 4 }
```

---

## 🔸 5. `_.pairs(object)`

Bir nesneyi [key, value] çiftleri dizisine çevirir.

```js
_.pairs({ a: 1, b: 2 });  
// [["a", 1], ["b", 2]]
```

---

## 🔸 6. `_.invert(object)`

Key'leri ve value’ları yer değiştirir.

```js
_.invert({ a: "x", b: "y" });  
// { x: "a", y: "b" }
```

---

## 🔸 7. `_.functions(object)` / `_.methods(object)`

Bir nesnedeki fonksiyon isimlerini döner (alfabetik sırayla).

```js
_.functions(_, true); // underscore içindeki tüm method adlarını verir
```

---

## 🔸 8. `_.extend(destination, *sources)`

Kaynak nesneleri hedef nesneye kopyalar.

```js
_.extend({ ad: "TkMatE" }, { yas: 25 });  
// { ad: "TkMatE", yas: 25 }
```

---

## 🔸 9. `_.extendOwn(destination, *sources)` (veya `_.assign`)

Sadece kendi özellikleri kopyalanır (prototype'dakiler değil).

```js
_.extendOwn({ ad: "TkMatE" }, { yas: 25 });  
// { ad: "TkMatE", yas: 25 }
```

---

## 🔸 10. `_.pick(object, *keys)`

Yalnızca belirtilen key’leri alır.

```js
_.pick({ ad: "TkMatE", yas: 25, sehir: "Ankara" }, "ad", "sehir");  
// { ad: "TkMatE", sehir: "Ankara" }
```

---

## 🔸 11. `_.omit(object, *keys)`

Belirtilen key’leri hariç tutar.

```js
_.omit({ ad: "TkMatE", yas: 25, sehir: "Ankara" }, "yas");  
// { ad: "TkMatE", sehir: "Ankara" }
```

---

## 🔸 12. `_.defaults(object, *defaults)`

Yalnızca eksik (tanımsız) değerleri doldurur.

```js
_.defaults({ ad: "TkMatE" }, { ad: "Anonim", yas: 25 });  
// { ad: "TkMatE", yas: 25 }
```

---

## 🔸 13. `_.clone(object)`

Nesnenin yüzeysel kopyasını döner.

```js
const orijinal = { ad: "TkMatE" };
const kopya = _.clone(orijinal);
```

---

## 🔸 14. `_.tap(object, interceptor)`

Zincirleme işlemlerde araya girip işlem yapmanı sağlar, nesne döner.

```js
_.tap([1, 2, 3], arr => console.log("Ara:", arr));  
// Konsol: Ara: [1, 2, 3]
```

---

## 🔸 15. `_.has(object, key)`

Nesne o key’e sahip mi diye kontrol eder.

```js
_.has({ ad: "TkMatE" }, "ad");  
// true
```

---

## 🔸 16. `_.property(key)`

Verilen key’e göre bir erişim fonksiyonu döner.

```js
const getAd = _.property("ad");
getAd({ ad: "TkMatE" });  
// "TkMatE"
```

---

## 🔸 17. `_.matches(attrs)` / `_.matcher(attrs)`

Verilen özelliklere uyan nesneleri kontrol eder.

```js
const isAdmin = _.matches({ rol: "admin" });
isAdmin({ ad: "TkMatE", rol: "admin" });  
// true
```

---

## 🔸 18. `_.isEqual(a, b)`

Derin karşılaştırma yapar.

```js
_.isEqual({ a: 1 }, { a: 1 });  
// true
```

---

## 🔸 19. `_.isMatch(object, properties)`

Nesne, belirtilen özelliklerle eşleşiyor mu?

```js
_.isMatch({ ad: "TkMatE", rol: "admin" }, { rol: "admin" });  
// true
```

---

## 🔸 20. `_.isEmpty(object)`

Dizi, nesne veya string boş mu?

```js
_.isEmpty({});       // true
_.isEmpty([1, 2]);    // false
```

---

## 🔸 21. Tür Kontrolleri

|Fonksiyon|Açıklama|
|---|---|
|`_.isElement(el)`|DOM öğesi mi?|
|`_.isArray(val)`|Dizi mi?|
|`_.isObject(val)`|Nesne mi (null değilse)?|
|`_.isArguments(val)`|`arguments` objesi mi?|
|`_.isFunction(val)`|Fonksiyon mu?|
|`_.isString(val)`|String mi?|
|`_.isNumber(val)`|Sayı mı?|
|`_.isFinite(val)`|Sonlu sayı mı?|
|`_.isBoolean(val)`|Boolean mu?|
|`_.isDate(val)`|Date objesi mi?|
|`_.isRegExp(val)`|RegExp objesi mi?|
|`_.isError(val)`|Error objesi mi?|
|`_.isNaN(val)`|NaN mi?|
|`_.isNull(val)`|`null` mu?|
|`_.isUndefined(val)`|`undefined` mı?|

---

Bir sonraki adımda istersen **Function işlemleri** ile (örneğin `_.bind`, `_.debounce`, `_.memoize`, `_.once`) devam edebiliriz. Devam edeyim mi TkMatE?