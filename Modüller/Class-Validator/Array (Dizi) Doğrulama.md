
#### 1. `@ArrayContains(values: any[], validationOptions?)`

> Dizi, belirtilen tüm değerleri içermeli.

```ts
@ArrayContains(['admin', 'user'])
roles: string[];
```

#### 2. `@ArrayNotContains(values: any[], validationOptions?)`

> Dizi, belirtilen değerlerden hiçbirini içermemeli.

```ts
@ArrayNotContains(['banned', 'suspended'])
statuses: string[];
```

#### 3. `@ArrayNotEmpty(validationOptions?)`

> Dizi boş olmamalı.

```ts
@ArrayNotEmpty()
tags: string[];
```

#### 4. `@ArrayMinSize(min: number, validationOptions?)`

> Dizi en az `min` kadar eleman içermeli.

```ts
@ArrayMinSize(2)
selectedIds: number[];
```

#### 5. `@ArrayMaxSize(max: number, validationOptions?)`

> Dizi en fazla `max` kadar eleman içermeli.

```ts
@ArrayMaxSize(5)
categories: string[];
```

#### 6. `@ArrayUnique(identifierOrOptions?, validationOptions?)`

> Dizideki tüm elemanlar benzersiz olmalı.

```ts
@ArrayUnique()
emails: string[];

// Nesneler içinde belirli alan bazında benzersizlik:
@ArrayUnique((o: any) => o.email)
participants: { email: string }[];
```

---

### 🧪 Örnek Sınıf Kullanımı

```ts
import { IsArray, ArrayMinSize, ArrayMaxSize, ArrayUnique, ArrayNotEmpty } from 'class-validator';

class UserPreferences {
  @IsArray()
  @ArrayNotEmpty()
  @ArrayMinSize(1)
  @ArrayMaxSize(5)
  @ArrayUnique()
  favoriteGenres: string[];
}
```

---

İsteğin doğrulama hataları oluşursa, her dekoratör özelleştirilmiş hata mesajları ile kullanılabilir:

```ts
@ArrayMinSize(1, { message: 'En az bir kategori seçilmelidir.' })
```

---

Devam etmek istediğin kategori şunlar olabilir:

- Nesne (Object) doğrulama dekoratörleri
    
- Özel doğrulama (custom validator)
    
- Koşullu doğrulama dekoratörleri (`@ValidateIf`)
    
- Nested validation (`@ValidateNested`, `Type()` ile birlikte)
    

Hangisiyle devam edelim?