
### ✅ `@IsString()`

**Amaç:** Değerin bir `string` olduğunu kontrol eder.

```ts
class UserDto {
  @IsString()
  username: string;
}
```

```ts
// Hatalı: sayı
{ username: 123 }
```

---

### 📏 `@Length(min, max)`

**Amaç:** String’in uzunluğunu aralık içinde sınırlar.

```ts
class PasswordDto {
  @Length(6, 12)
  password: string;
}
```

```ts
// Hatalı: 4 karakter
{ password: "1234" }
```

---

### 📏 `@MinLength(min)`

**Amaç:** Minimum karakter sayısını kontrol eder.

```ts
@MinLength(3)
nickname: string;
```

---

### 📏 `@MaxLength(max)`

**Amaç:** Maksimum karakter sınırı koyar.

```ts
@MaxLength(10)
shortNote: string;
```

---

### 🔍 `@Matches(regex: RegExp)`

**Amaç:** Değerin belirli bir regex ile eşleşip eşleşmediğini kontrol eder.

```ts
@Matches(/^[A-Z][a-z]+$/, { message: 'İlk harf büyük olmalı' })
name: string;
```

```ts
// Geçerli: "Ahmet"
// Hatalı: "ahmet", "123Ahmet"
```

---

### 🔡 `@IsAlpha()`

**Amaç:** Sadece harf içerip içermediğini kontrol eder (`a-zA-Z`).

```ts
@IsAlpha()
firstName: string;
```

```ts
// Hatalı: "Ali123"
```

---

### 🔠 `@IsAlphanumeric()`

**Amaç:** Harf + sayı içeriyor mu (boşluk ve sembol içeremez).

```ts
@IsAlphanumeric()
username: string;
```

```ts
// Geçerli: "TkMatE123"
// Hatalı: "Tk Mate!", "Tk@Mate"
```

---

### 🧾 `@IsAscii()`

**Amaç:** ASCII karakterlerden mi oluşuyor? (0x00 – 0x7F)

```ts
@IsAscii()
asciiText: string;
```

---

### 📡 `@IsBase32()`

### 🧬 `@IsBase64()`

**Amaç:** Base32 veya Base64 kodlamaya uygunluk kontrolü.

```ts
@IsBase64()
encoded: string;
```

---

### 💳 `@IsCreditCard()`

**Amaç:** Geçerli kredi kartı numarası mı?

```ts
@IsCreditCard()
cardNumber: string;
```

---

### 🌍 `@IsFQDN()`

**Amaç:** Geçerli bir alan adı mı? (FQDN = Fully Qualified Domain Name)

```ts
@IsFQDN()
website: string;
```

```ts
// Geçerli: "example.com"
// Hatalı: "http://example.com"
```

---

### 🔡 `@IsLowercase()`

### 🔠 `@IsUppercase()`

**Amaç:** Tüm karakterler küçük mü ya da büyük mü?

```ts
@IsLowercase()
tag: string;  // "nodejs"

@IsUppercase()
shout: string; // "HELLO"
```

---

### 🌐 `@IsHexColor()`

### 🔢 `@IsHexadecimal()`

**Amaç:** Renk kodları ve hex sayı kontrolü.

```ts
@IsHexColor()
color: string;  // "#FFEE00"

@IsHexadecimal()
code: string;  // "1A3F"
```

---

### 📶 `@IsMACAddress()`

**Amaç:** MAC adresi doğrulaması.

```ts
@IsMACAddress()
mac: string;  // "00:1A:2B:3C:4D:5E"
```

---

### 🔖 `@IsSemVer()`

**Amaç:** Semantic versioning formatına uygunluk (örnek: "1.2.3")

```ts
@IsSemVer()
version: string;
```

---

### 🌍 `@IsIBAN()`

### 🏦 `@IsBIC()`

**Amaç:** Banka IBAN ve BIC/SWIFT kodlarının geçerli olup olmadığını kontrol eder.

```ts
@IsIBAN()
iban: string;

@IsBIC()
bic: string;
```

---

### ✨ `@IsMultibyte()`

### 🧠 `@IsSurrogatePair()`

### 🧱 `@IsVariableWidth()`

Bunlar daha az kullanılan ama önemli Unicode karakter testleridir:

|Dekoratör|Açıklama|
|---|---|
|`@IsMultibyte()`|Japonca gibi çok byte’lı karakter içeriyor mu?|
|`@IsSurrogatePair()`|UTF-16 karakter çifti içeriyor mu?|
|`@IsVariableWidth()`|Hem tam hem yarım genişlikli karakter içeriyor mu?|

---

## 🧪 Örnek Uygulama

```ts
class ProductDto {
  @IsString()
  @Length(3, 20)
  name: string;

  @IsAlphanumeric()
  code: string;

  @IsHexColor()
  color: string;
}
```

---

## 🔚 Özet Tablo

|Dekoratör|Görevi|
|---|---|
|`@IsString()`|String olup olmadığını kontrol eder|
|`@Length(min, max)`|Karakter uzunluğu aralığını kontrol eder|
|`@MinLength(n)`|En az `n` karakter olmalı|
|`@MaxLength(n)`|En fazla `n` karakter olmalı|
|`@Matches(regex)`|Regex ile eşleşme|
|`@IsAlpha()`|Sadece harf|
|`@IsAlphanumeric()`|Harf + rakam|
|`@IsLowercase()`|Tüm harfler küçük|
|`@IsUppercase()`|Tüm harfler büyük|
|`@IsBase32()` / `@IsBase64()`|Base kodlama testleri|
|`@IsAscii()`|ASCII karakter seti|
|`@IsFQDN()`|Geçerli alan adı|
|`@IsMACAddress()`|MAC adres kontrolü|
|`@IsSemVer()`|Sürüm formatı|
|`@IsIBAN()` / `@IsBIC()`|IBAN ve SWIFT kod kontrolü|
|`@IsMultibyte()` / `@IsSurrogatePair()` / `@IsVariableWidth()`|Unicode testleri|

---

Hazırsan bir sonraki kategoriye, örneğin **Sayı Doğrulama Dekoratörleri**'ne geçelim mi `TkMatE`? Yoksa bu listedekilerden detaylı örnek istediğin bir dekoratör var mı?