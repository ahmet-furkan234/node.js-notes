
Date-fns’te tarih karşılaştırmaları için birkaç fonksiyon vardır. Rezervasyon, deadline ve validasyon işlemlerinde en çok kullanılır.

---

## **isBefore**

- **Amaç:** Bir tarihin başka bir tarihten önce olup olmadığını kontrol etmek.

```ts
import { isBefore } from 'date-fns';

const now = new Date(); // 2025-09-16T10:00
const target = new Date('2025-09-16T14:00');

console.log(isBefore(now, target)); // true
console.log(isBefore(target, now)); // false
```

✅ Kullanım:

- Rezervasyon en az 2 saat sonrası olmalı kontrolü
- Deadline geçip geçmediğini kontrol etme

---

## **isAfter**

- **Amaç:** Bir tarihin başka bir tarihten sonra olup olmadığını kontrol etmek.

```ts
import { isAfter } from 'date-fns';

const now = new Date(); // 10:00
const target = new Date('2025-09-16T14:00');

console.log(isAfter(target, now)); // true
console.log(isAfter(now, target)); // false
```

✅ Kullanım:

- Geçmiş tarihlere kayıt yapılmasını engelleme
- Rezervasyon veya etkinlik başlamış mı kontrolü

---

## **isEqual**

- **Amaç:** İki tarihin tam olarak eşit olup olmadığını kontrol etmek.

```ts
import { isEqual } from 'date-fns';

const date1 = new Date('2025-09-16T14:00:00');
const date2 = new Date('2025-09-16T14:00:00');
const date3 = new Date('2025-09-16T15:00:00');

console.log(isEqual(date1, date2)); // true
console.log(isEqual(date1, date3)); // false
```

✅ Kullanım:

- Aynı saatte rezervasyon var mı kontrolü
- Tam tarih ve saat eşitliği gerektiren işlemler

---

## **isWithinInterval**

- **Amaç:** Bir tarihin belirli bir aralık içinde olup olmadığını kontrol etmek.

```ts
import { isWithinInterval, addHours } from 'date-fns';

const now = new Date(); // 10:00
const intervalStart = now; // 10:00
const intervalEnd = addHours(now, 4); // 14:00

const target1 = new Date('2025-09-16T12:00');
const target2 = new Date('2025-09-16T15:00');

console.log(isWithinInterval(target1, { start: intervalStart, end: intervalEnd })); // true
console.log(isWithinInterval(target2, { start: intervalStart, end: intervalEnd })); // false
```

✅ Kullanım:

- Rezervasyon saat aralığı kontrolü
- Açık-kapalı saat aralığı
- Etkinlik aralıkları

---

## **isSameDay / isSameHour / isSameMinute**

- Tarih ve saat eşitliklerini daha rahat kontrol etmek için:    

```ts
import { isSameDay, isSameHour, isSameMinute } from 'date-fns';

const date1 = new Date('2025-09-16T14:30');
const date2 = new Date('2025-09-16T14:45');

console.log(isSameDay(date1, date2)); // true
console.log(isSameHour(date1, date2)); // true
console.log(isSameMinute(date1, date2)); // false
```

✅ Kullanım:

- Aynı gün ve aynı saat kontrolü
- Rezervasyon, etkinlik veya log kaydı    

---

💡 **İpucu:**

- `isBefore` ve `isAfter` ile birlikte `differenceInMinutes` veya `differenceInHours` kullanarak **minimum süre kısıtlamaları** uygulanabilir.
- `isWithinInterval` + `isSameDay` kombinasyonu, rezervasyon sistemlerinde **tarih ve saat çakışmalarını** önlemek için çok uygundur.