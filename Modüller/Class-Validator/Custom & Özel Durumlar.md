
## 1️⃣ Basit Özel Validator Oluşturma

### Adımlar:

1. `ValidatorConstraint` decorator'ı ile özel doğrulayıcı sınıf oluşturulur.
2. `validate()` metodu içinde doğrulama mantığı yazılır.
3. `defaultMessage()` metodu ile hata mesajı özelleştirilir.
4. `@Validate()` dekoratörü ile alanlarda kullanılır.

---

### Örnek: "Tekrar eden karakter yok" kuralı

```ts
import {
  ValidatorConstraint,
  ValidatorConstraintInterface,
  ValidationArguments,
  Validate,
} from 'class-validator';

@ValidatorConstraint({ name: 'noRepeatedChars', async: false })
class NoRepeatedChars implements ValidatorConstraintInterface {
  validate(text: string, args: ValidationArguments) {
    return !/(.)\1/.test(text); // aynı karakter yan yana tekrar etmiyor mu?
  }

  defaultMessage(args: ValidationArguments) {
    return `${args.property} alanında yan yana tekrar eden karakterler olmamalıdır!`;
  }
}

class UserDto {
  @Validate(NoRepeatedChars)
  username: string;
}
```

---

## 2️⃣ Async Özel Validator Örneği

Örneğin, kullanıcı adının veritabanında olup olmadığını asenkron olarak kontrol etmek isteyebiliriz.

```ts
@ValidatorConstraint({ async: true })
class IsUsernameAlreadyExist implements ValidatorConstraintInterface {
  async validate(username: string) {
    const user = await fakeUserRepository.findOne({ username });
    return !user; // kullanıcı yoksa true döner, varsa false
  }

  defaultMessage() {
    return 'Kullanıcı adı zaten kayıtlı!';
  }
}

class UserDto {
  @Validate(IsUsernameAlreadyExist)
  username: string;
}
```

---

## 3️⃣ `@ValidateIf()` - Koşullu Doğrulama

Belirli bir şart gerçekleştiğinde doğrulama yapmak için kullanılır.

```ts
class PostDto {
  @IsString()
  content: string;

  @ValidateIf(o => o.content && o.content.length > 100)
  @IsString()
  summary: string;
}
```

---

## 4️⃣ `@IsNotEmpty()` ve `@IsOptional()` ile kombinasyon

```ts
class UpdateUserDto {
  @IsOptional()
  @IsNotEmpty()
  email?: string;
}
```

- `email` varsa boş olmamalı
- `email` yoksa hata yok

---

## 5️⃣ Özel Validator Parametreleri Gönderme

```ts
@ValidatorConstraint({ name: 'minLengthCustom' })
class MinLengthCustom implements ValidatorConstraintInterface {
  validate(text: string, args: ValidationArguments) {
    const [minLength] = args.constraints;
    return typeof text === 'string' && text.length >= minLength;
  }

  defaultMessage(args: ValidationArguments) {
    const [minLength] = args.constraints;
    return `${args.property} en az ${minLength} karakter olmalı!`;
  }
}

class PasswordDto {
  @Validate(MinLengthCustom, [8])
  password: string;
}
```

---

## Özet

|Özellik|Açıklama|
|---|---|
|`ValidatorConstraint`|Özel doğrulayıcı sınıfı tanımlar|
|`validate()`|Doğrulama işlemi burada yapılır|
|`defaultMessage()`|Hata mesajı döner|
|`@Validate()`|Özel doğrulayıcıyı alanlarda kullanmak için|
|`async: true`|Asenkron doğrulama için|
|`@ValidateIf()`|Koşullu doğrulama sağlar|
