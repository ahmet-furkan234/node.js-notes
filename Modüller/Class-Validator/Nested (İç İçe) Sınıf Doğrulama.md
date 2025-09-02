
### 🎯 Kullanılan Ana Dekoratörler:

|Dekoratör|Açıklama|
|---|---|
|`@ValidateNested()`|İç sınıf doğrulaması yapılmasını sağlar.|
|`@Type(() => Class)`|class-transformer’dan gelir, hangi sınıfa dönüştürüleceğini belirtir.|

---

## 📦 Örnek Senaryo: Kullanıcı ve Adres Bilgisi

### 1. Adres sınıfı:

```ts
import { IsString, Length } from 'class-validator';

class Address {
  @IsString()
  @Length(2, 50)
  city: string;

  @IsString()
  @Length(2, 50)
  street: string;
}
```

### 2. Kullanıcı sınıfı (içinde Address var):

```ts
import { ValidateNested } from 'class-validator';
import { Type } from 'class-transformer';

class User {
  @IsString()
  name: string;

  @ValidateNested()                // class-validator için
  @Type(() => Address)            // class-transformer için
  address: Address;
}
```

### 3. Kullanım Örneği:

```ts
import { plainToInstance } from 'class-transformer';
import { validate } from 'class-validator';

const data = {
  name: 'Ahmet',
  address: {
    city: 'İstanbul',
    street: 'Abc Sk.'
  }
};

const user = plainToInstance(User, data);

validate(user).then(errors => {
  if (errors.length > 0) {
    console.log('Hatalar:', errors);
  } else {
    console.log('Geçerli!');
  }
});
```

---

## ✅ Notlar:

- `@ValidateNested()` sadece tek başına yeterli değildir, mutlaka `@Type(() => Class)` ile birlikte kullanılmalıdır.
    
- İç içe sınıflar derinleştikçe, her seviyede bu iki dekoratör kullanılmalıdır.
    
- Eğer `Address` içinde de başka bir sınıf varsa, aynı işlem zincir halinde devam eder.
    

---

## 🧠 Derinlemesine Nested Doğrulama

```ts
class Country {
  @IsString()
  name: string;
}

class Address {
  @IsString()
  city: string;

  @ValidateNested()
  @Type(() => Country)
  country: Country;
}

class User {
  @IsString()
  name: string;

  @ValidateNested()
  @Type(() => Address)
  address: Address;
}
```

---

Hazır nested doğrulama konusunu kavradıysan, bir sonraki adımda istersen şu başlıklardan birine geçebiliriz:

- 🔁 `@ValidateIf()` ile Koşullu Doğrulama
    
- ⚙️ `@Validate()` ile Özel Doğrulama ve `ValidatorConstraint`
    
- 🧪 Gerçek dünya senaryosu (örnek: kayıt formu, ürün nesnesi, vb.)
    

Hangisini istersin `TkMatE`?