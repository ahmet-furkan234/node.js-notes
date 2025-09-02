
## 🎯 Amaç:

> Sınıf içerisindeki bazı alanların **JSON’a dönüştürülmesini isterken**, bazılarını gizlemek (örneğin şifre, sistem içi ID vs.).

---

## 📌 Temel Mantık

- `@Exclude()` → varsayılan olarak **hiçbir alan JSON’a eklenmez**.
- `@Expose()` → sadece **işaretlenen alanlar serialize edilir**.
- `@Expose({ name: 'farkliAd' })` → JSON çıktısında alan adını değiştirir.
- `@Expose({ groups: [...] })` → Role bazlı gösterim sağlar.

---

## 🧪 Örnek: Şifre ve e-posta gizleme

```ts
import { Exclude, Expose, instanceToPlain } from 'class-transformer';

@Exclude() // sınıf genelinde her şeyi gizle
class User {
  @Expose()
  username: string;

  @Expose()
  fullName: string;

  password: string; // Expose yok: JSON’a çıkmaz
}

const user = Object.assign(new User(), {
  username: 'tkmate',
  fullName: 'Ahmet Kılıç',
  password: 'secret123'
});

const json = instanceToPlain(user);
console.log(json); // { username: 'tkmate', fullName: 'Ahmet Kılıç' }
```

---

## 📛 `@Expose({ name })`: JSON’da alan adını değiştirme

```ts
class Product {
  @Expose({ name: 'id' })
  productId: number;

  @Expose({ name: 'price_in_tl' })
  price: number;
}

const product = plainToInstance(Product, {
  id: 123,
  price_in_tl: 49.99
});

console.log(product); // { productId: 123, price: 49.99 }

const json = instanceToPlain(product);
console.log(json); // { id: 123, price_in_tl: 49.99 }
```

> **Hem JSON’dan sınıfa alırken** hem de **class’tan JSON’a çevirirken** bu isim geçerlidir.

---

## 👥 `@Expose({ groups })` ile Role-Based Serialize

```ts
class User {
  @Expose()
  username: string;

  @Expose({ groups: ['admin'] })
  email: string;

  @Expose({ groups: ['admin'] })
  isBanned: boolean;
}

const user = Object.assign(new User(), {
  username: 'tkmate',
  email: 'tk@example.com',
  isBanned: false,
});

const jsonForAdmin = instanceToPlain(user, { groups: ['admin'] });
console.log(jsonForAdmin);
// { username: 'tkmate', email: 'tk@example.com', isBanned: false }

const jsonForGuest = instanceToPlain(user, { groups: [] });
console.log(jsonForGuest);
// { username: 'tkmate' }
```

---

## 🚫 `@Exclude()` Alan Bazlı Kullanımı

Eğer tüm sınıfı değil sadece bir alanı gizlemek istersen:

```ts
class User {
  username: string;

  @Exclude()
  password: string;
}
```

---

## ✅ `@Expose()` ve `@Exclude()` ile İpucu

|Yapı|Etki|
|---|---|
|`@Exclude()` sınıf başında|Tüm alanları gizler, sadece `@Expose`’lar kalır|
|`@Exclude()` alan başında|Sadece o alan gizlenir|
|`@Expose({ name: 'jsonAdı' })`|JSON'a farklı adla serialize eder|
|`@Expose({ groups: [...] })`|Belirli gruplarda serialize edilir|

---

## 🧠 Pratik Notlar

- `classToPlain()` yerine **`instanceToPlain()`** kullan.
- Bu dekoratörler sadece **dışarıya veri gönderirken** kullanılır (serialize).
- `@Expose()` dönüşüm sırasında hem serialize hem deserialize işlemi için geçerlidir.

---

## 🧪 Kapsayıcı Örnek

```ts
import { Exclude, Expose, instanceToPlain } from 'class-transformer';

@Exclude()
class Profile {
  @Expose()
  username: string;

  @Expose({ name: 'full_name' })
  fullName: string;

  @Expose({ groups: ['admin'] })
  phone: string;

  @Exclude()
  password: string;
}

const profile = Object.assign(new Profile(), {
  username: 'tkmate',
  fullName: 'Ahmet',
  phone: '1234567890',
  password: 'secret'
});

console.log(instanceToPlain(profile)); // normal kullanıcı için
console.log(instanceToPlain(profile, { groups: ['admin'] })); // admin için
```

---

## 🎯 Özet

|Dekoratör|Görev|
|---|---|
|`@Exclude()`|Alanı gizler (ya da tüm sınıfı gizler)|
|`@Expose()`|Alanı JSON çıktısına dahil eder|
|`@Expose({ name })`|JSON’da alan adını değiştirir|
|`@Expose({ groups })`|Belirli rollere özel alanları kontrol eder|
