
`plainToInstance()` fonksiyonunda kullanılan bir ayardır.  
Amaç: JSON’dan gelen değerler (string, number, boolean vs.) sınıfın beklediği tipe otomatik olarak çevrilsin.

---

## 📌 Normalde Ne Olur?

```ts
class User {
  age: number;
}

const plain = { age: '25' }; // JSON'da age = string

const user = plainToInstance(User, plain);

console.log(typeof user.age); // "string" ❌
```

> Bu durumda `@IsInt()` gibi validator'lar çalışmaz çünkü `age` hâlâ string.

---

## ✅ `enableImplicitConversion: true` ile Ne Olur?

```ts
const user = plainToInstance(User, plain, {
  enableImplicitConversion: true,
});

console.log(typeof user.age); // number ✅
```

Artık `class-validator` tarafından `@IsInt()` gibi doğrulamalar sorunsuz çalışır çünkü tipi otomatik düzeltildi.

---

## 🧪 Örnek: Farkı Görelim

### DTO Sınıfı:

```ts
import { IsInt, IsDate } from 'class-validator';

class User {
  @IsInt()
  age: number;

  @IsDate()
  birthDate: Date;
}
```

### JSON Girdisi:

```ts
const input = {
  age: '30',              // string olarak geldi
  birthDate: '2000-01-01' // string tarih
};
```

### Kullanım:

```ts
const user = plainToInstance(User, input, {
  enableImplicitConversion: true
});
```

### Doğrulama:

```ts
validate(user).then(errors => {
  if (errors.length > 0) {
    console.log('Hatalar:', errors);
  } else {
    console.log('Geçerli!');
  }
});
```

> ✅ Artık `age` bir `number`, `birthDate` ise bir `Date` nesnesidir.

---

## 💡 Dönüştürülebilen Tipler

|JSON'daki Değer|Sınıf Tipi|Dönüşüm Sonucu|
|---|---|---|
|`"42"`|`number`|`42`|
|`"true"`|`boolean`|`true`|
|`"2000-01-01"`|`Date`|`new Date("2000-01-01")`|
|`"123"`|`string`|`"123"` (değişmez)|
|`"false"`|`boolean`|`false`|

> Tip kontrolü yapılırken JSON’daki string değerler beklenen tipe **otomatik çevrilir**.

---

## 🔥 Nested Objelerde de Çalışır

```ts
class Address {
  @IsInt()
  no: number;
}

class User {
  @ValidateNested()
  @Type(() => Address)
  address: Address;
}

const input = {
  address: {
    no: '5'
  }
};

const user = plainToInstance(User, input, {
  enableImplicitConversion: true
});
```

---

## 🎯 Ne Zaman Kullanılır?

- API'ye gelen JSON verilerinin türleri belirsizse (frontend her zaman doğru tipi göndermez).
    
- `@IsInt()`, `@IsBoolean()`, `@IsDate()` gibi doğrulamalarda **tip uyuşmazlığı** hataları alıyorsan.
    
- DTO'larda hem dönüşüm hem doğrulama yapıyorsan.
    

---

## 🧨 Uyarı

- Bu ayar sadece `class-transformer` dönüşümünde çalışır.
    
- Class içinde `@Type(() => Number)` gibi ek dönüşüm tanımlamak **zorunda değilsin**, ama karmaşık yapılar için `@Type()` hâlâ gereklidir.
    

---

## ✅ Özet

|Özellik|Açıklama|
|---|---|
|`enableImplicitConversion`|JSON’daki string değerleri sınıfın istediği tipe otomatik çevirir|
|Tip Uyuşmazlık Sorunu|Ortadan kalkar (`"42"` → `number`, `"true"` → `boolean` vs.)|
|`class-validator` ile uyum|`@IsInt()`, `@IsBoolean()` gibi kurallar düzgün çalışır|
|Nested nesnelerde de çalışır|`@ValidateNested()` ve `@Type()` ile beraber|

---

İstersen sıradaki konu olarak:

- 🔁 `@Transform()` ile özel alan dönüştürme
    
- 🎭 `@Expose({ name })` ile ad yeniden adlandırma
    
- 🧪 class-transformer + class-validator ile gerçek dünya örneği
    

ile devam edebiliriz.

Nasıl ilerleyelim `TkMatE`?