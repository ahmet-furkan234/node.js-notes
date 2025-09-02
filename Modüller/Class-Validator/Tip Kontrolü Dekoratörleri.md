
## 🎯 **1. `@IsDefined()`**

**Amaç:**  
Değerin `undefined` olmadığını kontrol eder.  
⚠️ `null` kabul edilir.

**Örnek:**

```ts
import { IsDefined } from 'class-validator';

class UserDto {
  @IsDefined()
  name: string;
}
```

```ts
// Hatalı
const user = { };  // name tanımlı değil
```

---

## 🎯 **2. `@IsOptional()`**

**Amaç:**  
Alan varsa doğrulama yapılır, yoksa es geçilir.

**Örnek:**

```ts
import { IsOptional, IsString } from 'class-validator';

class UserDto {
  @IsOptional()
  @IsString()
  nickname?: string;
}
```

```ts
// Geçerli: nickname yok
const user = { };

// Geçerli: nickname string
const user2 = { nickname: 'TkMatE' };

// Hatalı: nickname sayı
const user3 = { nickname: 123 };
```

---

## 🎯 **3. `@IsEmpty()`**

**Amaç:**  
Değerin boş olması beklenir (undefined, null, "", []) gibi.

**Örnek:**

```ts
import { IsEmpty } from 'class-validator';

class DeleteRequestDto {
  @IsEmpty()
  confirm?: string;
}
```

```ts
// Geçerli
const dto = { };

// Hatalı
const dto2 = { confirm: 'yes' };
```

---

## 🎯 **4. `@IsNotEmpty()`**

**Amaç:**  
Değerin boş olmaması gerekir ("" veya `null` olamaz).

**Örnek:**

```ts
import { IsNotEmpty } from 'class-validator';

class LoginDto {
  @IsNotEmpty()
  username: string;
}
```

```ts
// Hatalı: boş string
const user = { username: "" };
```

---

## 🎯 **5. `@Equals(comparison: any)`**

**Amaç:**  
Verilen değere tam eşit mi? (`===` ile karşılaştırılır)

**Örnek:**

```ts
import { Equals } from 'class-validator';

class ConfirmDto {
  @Equals('yes')
  confirm: string;
}
```

```ts
// Geçerli
const dto = { confirm: 'yes' };

// Hatalı
const dto2 = { confirm: 'no' };
```

---

## 🎯 **6. `@NotEquals(comparison: any)`**

**Amaç:**  
Verilen değere eşit olmamalı.

**Örnek:**

```ts
import { NotEquals } from 'class-validator';

class UserDto {
  @NotEquals('admin')
  role: string;
}
```

```ts
// Hatalı
const dto = { role: 'admin' };
```

---

## 🎯 **7. `@IsIn(values: any[])`**

**Amaç:**  
Verilen değerler dizisinin içinde mi?

**Örnek:**

```ts
import { IsIn } from 'class-validator';

class ColorDto {
  @IsIn(['red', 'green', 'blue'])
  color: string;
}
```

```ts
// Geçerli
const dto = { color: 'green' };

// Hatalı
const dto2 = { color: 'pink' };
```

---

## 🎯 **8. `@IsNotIn(values: any[])`**

**Amaç:**  
Verilen değer dizisinde **olmamalı**.

**Örnek:**

```ts
import { IsNotIn } from 'class-validator';

class CategoryDto {
  @IsNotIn(['forbidden', 'illegal'])
  category: string;
}
```

```ts
// Hatalı
const dto = { category: 'forbidden' };
```

---

## 🔄 Özet Tablo

|Dekoratör|Görevi|
|---|---|
|`@IsDefined()`|`undefined` değil mi?|
|`@IsOptional()`|Varsa kontrol et, yoksa geç|
|`@IsEmpty()`|Boş mu? (`null`, `""`, `[]`)|
|`@IsNotEmpty()`|Boş değil mi?|
|`@Equals(val)`|Tam olarak eşit mi?|
|`@NotEquals(val)`|Eşit değil mi?|
|`@IsIn([...])`|Şu değerlerden biri mi?|
|`@IsNotIn([...])`|Şu değerlerden biri olmamalı|

---

İstersen bu dekoratörlerden herhangi birinin hata mesajlarını özelleştirmeyi ya da `class-transformer` ile birlikte kullanım örneklerini gösterebilirim.

👉 Bir sonraki kategoriye geçelim mi? Örneğin `String` dekoratörleri?