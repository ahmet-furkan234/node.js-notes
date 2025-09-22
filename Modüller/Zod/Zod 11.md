
Zod, özellikle **Node.js / Express API** geliştirme sırasında request body’lerini doğrulamak için çok kullanışlıdır.  
Hem tip güvenliği sağlar hem de hatalı veri gelirse kullanıcıya anlamlı mesaj döner.

---

## 1. Örnek Kullanım: Express.js

```ts
import express from "express";
import { z } from "zod";

const app = express();
app.use(express.json());

// Zod şeması
const registerSchema = z.object({
  username: z.string().min(3, { message: "Username en az 3 karakter olmalı" }),
  email: z.string().email({ message: "Geçerli bir email giriniz" }),
  password: z.string().min(8, { message: "Parola en az 8 karakter olmalı" }),
  confirmPassword: z.string(),
}).refine((data) => data.password === data.confirmPassword, {
  message: "Parolalar eşleşmiyor",
  path: ["confirmPassword"],
});

// Route
app.post("/register", (req, res) => {
  const result = registerSchema.safeParse(req.body);

  if (!result.success) {
    return res.status(400).json({ errors: result.error.errors });
  }

  const userData = result.data; // Doğrulandı ve tip güvenli
  // DB kaydı, iş mantığı...
  res.json({ message: "Kayıt başarılı", user: userData });
});

app.listen(3000, () => console.log("Server çalışıyor 🚀"));
```

---

## 2. Özellikler

- `safeParse()` kullanarak **runtime hataları yakaladık**
- `refine()` ile **parola eşleşmesini kontrol ettik**
- `message` ve `path` ile **hata mesajlarını kullanıcıya bağladık**
- `result.data` → artık tip güvenli (`z.infer<typeof registerSchema>`) ✅

---

## 3. Optional & Default Örneği

```ts
const userSchema = z.object({
  username: z.string(),
  role: z.string().default("user"),
  age: z.number().optional(),
});

const result = userSchema.parse({ username: "TkMatE" });
// { username: "TkMatE", role: "user" } → age opsiyonel
```

---

## 4. Nested Object & Array Örneği

```ts
const orderSchema = z.object({
  userId: z.string(),
  items: z.array(
    z.object({
      productId: z.string(),
      quantity: z.number().min(1),
    })
  ),
});

const data = {
  userId: "abc123",
  items: [
    { productId: "p1", quantity: 2 },
    { productId: "p2", quantity: 1 },
  ],
};

orderSchema.parse(data); // ✅
```

---

📌 Özet:

- Zod ile **API request doğrulama** basit ve tip güvenli ✅
- Hatalar anlamlı mesajlarla dönüyor ✅
- Nested object, array, optional/default ve refine ile tüm gerçek hayat senaryoları kapsanıyor ✅
