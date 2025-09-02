
### ✅ `@IsDate()`

**Amaç:**  
Değerin bir `Date` nesnesi olup olmadığını kontrol eder.

📌 `new Date(...)` şeklinde verilmelidir, string olarak değil.

```ts
import { IsDate } from 'class-validator';

class EventDto {
  @IsDate()
  startDate: Date;
}
```

```ts
// Geçerli
{ startDate: new Date('2025-08-01') }

// Hatalı
{ startDate: '2025-08-01' } // string olarak verildi
```

---

### ✅ `@MinDate(minDate: Date)`

**Amaç:**  
Değerin **belirtilen tarihten sonra veya aynı** olup olmadığını kontrol eder.

```ts
import { MinDate } from 'class-validator';

class BookingDto {
  @MinDate(new Date())
  checkIn: Date;
}
```

```ts
// Hatalı: geçmiş tarih verildi
{ checkIn: new Date('2023-01-01') }
```

> ⚠️ Dikkat: `MinDate` her çalıştırıldığında **anlık tarih** alınmak isteniyorsa, dinamik olarak `new Date()` yazılmalı.

---

### ✅ `@MaxDate(maxDate: Date)`

**Amaç:**  
Değerin **belirtilen tarihten önce veya aynı** olup olmadığını kontrol eder.

```ts
import { MaxDate } from 'class-validator';

class BookingDto {
  @MaxDate(new Date('2030-01-01'))
  checkOut: Date;
}
```

```ts
// Hatalı: 2040 yılı verildi
{ checkOut: new Date('2040-01-01') }
```

---

### ✅ `@IsISO8601()`

**Amaç:**  
Tarihin geçerli bir [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) formatında string olup olmadığını kontrol eder.

Bu dekoratör `string` tipi tarihleri kontrol etmek için kullanılır.

```ts
import { IsISO8601 } from 'class-validator';

class DateDto {
  @IsISO8601()
  dateString: string;
}
```

```ts
// Geçerli: "2025-08-04T10:00:00Z"
// Hatalı: "04/08/2025"
```

---

## 💡 Karşılaştırma: `@IsDate()` vs `@IsISO8601()`

|Dekoratör|Veri Tipi|Açıklama|
|---|---|---|
|`@IsDate()`|`Date`|`Date` objesi mi?|
|`@IsISO8601()`|`string`|ISO 8601 formatında tarih string’i mi?|

```ts
// İkisi birlikte kullanılmaz.
@IsDate() start: Date;
@IsISO8601() start: string;
```

---

## 🧪 Uygulamalı Örnek

```ts
import { IsDate, MinDate, MaxDate } from 'class-validator';

class ReservationDto {
  @IsDate()
  @MinDate(new Date('2025-08-01'))
  @MaxDate(new Date('2025-12-31'))
  date: Date;
}
```

---

## 🔁 Özet Tablo

|Dekoratör|Görevi|
|---|---|
|`@IsDate()`|`Date` objesi olup olmadığını kontrol eder|
|`@MinDate(date)`|En erken şu tarihte mi? (`>=`)|
|`@MaxDate(date)`|En geç şu tarihte mi? (`<=`)|
|`@IsISO8601()`|ISO 8601 formatında geçerli tarih string’i mi?|

---

## 🛠️ Ekstra: Hata Mesajı Özelleştirme

```ts
@MinDate(new Date(), {
  message: 'Tarih bugünden sonra olmalı!',
})
start: Date;
```

---

İstersen şimdi bir sonraki kategori olan **Boolean ve Enum Doğrulama** dekoratörleri ile devam edebiliriz.  
Ya da `@IsDate()` ile birlikte `class-transformer` kullanımı gibi özel senaryolara geçebiliriz.  
Hangisiyle devam edelim `TkMatE`?