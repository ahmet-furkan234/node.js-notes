
# 🗂 1. Swagger Konfigürasyon Dosyası (`swagger.ts`)

### Amaç:

- API başlığı, versiyonu, açıklaması gibi temel bilgileri tanımlamak.
- Swagger’ın hangi dosyaları tarayacağını belirtmek.

---

### Örnek `swagger.ts` Dosyası

```ts
import swaggerJSDoc from "swagger-jsdoc";

const options: swaggerJSDoc.Options = {
  definition: {
    openapi: "3.0.0",  // OpenAPI versiyonu
    info: {
      title: "Benim TypeScript API Dokümantasyonum",
      version: "1.0.0",
      description: "Express + TypeScript için Swagger entegrasyonu örneği",
    },
    servers: [
      {
        url: "http://localhost:3000", // API base URL
      },
    ],
  },
  apis: ["./src/routes/*.ts"], // Swagger’ın route’ları tarayacağı dosyalar
};

export const swaggerSpec = swaggerJSDoc(options);
```

---

### Açıklamalar (Notluk Format)

- **definition** → Swagger dokümanının temel bilgilerini içerir (OpenAPI versiyonu, info, servers).
- **info** → API’nin başlığı, versiyonu, açıklaması.
- **servers** → API’nin çalıştığı URL(ler).
- **apis** → Swagger’ın JSDoc yorumlarını okuyacağı dosya yolları.
    - Örn: `"./src/routes/*.ts"` → `routes` klasöründeki tüm TypeScript dosyalarını tarar.

---

# 🔗 2. Express Uygulamasına Bağlama

`app.ts` veya `index.ts` dosyasında:

```ts
import express from "express";
import swaggerUi from "swagger-ui-express";
import { swaggerSpec } from "./swagger";

const app = express();

// Swagger UI endpoint
app.use("/api-docs", swaggerUi.serve, swaggerUi.setup(swaggerSpec));

// Örnek route
app.get("/api/hello", (req, res) => {
  res.json({ message: "Merhaba Swagger!" });
});

app.listen(3000, () => {
  console.log("Server çalışıyor: http://localhost:3000");
  console.log("Swagger dokümanı: http://localhost:3000/api-docs");
});
```

---

### Notlar:

- `/api-docs` → Tarayıcıda Swagger UI’yi açacağın endpoint.
- `swaggerSpec` → swagger-jsdoc ile üretilen JSON doküman.
- Bu yapı ile **kod değiştiğinde dokümantasyon otomatik güncellenir**.

---

# ✅ Özet (Notluk Format)

1. `swagger.ts` dosyası oluştur → OpenAPI info, servers, taranacak apis.
2. Express’e `/api-docs` route’u ekle → swagger-ui-express ile bağla.
3. Route’lar üzerinde JSDoc yorumları ile endpoint’leri belgelemeye başla.
4. Tarayıcıdan `http://localhost:3000/api-docs` ile Swagger UI’yi görüntüle.
