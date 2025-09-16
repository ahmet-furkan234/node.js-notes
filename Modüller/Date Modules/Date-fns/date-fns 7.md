
Date-fns, belirli bir tarih aralığında işlemler yapmak için güçlü fonksiyonlar sunar. Rezervasyon, etkinlik veya çalışma saatleri kontrollerinde çok kullanışlıdır.

---

## **isWithinInterval**

- Bir tarihin belirli bir aralıkta olup olmadığını kontrol eder.
- Immutable ve okunaklı bir yapı sunar.

```ts
import { isWithinInterval, addHours } from 'date-fns';

const now = new Date('2025-09-16T10:00:00');
const intervalStart = now;              // 10:00
const intervalEnd = addHours(now, 4);  // 14:00

const target1 = new Date('2025-09-16T12:00:00'); // Aralıkta
const target2 = new Date('2025-09-16T15:00:00'); // Aralık dışında

console.log(isWithinInterval(target1, { start: intervalStart, end: intervalEnd })); // true
console.log(isWithinInterval(target2, { start: intervalStart, end: intervalEnd })); // false
```

✅ Kullanım:

- Rezervasyon saat aralığı kontrolü
- Açık-kapalı saat aralıkları
- Etkinliklerin çakışma kontrolü

---

## **differenceInMinutes / differenceInHours ile aralık kontrolü**

- Eğer bir aralık süresinin uzunluğunu kontrol etmek istersen:

```ts
import { differenceInMinutes, addMinutes } from 'date-fns';

const start = new Date('2025-09-16T10:00:00');
const end = addMinutes(start, 120); // 2 saat sonra

const target = new Date('2025-09-16T11:00:00');

console.log(differenceInMinutes(end, target)); // 60
```

- Böylece aralıkta ne kadar süre kaldığını veya geçtiğini hesaplayabilirsin.

---

## **7.3 startOfDay / endOfDay ile günlük aralıklar**

- Günlük rezervasyon veya etkinlik kontrollerinde kullanılır:

```ts
import { startOfDay, endOfDay, isWithinInterval } from 'date-fns';

const sessionDate = new Date('2025-09-16T14:30:00');

const sessionStartDay = startOfDay(sessionDate); // 00:00
const sessionEndDay = endOfDay(sessionDate);     // 23:59:59.999

const target = new Date('2025-09-16T10:00:00');

console.log(isWithinInterval(target, { start: sessionStartDay, end: sessionEndDay })); // true
```

- Bu yöntem, **aynı gün içinde başka rezervasyon var mı** kontrolü için ideal.

---

## **7.4 startOfMonth / endOfMonth ile aylık aralıklar**

- Raporlama ve istatistiklerde faydalıdır:

```ts
import { startOfMonth, endOfMonth, isWithinInterval } from 'date-fns';

const now = new Date('2025-09-16T10:00:00');
const monthStart = startOfMonth(now); // 2025-09-01T00:00:00
const monthEnd = endOfMonth(now);     // 2025-09-30T23:59:59.999

const target = new Date('2025-09-16T14:00:00');

console.log(isWithinInterval(target, { start: monthStart, end: monthEnd })); // true
```

- Aylık istatistik, faturalar veya rapor filtreleri için kullanılır.

---

## **7.5 Örnek Senaryo: Rezervasyon Çakışma Kontrolü**

```ts
import { isWithinInterval, setHours, startOfDay, endOfDay } from 'date-fns';

const sessionDateTime = setHours(new Date('2025-09-16'), 14); // Saat 14:00

const existingSessions = [
  setHours(new Date('2025-09-16'), 12),
  setHours(new Date('2025-09-16'), 16),
];

for (const existing of existingSessions) {
  if (isWithinInterval(sessionDateTime, { start: existing, end: addHours(existing, 2) })) {
    console.log('Çakışma var!');
  }
}
// Bu örnek, 14:00 ile 12:00-14:00 arası çakışma olduğu için 'Çakışma var!' döner
```

---

💡 **İpucu:**

- Interval kontrollerini **immutable** fonksiyonlarla kullan → orijinal Date objesi değişmez.
- Rezervasyon sistemlerinde start/end kombinasyonu + isWithinInterval = mükemmel çözüm.
- Günlük ve saatlik kontrol için startOfDay / endOfDay + isWithinInterval kullanılabilir.