
Zod, en çok kullanılan **temel tipler** için hazır şemalar sunar. Bunları zincirleme (chaining) ile kurallarla güçlendirebiliriz.

---

## 1. String

```ts
const usernameSchema = z.string();

// ✅ Geçer
usernameSchema.parse("TkMatE");

// ❌ Geçmez
usernameSchema.parse(123); 
// Error: Expected string, received number
```

### String Kuralları

```ts
z.string().min(3); // minimum 3 karakter
z.string().max(10); // maksimum 10 karakter
z.string().email(); // email formatı
z.string().url();   // URL formatı
z.string().uuid();  // UUID formatı
z.string().regex(/^[a-z]+$/i); // regex ile kontrol
```

---

## 2. Number

```ts
const ageSchema = z.number();

// ✅ Geçer
ageSchema.parse(25);

// ❌ Geçmez
ageSchema.parse("25"); 
// Error: Expected number, received string
```

### Number Kuralları

```ts
z.number().min(18);     // en az 18
z.number().max(99);     // en fazla 99
z.number().int();       // tam sayı olmalı
z.number().positive();  // > 0
z.number().nonnegative(); // >= 0
z.number().finite();    // sonsuz olamaz
```

---

## 3. Boolean

```ts
const isAdminSchema = z.boolean();

isAdminSchema.parse(true);  // ✅
isAdminSchema.parse(false); // ✅
isAdminSchema.parse("true"); // ❌ Error
```

---

## 4. Date

```ts
const birthDateSchema = z.date();

birthDateSchema.parse(new Date("2000-01-01")); // ✅
birthDateSchema.parse("2000-01-01"); // ❌ string olduğu için hata
```

### Özel Kurallar

```ts
z.date().max(new Date()); // bugünden küçük/eşit olmalı
z.date().min(new Date("2000-01-01")); // 2000 sonrası olmalı
```

---

## 5. Null & Undefined

```ts
z.null().parse(null);   // ✅ sadece null geçerli
z.undefined().parse(undefined); // ✅ sadece undefined geçerli
```

Bir değeri **hem tipli hem null/undefined** yapmak için:

```ts
z.string().nullable();   // string veya null
z.string().optional();   // string veya undefined
z.string().nullish();    // string veya null veya undefined
```

---

## 6. Any & Unknown

```ts
z.any().parse(123);       // ✅ her şey geçerli
z.unknown().parse("abc"); // ✅ her şey geçerli
```

⚠️ Ama genelde tavsiye edilmez çünkü tip güvenliği bozulur.

---

📌 Özet:

- String, number, boolean, date gibi **temel tipleri** gördük ✅
- Her tip için doğrulama kurallarını zincirleme kullanabildiğimizi öğrendik ✅
- Null, undefined, any, unknown gibi özel tipleri gördük ✅
