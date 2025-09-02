
### 🔧 1. `_.bind(function, object, *arguments)`

Belirli bir nesneye bağlanmış bir fonksiyon döner.

```js
function greet() { return "Hello " + this.name; }
const user = { name: "TkMatE" };
const bound = _.bind(greet, user);
console.log(bound()); // "Hello TkMatE"
```

---

### 🔧 2. `_.bindAll(object, *methodNames)`

Bir nesne içindeki fonksiyonları bağlar (this kaymasını önler).

```js
const user = {
  name: "Ersin",
  sayHi() {
    return "Hi " + this.name;
  }
};
_.bindAll(user, "sayHi");
const say = user.sayHi;
console.log(say()); // "Hi Ersin"
```

---

### 🔧 3. `_.partial(function, *arguments)`

Bir fonksiyona önceden bazı argümanlar tanımlayarak kısmen uygulanmış bir fonksiyon oluşturur.

```js
function multiply(a, b) { return a * b; }
const double = _.partial(multiply, 2);
console.log(double(5)); // 10
```

---

### 🔧 4. `_.memoize(function, [hashFunction])`

Bir fonksiyonun çıktısını cache'leyerek aynı argümanlarla yapılan çağrılarda performansı artırır.

```js
const slowSquare = _.memoize(n => {
  console.log("Calculating...");
  return n * n;
});
console.log(slowSquare(4)); // Hesaplar ve 16 döner
console.log(slowSquare(4)); // Cache kullanır, tekrar hesaplamaz
```

---

### 🔧 5. `_.delay(function, wait, *arguments)`

Belirtilen süre sonra fonksiyonu çalıştırır (setTimeout alternatifi).

```js
_.delay(() => console.log("2 saniye sonra yazıldı"), 2000);
```

---

### 🔧 6. `_.defer(function, *arguments)`

Fonksiyonu bir sonraki event loop'ta çalıştırır (setTimeout(fn, 0) gibi).

```js
_.defer(() => console.log("Bu satır en sona ertelenir"));
console.log("Bu satır önce yazılır");
```

---

### 🔧 7. `_.throttle(function, wait, [options])`

Belirli aralıklarla sadece bir kez çalışmasına izin verir (scroll gibi olaylarda kullanılır).

```js
const throttled = _.throttle(() => console.log("Scroll olayı"), 1000);
window.addEventListener("scroll", throttled);
```

---

### 🔧 8. `_.debounce(function, wait, [immediate])`

Fonksiyon çağrılarını geciktirir; belirli bir sürede tekrar çağrılmazsa çalışır (search bar gibi).

```js
const debounced = _.debounce(() => console.log("Yazma bitti"), 1000);
document.addEventListener("keyup", debounced);
```

---

### 🔧 9. `_.once(function)`

Sadece bir kez çalışmasına izin verir.

```js
const initialize = _.once(() => console.log("İlk ve son kez çalıştı"));
initialize(); // Çalışır
initialize(); // Çalışmaz
```

---

### 🔧 10. `_.after(count, function)`

Belirli sayıda çağrıdan sonra çalışır.

```js
const done = _.after(3, () => console.log("Tüm işlemler bitti"));
done(); // yok
done(); // yok
done(); // "Tüm işlemler bitti"
```

---

### 🔧 11. `_.before(count, function)`

Yalnızca belirli sayıda çalışmasına izin verir.

```js
const limited = _.before(3, () => console.log("Sadece 2 defa çalışır"));
limited(); // çalışır
limited(); // çalışır
limited(); // çalışmaz
```

---

### 🔧 12. `_.wrap(function, wrapper)`

Bir fonksiyonu başka bir fonksiyonla sarar (decorator gibi).

```js
const greet = name => "Hello " + name;
const wrapped = _.wrap(greet, (fn, name) => {
  return ">>> " + fn(name) + " <<<";
});
console.log(wrapped("TkMatE")); // ">>> Hello TkMatE <<<"
```

---

### 🔧 13. `_.negate(predicate)`

Verilen koşul fonksiyonunun tersini döner (true → false, false → true).

```js
const isEven = x => x % 2 === 0;
const isOdd = _.negate(isEven);
console.log(isOdd(3)); // true
```

---

### 🔧 14. `_.compose(*functions)`

Fonksiyonları sağdan sola doğru birbirine zincirler.

```js
const greet = name => "hi: " + name;
const exclaim = sentence => sentence.toUpperCase() + "!";
const welcome = _.compose(exclaim, greet);
console.log(welcome("ersin")); // "HI: ERSIN!"
```

---

Tüm fonksiyonel metotlar tamamlandı ✅  
İstersen şimdi **Utility (Yardımcı Araçlar)** grubuna geçebiliriz. Hazırsan söyle.