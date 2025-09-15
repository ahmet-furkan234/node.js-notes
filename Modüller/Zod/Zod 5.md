
Zod’un en güçlü yanı, nesneleri (object) şema halinde tanımlayıp iç içe doğrulama yapabilmesidir.

---

## 1. Basit Object

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.number(),
});

userSchema.parse({ username: "TkMatE", age: 25 }); // ✅
userSchema.parse({ username: "TkMatE", age: "25" }); // ❌ Error
```

---

## 2. Nested Object (İç İçe)

```ts
const addressSchema = z.object({
  city: z.string(),
  zipCode: z.string().min(5),
});

const userSchema = z.object({
  name: z.string(),
  address: addressSchema,
});

userSchema.parse({
  name: "TkMatE",
  address: { city: "Istanbul", zipCode: "34000" },
}); // ✅
```

---

## 3. Object içinde Array

```ts
const postSchema = z.object({
  title: z.string(),
  tags: z.array(z.string()),
});

postSchema.parse({
  title: "Zod Anlatımı",
  tags: ["typescript", "validation", "zod"],
}); // ✅
```

---

## 4. Object içinde Union

```ts
const shapeSchema = z.object({
  type: z.enum(["circle", "square"]),
  size: z.union([z.number(), z.string()]),
});

shapeSchema.parse({ type: "circle", size: 10 });   // ✅
shapeSchema.parse({ type: "square", size: "big" }); // ✅
shapeSchema.parse({ type: "triangle", size: 10 });  // ❌ Error
```

---

## 5. Strict, Passthrough, Strip

Zod ile **fazla alanlara nasıl davranacağını** belirleyebilirsin.

```ts
const userSchema = z.object({
  username: z.string(),
}).strict(); // Fazladan alan olursa hata

userSchema.parse({ username: "TkMatE" });            // ✅
userSchema.parse({ username: "TkMatE", age: 25 });   // ❌ Error
```

Alternatifler:

```ts
z.object({...}).passthrough(); // fazladan alanlara izin ver
z.object({...}).strip();       // fazladan alanları yok say
```

---

## 6. Partial ve Pick

Object şemalarını esnekleştirmek için:

```ts
const userSchema = z.object({
  username: z.string(),
  age: z.number(),
});

// Partial → tüm alanlar optional
const partialUser = userSchema.partial();
partialUser.parse({}); // ✅ age ve username opsiyonel oldu

// Pick → belli alanları seç
const usernameOnly = userSchema.pick({ username: true });
usernameOnly.parse({ username: "TkMatE" }); // ✅
```

---

## 7. Merge

İki object şemasını birleştirmek:

```ts
const baseUser = z.object({ username: z.string() });
const extra = z.object({ age: z.number() });

const mergedUser = baseUser.merge(extra);

mergedUser.parse({ username: "TkMatE", age: 25 }); // ✅
```

---

📌 Özet:

- Object ile alan doğrulamayı öğrendik ✅
- Nested object, array, union gibi iç içe yapılara baktık ✅
- strict/passthrough/strip farklarını gördük ✅
- partial, pick, merge gibi şema manipülasyonlarını öğrendik ✅
