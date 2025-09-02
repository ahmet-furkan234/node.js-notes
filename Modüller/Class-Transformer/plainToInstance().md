
## 1. Temel Kullanımı

```ts
import { plainToInstance } from 'class-transformer';

class User {
  name: string;
  age: number;
}

const plainObj = { name: 'Ahmet', age: 30 };

// Düz objeyi User örneğine dönüştürür
const userInstance = plainToInstance(User, plainObj);

console.log(userInstance instanceof User); // true
```

> Not: `userInstance` artık `User` sınıfının gerçek örneği, yani metodları varsa kullanılabilir.

---

## 2. Özellikleri ve Seçenekleri

`plainToInstance()` 3 parametre alır:

```ts
plainToInstance(cls, plainObjectOrArray, options?)
```

|Parametre|Açıklama|
|---|---|
|`cls`|Dönüştürülecek sınıf (constructor function)|
|`plainObjectOrArray`|JSON veya düz obje (tek obje veya dizi)|
|`options`|Opsiyonel ayarlar (aşağıda detayları)|

---

## 3. Önemli `options` ayarları

|Option|Açıklama|
|---|---|
|`excludeExtraneousValues`|Sadece sınıfın `@Expose()` ile işaretli alanlarını alır (extra alanları çıkarır)|
|`enableImplicitConversion`|Düz tip dönüşümü yapar (örneğin string → number, string → Date)|
|`strategy`|`excludeAll` veya `exposeAll` — expose/exclude davranışı kontrolü|

---

## 4. Örnek: `enableImplicitConversion` kullanımı

```ts
import { plainToInstance } from 'class-transformer';

class User {
  name: string;
  age: number;
  birthDate: Date;
}

const plain = {
  name: 'Ersin',
  age: '40',
  birthDate: '1980-01-01',
};

const user = plainToInstance(User, plain, { enableImplicitConversion: true });

console.log(typeof user.age);          // number (dönüştü)
console.log(user.birthDate instanceof Date); // true
```

---

## 5. Array Dönüşümü

Bir dizi JSON objesini sınıf örnekleri dizisine çevirebilir:

```ts
const plainArray = [
  { name: 'Ahmet', age: 30 },
  { name: 'Mehmet', age: 25 }
];

const users = plainToInstance(User, plainArray);

console.log(Array.isArray(users)); // true
console.log(users[0] instanceof User); // true
```

---

## 6. `excludeExtraneousValues` örneği

```ts
import { Expose, plainToInstance } from 'class-transformer';

class User {
  @Expose()
  name: string;

  age: number;  // expose edilmediği için çıkarılır
}

const plain = { name: 'Ahmet', age: 30, city: 'Istanbul' };

const user = plainToInstance(User, plain, { excludeExtraneousValues: true });

console.log(user); // { name: 'Ahmet' }, age ve city yok!
```

---

## 7. Sık kullanılan diğer dekoratörler (özet)

|Dekoratör|İşlevi|
|---|---|
|`@Expose()`|Alanın expose edilmesini sağlar (dönüşümde)|
|`@Exclude()`|Alanın dönüşümden çıkarılmasını sağlar|
|`@Type(() => Class)`|Nested (iç içe) nesne dönüşümünü sağlar|

---

## Özet

- `plainToInstance()` düz objeleri class örneklerine dönüştürür.
    
- `enableImplicitConversion` ile string → number / Date dönüşümleri otomatik olur.
    
- `excludeExtraneousValues` ile sadece açıkça expose edilmiş alanlar alınır.
    
- Array yapılar için de aynı şekilde çalışır.
    
- `@Type()` ile iç içe sınıfların dönüşümü desteklenir.
    

---

İstersen `plainToInstance()` ile birlikte **custom dönüşümler**, **expose/exclude** detayları veya örnek bir uygulama yapabiliriz.  
Nasıl devam edelim `TkMatE`?