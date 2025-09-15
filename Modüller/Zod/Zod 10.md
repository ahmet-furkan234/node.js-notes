
Zod’un en büyük avantajlarından biri, **doğrulama şemalarından otomatik olarak TypeScript tipini üretmesidir**.  
Böylece hem runtime doğrulama hem de compile-time tip kontrolü tek yerde yapılabilir.

---

## 1. `z.infer` ile Tip Çıkarma

```ts
import { z } from "zod";

const userSchema = z.object({
  username: z.string(),
  age: z.number(),
  isAdmin: z.boolean().optional(),
});

// TypeScript tipi çıkar
type User = z.infer<typeof userSchema>;
```

Artık `User` tipi şöyle olur:

```ts
type User = {
  username: string;
  age: number;
  isAdmin?: boolean;
};
```

✅ Avantaj: Tipi manuel yazmana gerek yok, şemaya göre otomatik oluşur.

---

## 2. Transform ile Tip Dönüşümü

```ts
const schema = z.string().transform((val) => parseInt(val, 10));

type Num = z.infer<typeof schema>;
// Num artık number
```

---

## 3. Union, Literal, Enum ile Tip

```ts
const roleSchema = z.enum(["user", "admin"]);
type Role = z.infer<typeof roleSchema>;
// Role = "user" | "admin"

const unionSchema = z.union([z.string(), z.number()]);
type StringOrNumber = z.infer<typeof unionSchema>;
// StringOrNumber = string | number
```

---

## 4. Nested Object ve Array

```ts
const userSchema = z.object({
  username: z.string(),
  posts: z.array(z.object({ title: z.string() })),
});

type User = z.infer<typeof userSchema>;
/*
User = {
  username: string;
  posts: { title: string }[];
}
*/
```

---

## 5. Optional ve Default ile Tip

```ts
const schema = z.object({
  name: z.string(),
  role: z.string().default("user"),
  age: z.number().optional(),
});

type User = z.infer<typeof schema>;
/*
User = {
  name: string;
  role?: string;   // default var ama parse sonrası dolu
  age?: number;
}
*/
```

---

📌 Özet:

- Zod şeması → otomatik TypeScript tipi ✅
- Tip güvenliği tek yerde sağlanır, duplication yok ✅
- Transform, Union, Enum, Optional/Default ile tip uyumu korunur ✅
- Compile-time ve runtime doğrulama birlikte çalışır ✅