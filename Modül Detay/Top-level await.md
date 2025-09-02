
👉 **Top-level await**, bir modül dosyasının en üst seviyesinde (bir fonksiyonun, bloğun içinde olmadan) doğrudan `await` ifadesini kullanabilmeyi sağlar.

📌 **Önceden ne olurdu?

```js
// ❌ Hata verirdi (ES6 öncesi ve ES6 modüller desteklenmeden)
const data = await fetchData();  // SyntaxError: await is only valid in async function
```

`await` sadece bir `async function` içinde kullanılabilirdi.

---

# 🌟 **Top-level await ile ne değişti?**

✅ ES2022 (ES13) ile, **ES6 modül dosyalarının içinde doğrudan `await` kullanabiliyoruz.**  
✅ Yani artık şöyle yazmak mümkün:

```js
// module.js
const veri = await fetch("https://jsonplaceholder.typicode.com/posts/1")
                  .then(res => res.json());

console.log(veri);
```

👉 Burada `await` bir fonksiyonun içinde değil; dosyanın en üst seviyesinde.

---

# 🎯 **Neden top-level await geldi?**

💡 Önceden bir modülde async bir işlem yapman gerektiğinde:

```js
async function baslat() {
  const data = await fetch(...);
  console.log(data);
}
baslat();
```

yapmak zorundaydın.

💡 Artık bunu fonksiyon sarmalına gerek kalmadan doğrudan yazabilirsin:

```js
const data = await fetch(...);
console.log(data);
```

---

# 🚀 **Top-level await nerede çalışır?**

✅ **ES6 modül dosyalarında (.mjs veya .js + `type: module`)**
✅ Node.js + tarayıcı ortamında

❌ **CommonJS dosyalarında (require/module.exports)** desteklenmez!

---

# 📌 **Küçük bir örnek**

### math.mjs

```js
export const PI = 3.14;
export async function getRandomNumber() {
  return Math.random();
}
```

### app.mjs

```js
import { PI, getRandomNumber } from './math.mjs';

console.log("PI:", PI);

const rnd = await getRandomNumber();
console.log("Rastgele sayı:", rnd);
```

✅ Çalıştır:

```js
node app.mjs
```

---
# ⚡ **Top-level await avantajları**

|Avantaj|Açıklama|
|---|---|
|Daha basit sözdizimi|async fonksiyon yazmadan doğrudan await|
|Daha okunabilir modüller|modül başlatılırken async işlemler doğal bir akışta yazılabilir|
|import dinamik kullanımı kolaylaşır|await ile dinamik import kullanılabilir|

---

# 📝 **Top-level await + dinamik import örneği**

```js
const mod = await import('./math.mjs');
console.log(await mod.getRandomNumber());
```

✅ Dinamik modül yüklemede artık promise then yazmaya gerek yok.

---

# ⚠ **Top-level await’in yan etkileri**

💡 Modülün yüklenmesi gecikebilir → import eden modüller de await tamamlanana kadar bekler.  
💡 Aşırı bekleme durumları zincirleme bloklanmaya yol açabilir → dikkatli kullanılmalı.

---

# 🎨 **Özet**

|                                 | Top-level await                                          | Normal await           |
|:--------------------------------|:---------------------------------------------------------|:-----------------------|
| Kullanım yeri                   | ES6 modülün en üst seviyesi                              | async fonksiyon içinde |
| Fonksiyon sarmalaması gerek mi? | Hayır                                                    | Evet                   |
| Destek                          | ES2022+, Node.js 14+ (flag'lı), Node.js 16+ (tam destek) | Her yerde              |  
