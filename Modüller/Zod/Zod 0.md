
---
## Zod 1: Kurulum

````bash
npm install zod
# veya
yarn add zod
````

---

## Zod 2: Basit Örnek

```ts
import { z } from "zod";

const nameSchema = z.string();
nameSchema.parse("TkMatE");       // ✅
nameSchema.safeParse(123);        // { success: false, error: ... }
```

---

## Zod 3: Temel Tipler

- `z.string()`, `z.number()`, `z.boolean()`, `z.date()`
- Kurallar: `.min()`, `.max()`, `.email()`, `.regex()`, `.int()`, `.positive()`, `.nullable()`, `.optional()`, `.default()`
- `z.any()`, `z.unknown()`

---

## Zod 4: Array, Tuple, Enum, Union, Literal

- `z.array()`, `z.tuple()`
- `z.enum([...])`
- `z.literal(value)`
- `z.union([...])`, `z.intersection(a,b)`

---

## Zod 5: Object ve Nested Yapılar

- `z.object({ ... })`
- İç içe object ve array
- `.strict()`, `.passthrough()`, `.strip()`
- `.partial()`, `.pick()`, `.merge()`

---

## Zod 6: Opsiyonel ve Default

- `.optional()` → undefined olabilir
- `.nullable()` → null olabilir
- `.nullish()` → null veya undefined olabilir
- `.default(value)` → varsayılan değer atanır

---

## Zod 7: Refinement / Özel Doğrulama

- `.refine()` → tek koşul
- `.superRefine()` → birden fazla koşul ve custom hata
- `ctx.addIssue({ code, message, path })`

---

## Zod 8: Transform / Veri Dönüştürme

- `.transform(val => ...)` → parse sırasında dönüştürme
- Zincirleme transform
- Optional ve default ile kombinlenebilir

---

## Zod 9: Hata Yakalama ve Custom Mesaj

- `parse()` → exception fırlatır
- `safeParse()` → objede success/error döner
- Hata mesajı: `message`
- Hata alanı: `path`
- `refine()` ve `superRefine()` ile custom mesaj

---

## Zod 10: TypeScript Entegrasyonu

- `type User = z.infer<typeof schema>` ile otomatik tip
- Transform, Union, Enum, Optional/Default tip uyumlu
- Compile-time + runtime tip güvenliği

---

## Zod 11: API Request Body Doğrulama

- Express.js ile request.body doğrulama
- Nested object, array, optional/default, refine kullanımı
- safeParse ile hataları yakalama
- result.data ile tip güvenli veri

---