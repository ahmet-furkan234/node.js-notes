
Aslında `export as` diye **doğrudan bir ifade** yoktur ama:

- `as` anahtar kelimesi hem **export** hem de **import** işlemlerinde "isim değiştirerek kullanma" amacıyla kullanılır.

---

## ✅ 1. `export { something as newName }`

Bir değeri farklı bir adla dışa aktarmak.

### 📁 math.ts

```ts
function topla(a: number, b: number): number {
  return a + b;
}

function cikar(a: number, b: number): number {
  return a - b;
}

export { topla as add, cikar }; // topla'yı add adıyla dışa aktarıyoruz
```

### 📁 main.ts

```ts
import { add, cikar } from "./math";

console.log(add(3, 2));   // 5
console.log(cikar(3, 2)); // 1
```

---

## ✅ 2. `import { something as newName }`

Bir değeri dışa aktarıldığı adından farklı bir adla **içe aktarmak**.

### 📁 math.ts

```ts
export function carp(a: number, b: number): number {
  return a * b;
}
```

### 📁 main.ts

```ts
import { carp as multiply } from "./math";

console.log(multiply(3, 4)); // 12
```

---

## ✅ 3. Tipleri export ederken `as` kullanmak

### 📁 types.ts

```ts
export type { User as AppUser, Product as AppProduct } from "./models";
```

Bu durumda `./types.ts` üzerinden `AppUser` ve `AppProduct` adlarıyla tiplere erişilebilir.

---

## 🎯 Nerelerde Kullanılır?

- Kodun daha okunaklı veya standart olmasını sağlamak için.
- Kütüphaneleri kendi projene uygun isimlerle kullanmak için.
- Aynı modülden gelen isim çakışmalarını önlemek için.

---

## 🧠 Özet Tablo

|Kullanım|Amaç|Örnek|
|---|---|---|
|`export { x as y }`|Farklı adla dışa aktar|`export { topla as add }`|
|`import { x as y }`|Farklı adla içe aktar|`import { add as topla }`|
|`export type { A as B }`|Tip adını değiştirerek dışa aktar|`export type { User as AppUser }`|
