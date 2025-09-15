
Zod’un `transform()` fonksiyonu, doğrulama sırasında **veriyi istediğin şekilde dönüştürmene** olanak sağlar.  
Yani hem validation hem de **mapping** işlemi tek adımda yapılabilir.

---

## 1. Basit Transform Örneği

```ts
import { z } from "zod";

const stringToNumber = z.string().transform((val) => parseInt(val, 10));

const result = stringToNumber.parse("123");
console.log(result); // 123 (number)
```

- `val` → gelen orijinal veri
- `transform()` → yeni değeri döndürür
- `parse()` → dönen değer artık **dönüştürülmüş tip** olur

---

## 2. Object Transform

Object içinde de kullanılabilir:

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.string().transform((val) => parseInt(val, 10)),
});

const result = userSchema.parse({ username: "TkMatE", age: "25" });
console.log(result);
// { username: "TkMatE", age: 25 }  → age artık number
```

---

## 3. Transform ile Zincirleme

```ts
const trimmedUppercase = z.string()
  .transform((val) => val.trim())
  .transform((val) => val.toUpperCase());

console.log(trimmedUppercase.parse("   tkMatE  ")); 
// "TKMATE"
```

---

## 4. Optional/Default ile Transform

```ts
const schema = z.string().optional().transform((val) => val?.trim() ?? "DEFAULT");

console.log(schema.parse("   hello ")); // "hello"
console.log(schema.parse(undefined));   // "DEFAULT"
```

---

## 5. Örnek: Form Verisi Dönüştürme

```ts
const formSchema = z.object({
  email: z.string().email().transform((val) => val.toLowerCase()),
  age: z.string().transform((val) => parseInt(val, 10)),
});

const result = formSchema.parse({ email: "USER@MAIL.COM", age: "30" });
console.log(result);
// { email: "user@mail.com", age: 30 }
```

---

📌 Özet:

- `transform()` → doğrulama sonrası veriyi dönüştürmek için ✅
- Zincirleme ile birden fazla işlem yapılabilir ✅
- Optional/default ile birlikte kullanılabilir ✅
- Tip güvenliğini korur, çünkü dönüş tipi artık `parse` sonucu tipinde olur ✅
