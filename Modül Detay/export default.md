
## 🔹 `export default` Ne Demek?

`export default`:

- Bir dosyada **yalnızca bir kere** kullanılabilir.
- Bu ifadeyle dışa aktarılan değer, başka bir dosyada **istediğin herhangi bir isimle** içe aktarılabilir.

### Örnek:

#### 📁 math.ts

```ts
export default function topla(a: number, b: number): number {
  return a + b;
}
```

#### 📁 main.ts

```ts
import islem from "./math"; // topla demedik ama çalışır
console.log(islem(2, 3)); // 5
```

Burada `topla` fonksiyonu `default` olarak dışa aktarıldığı için, `main.ts` dosyasında istediğin herhangi bir isimle (`islem`, `toplama`, `x`, vs.) içe aktarabilirsin.

---

## 🔸 Peki `default` olmazsa ne olur?

Eğer `export default` yerine sadece `export` kullanırsan, **adlı (named)** export olur.

### Örnek:

#### 📁 math.ts

```ts
export function topla(a: number, b: number): number {
  return a + b;
}
```

#### 📁 main.ts

```ts
import { topla } from "./math"; // süslü parantez ZORUNLU
console.log(topla(2, 3)); // 5
```

### Fark:

|Özellik|`export default`|`export` (named)|
|---|---|---|
|Kaç tane olabilir?|Yalnızca 1|İstediğin kadar|
|İçe aktarma şekli|İstediğin isimle|Aynı isimle, süslü parantez içinde|
|Tipik kullanım|Ana bileşen/fonksiyon|Yardımcı fonksiyonlar, sabitler|

---

## 🧠 Özetle

| Terim               | Anlamı                                    |
| ------------------- | ----------------------------------------- |
| `export default`    | Modülden varsayılan bir değer dışa aktar. |
| `import X from`     | Default export olanı içe aktarır.         |
| `export`            | Adlı export (birden fazla olabilir).      |
| `import { X } from` | Adlı export edilen `X`’i içe aktarır.     |

---

İstersen hem default hem de named export'u bir dosyada kullanabilirsin:

```ts
export default function topla(a: number, b: number): number {
  return a + b;
}

export function carp(a: number, b: number): number {
  return a * b;
}
```

```ts
import topla, { carp } from "./math";
```
