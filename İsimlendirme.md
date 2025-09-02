Projende Repository (repo) ve Service katmanlarını ayrı tutman çok doğru bir yaklaşımdır. Bu iki katmanın isimlendirme (naming) stratejileriyle ilgili en iyi pratikler ise şu şekilde:

---

## 🔹 1. Repository Katmanında Method İsimlendirme

Repository katmanı **veritabanı işlemlerini** (CRUD) yapar. Bu yüzden method isimleri **veritabanı odaklı** ve genellikle şu şekilde olur:

| Amaç             | Repository Method Örneği  |
| ---------------- | ------------------------- |
| Tek kayıt bulmak | `findById`, `findByEmail` |
| Hepsini getirmek | `findAll`                 |
| Kayıt eklemek    | `create`, `insert`        |
| Güncellemek      | `update`, `updateById`    |
| Silmek           | `delete`, `deleteById`    |

➡️ _Kısaca: method isimleri "veri tabanı aksiyonu + filtre" şeklinde olur._

---

## 🔹 2. Service Katmanında Method İsimlendirme

Service katmanı **iş kurallarını** (business logic) barındırır. Repository'i kullanarak **daha anlamlı, işleve yönelik methodlar** üretir. Bu nedenle isimlendirme daha anlamlı olmalıdır:

| Amaç                   | Service Method Örneği               |
| ---------------------- | ----------------------------------- |
| Kullanıcıyı getir      | `getUserById`, `getUserProfile`     |
| Yeni kullanıcı oluştur | `registerUser`, `createUserAccount` |
| Giriş kontrolü yap     | `authenticateUser`                  |
| Sipariş ver            | `placeOrder`                        |
| Şifre sıfırla          | `resetPassword`                     |

➡️ _Burada odak, domain odaklıdır. Yani "ne iş yapılmak isteniyor" anlatılır._

---

## ⚖️ Aynı Olmalı mı? Farklı Olmalı mı?

Hayır, **aynı olmak zorunda değil.** Çünkü:

- **Repository** veri erişimini temsil eder (teknik).
- **Service** iş mantığını temsil eder (işlevsel).

Ama bazı küçük projelerde eğer Service katmanı çok fazla iş yapmıyorsa, method isimleri birebir aynı olabilir. Yine de orta ve büyük projelerde **ayırmak her zaman daha sürdürülebilirdir.**

---

## ✅ Örnek:

```ts
// user.repository.ts
findByEmail(email: string): Promise<User | null> {
   return this.model.findOne({ email });
}

// user.service.ts
async getUserByEmail(email: string): Promise<UserDto | null> {
   const user = await this.userRepository.findByEmail(email);
   return user ? this.mapper.toDto(user) : null;
}
```

---

## 🔸 Özet

|Katman|Görev|Method İsmi Nasıl Olmalı|
|---|---|---|
|Repository|Veritabanı işlemleri|`find`, `create`, `update`, `deleteById`|
|Service|İş mantığı / domain|`getUser`, `registerUser`, `resetPassword`|

---

İstersen kendi propendeki methodları örnek verip birlikte isimlendirme yapabiliriz, TkMatE.