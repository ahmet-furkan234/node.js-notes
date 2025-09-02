
> Bir class örneğini (instance) düz bir JavaScript objesine (plain object) çevirir.  
> Bu sayede nesneyi JSON olarak API'ye dönebilir veya dosyaya kaydedebilirsin.

---

## ✅ Basit Kullanım

```ts
import { classToPlain } from 'class-transformer';

class User {
  name: string;
  age: number;
}

const user = new User();
user.name = 'TkMatE';
user.age = 25;

const plain = classToPlain(user);

console.log(plain); // { name: 'TkMatE', age: 25 }
```

---

## ⚠️ Not: `classToPlain()` Artık Deprecated

Yeni projelerde `instanceToPlain()` kullanılmalı.  
İkisi aynı işi yapar. Biz yine de `classToPlain()`'ı öğrenelim, sonra `instanceToPlain()` ile karşılaştırırız.

```ts
import { instanceToPlain } from 'class-transformer';
```

---

## 🛠️ `@Expose()` ve `@Exclude()` ile Kullanımı

### 🎯 Amaç: Sadece belirli alanları JSON’a dönüştürmek

```ts
import { Exclude, Expose, classToPlain } from 'class-transformer';

class User {
  @Expose()
  name: string;

  @Exclude()
  password: string;
}

const user = new User();
user.name = 'Ersin';
user.password = 'secret123';

const plain = classToPlain(user);
console.log(plain); // { name: 'Ersin' } -> password yok!
```

> Bu işlem için `@Exclude()` sınıf başına konulmazsa tüm alanlar otomatik serialize edilir.

```ts
@Exclude() // Tüm alanları başta gizle, sadece @Expose olanları göster
class User {
  @Expose()
  name: string;

  @Expose()
  age: number;

  password: string; // serialize edilmez
}
```

---

## ⚙️ Nested (İç İçe) Nesnelerle Kullanım

```ts
import { Type, Exclude, Expose, classToPlain } from 'class-transformer';

class Address {
  @Expose()
  city: string;

  @Expose()
  street: string;
}

class User {
  @Expose()
  name: string;

  @Type(() => Address)
  @Expose()
  address: Address;
}

const user = new User();
user.name = 'Ahmet';
user.address = Object.assign(new Address(), { city: 'İstanbul', street: 'Meydan' });

const plain = classToPlain(user);
console.log(plain);
// {
//   name: 'Ahmet',
//   address: { city: 'İstanbul', street: 'Meydan' }
// }
```

---

## 📌 `groups` Desteği (Role-based serialization)

```ts
class Product {
  @Expose({ groups: ['user'] })
  name: string;

  @Expose({ groups: ['admin'] })
  costPrice: number;

  @Expose()
  salePrice: number;
}

const product = Object.assign(new Product(), {
  name: 'Klavye',
  costPrice: 50,
  salePrice: 100,
});

const plainUser = classToPlain(product, { groups: ['user'] });
console.log(plainUser); // { name: 'Klavye', salePrice: 100 }

const plainAdmin = classToPlain(product, { groups: ['admin'] });
console.log(plainAdmin); // { costPrice: 50, salePrice: 100 }
```

---

## 🔄 `classToPlain()` vs `plainToInstance()`

|Fonksiyon|Görevi|
|---|---|
|`plainToInstance()`|JSON → Class (doğrulama öncesi dönüştürme)|
|`classToPlain()`|Class → JSON (response öncesi dönüştürme)|

---

## 🎯 Öneri: Yeni Kullanım

```ts
import { instanceToPlain } from 'class-transformer';
```

`classToPlain()` ile aynı işi yapar. Yeni projelerde bunu kullan:

```ts
const json = instanceToPlain(user, { groups: ['user'] });
```

---

## 🔚 Özet

|Özellik|Açıklama|
|---|---|
|`classToPlain()`|Class örneğini JSON objesine çevirir|
|`@Expose()`|Serialize edilecek alanları belirtir|
|`@Exclude()`|Gizlenecek alanları belirtir|
|`groups`|Role/group bazlı alan gösterimi sağlar|
|`@Type()`|Nested objelerin düzgün serialize edilmesini sağlar|

---

İstersen sıradaki konulardan biriyle devam edebiliriz:

- `@Transform()` ile özel alan dönüşümleri
    
- `@Expose({ name })` ile alan adlarını yeniden adlandırma
    
- `class-transformer` ile JSON → DTO → DB objesi üçgeni
    

Nasıl devam edelim `TkMatE`?