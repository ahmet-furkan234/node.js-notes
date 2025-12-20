
> İncelediğimiz satır:

```js
Error.captureStackTrace(this, this.constructor);
```

Bu **Node.js’e özel** bir API’dir ve stack trace’in **nereden başlatılacağını** kontrol eder.

---

# 1️⃣ Bu satır YOKKEN oluşan çıktı

### Kod

```js
class MyError extends Error {
  constructor(message) {
    super(message);
  }
}

function a() {
  throw new MyError("Something went wrong");
}

function b() {
  a();
}

b();
```

### Stack Trace (çıktı)

```
MyError: Something went wrong
    at new MyError (error.js:3:5)
    at a (error.js:8:9)
    at b (error.js:12:3)
    at Object.<anonymous> (error.js:15:1)
```

### ❌ Problem

- `new MyError` **stack’e giriyor**
- Asıl hata **a()** fonksiyonunda olmasına rağmen
- Debug sırasında **gürültü** oluşuyor

---

# 2️⃣ `Error.captureStackTrace(this, this.constructor);` VARKEN

### Kod

```js
class MyError extends Error {
  constructor(message) {
    super(message);
    Error.captureStackTrace(this, this.constructor);
  }
}

function a() {
  throw new MyError("Something went wrong");
}

function b() {
  a();
}

b();
```

### Stack Trace (çıktı)

```
MyError: Something went wrong
    at a (error.js:9:9)
    at b (error.js:13:3)
    at Object.<anonymous> (error.js:16:1)
```

### ✅ Kazanım

- `new MyError` **stack’ten çıkarıldı**
- Stack trace **gerçek hata noktasından** başlıyor
- Okunabilirlik ciddi şekilde arttı

---

# 3️⃣ Ne Yaptı Bu Satır? (Teknik açıklama)

```js
Error.captureStackTrace(target, constructorOpt)
```

|Parametre|Anlam|
|---|---|
|`target`|Stack’in yazılacağı nesne|
|`constructorOpt`|**Bu fonksiyona kadar olan stack’i kes**|

Yani:

```js
this.constructor
```

→ **MyError constructor’ına kadar olan çağrıları stack’ten sil**

---

# 4️⃣ Error Stack Tree mantığında fark

### ❌ Olmadan

```
b()
 └── a()
      └── new MyError()
           └── ❌ Error
```

### ✅ Varken

```
b()
 └── a()
      └── ❌ Error
```

➡️ Tree **temizlenmiş** olur  
➡️ Root-cause daha net çıkar

---

# 5️⃣ Clean Architecture / DDD’de neden kritik?

Senin kurduğun yapılarda:

```
Controller
 └── UseCase
      └── DomainError (constructor)
```

Eğer `captureStackTrace` yoksa:

- Her DomainError stack’te görünür
- Infra + domain + wrapper katmanları **log’u kirletir**

Varken:

- **Hata nerede fırlatıldıysa** oradan başlar
- Log = olayın kendisi

---

# 6️⃣ Ne Zaman MUTLAKA kullanmalısın?

✔ Custom Error sınıfı yazıyorsan  
✔ Domain / Application / Infra error ayrımı yapıyorsan  
✔ Log’ları APM / ELK / Sentry’ye atıyorsan  
✔ Plugin-based mimaride hata ayıklıyorsan

🚫 Browser tarafında gerekmez (Node’a özel)