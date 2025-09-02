
## 🎯 Amaç

`@Transform()` ile bir alanın:

- JSON’dan sınıfa aktarılırken (deserialize),
- sınıftan JSON’a dönüştürülürken (serialize),

**özel bir dönüşüm** geçirmesini sağlayabiliriz.

---

## ✅ Temel Kullanım

```ts
import { Transform } from 'class-transformer';

class User {
  @Transform(({ value }) => value.toUpperCase())
  name: string;
}

const user = plainToInstance(User, { name: 'tkmate' });
console.log(user.name); // 'TKMATE'
```

---

## 🔍 `@Transform()` Fonksiyonu Parametreleri

```ts
@Transform(({ value, key, obj, type }) => ...)
```

|Parametre|Açıklama|
|---|---|
|`value`|Dönüştürülen alanın değeri|
|`key`|Alan adı|
|`obj`|Kaynak obje (JSON tarafı)|
|`type`|"plainToClass", "classToPlain" gibi işlem türü|

---

## 🧪 Örnek: Tarih string → Date objesi

```ts
class Event {
  @Transform(({ value }) => new Date(value))
  date: Date;
}

const plain = { date: '2024-05-10T00:00:00Z' };
const event = plainToInstance(Event, plain);
console.log(event.date instanceof Date); // true
```

---

## 🔁 Serialize ve Deserialize Farkı

```ts
class User {
  @Transform(({ value, type }) => {
    if (type === 'plainToClass') {
      return value.toUpperCase(); // JSON → Class
    }
    if (type === 'classToPlain') {
      return value.toLowerCase(); // Class → JSON
    }
  })
  name: string;
}

const plain = { name: 'Ahmet' };
const user = plainToInstance(User, plain);
console.log(user.name); // 'AHMET'

const json = instanceToPlain(user);
console.log(json); // { name: 'ahmet' }
```

---

## 🧠 Komple Örnek: Fiyatı kuruş bazında JSON’dan al, TL’ye çevir

```ts
class Product {
  @Transform(({ value }) => value / 100)
  price: number; // JSON'da 12345 (kuruş), class içinde 123.45 TL
}

const plain = { price: 12345 };
const product = plainToInstance(Product, plain);
console.log(product.price); // 123.45
```

---

## ⚙️ Serialize-only veya Deserialize-only Dönüşüm

- `toClassOnly: true` → sadece JSON’dan Class’a geçişte çalışır
- `toPlainOnly: true` → sadece Class’tan JSON’a dönüşte çalışır

```ts
class User {
  @Transform(({ value }) => value.toUpperCase(), { toClassOnly: true })
  name: string;
}
```

---

## 📅 Örnek: Tarih formatlama (Serialize sırasında)

```ts
import { format } from 'date-fns';

class Event {
  @Transform(({ value }) => format(value, 'dd/MM/yyyy'), { toPlainOnly: true })
  date: Date;
}

const e = Object.assign(new Event(), { date: new Date('2025-08-04') });
const json = instanceToPlain(e);
console.log(json); // { date: '04/08/2025' }
```

---

## 🎯 Özet

|Özellik|Açıklama|
|---|---|
|`@Transform()`|Alan üzerinde özel dönüşüm uygular|
|`value`, `type`, `obj`|Dönüşüm işlevine bilgi sağlar|
|`toClassOnly`, `toPlainOnly`|Yön kontrolü: serialize vs. deserialize|
|Dönüş türleri|string → number, string → Date, maskeleme vs.|

---

## 🔐 Uygulama Fikri: Şifre maskesi

```ts
class User {
  password: string;

  @Transform(({ obj }) => '********', { toPlainOnly: true })
  get maskedPassword() {
    return this.password;
  }
}

const u = Object.assign(new User(), { password: 'secret123' });
console.log(instanceToPlain(u)); // { maskedPassword: '********' }
```
