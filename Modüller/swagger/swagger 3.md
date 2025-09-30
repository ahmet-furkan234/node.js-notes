
# 🧩 1. Hangi Paketleri Kullanacağız ve Neden?

## 1. swagger-ui-express

- **Ne işe yarar?**
    - Swagger UI’yi Express uygulamanda `/api-docs` gibi bir endpoint’e bağlamanı sağlar.
    - API’yi görsel olarak tarayıcıda test etmeye imkân verir.
- **Avantajı:**
    - Kolay entegrasyon.
    - Route’ları elle yazmak yerine Swagger JSON’u kullanır.

## 2. swagger-jsdoc

- **Ne işe yarar?**
    - Kod içindeki **JSDoc yorumlarını** okuyarak otomatik OpenAPI (Swagger) dokümanı üretir.
    - Route’ları tek tek JSON’a çevirmen gerekmez.
- **Avantajı:**
    - Kod ile dokümantasyon senkron olur.
    - Route açıklamaları ve parametreleri kolayca tanımlanır.

## 3. @types/swagger-ui-express

- **Ne işe yarar?**
    - TypeScript için tip tanımları sağlar.
    - Kod tamamlama ve type-check desteği verir.

---

# 🛠️ 2. Paket Kurulumu

```bash
npm install swagger-ui-express swagger-jsdoc
npm install --save-dev @types/swagger-ui-express
```

- `npm install` → production runtime paketler (swagger-ui-express, swagger-jsdoc)
- `--save-dev` → sadece development sırasında kullanılan type paketleri

---

# 📝 3. Neden Bu Yapıyı Kullanıyoruz?

- **swagger-ui-express** → görselleştirme + test ortamı sağlar.
- **swagger-jsdoc** → otomatik dokümantasyon üretir.
- **TypeScript tipleri** → projenin tip güvenliğini bozmadan kullanabilirsin.

> Bu ikili kombinasyon Express projeleri için en yaygın ve önerilen yöntemdir.

---

# 🔹 4. Özet (Notluk Format)

1. **swagger-ui-express** → Tarayıcıda Swagger UI sağlamak için.
2. **swagger-jsdoc** → Koddan otomatik OpenAPI dokümanı üretmek için.
3. **@types/swagger-ui-express** → TypeScript tip desteği.
4. **Kurulum** → `npm install` ve `--save-dev` ile paketleri projeye ekle.
5. **Avantaj** → Kod ve dokümantasyon senkron, kolay test, minimal manuel iş.