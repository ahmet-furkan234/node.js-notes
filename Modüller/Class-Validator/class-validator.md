`class-validator`, Node.js (özellikle TypeScript) projelerinde sınıf temelli veri doğrulaması yapmanızı sağlayan bir kütüphanedir. Genellikle `class-transformer` ile birlikte kullanılır ve **DTO (Data Transfer Object)** yapılarında doğrulama (validation) kurallarını dekoratörlerle tanımlar. Express.js gibi framework'lerle birlikte çok kullanılır.

---

## 🔧 Kurulum

```bash
npm install class-validator class-transformer
```

---

## 📦 Basit Kullanım

### 1. DTO Sınıfı Oluştur

```ts
import { IsString, IsInt, MinLength, Min, Max } from 'class-validator';

export class CreateUserDto {
  @IsString()
  @MinLength(3)
  username: string;

  @IsInt()
  @Min(18)
  @Max(99)
  age: number;
}
```

---

### 2. Doğrulama İşlemi

```ts
import { plainToInstance } from 'class-transformer';
import { validate } from 'class-validator';
import express from 'express';
import { CreateUserDto } from './dto/CreateUserDto';

const app = express();
app.use(express.json());

app.post('/users', async (req, res) => {
  const dto = plainToInstance(CreateUserDto, req.body);

  const errors = await validate(dto);

  if (errors.length > 0) {
    return res.status(400).json(errors);
  }

  res.send('User is valid!');
});

app.listen(3000);
```

---

## ✅ Sık Kullanılan Dekoratörler

| Dekoratör           | Açıklama                                                |
| ------------------- | ------------------------------------------------------- |
| `@IsString()`       | Değerin string olduğunu doğrular                        |
| `@IsInt()`          | Tam sayı olduğunu doğrular                              |
| `@Min(n)`           | Sayı için minimum değer sınırı                          |
| `@Max(n)`           | Sayı için maksimum değer sınırı                         |
| `@IsEmail()`        | Geçerli bir e-posta adresi olup olmadığını kontrol eder |
| `@IsOptional()`     | Alan isteğe bağlıysa kullanılır                         |
| `@IsBoolean()`      | Boolean olduğunu doğrular                               |
| `@Length(min, max)` | Metin uzunluğu sınırı                                   |
| `@Matches(regex)`   | Regex eşleşmesi arar                                    |
| `@IsArray()`        | Değerin dizi olduğunu doğrular                          |
| `@ArrayMinSize(n)`  | Dizinin minimum eleman sayısı                           |
| `@ArrayMaxSize(n)`  | Dizinin maksimum eleman sayısı                          |

---

## 🧪 Manuel Kullanım Örneği

```ts
const user = new CreateUserDto();
user.username = 'tk';  // kısa
user.age = 17;         // küçük

const errors = await validate(user);
console.log(errors);   // Hataları detaylı verir
```

---

## 🧠 Gelişmiş Özellikler

### 🔄 Nested Validation

```ts
class Address {
  @IsString()
  city: string;
}

class User {
  @ValidateNested()
  @Type(() => Address)
  address: Address;
}
```

---

### 🎯 Custom Validator

```ts
import { registerDecorator, ValidationOptions, ValidationArguments } from 'class-validator';

export function IsUsername(validationOptions?: ValidationOptions) {
  return function (object: Object, propertyName: string) {
    registerDecorator({
      name: 'isUsername',
      target: object.constructor,
      propertyName,
      options: validationOptions,
      validator: {
        validate(value: any, args: ValidationArguments) {
          return /^[a-zA-Z0-9]+$/.test(value); // sadece harf ve sayı
        },
        defaultMessage(args: ValidationArguments) {
          return `${args.property} sadece harf ve rakam içerebilir`;
        }
      },
    });
  };
}
```

---

## 📌 Notlar

- `validateSync()` ile senkron doğrulama yapılabilir.
- `class-transformer` ile JSON'dan sınıf nesnesine dönüşüm yapılmalı.
- Hatalar genellikle `ValidationError[]` olarak döner. JSON olarak formatlanabilir.
