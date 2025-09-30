
### Temel Format

Her route’un üstüne bir **JSDoc bloğu** ekliyoruz ve `@swagger` etiketi kullanıyoruz:

```ts
/**
 * @swagger
 * /api/hello:
 *   get:
 *     summary: Merhaba mesajı döndürür
 *     description: Bu endpoint sadece örnek olarak "Merhaba Swagger!" döndürür.
 *     responses:
 *       200:
 *         description: Başarılı cevap
 *         content:
 *           application/json:
 *             schema:
 *               type: object
 *               properties:
 *                 message:
 *                   type: string
 *                   example: Merhaba Swagger!
 */
```

---

### Açıklamalar

- **`/api/hello`** → Endpoint URL’i.
- **`get`** → HTTP metodu (get, post, put, delete vb.).
- **`summary`** → Kısa açıklama.
- **`description`** → Daha detaylı açıklama (isteğe bağlı).
- **`responses`** → Dönebilecek HTTP durum kodları ve örnek response.
- **`content` + `schema`** → Response JSON yapısı.

---

# 📌 2. Parametre Örneği

Route’ta path veya query parametre varsa:

```ts
/**
 * @swagger
 * /api/users/{id}:
 *   get:
 *     summary: Belirli bir kullanıcıyı getirir
 *     parameters:
 *       - in: path
 *         name: id
 *         schema:
 *           type: string
 *         required: true
 *         description: Kullanıcı ID
 *     responses:
 *       200:
 *         description: Başarılı cevap
 *         content:
 *           application/json:
 *             schema:
 *               type: object
 *               properties:
 *                 id:
 *                   type: string
 *                 name:
 *                   type: string
 */
```

---

# 📌 3. Request Body Örneği (POST/PUT)

```ts
/**
 * @swagger
 * /api/users:
 *   post:
 *     summary: Yeni kullanıcı oluşturur
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             properties:
 *               name:
 *                 type: string
 *                 example: Ahmet
 *               age:
 *                 type: integer
 *                 example: 25
 *     responses:
 *       201:
 *         description: Kullanıcı başarıyla oluşturuldu
 */
```

---

# 🔹 4. Notlar (Notluk Format)

- **Path parametreleri** → `parameters: - in: path`
- **Query parametreleri** → `parameters: - in: query`
- **Request body** → `requestBody` ile JSON şemasını tanımla
- **Responses** → HTTP kodlarına göre dönecek veri yapısını schema ile göster
- **Example** → Gerçekçi örnekler ekle, Swagger UI’de gösterilir
