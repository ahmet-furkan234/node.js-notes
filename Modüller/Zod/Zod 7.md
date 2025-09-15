
Bazen Zod’un hazır sunduğu `min`, `max`, `email` gibi doğrulamalar yeterli olmaz.  
İşte bu durumda **refinement** kullanarak **kendi özel kurallarımızı** tanımlarız.

---

## 1. `refine()`

`refine` ile istediğin koşulu yazabilirsin. Eğer koşul sağlanmazsa hata fırlatır.

```ts
const passwordSchema = z.string().refine((val) => val.length >= 8, {
  message: "Parola en az 8 karakter olmalı",
});

passwordSchema.parse("12345678"); // ✅
passwordSchema.parse("123");      
// ❌ Error: Parola en az 8 karakter olmalı
```

---

## 2. Birden Fazla Koşul

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.number(),
}).refine((data) => data.age >= 18, {
  message: "Yaş 18 veya üstü olmalı",
  path: ["age"], // hatayı ilgili alana bağlar
});

userSchema.parse({ username: "TkMatE", age: 20 }); // ✅
userSchema.parse({ username: "TkMatE", age: 15 }); // ❌
```

---

## 3. `superRefine()`

Daha gelişmiş doğrulama için `superRefine` kullanılır.  
Birden fazla hata ekleyebilirsin.

```ts
const passwordSchema = z.string().superRefine((val, ctx) => {
  if (val.length < 8) {
    ctx.addIssue({
      code: z.ZodIssueCode.too_small,
      minimum: 8,
      type: "string",
      message: "Parola en az 8 karakter olmalı",
    });
  }
  if (!/[A-Z]/.test(val)) {
    ctx.addIssue({
      code: z.ZodIssueCode.custom,
      message: "Parola en az bir büyük harf içermeli",
    });
  }
});

passwordSchema.parse("tkmate123"); // ❌ (büyük harf yok)
passwordSchema.parse("TkMatE123"); // ✅
```

- `val` = doğrulanan değer
- `ctx` = hata ekleme (ve gerektiğinde daha fazla kontrol yapma) bağlamı

---

## 4. Örnek: Şifre Tekrar Doğrulama

```ts
const registerSchema = z.object({
  password: z.string(),
  confirmPassword: z.string(),
}).refine((data) => data.password === data.confirmPassword, {
  message: "Parolalar eşleşmiyor",
  path: ["confirmPassword"],
});

registerSchema.parse({ password: "12345678", confirmPassword: "12345678" }); // ✅
registerSchema.parse({ password: "12345678", confirmPassword: "87654321" }); // ❌
```

---

📌 Özet:

- `refine` → tek bir koşul eklemek için ✅
- `superRefine` → daha karmaşık ve birden fazla hata üretmek için ✅
- Hata mesajı özelleştirme (`message`) ve hatayı ilgili alana bağlama (`path`) öğrendik ✅
