
### 1. `@IsBoolean()`

Verinin `boolean` (`true` / `false`) tipinde olduğunu doğrular.

```ts
@IsBoolean()
isPublished: boolean;
```

---

### 2. `@IsArray()`

Değerin bir `Array` olup olmadığını doğrular.

```ts
@IsArray()
tags: string[];
```

---

### 3. `@ArrayNotEmpty()`

Array’in boş olmamasını sağlar (en az 1 eleman içermeli).

```ts
@IsArray()
@ArrayNotEmpty()
categories: string[];
```

---

### 4. `@ArrayMinSize(size: number)`

Array’in en az `size` kadar eleman içermesi gerekir.

```ts
@ArrayMinSize(2)
selectedOptions: number[];
```

---

### 5. `@ArrayMaxSize(size: number)`

Array’in en fazla `size` kadar eleman içermesi gerekir.

```ts
@ArrayMaxSize(5)
selectedOptions: number[];
```

---

### 6. `@ArrayUnique([identifier])`

Array içindeki değerlerin benzersiz (unique) olmasını sağlar. Gerekirse bir `key` belirtilebilir (object array’lerde).

```ts
@ArrayUnique()
@IsArray()
usernames: string[];

// Object array için:
@ArrayUnique(user => user.id)
users: { id: number; name: string }[];
```

---

### 7. `@IsOptional()`

Bu alanın doğrulanmasını **isteğe bağlı** hale getirir. Eğer değer varsa diğer doğrulamalar çalışır, yoksa atlanır.

```ts
@IsOptional()
@IsString()
bio?: string;
```

---

### 8. `@IsDefined()`

Değerin `undefined` olmamasını sağlar. (Ama `null` olabilir.)

```ts
@IsDefined()
@IsNumber()
age: number;
```

---

### 9. `@IsEmpty()`

Değerin boş olması gerektiğini belirtir (`null`, `undefined`, `''`, `[]`, `{}` gibi değerler kabul edilir).

```ts
@IsEmpty()
temporaryField?: string;
```

---

### 10. `@IsNotEmpty()`

Değerin boş **olmaması** gerektiğini belirtir (örneğin `""` gibi boş string kabul edilmez).

```ts
@IsNotEmpty()
@IsString()
title: string;
```

---

### 11. `@IsNotEmptyObject([options])`

Object'in **boş olmaması** gerektiğini belirtir.

```ts
@IsNotEmptyObject()
@IsObject()
profile: object;

// nested check için:
@IsNotEmptyObject(true)
@ValidateNested()
details: { name: string; age: number };
```

---

### 12. `@IsInstance(classType)`

Verinin belirli bir class örneği olup olmadığını kontrol eder.

```ts
class Address {
  @IsString()
  street: string;
}

@IsInstance(Address)
address: Address;
```

---

### 13. `@IsObject()`

Değerin bir `object` olup olmadığını doğrular.

```ts
@IsObject()
metadata: object;
```

---

### 14. `@IsIn(valuesArray)`

Verinin belirtilen sabit değerler arasında olup olmadığını kontrol eder.

```ts
@IsIn(['admin', 'user', 'moderator'])
role: string;
```

---

### 15. `@IsEnum(MyEnum)`

Verinin bir enum değerine denk geldiğini kontrol eder.

```ts
enum Status {
  Active = 'active',
  Inactive = 'inactive',
}

@IsEnum(Status)
status: Status;
```

---

### 16. `@ValidateNested()`

İç içe `class` yapılarında iç class’ın da validasyon kurallarının çalışmasını sağlar.

```ts
class Profile {
  @IsString()
  name: string;
}

class User {
  @ValidateNested()
  @Type(() => Profile)
  profile: Profile;
}
```

---

### 17. `@IsPromise()`

Değerin bir `Promise` olup olmadığını kontrol eder.

```ts
@IsPromise()
asyncOperation: Promise<any>;
```

---

İstersen sırada `Custom Validators` yani özel doğrulayıcılar ve `@ValidateIf`, `@Matches`, `@Validate` gibi gelişmiş kullanım alanlarıyla devam edebiliriz. Devam edelim mi?