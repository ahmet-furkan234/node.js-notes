
### ✅ `@IsNumber(options?: { allowNaN?: boolean, allowInfinity?: boolean, maxDecimalPlaces?: number })`

**Amaç:**  
Değerin bir sayı (`number`) olup olmadığını kontrol eder.

**Örnek:**

```ts
import { IsNumber } from 'class-validator';

class PriceDto {
  @IsNumber()
  price: number;
}
```

```ts
// Geçerli: { price: 100 }
// Hatalı: { price: "100" } // string olduğu için
```

---

### ✅ `@IsInt()`

**Amaç:**  
Sadece tam sayı (integer) kontrolü yapar.

```ts
import { IsInt } from 'class-validator';

class QuantityDto {
  @IsInt()
  quantity: number;
}
```

```ts
// Hatalı: 3.14, çünkü tam sayı değil
```

---

### ✅ `@IsPositive()`

**Amaç:**  
Pozitif sayı olup olmadığını kontrol eder (`> 0`)

```ts
@IsPositive()
amount: number;
```

```ts
// Hatalı: 0, -5
```

---

### ✅ `@IsNegative()`

**Amaç:**  
Negatif sayı olup olmadığını kontrol eder (`< 0`)

```ts
@IsNegative()
debt: number;
```

---

### ✅ `@Min(minValue: number)`

**Amaç:**  
Verilen değerin minimum bir sayının altında olup olmadığını kontrol eder.

```ts
@Min(10)
score: number;
```

```ts
// Geçerli: 12
// Hatalı: 9
```

---

### ✅ `@Max(maxValue: number)`

**Amaç:**  
Verilen değerin maksimum sınırı aşıp aşmadığını kontrol eder.

```ts
@Max(100)
score: number;
```

---

### ✅ `@IsDivisibleBy(num: number)`

**Amaç:**  
Belirtilen sayıya tam bölünüp bölünmediğini kontrol eder.

```ts
@IsDivisibleBy(5)
rating: number;
```

```ts
// Geçerli: 10
// Hatalı: 11
```

---

### ✅ `@IsDecimal(options?)`

**Amaç:**  
Ondalık sayı olup olmadığını kontrol eder. Genellikle `string` olarak kontrol yapılır.

```ts
@IsDecimal()
decimalValue: string;
```

> Not: Genellikle decimal doğrulamalar `string` tipindedir (`"12.5"` gibi), çünkü `number` tipi yuvarlama yapabilir.

---

### ✅ `@IsPort()`

**Amaç:**  
Geçerli port numarası mı? (0 ile 65535 arasında)

```ts
@IsPort()
port: number;
```

```ts
// Geçerli: 3000
// Hatalı: 70000
```

---

## 🧪 Uygulamalı Örnek

```ts
import { IsNumber, IsInt, Min, Max, IsPositive } from 'class-validator';

class ProductDto {
  @IsNumber()
  @Min(0)
  price: number;

  @IsInt()
  @Max(100)
  stock: number;

  @IsPositive()
  rating: number;
}
```

---

## 🔁 Özet Tablo

|Dekoratör|Görevi|
|---|---|
|`@IsNumber()`|Sayı mı?|
|`@IsInt()`|Tam sayı mı?|
|`@IsPositive()`|0'dan büyük mü?|
|`@IsNegative()`|0'dan küçük mü?|
|`@Min(n)`|En az `n` değeri|
|`@Max(n)`|En fazla `n` değeri|
|`@IsDivisibleBy(n)`|`n` ile tam bölünüyor mu?|
|`@IsDecimal()`|Ondalık sayı mı (`string` olarak kontrol edilir)?|
|`@IsPort()`|Geçerli port numarası mı? (0-65535)|

---

Hazırsan bir sonraki kategoriye, örneğin **Tarih ve Zaman (Date)** dekoratörlerine geçebiliriz.  
Ya da istersen buradaki dekoratörlerin her biri için özel hata mesajı tanımlama örnekleri de gösterebilirim. Hangisiyle devam etmek istersin `TkMatE`?