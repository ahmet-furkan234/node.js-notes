
## 1. ValidationError Yapısı

`class-validator` ile bir DTO’yu validate ettiğinde, sana şu tipte bir dizi döner:

```ts
ValidationError[] = [
  {
    target: UserDto,             // doğrulanan obje
    property: "email",           // hatalı alan
    value: "abc",                // gönderilen değer
    constraints: {               // kurallar ve mesajları
      isEmail: "email must be an email"
    },
    children: []                 // nested objeler varsa
  },
  ...
]
```

Bunu direkt API’de döndürmek kullanıcıya çok karmaşık gelir. Genelde biz sadece **alan adı + mesajlar** formatına dönüştürürüz.

---

## 2. Basit Formatlama Fonksiyonu

```ts
import { validate } from "class-validator";

function formatErrors(errors: ValidationError[]) {
  return errors.map(err => {
    return {
      field: err.property,
      messages: Object.values(err.constraints ?? {})
    };
  });
}
```

Örnek kullanım:

```ts
import { plainToInstance } from "class-transformer";
import { IsEmail, Length } from "class-validator";

class UserDto {
  @IsEmail({}, { message: "Geçerli bir email giriniz" })
  email: string;

  @Length(6, 20, { message: "Şifre 6-20 karakter arasında olmalı" })
  password: string;
}

async function testValidation() {
  const input = { email: "abc", password: "12" };
  const dto = plainToInstance(UserDto, input);

  const errors = await validate(dto);

  if (errors.length > 0) {
    console.log(formatErrors(errors));
  }
}

testValidation();
```

**Çıktı:**

```json
[
  {
    "field": "email",
    "messages": ["Geçerli bir email giriniz"]
  },
  {
    "field": "password",
    "messages": ["Şifre 6-20 karakter arasında olmalı"]
  }
]
```

---

## 3. Nested Object veya Array İçin (children)

`children` property’si doluysa, recursive bir fonksiyon kullanman gerekir:

```ts
function formatErrorsRecursive(errors: ValidationError[]) {
  return errors.map(err => {
    return {
      field: err.property,
      messages: Object.values(err.constraints ?? {}),
      children: err.children ? formatErrorsRecursive(err.children) : []
    };
  });
}
```

---

## 4. Pratik: Middleware’de Kullanım

Express.js API’de çoğu zaman middleware içine gömülür:

```ts
export async function validationMiddleware(dtoClass: any) {
  return async (req, res, next) => {
    const dto = plainToInstance(dtoClass, req.body);
    const errors = await validate(dto);

    if (errors.length > 0) {
      return res.status(400).json({
        errors: formatErrors(errors)
      });
    }

    next();
  };
}
```
