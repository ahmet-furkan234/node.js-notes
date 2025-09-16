
## 🔹 Amaç

- Bir tarihe **saat, gün, ay, yıl eklemek veya çıkarmak**
- Rezervasyon, deadline, süre kontrolü, planlama gibi işlemler için kritik

---

## 🔹 Temel Fonksiyonlar

|Fonksiyon|Açıklama|
|---|---|
|`addHours(date, n)`|Verilen tarihe n saat ekler|
|`subHours(date, n)`|Verilen tarihten n saat çıkarır|
|`addDays(date, n)`|Verilen tarihe n gün ekler|
|`subDays(date, n)`|Verilen tarihten n gün çıkarır|
|`addMonths(date, n)`|Verilen tarihe n ay ekler|
|`subMonths(date, n)`|Verilen tarihten n ay çıkarır|
|`addYears(date, n)`|Verilen tarihe n yıl ekler|
|`subYears(date, n)`|Verilen tarihten n yıl çıkarır|

> Tüm fonksiyonlar **immutable** çalışır. Orijinal Date değişmez, yeni Date objesi döner.

---

## 🔹 Örnek Kullanım

```ts
import { addHours, subHours, addDays, subDays, addMonths, subMonths, addYears, subYears } from 'date-fns';

const now = new Date(); // Örn: 2025-09-16 10:30:00

// Saat ekleme / çıkarma
const twoHoursLater = addHours(now, 2);
const oneHourAgo = subHours(now, 1);

// Gün ekleme / çıkarma
const tomorrow = addDays(now, 1);
const yesterday = subDays(now, 1);

// Ay ekleme / çıkarma
const nextMonth = addMonths(now, 1);
const lastMonth = subMonths(now, 1);

// Yıl ekleme / çıkarma
const nextYear = addYears(now, 1);
const lastYear = subYears(now, 1);

console.log({ now, twoHoursLater, oneHourAgo, tomorrow, yesterday, nextMonth, lastMonth, nextYear, lastYear });
```

---

## 🔹 Detaylı Açıklama

1. **Immutable**
    
    - Orijinal `now` değişmez, her fonksiyon **yeni bir Date** döner.
        
    - Bu, hataları önler ve chain kullanımına uygundur.
        
2. **Local Time Üzerinden Çalışır**
    
    - Sistem saat dilimi (timezone) dikkate alınır.
        
    - Örn: Türkiye’de GMT+3 → +2 saat eklediğinde local time otomatik hesaplanır.
        
3. **Kullanım Senaryoları**
    
    - Rezervasyon: +2 saat sonrası, +1 gün sonrası gibi kurallar
        
    - Deadline: Bugünden 3 gün sonra bitiş tarihi
        
    - Planlama: Haftalık, aylık veya yıllık aktiviteler
        

---

## 🔹 Örnek Rezervasyon Kontrolü

```ts
import { addHours } from 'date-fns';

const now = new Date();
const sessionDate = new Date('2025-09-16T14:00:00');

const minReservationTime = addHours(now, 2);

if (sessionDate <= minReservationTime) {
  console.log("Rezervasyon en az 2 saat sonrası olmalı");
} else {
  console.log("Rezervasyon geçerli");
}
```

---

💡 **İpucu:**

- Tüm ekleme/çıkarma fonksiyonları **Date objesi alır** → doğrudan string veya timestamp de kullanılabilir.
    
- Chainleme yapılabilir:
    

```ts
import { addDays, addHours } from 'date-fns';
const newDate = addHours(addDays(new Date(), 1), 2); // Bugüne 1 gün + 2 saat
```

---

TkMatE, bu başlık tamam ✅

Şimdi sırada **4️⃣ Tarihler Arası Fark Hesaplama (difference Functions)** konusuna geçebiliriz ve detaylı inceleyebiliriz.

Bunu başlatalım mı?