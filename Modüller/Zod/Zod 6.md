
Uygulamada çoğu zaman **her alan zorunlu olmaz**, bazıları opsiyoneldir veya varsayılan değer alır. Zod bu durumları kolayca yönetir.

---

## 1. `optional()`

Bir alanı `undefined` olmasına izin verir.

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.number().optional(),
});

userSchema.parse({ username: "TkMatE" });       
// ✅ age opsiyonel
userSchema.parse({ username: "TkMatE", age: 25 });
// ✅ age verilebilir
```

---

## 2. `nullable()`

Bir alanın `null` olmasına izin verir.

```ts
const userSchema = z.object({
  middleName: z.string().nullable(),
});

userSchema.parse({ middleName: "Furkan" }); // ✅
userSchema.parse({ middleName: null });     // ✅
userSchema.parse({ middleName: 123 });      // ❌
```

---

## 3. `nullish()`

Hem `null` hem `undefined` kabul eder.

```ts
const schema = z.string().nullish();

schema.parse("TkMatE"); // ✅
schema.parse(null);     // ✅
schema.parse(undefined);// ✅
```

---

## 4. `default()`

Bir alan girilmezse **varsayılan değer** atanır.

```ts
const userSchema = z.object({
  username: z.string(),
  role: z.string().default("user"),
});

console.log(userSchema.parse({ username: "TkMatE" }));
// { username: "TkMatE", role: "user" }
```

👉 `default()` ile `undefined` verilirse bile otomatik varsayılır:

```ts
userSchema.parse({ username: "TkMatE", role: undefined });
// { username: "TkMatE", role: "user" }
```

---

## 5. Kombinasyonlar

```ts
z.string().optional().default("guest");
// Eğer değer verilmezse → "guest"
// Eğer undefined verilirse → "guest"
// Eğer string verilirse → verilen değer
```

---

📌 Özet:

- `optional()` → undefined olabilir ✅
- `nullable()` → null olabilir ✅
- `nullish()` → null veya undefined olabilir ✅
- `default()` → varsayılan değer atanır ✅
- Bunları kombinleyerek esnek şemalar oluşturabiliriz ✅
