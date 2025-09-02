
## 🔁 Doğrulama Mekanizması

### Örnek:

```ts
const plainPassword = "admin123"; // Kullanıcının formdan girdiği şifre
const hashedPassword = "$2b$10$aFvA2B5b..."; // DB'den gelen hash

const isMatch = await bcrypt.compare(plainPassword, hashedPassword);
console.log(isMatch); // true veya false
```

> ✅ `bcrypt.compare()` fonksiyonu:
> 
> - Hash içindeki salt’ı **otomatik çıkarır**
> - Girilen şifreyi **aynı yöntemle hash’ler**
> - Sonra ikisini karşılaştırır  
>     → Tüm bu işlemler **timestamp'siz**, sadece hash'e ve plain şifreye dayanır.

---

## 🧠 bcrypt Hash Formatı

Bir `bcrypt` hash’i 3 parçadan oluşur:

```
$2b$10$T0fYuENI/06hdmygGuxQlu/erTSLJZuZEO2zTfTo7v7LgBiXZVKgS
│ │ │ │
│ │ │ └─ Hash değeri
│ │ └─── Salt (otomatik gömülür)
│ └───── Cost factor (10 → 2^10 iterasyon)
└─────── Algoritma versiyonu
```

Yani `bcrypt.compare` bu hash’in içindeki **salt** ve **cost** bilgisini da çıkarır → tekrar üretip doğrular.

---

## ✅ Özetle

|Şifre Doğrulama İçin|Gerekli|
|---|---|
|Kullanıcının girdiği şifre|✅|
|Veri tabanında kayıtlı hash|✅|
|timestamp veya başka veri|❌|
|Salt'ı ayrıca saklamak|❌ (hash içinde var)|
