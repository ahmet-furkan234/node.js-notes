
`setImmediate`, Node.js’in event loop’unda **bir sonraki “check” fazında** callback fonksiyonunu çalıştıran bir zamanlayıcıdır. Yani, hemen değil, şu anki event loop turu tamamlandıktan sonra çalışır.

---

## 1. **`setImmediate` Nasıl Çalışır?**

- Callback fonksiyonunu, şu anki I/O olaylarının ardından ama sonraki event loop döngüsünde çalıştırır.
- **`setTimeout(fn, 0)`**’den farklıdır, çünkü `setTimeout` timer fazında işler, `setImmediate` check fazında.

---

## 2. **Kullanımı**

```js
console.log("Başladı");

setImmediate(() => {
  console.log("setImmediate callback çalıştı");
});

console.log("Bitti");
```

**Çıktı:**

```
Başladı
Bitti
setImmediate callback çalıştı
```

---

## 3. **`setImmediate` vs `setTimeout(fn, 0)`**

Her ikisi de asenkron olarak callback çalıştırır ama zamanlama farklıdır.

- `setTimeout(fn, 0)` → Timer fazında, minimum 1 ms gecikme olabilir.
- `setImmediate(fn)` → I/O tamamlandıktan sonra, check fazında çalışır, genellikle daha hızlıdır.

### Örnek:

```js
setTimeout(() => console.log("timeout"), 0);
setImmediate(() => console.log("immediate"));
```

Çıktı çoğunlukla:

```
immediate
timeout
```

---

## 4. **Ne Zaman Kullanılır?**

- I/O işlemlerinden sonra, hemen çalışması gereken ama şu anki kodun bitmesini bekleyecek işleri koymak için.
- Döngüsel işlemler veya event loop kontrolü için.

---

## 5. **`setImmediate` ile Recursive (Özyinelemeli) Örnek**

```js
let count = 0;

function sayHello() {
  console.log("Merhaba", count);
  count++;
  if (count < 5) {
    setImmediate(sayHello);
  }
}

sayHello();
```

---

## 6. **Özet**

|Özellik|Açıklama|
|---|---|
|`setImmediate`|Callback’i event loop’un check fazında çalıştırır|
|`setTimeout(fn,0)`|Timer fazında, biraz daha gecikmeli çalışır|
|Kullanım alanı|I/O sonrası hızlı, asenkron işlemler için|
