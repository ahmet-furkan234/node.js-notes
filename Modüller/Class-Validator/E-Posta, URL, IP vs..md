
#### 1. `@IsEmail(options?, validationOptions?)`

> Değer geçerli bir e-posta olmalı.

```ts
@IsEmail()
email: string;

// Örnek seçenek: sadece belirli domainleri kabul etmek
@IsEmail({}, { message: 'Lütfen geçerli bir e-posta adresi girin.' })
```

#### 2. `@IsURL(options?, validationOptions?)`

> Değer geçerli bir URL olmalı. `validator.js`'in `isURL` fonksiyonu kullanılır.

```ts
@IsURL()
website: string;

@IsURL({ protocols: ['https'] }, { message: 'Sadece HTTPS bağlantıları kabul edilir.' })
secureLink: string;
```

#### 3. `@IsIP(version?: "4" | "6", validationOptions?)`

> Değer geçerli bir IP adresi olmalı.

```ts
@IsIP()
ipAddress: string;

@IsIP('4')
ipv4: string;

@IsIP('6')
ipv6: string;
```

#### 4. `@IsMACAddress(options?, validationOptions?)`

> Geçerli bir MAC adresi.

```ts
@IsMACAddress()
mac: string;
```

#### 5. `@IsFQDN(validationOptions?)`

> Değer geçerli bir alan adı (Fully Qualified Domain Name) olmalı.

```ts
@IsFQDN()
domain: string;
```

#### 6. `@IsUUID(version?: "3" | "4" | "5" | "all", validationOptions?)`

> Geçerli bir UUID olmalı.

```ts
@IsUUID()
uuid: string;

@IsUUID('4')
uuid4: string;
```

#### 7. `@IsBase64(validationOptions?)`

> Base64 formatında olup olmadığını kontrol eder.

```ts
@IsBase64()
imageData: string;
```

#### 8. `@IsDataURI(validationOptions?)`

> Data URI formatını kontrol eder (örneğin `data:image/png;base64,...`).

```ts
@IsDataURI()
image: string;
```

#### 9. `@IsMagnetURI(validationOptions?)`

> Magnet URI formatında olup olmadığını kontrol eder (torrent).

```ts
@IsMagnetURI()
torrentLink: string;
```

---

### 🧪 Uygulamalı Örnek

```ts
import { IsEmail, IsURL, IsIP, IsUUID } from 'class-validator';

class ContactInfo {
  @IsEmail()
  email: string;

  @IsURL()
  website: string;

  @IsIP('4')
  lastLoginIP: string;

  @IsUUID('4')
  userId: string;
}
```

---

İsteğe bağlı olarak bu dekoratörlere `message` parametresiyle özel hata mesajları da verilebilir:

```ts
@IsEmail({}, { message: 'Geçerli bir e-posta giriniz!' })
```
