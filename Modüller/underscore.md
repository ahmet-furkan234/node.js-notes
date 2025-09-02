
**Underscore.js**, JavaScript'in yetersiz kaldığı bazı alanlarda işe yarayan **yardımcı (utility) fonksiyonlar** sunan hafif bir kütüphanedir.
> Lodash çıkmadan önce en popüler "utility" kütüphaneydi. Hâlâ bazı projelerde kullanılmaktadır.

---

## 📦 Kurulum

```bash
npm install underscore
```

veya TypeScript kullanıyorsan tipi de kur:

```bash
npm install --save-dev @types/underscore
```

---

## 🧠 Kategorilere Göre Fonksiyonlar

Aşağıda `underscore` kütüphanesinin **en çok kullanılan fonksiyonlarını kategori kategori** açıklıyorum. Her birinin kısa örneğiyle birlikte.

---

### 🔹 1. **Collections (Diziler ve Nesneler)**

#### `_.each(list, iteratee)`

Her elemanı dolaşır (`forEach` gibi):

```ts
import _ from 'underscore';

_.each([1, 2, 3], (num) => console.log(num * 2)); // 2, 4, 6
```

---

#### `_.map(list, iteratee)`

Her elemanı dönüştürür:

```ts
_.map([1, 2, 3], (num) => num * 3); // ➤ [3, 6, 9]
```

---

#### `_.filter(list, predicate)`

Filtreleme:

```ts
_.filter([1, 2, 3, 4], num => num % 2 === 0); // ➤ [2, 4]
```

---

#### `_.find(list, predicate)`

İlk eşleşeni bulur:

```ts
_.find([1, 2, 3], num => num > 1); // ➤ 2
```

---

#### `_.reduce(list, iteratee, memo)`

Toplama veya gruplama gibi işlemler:

```ts
_.reduce([1, 2, 3], (sum, num) => sum + num, 0); // ➤ 6
```

---

### 🔹 2. **Arrays**

#### `_.first(array, n?)`

İlk eleman(lar):

```ts
_.first([5, 4, 3, 2], 2); // ➤ [5, 4]
```

---

#### `_.last(array, n?)`

Son eleman(lar):

```ts
_.last([5, 4, 3, 2], 2); // ➤ [3, 2]
```

---

#### `_.uniq(array)`

Tekrarsız hale getirir:

```ts
_.uniq([1, 2, 2, 3, 3]); // ➤ [1, 2, 3]
```

---

#### `_.flatten(array)`

Çok boyutlu diziyi düzleştirir:

```ts
_.flatten([1, [2], [3, [[4]]]]); // ➤ [1, 2, 3, 4]
```

---

#### `_.without(array, ...values)`

Belirli elemanları dışla:

```ts
_.without([1, 2, 1, 3], 1); // ➤ [2, 3]
```

---

### 🔹 3. **Objects**

#### `_.keys(obj)` & `_.values(obj)`

```ts
const obj = { a: 1, b: 2 };
_.keys(obj);   // ➤ ['a', 'b']
_.values(obj); // ➤ [1, 2]
```

---

#### `_.extend(destObj, ...sourceObjs)`

Birleştirme:

```ts
_.extend({ name: 'Tk' }, { age: 25 }); // ➤ { name: 'Tk', age: 25 }
```

---

#### `_.pick(obj, keys)` & `_.omit(obj, keys)`

```ts
_.pick({ a: 1, b: 2, c: 3 }, ['a', 'c']); // ➤ { a: 1, c: 3 }
_.omit({ a: 1, b: 2, c: 3 }, ['b']);      // ➤ { a: 1, c: 3 }
```

---

### 🔹 4. **Functions**

#### `_.debounce(fn, wait)`

Bir fonksiyonu belirli süre içinde sadece bir kez çalıştırır. (Lodash’ta daha çok kullanılır)

#### `_.once(fn)`

Fonksiyon sadece 1 kez çalışır:

```ts
const initialize = _.once(() => console.log("Başlatıldı!"));
initialize(); // çalışır
initialize(); // çalışmaz
```

---

### 🔹 5. **Utility (Yardımcılar)**

#### `_.identity(value)`

Gelen değeri aynen döndürür. Bazı varsayılan işlemlerde kullanılır.

#### `_.random(min, max)`

Rastgele sayı üretir:

```ts
_.random(10, 20); // 10 ile 20 arasında rastgele bir sayı
```

---

## 📌 Neden `underscore` kullanılır?

- Kapsamlı utility fonksiyonları sayesinde kısa ve okunabilir kod yazmanı sağlar
- Karmaşık işlemleri sadeleştirir
- Node.js, tarayıcı, TypeScript gibi ortamlarda rahatça kullanılabilir

---

## 🔄 `Underscore` vs `Lodash`

|Özellik|Underscore|Lodash|
|---|---|---|
|Yaygınlık|Daha eski|Daha güncel|
|Performans|Orta|Daha iyi|
|Modüler yapılar|Yok|✅ Evet (tek tek import)|
|Tavsiye|Orta projelerde|✅ Modern projelerde|

---

## 🔚 Sonuç

`underscore`, hâlâ öğrenmeye ve bazı projelerde kullanmaya değer bir kütüphanedir.  
Ama modern projelerde Lodash veya native JS methodlar (`Array.map`, `Object.entries` vs.) daha çok tercih edilir.
