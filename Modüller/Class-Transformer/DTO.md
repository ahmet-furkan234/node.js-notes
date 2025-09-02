
# 📦 DTO Nedir? — Data Transfer Object (Veri Transfer Nesnesi)

---

## 1️⃣ Tanım

> **DTO**, farklı katmanlar veya sistemler arasında veri taşıma amacıyla kullanılan, sadeleştirilmiş ve genellikle sadece veri tutan nesnelerdir.

---

## 2️⃣ Neden Kullanılır?

- **Veri güvenliği**: İstemciye veya dış servise hassas verileri doğrudan vermek yerine sadece gerekli alanları taşımak.
- **Veri biçimlendirme**: Veri tabanından veya başka kaynaktan gelen karmaşık veriyi, API katmanında temiz ve düzenli hale getirmek.
- **Bağımsızlık**: İç veri modelleri (entity, ORM modelleri) ile dış veri yapısını birbirinden ayırmak.
- **Validasyon**: Gelen veya giden verinin yapısını ve kurallarını kolayca kontrol etmek.
- **Bakım kolaylığı**: Kodda anlaşılır ve modüler yapı sağlar.

---

## 3️⃣ Nerelerde Kullanılır?

- **API katmanında**: İstemciden gelen veriyi temsil etmek veya istemciye gönderilecek veriyi formatlamak.
- **Servis katmanında**: İş kurallarına uygun veri taşıma.
- **Veritabanı katmanında**: ORM entity’lerinden bağımsız soyutlama yapmak için.

---

## 4️⃣ Örnek Basit DTO

```ts
class UserDto {
  id: number;
  username: string;
  email: string;
}
```

---

## 5️⃣ DTO vs Entity

|Özellik|DTO|Entity / Model|
|---|---|---|
|Amaç|Veri taşıma, validasyon|Veritabanı işlemleri, iş kuralları|
|İçerik|Sadece gerekli alanlar|Tüm veri ve ilişkiler|
|Bağımlılık|Diğer katmanlardan bağımsız|ORM veya iş katmanına bağlı|
|Karmaşıklık|Basit, sade|Karmaşık, ilişkili|
|Kullanım Yeri|API, servis katmanı|ORM, veri erişim katmanı|

---

## 6️⃣ class-validator + class-transformer ile DTO

DTO’lar genellikle validasyon ve veri dönüşümü için `class-validator` ve `class-transformer` ile birlikte kullanılır. Böylece:

- JSON verisi DTO’ya dönüşür,
- DTO validasyonla kontrol edilir,
- Hatalar yakalanır,
- Güvenli ve temiz veri işlenir.

---

## 7️⃣ Özet

|Avantajlar|
|---|
|- Veri güvenliğini artırır|
|- API iskeletini standartlaştırır|
|- Karmaşık nesneleri sadeleştirir|
|- Validasyon ve dönüşüm sürecini kolaylaştırır|
|- Kodun bakımı ve testi daha kolay olur|
