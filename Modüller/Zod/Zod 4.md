
## 1. Array (Dizi)

Bir tipin dizisini doğrulamak için `z.array()` kullanılır.

```ts
const stringArray = z.array(z.string());

stringArray.parse(["a", "b", "c"]);   // ✅
stringArray.parse([1, 2, 3]);         // ❌ Error
```

### Kurallarla Güçlendirme

```ts
z.array(z.number()).min(2); // en az 2 eleman
z.array(z.string()).max(5); // en fazla 5 eleman
z.array(z.boolean()).length(3); // tam 3 eleman
```

---

## 2. Tuple

Sabit uzunlukta ve her index farklı tipte olabilir.

```ts
const tupleSchema = z.tuple([z.string(), z.number(), z.boolean()]);

tupleSchema.parse(["TkMatE", 25, true]); // ✅
tupleSchema.parse(["TkMatE", "25", true]); // ❌ Error
```

---

## 3. Enum

Enum değerlerinden sadece biri geçerli olur.

```ts
const roleSchema = z.enum(["user", "admin", "moderator"]);

roleSchema.parse("admin");  // ✅
roleSchema.parse("guest");  // ❌ Error
```

Enum değerlerine **tip** olarak da erişebilirsin:

```ts
type Role = z.infer<typeof roleSchema>;
// "user" | "admin" | "moderator"
```

---

## 4. Literal

Belirli tek bir değeri doğrular.

```ts
const trueSchema = z.literal(true);

trueSchema.parse(true);  // ✅
trueSchema.parse(false); // ❌ Error
```

Örneğin HTTP metodlarını kısıtlamak için:

```ts
const methodSchema = z.union([
  z.literal("GET"),
  z.literal("POST"),
  z.literal("PUT"),
  z.literal("DELETE"),
]);
```

---

## 5. Union

Birden fazla tipten herhangi biri olabilir.

```ts
const stringOrNumber = z.union([z.string(), z.number()]);

stringOrNumber.parse("TkMatE"); // ✅
stringOrNumber.parse(123);      // ✅
stringOrNumber.parse(true);     // ❌ Error
```

---

## 6. Intersection (Ekstra)

İki şemayı birleştirir → ikisinin de kurallarına uymalıdır.

```ts
const a = z.object({ name: z.string() });
const b = z.object({ age: z.number() });

const person = z.intersection(a, b);

person.parse({ name: "TkMatE", age: 25 }); // ✅
person.parse({ name: "TkMatE" }); // ❌ Error (age eksik)
```

---

📌 Özet:

- Array ile listeler doğrulandı ✅
- Tuple ile sabit uzunluklu diziler ✅
- Enum ile belirli seçenekler ✅
- Literal ile tek değer ✅
- Union & Intersection ile tip birleşimleri ✅
