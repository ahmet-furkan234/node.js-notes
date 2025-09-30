
# 🌟 1. Schema Reuse (components/schemas)

- Aynı veri yapısını birden fazla endpoint’te kullanmak için **components/schemas** kullanılır.
- Tekrar tekrar schema tanımlamaktan kurtarır.

### Örnek

```ts
/**
 * @swagger
 * components:
 *   schemas:
 *     User:
 *       type: object
 *       properties:
 *         id:
 *           type: string
 *           example: 123
 *         name:
 *           type: string
 *           example: Ahmet
 */

/**
 * @swagger
 * /api/users/{id}:
 *   get:
 *     summary: Belirli kullanıcıyı getirir
 *     parameters:
 *       - in: path
 *         name: id
 *         schema:
 *           type: string
 *         required: true
 *     responses:
 *       200:
 *         description: Başarılı cevap
 *         content:
 *           application/json:
 *             schema:
 *               $ref: '#/components/schemas/User'
 */
```

> `$ref` ile tek bir User schema’sını birçok endpoint’te kullanabilirsin.

---

# 🔒 2. Authentication (JWT veya API Key)

Swagger üzerinden auth işlemlerini tanımlamak için `securitySchemes` kullanılır.

### Örnek (JWT Bearer)

```ts
/**
 * @swagger
 * components:
 *   securitySchemes:
 *     bearerAuth:
 *       type: http
 *       scheme: bearer
 *       bearerFormat: JWT
 */

/**
 * @swagger
 * /api/profile:
 *   get:
 *     summary: Kullanıcı profilini getirir
 *     security:
 *       - bearerAuth: []
 *     responses:
 *       200:
 *         description: Başarılı cevap
 */
```

- **securitySchemes** → Kullanılacak auth tipini tanımlar
- **security** → Hangi endpoint’te auth gerektiğini belirtir

---

# ⚡ 3. Global Response Tanımları

- Aynı HTTP response’ları birden fazla endpoint için tekrar tekrar tanımlamak yerine **components/responses** kullanabilirsin.
    

### Örnek

```ts
/**
 * @swagger
 * components:
 *   responses:
 *     NotFound:
 *       description: Kayıt bulunamadı
 */

/**
 * @swagger
 * /api/users/{id}:
 *   get:
 *     summary: Kullanıcı getir
 *     parameters:
 *       - in: path
 *         name: id
 *         schema:
 *           type: string
 *         required: true
 *     responses:
 *       200:
 *         description: Başarılı
 *       404:
 *         $ref: '#/components/responses/NotFound'
 */
```

---

# 🔹 4. Ekstra İpuçları

- **Tags**: Endpoint’leri gruplamak için kullanılır (`tags: ["User"]`).
- **Multiple servers**: Prod ve dev server’ları ekleyebilirsin.
- **Examples**: Her parametre ve response için örnek ver, UI’de gösterilir.
- **Versioning**: `/api/v1/...`, `/api/v2/...` ile dokümantasyonu versiyonlayabilirsin.

---

# ✅ 5. Notluk Özet

1. **Schema reuse** → `$ref: '#/components/schemas/...'` ile tekrar eden yapıları tek yerde tanımla.
2. **Authentication** → JWT veya API Key tanımları ile Swagger UI üzerinden auth test edilebilir.
3. **Global responses** → Tekrar eden response’lar için components/responses kullan.
4. **Tags & Examples** → UI’de endpoint’leri grupla ve örnek göster.
5. **Versioning & Servers** → Farklı environment ve API versiyonlarını destekle.
