
# 🚀 Gerçek Dünya DTO Yapıları ile class-transformer + class-validator Kullanımı

---

## 1️⃣ Senaryo: Kullanıcı Kayıt & Güncelleme Sistemi

Kullanıcılar kayıt olurken ve profillerini güncellerken validasyon yapılacak. İç içe adres nesnesi, roller, opsiyonel alanlar, tarih vb. detaylar var.

---

## 2️⃣ Proje Hazırlığı

- `class-transformer` ve `class-validator` yüklü olmalı
- `tsconfig.json`’da `experimentalDecorators` ve `emitDecoratorMetadata` açık olmalı
- `reflect-metadata` import edilmeli

---

## 3️⃣ DTO Yapısı

### `src/dto/Address.dto.ts`

```ts
import { IsString, Length } from 'class-validator';

export class AddressDto {
  @IsString()
  @Length(2, 50)
  city: string;

  @IsString()
  @Length(5, 100)
  street: string;
}
```

---

### `src/dto/User.dto.ts`

```ts
import {
  IsString,
  Length,
  IsEmail,
  ValidateNested,
  IsOptional,
  IsEnum,
  IsDate,
  MinDate,
  IsBoolean,
} from 'class-validator';
import { Type } from 'class-transformer';
import { AddressDto } from './Address.dto';

export enum UserRole {
  ADMIN = 'admin',
  USER = 'user',
  GUEST = 'guest',
}

export class CreateUserDto {
  @IsString()
  @Length(3, 20)
  username: string;

  @IsEmail()
  email: string;

  @IsString()
  @Length(6, 100)
  password: string;

  @ValidateNested()
  @Type(() => AddressDto)
  address: AddressDto;

  @IsDate()
  @MinDate(new Date('1900-01-01'))
  @Type(() => Date)  // Tarih dönüşümü için gerekli
  birthDate: Date;

  @IsEnum(UserRole)
  role: UserRole;

  @IsBoolean()
  isActive: boolean;
}
```

---

### `src/dto/UpdateUser.dto.ts`

```ts
import {
  IsString,
  Length,
  IsEmail,
  ValidateNested,
  IsOptional,
  IsEnum,
  IsDate,
  MinDate,
  IsBoolean,
} from 'class-validator';
import { Type } from 'class-transformer';
import { AddressDto } from './Address.dto';
import { UserRole } from './User.dto';

export class UpdateUserDto {
  @IsOptional()
  @IsString()
  @Length(3, 20)
  username?: string;

  @IsOptional()
  @IsEmail()
  email?: string;

  @IsOptional()
  @IsString()
  @Length(6, 100)
  password?: string;

  @IsOptional()
  @ValidateNested()
  @Type(() => AddressDto)
  address?: AddressDto;

  @IsOptional()
  @IsDate()
  @MinDate(new Date('1900-01-01'))
  @Type(() => Date)
  birthDate?: Date;

  @IsOptional()
  @IsEnum(UserRole)
  role?: UserRole;

  @IsOptional()
  @IsBoolean()
  isActive?: boolean;
}
```

---

## 4️⃣ Kullanım Örneği: Controller/Servis Katmanı

```ts
import 'reflect-metadata';
import { plainToInstance } from 'class-transformer';
import { validate } from 'class-validator';
import { CreateUserDto, UpdateUserDto } from './dto/User.dto';

async function createUser(input: object) {
  const userDto = plainToInstance(CreateUserDto, input, { enableImplicitConversion: true });

  const errors = await validate(userDto);

  if (errors.length > 0) {
    // Hataları formatla ve döndür
    console.error(errors);
    throw new Error('Validation failed!');
  }

  // Validasyon başarılı, işleme devam et
  console.log('User is valid:', userDto);
}

const newUserInput = {
  username: 'tkmate',
  email: 'tkmate@example.com',
  password: 'securepass123',
  address: { city: 'Istanbul', street: 'Main St' },
  birthDate: '1990-01-01',
  role: 'admin',
  isActive: true,
};

createUser(newUserInput);
```

---

## 5️⃣ Neden Bu Yapı?

- **`plainToInstance`** sayesinde JSON → DTO dönüşümü kolay.
- **`enableImplicitConversion`** ile tip dönüşümü (string → Date vb.) otomatik.
- **`class-validator`** ile güçlü, okunabilir validasyon.
- DTO’lar proje içerisinde standart veri yapısı olarak kullanılır, ileride ORM veya API katmanına kolay entegre edilir.
- Güncelleme DTO’sunda **`@IsOptional()`** ile opsiyonel alanlar rahatça belirtilir.

---

## 6️⃣ İleri Seviye İpuçları

- **Custom Validator** yazıp özel kurallar ekleyebilirsin.
- `@Transform()` ile özel dönüşümler yapabilirsin (örn. tarih formatı, string temizleme).
- `@Expose()`, `@Exclude()` ile JSON’a çıkacak alanları kontrol edebilirsin.
- NestJS veya Express projene bu DTO’ları pipe veya middleware ile kolayca entegre edebilirsin.
