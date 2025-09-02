
### 1. `_.first(array, [n])`

İlk elemanı veya ilk `n` elemanı döner.

```ts
_.first([10, 20, 30]);         // ➤ 10
_.first([10, 20, 30], 2);      // ➤ [10, 20]
```

---

### 2. `_.initial(array, [n])`

Son eleman haricindeki tüm elemanlar veya son `n` elemanı atlayarak döner.

```ts
_.initial([10, 20, 30, 40]);     // ➤ [10, 20, 30]
_.initial([10, 20, 30, 40], 2);  // ➤ [10, 20]
```

---

### 3. `_.last(array, [n])`

Son elemanı veya son `n` elemanı döner.

```ts
_.last([10, 20, 30]);        // ➤ 30
_.last([10, 20, 30], 2);     // ➤ [20, 30]
```

---

### 4. `_.rest(array, [n])`

İlk eleman(lar) hariç geri kalanları döner.

```ts
_.rest([10, 20, 30]);        // ➤ [20, 30]
_.rest([10, 20, 30], 2);     // ➤ [30]
```

---

### 5. `_.compact(array)`

Falsy (false, null, 0, "", undefined, NaN) değerleri çıkarır.

```ts
_.compact([0, 1, false, 2, '', 3]); // ➤ [1, 2, 3]
```

---

### 6. `_.flatten(array, [shallow])`

Çok katmanlı diziyi düzleştirir.

```ts
_.flatten([1, [2], [3, [[4]]]]);        // ➤ [1, 2, 3, 4]
_.flatten([1, [2], [3, [[4]]]], true);  // ➤ [1, 2, 3, [[4]]]
```

---

### 7. `_.without(array, *values)`

Belirtilen değerleri diziden çıkarır.

```ts
_.without([1, 2, 1, 0, 3, 1, 4], 0, 1); // ➤ [2, 3, 4]
```

---

### 8. `_.union(*arrays)`

Tüm dizileri birleştirir, tekrarsız hale getirir.

```ts
_.union([1, 2], [2, 3], [3, 4]); // ➤ [1, 2, 3, 4]
```

---

### 9. `_.intersection(*arrays)`

Tüm dizilerde ortak olan elemanları döner.

```ts
_.intersection([1, 2, 3], [2, 3, 4]); // ➤ [2, 3]
```

---

### 10. `_.difference(array, *others)`

İlk dizide olup diğerlerinde olmayanları döner.

```ts
_.difference([1, 2, 3, 4], [2, 4]); // ➤ [1, 3]
```

---

### 11. `_.uniq(array, [isSorted], [iteratee])`

Tekrarlı değerleri kaldırır.

```ts
_.uniq([1, 2, 1, 3, 1, 4]); // ➤ [1, 2, 3, 4]
```

---

### 12. `_.zip(*arrays)`

Aynı indeksleri gruplayarak dizileri birleştirir.

```ts
_.zip(['a', 'b'], [1, 2], [true, false]);
// ➤ [['a', 1, true], ['b', 2, false]]
```

---

### 13. `_.unzip(array)`

Zip'in tersini yapar.

```ts
_.unzip([['a', 1, true], ['b', 2, false]]);
// ➤ [['a', 'b'], [1, 2], [true, false]]
```

---

### 14. `_.object(list, [values])`

Anahtar-değer çifti oluşturur.

```ts
_.object(['ad', 'yas'], ['TkMatE', 25]); // ➤ { ad: 'TkMatE', yas: 25 }

_.object([['ad', 'Tk'], ['yas', 30]]);   // ➤ { ad: 'Tk', yas: 30 }
```

---

### 15. `_.indexOf(array, value, [isSorted])`

İlk eşleşen elemanın indeksini döner.

```ts
_.indexOf([1, 2, 3, 1, 2, 3], 2); // ➤ 1
```

---

### 16. `_.lastIndexOf(array, value, [fromIndex])`

Son eşleşen elemanın indeksini döner.

```ts
_.lastIndexOf([1, 2, 3, 1, 2, 3], 2); // ➤ 4
```

---

### 17. `_.sortedIndex(array, value, [iteratee])`

Sıralı dizide bir değerin yerleştirileceği index.

```ts
_.sortedIndex([10, 20, 30, 40], 25); // ➤ 2
```

---

### 18. `_.range([start], stop, [step])`

Belirli aralıkta dizi oluşturur.

```ts
_.range(5);           // ➤ [0, 1, 2, 3, 4]
_.range(1, 5);        // ➤ [1, 2, 3, 4]
_.range(0, 10, 2);    // ➤ [0, 2, 4, 6, 8]
```

---

Bu kısımda toplam **18 array fonksiyonunun tamamını** örnekleriyle ele aldık.

Sıradaki kategoriye geçelim mi?

- ✅ `Objects (nesne işlemleri)`
    
- ✅ `Functions (fonksiyon yardımcıları)`
    
- ✅ `Utilities`
    
- ✅ `Chaining`
    

Hangisini önce istersin TkMatE?