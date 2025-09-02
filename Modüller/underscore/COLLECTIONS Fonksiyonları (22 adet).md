
### 1. `_.each(list, iteratee)`

Her öğe için işlem yapar.

```ts
_.each([1, 2, 3], function(num) {
  console.log(num * 2); // 2, 4, 6
});
```

---

### 2. `_.map(list, iteratee)`

Yeni dizi oluşturur, her elemanı dönüştürür.

```ts
_.map([1, 2, 3], function(num) {
  return num * 3;
}); // ➤ [3, 6, 9]
```

---

### 3. `_.reduce(list, iteratee, memo)`

Tek bir değere indirger.

```ts
_.reduce([1, 2, 3], function(memo, num) {
  return memo + num;
}, 0); // ➤ 6
```

---

### 4. `_.reduceRight(list, iteratee, memo)`

Sağdan sola indirger.

```ts
_.reduceRight([[0, 1], [2, 3], [4, 5]], function(a, b) {
  return a.concat(b);
}, []); // ➤ [4, 5, 2, 3, 0, 1]
```

---

### 5. `_.find(list, predicate)`

İlk eşleşen öğeyi bulur.

```ts
_.find([1, 2, 3, 4], num => num % 2 === 0); // ➤ 2
```

---

### 6. `_.filter(list, predicate)`

Koşulu sağlayanları döndürür.

```ts
_.filter([1, 2, 3, 4], num => num % 2 === 0); // ➤ [2, 4]
```

---

### 7. `_.where(list, properties)`

Nesne dizisinde belirtilen özelliklere göre eşleşenleri bulur.

```ts
_.where([
  { ad: "Ali", yas: 20 },
  { ad: "Ayşe", yas: 25 }
], { yas: 25 }); // ➤ [{ ad: "Ayşe", yas: 25 }]
```

---

### 8. `_.findWhere(list, properties)`

İlk eşleşeni döndürür.

```ts
_.findWhere([
  { ad: "Ali", yas: 20 },
  { ad: "Ayşe", yas: 25 }
], { yas: 25 }); // ➤ { ad: "Ayşe", yas: 25 }
```

---

### 9. `_.reject(list, predicate)`

Koşulu sağlamayanları döndürür.

```ts
_.reject([1, 2, 3, 4], num => num % 2 === 0); // ➤ [1, 3]
```

---

### 10. `_.every(list, predicate)`

Tüm elemanlar koşulu sağlıyor mu?

```ts
_.every([2, 4, 6], num => num % 2 === 0); // ➤ true
```

---

### 11. `_.some(list, predicate)`

En az bir eleman koşulu sağlıyor mu?

```ts
_.some([1, 3, 4], num => num % 2 === 0); // ➤ true
```

---

### 12. `_.contains(list, value)`

Dizi/nesnede belirli bir öğe var mı?

```ts
_.contains([1, 2, 3], 3); // ➤ true
```

---

### 13. `_.invoke(list, methodName)`

Listedeki her nesnede aynı metodu çağırır.

```ts
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort'); // ➤ [[1, 5, 7], [1, 2, 3]]
```

---

### 14. `_.pluck(list, propertyName)`

Nesne dizisinden belirli alanı çeker.

```ts
_.pluck([
  { ad: "Ali", yas: 20 },
  { ad: "Ayşe", yas: 25 }
], 'ad'); // ➤ ["Ali", "Ayşe"]
```

---

### 15. `_.max(list, iteratee?)`

En büyük değeri bulur.

```ts
_.max([10, 5, 100, 2]); // ➤ 100
```

---

### 16. `_.min(list, iteratee?)`

En küçük değeri bulur.

```ts
_.min([10, 5, 100, 2]); // ➤ 2
```

---

### 17. `_.sortBy(list, iteratee)`

Belirli kritere göre sırala.

```ts
_.sortBy([1, 2, 3, 4], num => -num); // ➤ [4, 3, 2, 1]
```

---

### 18. `_.groupBy(list, iteratee)`

Elemanları grupla.

```ts
_.groupBy([1.3, 2.1, 2.4], Math.floor); 
// ➤ { '1': [1.3], '2': [2.1, 2.4] }
```

---

### 19. `_.indexBy(list, iteratee)`

Anahtar olarak dönen değeri kullanır.

```ts
_.indexBy([
  { id: 'a', name: 'Ali' },
  { id: 'b', name: 'Ayşe' }
], 'id');
// ➤ { a: {...}, b: {...} }
```

---

### 20. `_.countBy(list, iteratee)`

Grupları sayar.

```ts
_.countBy([1, 2, 3, 4, 5], num => num % 2 === 0 ? 'even' : 'odd');
// ➤ { odd: 3, even: 2 }
```

---

### 21. `_.shuffle(list)`

Rastgele sırala.

```ts
_.shuffle([1, 2, 3, 4, 5]);
```

---

### 22. `_.sample(list, n?)`

Rastgele eleman(lar) seç.

```ts
_.sample([1, 2, 3, 4], 2); // ➤ Örn: [4, 2]
```

---

### 23. `_.toArray(list)`

Bir nesne/diziyi diziye çevirir.

```ts
_.toArray({ 0: 'a', 1: 'b', length: 2 }); // ➤ ['a', 'b']
```

---

### 24. `_.size(list)`

Uzunluğunu verir.

```ts
_.size({ a: 1, b: 2 }); // ➤ 2
```

---

Bu sadece ilk grup — **Collections (24 fonksiyon)**.

Bir sonraki adımda:

- 🔹 Arrays (dizi işlemleri)
    
- 🔹 Objects (nesne işlemleri)
    
- 🔹 Functions (fonksiyon yardımcıları)
    
- 🔹 Utilities
    
- 🔹 Chaining
    

isteğine göre sırayla detaylı örneklerle paylaşacağım.

👉 Devam etmek istediğin kategori hangisi olsun TkMatE?