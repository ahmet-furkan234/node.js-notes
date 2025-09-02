 
## 📌 GENEL KATEGORİLER

---

### 🔤 **Tip Kontrolü Dekoratörleri**

|Dekoratör|Açıklama|
|---|---|
|`@IsDefined()`|Değer tanımlı mı (undefined değil mi?)|
|`@IsOptional()`|Alan isteğe bağlı olarak işaretlenir|
|`@IsEmpty()`|Boş mu (`null`, `undefined`, `""`)|
|`@IsNotEmpty()`|Boş değil mi (`null`, `""` hariç)|
|`@Equals(comparison)`|Tam eşitlik kontrolü (`===`)|
|`@NotEquals(comp)`|Tam eşit değil mi|
|`@IsIn(values)`|Belirtilen değerlerden biri mi?|
|`@IsNotIn(values)`|Belirtilen değerlerden biri değil mi?|

---

### 📏 **String Doğrulama**

| Dekoratör                 | Açıklama                                  |
| ------------------------- | ----------------------------------------- |
| `@IsString()`             | Değer string mi?                          |
| `@Length(min, max)`       | Karakter uzunluğu belirtilen aralıkta mı? |
| `@MinLength(min)`         | En az `min` karakter mi?                  |
| `@MaxLength(max)`         | En fazla `max` karakter mi?               |
| `@Matches(regex)`         | Belirtilen regex ile eşleşiyor mu?        |
| `@IsAlpha()`              | Sadece harf içeriyor mu? (a-zA-Z)         |
| `@IsAlphanumeric()`       | Harf ve sayı içeriyor mu?                 |
| `@IsAscii()`              | ASCII karakterleri mi?                    |
| `@IsBase32()`             | Base32 kodlanmış mı?                      |
| `@IsBase64()`             | Base64 kodlu mu?                          |
| `@IsIBAN()`               | Geçerli IBAN mı?                          |
| `@IsBIC()`                | Geçerli BIC/SWIFT kodu mu?                |
| `@IsByteLength(min, max)` | Byte uzunluğu uygun mu?                   |
| `@IsFQDN()`               | Geçerli alan adı mı (example.com)?        |
| `@IsLowercase()`          | Tamamen küçük harf mi?                    |
| `@IsUppercase()`          | Tamamen büyük harf mi?                    |
| `@IsMultibyte()`          | Multibyte karakter içeriyor mu?           |
| `@IsSurrogatePair()`      | UTF-16 çift karakter içeriyor mu?         |
| `@IsVariableWidth()`      | Farklı genişlikte karakter içeriyor mu?   |
| `@IsHexColor()`           | Geçerli hex renk mi?                      |
| `@IsHexadecimal()`        | Hexadecimal sayı mı?                      |
| `@IsMACAddress()`         | Geçerli MAC adresi mi?                    |
| `@IsSemVer()`             | Geçerli semver string mi? (1.0.0)         |

---

### 🔢 **Sayı Doğrulama**

|Dekoratör|Açıklama|
|---|---|
|`@IsNumber()`|Sayı mı? (`number`)|
|`@IsInt()`|Tam sayı mı? (`integer`)|
|`@IsPositive()`|Pozitif sayı mı?|
|`@IsNegative()`|Negatif sayı mı?|
|`@Min(n)`|En az `n` değeri|
|`@Max(n)`|En fazla `n` değeri|
|`@IsDivisibleBy(n)`|`n` sayısına kalansız bölünüyor mu?|
|`@IsDecimal()`|Ondalık sayı mı?|
|`@IsPort()`|Geçerli port numarası mı? (0–65535)|

---

### 📆 **Tarih ve Zaman**

|Dekoratör|Açıklama|
|---|---|
|`@IsDate()`|Değer geçerli `Date` objesi mi?|
|`@MinDate(date)`|Belirli bir tarihten sonra mı?|
|`@MaxDate(date)`|Belirli bir tarihten önce mi?|
|`@IsISO8601()`|ISO 8601 formatına uygun tarih mi?|

---

### ✅ **Boolean ve Diğer Tipler**

|Dekoratör|Açıklama|
|---|---|
|`@IsBoolean()`|Boolean (`true/false`) mı?|
|`@IsEnum(Enum)`|Değer belirtilen enum'da mı?|
|`@IsJSON()`|Geçerli JSON string mi?|
|`@IsObject()`|Object türünde mi?|
|`@IsInstance(cls)`|Belirli sınıfın örneği mi?|

---

### 📨 **E-Posta, URL, IP vs.**

| Dekoratör             | Açıklama                         |
| --------------------- | -------------------------------- |
| `@IsEmail()`          | Geçerli e-posta mı?              |
| `@IsURL()`            | Geçerli URL mi?                  |
| `@IsUUID(version?)`   | Geçerli UUID mi? (v1, v4 vs.)    |
| `@IsMongoId()`        | Geçerli MongoDB ObjectId mi?     |
| `@IsIP(version?)`     | IPv4 ya da IPv6 mı?              |
| `@IsPostalCode(code)` | Posta kodu formatı (ülkeye göre) |
| `@IsPhoneNumber(cc)`  | Geçerli telefon numarası mı?     |
| `@IsCreditCard()`     | Geçerli kredi kartı numarası mı? |

---

### 🧩 **Array (Dizi) Doğrulama**

|Dekoratör|Açıklama|
|---|---|
|`@IsArray()`|Değer bir array mi?|
|`@ArrayNotEmpty()`|Dizi boş mu kontrol eder|
|`@ArrayMinSize(n)`|Minimum eleman sayısı|
|`@ArrayMaxSize(n)`|Maksimum eleman sayısı|
|`@ArrayContains(values)`|Belirtilen değerleri içeriyor mu?|
|`@ArrayNotContains(values)`|Belirtilen değerleri içermiyor mu?|
|`@ArrayUnique()`|Elemanlar benzersiz mi?|
|`@IsArray()` + `@ValidateNested({ each: true })`|Dizi elemanlarını da doğrular|

---

### 🧬 **Nested (İç İçe) Sınıf Doğrulama**

|Dekoratör|Açıklama|
|---|---|
|`@ValidateNested()`|İç içe nesnelerde alt sınıfları doğrular|
|`@Type(() => Class)`|`class-transformer` ile birlikte sınıf dönüşümü|

---

### 🔧 **Custom & Özel Durumlar**

|Dekoratör|Açıklama|
|---|---|
|`@Validate()`|Özel sınıf validator ile doğrulama|
|`@ValidateIf(condFn)`|Şartlı doğrulama|
|`@ValidatePromise()`|Promise döndüren validator'lar için|
