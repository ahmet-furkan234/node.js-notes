
✅ **Dinamik import**, bir modülü **kodun çalışması sırasında (runtime)** yüklemene yarayan bir tekniktir.  
✅ Şöyle bir yapıdadır:

```js
const mod = await import('./modul.js');
```

veya

```js
import('./modul.js').then(mod => {
  // mod ile işlem yapılır
});
```

💡 Yani **import() fonksiyon gibi çalışır ve Promise döner.**

---

## 🔑 **Normal import (statik import) ile farkı**

Statik import:

```js
import { topla } from './math.js';
```

✅ Kod yüklenirken hemen işlenir.
✅ Tüm modül baştan yüklenir.

Dinamik import:

```js
const mod = await import('./math.js');
console.log(mod.topla(2,3));
```

✅ İhtiyaç duyulana kadar modül yüklenmez.  
✅ Daha esnek ve koşula bağlı modül yüklenebilir.

---

# 🚀 **Nerelerde kullanılır?**

✅ Kullanıcının bir butona tıklamasıyla modül yüklemek  
✅ Belirli bir koşul sağlanınca modül yüklemek  
✅ Ağır modülleri sayfa başında değil, ihtiyaç olduğunda yüklemek (lazy loading)  
✅ Kod parçalarını bölüp performansı artırmak

---

# 🌟 **Örnek**

### 📂 Dizinin

```lua
proje/
 ├── app.mjs
 └── math.mjs
```

### math.mjs

```js
export function topla(a, b) {
  return a + b;
}
```

### app.mjs

```js
if (Math.random() > 0.5) {
  const mod = await import('./math.mjs');
  console.log("Toplam:", mod.topla(4, 5));
} else {
  console.log("Modül yüklenmedi çünkü koşul sağlanmadı.");
}
```

▶ Çalıştır:

```js
node app.mjs
```

👉 Bazen modül yüklenir, bazen yüklenmez. Koşula bağlı!

---

# 🌟 **Dinamik import’un avantajları**

|Avantaj|Açıklama|
|---|---|
|Lazy loading|Büyük modüller başta yüklenmez, ihtiyaç olduğunda yüklenir|
|Koşullu yükleme|Modülleri sadece gerekli olduğunda yükleyebilirsin|
|Performans|Başlangıçta daha az dosya yüklenir, sayfa ya da uygulama daha hızlı açılır|
|Promise desteği|import() Promise döner, async/await ile uyumludur|

---

# 📌 **Dinamik import + async/await**

```js
const mod = await import('./math.mjs');
console.log(mod.topla(2,3));
```

# 📌 **Dinamik import + then**

```js
import('./math.mjs').then(mod => {
  console.log(mod.topla(2,3));
});
```

---

# ⚠ **Nelere dikkat etmeli?**

❗ Sadece ES6 modüllerle çalışır (CommonJS değil)  
❗ import edilen dosya ES6 modül olmalı (ör. `.mjs` ya da `.js` + `"type":"module"`)  
❗ Kod yapısında await kullanıyorsan top-level await destekli bir ortam gerekir (ör. ES6 modül dosyası)

---


|                      | Statik import            | Dinamik import           |
|:---------------------|:-------------------------|:-------------------------|
| Yazım şekli          | `import {x} from ...`    | `import('...')`          |
| Yükleme zamanı       | Kod başında (build-time) | Çalışma zamanı (runtime) |
| Promise döner mi?    | Hayır                    | Evet                     |
| Koşullu olabilir mi? | Hayır                    | Evet                     |
| Lazy loading desteği | Yok                      | Var                      |  