
## 🔹 1. `populate` Nedir?

Mongoose’ta bir modelin başka bir modele **referans** (yabancı anahtar / foreign key) tuttuğu durumlarda, `populate` sayesinde ilişkili **tam belgeyi** otomatik olarak çekebilirsin.

- Normalde sadece ObjectId gelir.
- `populate` ile ObjectId yerine **ilgili doküman** gelir.

---

## 🔹 2. Örnek Schema

### Role Model

```ts
import { Schema, model } from "mongoose";

const roleSchema = new Schema({
  name: { type: String, required: true }
});

export default model("Role", roleSchema);
```

### User Model

```ts
import { Schema, model } from "mongoose";

const userSchema = new Schema({
  email: { type: String, required: true },
  password: { type: String, required: true },
  roleId: { type: Schema.Types.ObjectId, ref: "Role" } // reference
});

export default model("User", userSchema);
```

- `roleId` alanı **Role tablosuna referans** veriyor.
    
- Normalde `roleId` sadece bir ObjectId tutar.
    

---

## 🔹 3. `populate` Kullanımı

### ObjectId Çekme (populate yok)

```ts
const user = await userModel.findOne({ email: "test@test.com" });
console.log(user.roleId); 
// Çıktı: 64f1a8c5b1234e5f67890abc  (ObjectId)
```

### populate ile Rol Bilgisini Çekme

```ts
const user = await userModel.findOne({ email: "test@test.com" }).populate("roleId");
console.log(user.roleId.name); 
// Çıktı: "Admin"
```

- Artık roleId sadece ObjectId değil, **Role dokümanı** oldu.
- Böylece aggregation + `$lookup` yazmana gerek kalmaz.

---

## 🔹 4. populate ile İsteğe Bağlı Alan Seçme

```ts
const user = await userModel
  .findOne({ email: "test@test.com" })
  .populate("roleId", "name"); // sadece name alanı gelir
console.log(user.roleId.name); 
```

- Burada sadece `name` alanını çekiyoruz, gereksiz alanlar gelmez.
    

---

## 🔹 5. Avantajları

- Kod daha **temiz ve okunabilir** olur.
    
- `$lookup` pipeline yazmana gerek kalmaz.
    
- Tek bir sorgu ile ilişkili veriyi getirir.
    
- Performans genellikle aggregation’dan daha iyi, özellikle **tek kayıt** çekiyorsan.
    

---

Özetle:

- `populate` = Mongoose’un **join gibi davranan** özelliği.
    
- İlişkili veri ObjectId’den gerçek dokümana dönüşür.
    
- `findOne + populate` = tek kullanıcı + rol bilgisini çekmek için en basit ve hızlı yöntem.
    

---

İstersen ben sana **senin refresh token kodunu populate ile optimize edilmiş şekilde** gösterebilirim, böylece farkı direkt görebilirsin. Bunu yapayım mı?