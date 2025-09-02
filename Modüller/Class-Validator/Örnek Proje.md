
## 1️⃣ Proje Hazırlığı

### Aşağıdaki paketleri kullanacağız:

- `typescript`
- `class-validator`
- `class-transformer`
- `ts-node` (TypeScript doğrudan çalıştırmak için)
- `reflect-metadata` (class-validator için zorunlu)
- `@types/node` (tip desteği için)

---

## 2️⃣ Proje Kurulumu

Terminalden şu komutları çalıştır:

```bash
mkdir user-validation-demo
cd user-validation-demo

npm init -y

npm install class-validator class-transformer reflect-metadata
npm install -D typescript ts-node @types/node
```

---

## 3️⃣ `tsconfig.json` oluştur (örnek)

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true,
    "esModuleInterop": true,
    "outDir": "./dist"
  },
  "include": ["src"]
}
```

---

## 4️⃣ Proje Klasör Yapısı

```
user-validation-demo/
│
├── src/
│   ├── dto/
│   │   ├── Address.ts
│   │   └── User.ts
│   └── index.ts
├── package.json
└── tsconfig.json
```

---

## 5️⃣ Kodları Yazalım

---

### `src/dto/Address.ts`

```ts
import { IsString, Length } from 'class-validator';

export class Address {
  @IsString()
  @Length(2, 50)
  city: string;

  @IsString()
  @Length(2, 100)
  street: string;
}
```

---

### `src/dto/User.ts`

```ts
import {
  IsString,
  Length,
  IsEmail,
  ValidateNested,
  IsOptional,
  IsDate,
  MinDate,
  IsEnum,
  IsBoolean,
} from 'class-validator';

import { Type } from 'class-transformer';
import { Address } from './Address';

export enum UserRole {
  ADMIN = 'admin',
  USER = 'user',
  GUEST = 'guest',
}

export class User {
  @IsString()
  @Length(3, 20)
  username: string;

  @IsEmail()
  email: string;

  @IsOptional()
  @IsString()
  @Length(6, 100)
  password?: string;

  @ValidateNested()
  @Type(() => Address)
  address: Address;

  @IsDate()
  @MinDate(new Date('2000-01-01'))
  birthDate: Date;

  @IsEnum(UserRole)
  role: UserRole;

  @IsBoolean()
  isActive: boolean;
}
```

---

### `src/index.ts`

```ts
import 'reflect-metadata'; // ZORUNLU: Decorators için metadata
import { plainToInstance } from 'class-transformer';
import { validate } from 'class-validator';
import { User, UserRole } from './dto/User';

const input = {
  username: 'TkMatE',
  email: 'tkmate@example.com',
  password: 'securePassword123',
  address: {
    city: 'Istanbul',
    street: 'Ataturk Blvd',
  },
  birthDate: '2001-05-15',
  role: 'admin',
  isActive: true,
};

// plain object → class instance dönüşümü + tip dönüşümü
const user = plainToInstance(User, input, {
  enableImplicitConversion: true,
});

validate(user).then((errors) => {
  if (errors.length > 0) {
    console.log('Validation errors:');
    errors.forEach((err) => {
      console.log(err.property, Object.values(err.constraints || {}).join(', '));
    });
  } else {
    console.log('Validation succeeded!');
    console.log(user);
  }
});
```

---

## 6️⃣ Çalıştırma

```bash
npx ts-node src/index.ts
```

---

# 📋 Açıklamalar

- `plainToInstance()` ile düz JSON objesi otomatik olarak sınıfa ve tip dönüşümlerine çevriliyor.
- `@ValidateNested()` ile iç içe sınıflar da doğrulanıyor.
- `@MinDate()` ile doğum tarihinin 2000 sonrası olması isteniyor.
- `enum` kontrolü `@IsEnum()` ile yapılıyor.
- `reflect-metadata` import edilmeli, aksi halde dekoratörler çalışmaz.
- `enableImplicitConversion` otomatik `string` → `Date` veya `number` dönüşümü sağlar.
