
`format` fonksiyonu, Date objelerini okunabilir string hâline getirir. Rezervasyon sistemlerinde tarih/saat gösterimi ve loglama için çok kullanışlıdır.

---

## **8.1 Temel Kullanım**

```ts
import { format } from 'date-fns';

const now = new Date('2025-09-16T14:30:45');

console.log(format(now, 'yyyy-MM-dd')); // 2025-09-16
console.log(format(now, 'HH:mm:ss'));   // 14:30:45
console.log(format(now, 'yyyy/MM/dd HH:mm')); // 2025/09/16 14:30
```

- İlk parametre: Date objesi
- İkinci parametre: format string

---

## **8.2 Yaygın Format Karakterleri**

|Karakter|Açıklama|
|---|---|
|`yyyy`|4 haneli yıl (2025)|
|`yy`|2 haneli yıl (25)|
|`MM`|Ay (01–12)|
|`MMM`|Ay kısa (Sep)|
|`MMMM`|Ay tam (September)|
|`dd`|Gün (01–31)|
|`do`|Gün ordinal (16th)|
|`HH`|24 saat formatı (00–23)|
|`hh`|12 saat formatı (01–12)|
|`mm`|Dakika (00–59)|
|`ss`|Saniye (00–59)|
|`a`|AM/PM|

---

## **8.3 Örnekler**

```ts
const date = new Date('2025-09-16T14:30:45');

console.log(format(date, 'eeee, MMMM do yyyy')); 
// Tuesday, September 16th 2025

console.log(format(date, 'HH:mm')); 
// 14:30

console.log(format(date, 'hh:mm a')); 
// 02:30 PM
```

---

## **8.4 Rezervasyon Sistemine Örnek**

- Oturum tarihini kullanıcıya güzel şekilde göstermek için:

```ts
const sessionDateTime = new Date('2025-09-16T14:00:00');

const formatted = format(sessionDateTime, 'dd/MM/yyyy HH:mm');
console.log(`Rezervasyon tarihi: ${formatted}`); 
// Rezervasyon tarihi: 16/09/2025 14:00
```

- Raporlama, loglama veya kullanıcı arayüzü için ideal.

---

## **8.5 Timezone ile Formatlama**

- Native Date objesi local timezone’a göre formatlanır.
- Farklı timezone göstermek için `date-fns-tz` kullanılır:

```ts
import { utcToZonedTime, format } from 'date-fns-tz';

const utcDate = new Date('2025-09-16T11:00:00Z');
const timeZone = 'Europe/Istanbul';
const zonedDate = utcToZonedTime(utcDate, timeZone);

console.log(format(zonedDate, 'yyyy-MM-dd HH:mm:ssXXX', { timeZone }));
// 2025-09-16 14:00:00+03:00
```

---

💡 **İpucu:**

- `format` + `startOfDay` / `endOfDay` → tarih aralıklarını string hâline getirip loglamak veya API response olarak göndermek için ideal.
- Her zaman **immutable** çalışır, orijinal Date objesi değişmez.
