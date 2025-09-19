
## 🔹 Kurulum

Zod’u NPM veya Yarn ile kurabilirsin:

```bash
npm install zod
# veya
yarn add zod
```

TypeScript kullanıyorsan ekstra paket kurmana gerek yok çünkü Zod zaten **TypeScript dostu** gelir.

---

## 🔹 İlk Örnek: Basit String Doğrulama

```ts
import { z } from "zod";

// Şema tanımla
const nameSchema = z.string();

// Doğru veri
console.log(nameSchema.parse("TkMatE")); 
// Çıktı: "TkMatE"

// Yanlış veri
console.log(nameSchema.parse(123)); 
// ❌ Error: Expected string, received number
```

👉 `parse()` metodu, verilen veriyi kontrol eder.

- Eğer doğruysa **aynı veriyi geri döner**
- Yanlışsa **hata fırlatır**

---

## 🔹 Hataları Daha Güvenli Yakalamak

`parse` hata fırlatır. Eğer hata yakalamak yerine **safe** (güvenli) şekilde dönmesini istersen:

```ts
const result = nameSchema.safeParse("TkMatE");
console.log(result);
// { success: true, data: "TkMatE" }

const badResult = nameSchema.safeParse(123);
console.log(badResult);
// { success: false, error: [ZodError: ...] }
```

👉 `safeParse` her zaman obje döner:

- `{ success: true, data: ... }` → Doğru veri
- `{ success: false, error: ... }` → Hatalı veri

---

## 🔹 Birden Fazla Alanı Doğrulamak (Object Örneği)

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.number(),
});

// Doğru veri
console.log(userSchema.parse({ username: "TkMatE", age: 25 }));

// Yanlış veri
console.log(userSchema.parse({ username: "TkMatE", age: "25" }));
// ❌ Error: Expected number, received string
```

---

📌 Buraya kadar:

- Zod kurulumunu yaptık ✅
- `parse` ve `safeParse` arasındaki farkı gördük ✅
- İlk basit `string` ve `object` örneklerini yaptık ✅
