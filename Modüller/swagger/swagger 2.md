
# 🛠️ Swagger Ekosistemi ve Araçlar

## 1. Swagger UI

- **Ne işe yarar?**
    - OpenAPI dokümanını (JSON/YAML) alır, tarayıcıda interaktif bir arayüzde gösterir.
    - API endpoint’lerini listeler.
    - Doğrudan tarayıcı üzerinden request atıp response’u görmeni sağlar.
- **Nerede kullanılır?**
    - Express projelerinde `/api-docs` endpointine bağlanır.
    - Takım arkadaşları, frontend veya QA ekipleri API’yi buradan test eder.
- **Avantajı:**
    - Kod yazmaya gerek kalmadan API’yi görselleştirir.

📌 Örnek:  
`http://localhost:3000/api-docs` →

- Sol tarafta tüm endpoint listesi.
- Sağda parametre girip "Try it out" diyerek request atabilirsin.

---

## 2. Swagger Editor

- **Ne işe yarar?**
    - Online veya localde çalışan bir **OpenAPI Specification (OAS) editorüdür**.
    - JSON/YAML formatında OpenAPI dokümanı yazmaya izin verir.
    - Gerçek zamanlı olarak yazdığın dökümanın Swagger UI çıktısını gösterir.
- **Kullanım Alanı:**
    - API’yi henüz geliştirmeden önce tasarlamak için → **API First Development** yaklaşımı.
    - Takımın “API sözleşmesi”ni önceden hazırlaması.

📌 Online versiyon: [editor.swagger.io](https://editor.swagger.io/)

---

## 3. Swagger Codegen

- **Ne işe yarar?**
    - OpenAPI dokümanını alıp otomatik olarak **client SDK’ları** veya **server stub’ları** üretir.
    - Örneğin:
        - Bir OpenAPI dokümanından **TypeScript client** kodu oluşturabilirsin.
        - Veya Java, Python, C# gibi diller için hazır client kütüphaneleri çıkarabilirsin.
- **Avantajı:**
    - Tekrarlı işleri ortadan kaldırır.
    - API tüketen uygulamalar hızlıca entegre olur.

📌 Örnek:

- Elinde bir ödeme API’si var. Swagger Codegen ile JavaScript client üretiyorsun → frontend direkt bu kütüphaneyi kullanıyor.

---

## 4. SwaggerHub

- **Ne işe yarar?**
    - Swagger’ın bulut tabanlı sürümü.
    - API’lerini online ortamda **tasarlama, versiyonlama ve paylaşma** imkânı verir.
- **Özellikler:**
    - Takım işbirliği (collaboration).
    - Versiyon kontrolü.
    - Public/Private API yayınlama.

---

## 5. OpenAPI Generator (Yeni Nesil)

- Swagger Codegen’in geliştirilmiş versiyonu → **OpenAPI Generator**.
- Çok daha fazla dil ve framework desteği var.
- Community tarafından aktif geliştirilmekte.

---

# 🎯 Ekosistem Özeti (Notluk)

- **Swagger UI** → Dokümantasyonu görsel arayüzde gösterir, test eder.
- **Swagger Editor** → OpenAPI dokümanı yazmak ve görmek için editor.
- **Swagger Codegen** → OpenAPI dokümanından client/server kodu üretir.
- **SwaggerHub** → Bulut tabanlı API tasarlama & paylaşma platformu.
- **OpenAPI Generator** → Codegen’in gelişmiş halidir.
