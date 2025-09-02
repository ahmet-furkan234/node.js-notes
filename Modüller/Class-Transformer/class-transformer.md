
- Düz JavaScript objelerini (JSON) **class örneklerine dönüştürür**.
- Dönüşüm esnasında **tip dönüşümü, tarih, array, nested object** gibi yapıları destekler.
- Class örneklerini tekrar JSON’a dönüştürmek için de yöntemler sunar.
- Özellikle `class-validator` ile beraber kullanıldığında, doğrulama öncesi tip uyumu sağlar.

---

# 📚 Temel Kavramlar ve Kullanımı

## 1️⃣ `plainToInstance()` (eski adıyla `plainToClass`)

Düz objeyi belirtilen sınıf örneğine dönüştürür.

```ts
import { plainToInstance } from 'class-transformer';

class User {
  name: string;
  age: number;
}

const plain = { name: 'Ahmet', age: '30' };

const user = plainToInstance(User, plain);

console.log(user instanceof User); // true
console.log(user.age);              // "30" (string)
```

---

## 2️⃣ `@Type(() => Class)`

Nested (iç içe) sınıfların dönüşümünü belirtir.

```ts
import { Type } from 'class-transformer';

class Address {
  city: string;
}

class User {
  @Type(() => Address)
  address: Address;
}

const plain = {
  address: { city: 'Istanbul' },
};

const user = plainToInstance(User, plain);

console.log(user.address instanceof Address); // true
```

---

## 3️⃣ `enableImplicitConversion: true`

`plainToInstance()` fonksiyonuna opsiyon olarak verildiğinde, otomatik tip dönüşümü yapar (örneğin string -> number, string -> Date).

```ts
class User {
  age: number;
  birthDate: Date;
}

const plain = {
  age: '40',
  birthDate: '2000-01-01',
};

const user = plainToInstance(User, plain, { enableImplicitConversion: true });

console.log(typeof user.age);          // number
console.log(user.birthDate instanceof Date); // true
```

---

## 4️⃣ `classToPlain()`

Class örneğini JSON objesine çevirir.

```ts
import { classToPlain } from 'class-transformer';

const plainObj = classToPlain(user);
console.log(plainObj);
```

---

# 🔥 Örnek Kullanım (class-validator ile birlikte)

```ts
import 'reflect-metadata';
import { plainToInstance } from 'class-transformer';
import { validate, IsString, IsInt, ValidateNested } from 'class-validator';
import { Type } from 'class-transformer';

class Address {
  @IsString()
  city: string;
}

class User {
  @IsString()
  name: string;

  @IsInt()
  age: number;

  @ValidateNested()
  @Type(() => Address)
  address: Address;
}

const input = {
  name: 'Ersin',
  age: '35',
  address: { city: 'Ankara' },
};

const user = plainToInstance(User, input, { enableImplicitConversion: true });

validate(user).then(errors => {
  if (errors.length > 0) {
    console.log('Validation failed:', errors);
  } else {
    console.log('Validation succeeded', user);
  }
});
```

---

# Özet Tablo

| Fonksiyon / Dekoratör      | Görevi                               |
| -------------------------- | ------------------------------------ |
| `plainToInstance()`        | Düz objeyi class örneğine dönüştürür |
| `classToPlain()`           | Class örneğini düz objeye dönüştürür |
| `@Type(() => Class)`       | Nested objelerin dönüşümünü belirtir |
| `enableImplicitConversion` | Tip dönüşümünü otomatik yapar        |
