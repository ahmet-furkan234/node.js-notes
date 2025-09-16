
JavaScript’in native `Date` objesi **local timezone** üzerinden çalışır.  
Date-fns tek başına timezone dönüşümü içermez, bunun için `date-fns-tz` kullanılır.

---

## **Native Date ve Timezone**

```ts
const now = new Date(); // Local timezone (örn. GMT+3)
console.log(now.toString()); // Tue Sep 16 2025 14:30:00 GMT+0300 (Turkey Standard Time)
console.log(now.toISOString()); // 2025-09-16T11:30:00.000Z → UTC
```

- `toString()` → local timezone
- `toISOString()` → UTC / GMT 0

---

## **date-fns-tz Kurulum**

```bash
npm install date-fns-tz
```

### Import

```ts
import { utcToZonedTime, zonedTimeToUtc, format } from 'date-fns-tz';
```

---

## **UTC → Local Timezone**

```ts
const utcDate = new Date('2025-09-16T11:00:00Z'); // UTC 11:00
const timeZone = 'Europe/Istanbul';               // GMT+3

const zonedDate = utcToZonedTime(utcDate, timeZone);
console.log(zonedDate.toString()); 
// Tue Sep 16 2025 14:00:00 GMT+0300 (Turkey Standard Time)
```

- UTC tarihi İstanbul saatine çevirdik → 11:00 UTC = 14:00 GMT+3

---

## **Local → UTC**

```ts
const localDate = new Date('2025-09-16T14:00:00'); // Local 14:00 (GMT+3)
const utcDate2 = zonedTimeToUtc(localDate, 'Europe/Istanbul');

console.log(utcDate2.toISOString()); // 2025-09-16T11:00:00.000Z
```

- Local tarih UTC’ye dönüştürüldü.

---

## **Timezone ile Formatlama**

```ts
const date = new Date('2025-09-16T11:00:00Z');
const timeZone = 'Europe/Istanbul';
const zonedDate = utcToZonedTime(date, timeZone);

console.log(format(zonedDate, 'yyyy-MM-dd HH:mm:ssXXX', { timeZone }));
// 2025-09-16 14:00:00+03:00
```

- `XXX` → offset gösterimi
- API response veya kullanıcı arayüzü için çok kullanışlı.

---

## **Örnek Senaryo: Rezervasyon Sistemi**

- Kullanıcı İstanbul saatinde 14:00 rezervasyon yaptı
- Backend UTC ile saklıyor

```ts
import { zonedTimeToUtc, utcToZonedTime, format } from 'date-fns-tz';

const userTimeZone = 'Europe/Istanbul';
const userInput = '2025-09-16T14:00:00';

// Local → UTC
const utcDate = zonedTimeToUtc(userInput, userTimeZone);
console.log(utcDate.toISOString()); // 2025-09-16T11:00:00.000Z

// UTC → Local
const backToLocal = utcToZonedTime(utcDate, userTimeZone);
console.log(format(backToLocal, 'yyyy-MM-dd HH:mm')); // 2025-09-16 14:00
```

- Böylece **tüm rezervasyonlar UTC’de saklanır, kullanıcıya local gösterilir**
- Zaman dilimi hatası riskini tamamen ortadan kaldırır.

---

💡 **İpucu:**

- Backend UTC saklamalı → frontend kullanıcı local timezone’da gösterir.
- `date-fns-tz` ile conversion + `format` ile stringleme → güvenli ve temiz çözüm.
- Native Date tek başına GMT offset’i anlamaz → timezone dönüşümü manuel yapılmalı.
