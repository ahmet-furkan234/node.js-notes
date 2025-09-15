
Zod, **TypeScript ve JavaScript için bir veri doğrulama (validation) ve tip güvence (type safety) kütüphanesidir.**  
Amaç: Uygulamada aldığımız verilerin (örneğin API’den gelen body, query, parametre, form inputları vs.) **beklenen formatta olup olmadığını** kontrol etmektir.

---

## 🔹 Neden Kullanılır?

1. **Tip Güvenliği (Type Safety):**  
    TypeScript compile-time’da (derleme zamanı) tip kontrolü yapar. Ama runtime’da (çalışma anında) dışarıdan gelen verilerin doğru olup olmadığını bilemez.
    - Örn: API body’sinde `age: "25"` (string) gelebilir, ama sen `number` bekliyorsun.
    İşte Zod burada devreye girer: Çalışma anında tip kontrolü yapar.

---

2. **Doğrulama (Validation):**  
    Sadece tip değil, **kuralları da doğrular.**
    - Örn: `password` en az 8 karakter olmalı.
    - Örn: `email` geçerli formatta olmalı.
    - Örn: `age` 18’den büyük olmalı.

---

3. **Tek Kaynaktan Gerçek (Single Source of Truth):**  
    Hem **TypeScript tipi** hem de **doğrulama şeması** tek yerden üretilir.  
    Yani: Zod şemasını yaz → hem doğrulamada hem de tip üretiminde kullan → **tekrar kod yazmaya gerek yok**.

    ```ts
    const UserSchema = z.object({
      username: z.string(),
      age: z.number(),
    });
    
    type User = z.infer<typeof UserSchema>;
    ```

Burada `User` tipini ayrıca yazmana gerek kalmaz.

---

4. **Basit ve Fonksiyonel API:**
    - `z.string().email()`
    - `z.number().min(18)`
    - `z.array(z.string())`
    Zincirleme (chaining) ile çok okunabilir kurallar tanımlanır.

---

## 🔹 Nerelerde Kullanılır?

- **API geliştirme:** Request body, query param, response validation
- **Form doğrulama:** Kullanıcının girdiği inputların kontrolü
- **Config dosyaları:** Ortam değişkenlerinin (env) doğrulanması
- **Veri tabanı CRUD işlemleri:** Insert/Update için gelen dataların validasyonu

---

👉 Özetle:  
Zod, **TypeScript’in eksik kaldığı runtime doğrulama kısmını tamamlar** ve hem tip hem de validation tek bir şemada toplanır.
