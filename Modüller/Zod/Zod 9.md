
Zod’da doğrulama hataları **otomatik olarak `ZodError`** nesnesi şeklinde gelir.  
Ama çoğu zaman **custom mesajlar veya kullanıcıya anlamlı hata bilgisi** göstermek isteriz.

---

## 1. `parse()` ile Hata Yakalama

`parse()` metodu hatalı veri girildiğinde **throw (fırlatma)** yapar.  
Bunu try/catch ile yakalayabiliriz:

```ts
import { z } from "zod";

const ageSchema = z.number().min(18, { message: "Yaş 18 veya üstü olmalı" });

try {
  ageSchema.parse(15);
} catch (e) {
  if (e instanceof z.ZodError) {
    console.log(e.errors);
  }
}
```

Çıktı:

```json
[
  {
    "code": "too_small",
    "minimum": 18,
    "type": "number",
    "inclusive": true,
    "message": "Yaş 18 veya üstü olmalı",
    "path": []
  }
]
```

---

## 2. `safeParse()` ile Hata Yakalama

`safeParse()` hata fırlatmaz, **objeyi döndürür**:

```ts
const result = ageSchema.safeParse(15);

console.log(result);
// {
//   success: false,
//   error: ZodError { errors: [ { message: "Yaş 18 veya üstü olmalı", ... } ] }
// }
```

- `{ success: true, data: ... }` → veri doğru
- `{ success: false, error: ... }` → veri hatalı

---

## 3. Object Hatalarında Path Kullanımı

Object içinde hangi alan hatalıysa, `path` ile belirtilir:

```ts
const userSchema = z.object({
  username: z.string().min(3, { message: "Username en az 3 karakter olmalı" }),
  age: z.number().min(18, { message: "Yaş 18 veya üstü olmalı" }),
});

const result = userSchema.safeParse({ username: "Tk", age: 15 });
console.log(result.error?.errors);
```

Çıktı:

```json
[
  { "message": "Username en az 3 karakter olmalı", "path": ["username"], ... },
  { "message": "Yaş 18 veya üstü olmalı", "path": ["age"], ... }
]
```

---

## 4. Custom Error Mesajı `refine()` ile

```ts
const passwordSchema = z.string().refine((val) => val.length >= 8, {
  message: "Parola en az 8 karakter olmalı",
});

passwordSchema.safeParse("123"); 
// → Hata: "Parola en az 8 karakter olmalı"
```

---

## 5. Custom Error Mesajı `superRefine()` ile

`superRefine` ile birden fazla özel hata ekleyebilirsin ve her hatayı alanına bağlayabilirsin:

```ts
const registerSchema = z.object({
  password: z.string(),
  confirmPassword: z.string(),
}).superRefine((val, ctx) => {
  if (val.password.length < 8) {
    ctx.addIssue({ message: "Parola en az 8 karakter olmalı", path: ["password"], code: z.ZodIssueCode.too_small });
  }
  if (val.password !== val.confirmPassword) {
    ctx.addIssue({ message: "Parolalar eşleşmiyor", path: ["confirmPassword"], code: z.ZodIssueCode.custom });
  }
});
```

---

📌 Özet:

- `parse()` → hatalı veride exception fırlatır ✅
- `safeParse()` → hatayı objede döndürür ✅
- `message` → her doğrulama için özel mesaj eklenebilir ✅
- `path` → hatanın hangi alanla ilgili olduğunu belirtir ✅
- `superRefine` → birden fazla özel hata eklemek mümkün ✅
