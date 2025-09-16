
## 1️⃣ Kurulum ve Import

```bash
npm install date-fns
npm install date-fns-tz
```

```ts
import { addHours, format, differenceInMinutes } from 'date-fns';
import { utcToZonedTime, zonedTimeToUtc } from 'date-fns-tz';
```

---

## 2️⃣ Date Oluşturma

```ts
const now = new Date();
const specific = new Date('2025-09-16T14:30:00');
```

---

## 3️⃣ Addition / Subtraction

```ts
addHours(now, 2);
addMinutes(now, 30);
subDays(now, 1);
```

---

## 4️⃣ Difference

```ts
differenceInMinutes(date1, date2);
differenceInHours(date1, date2);
differenceInDays(date1, date2);
```

---

## 5️⃣ Karşılaştırma (Comparison)

```ts
isBefore(date1, date2);
isAfter(date1, date2);
isEqual(date1, date2);
isWithinInterval(date, { start, end });
```

---

## 6️⃣ Interval ve Aralık

```ts
startOfDay(date);
endOfDay(date);
startOfMonth(date);
endOfMonth(date);
isWithinInterval(date, { start, end });
```

---

## 7️⃣ Formatlama (Temel)

```ts
format(date, 'yyyy-MM-dd');
format(date, 'HH:mm');
format(date, 'eeee, MMMM do yyyy');
```

---

## 8️⃣ Formatlama (Timezone ve Gelişmiş)

```ts
const utcDate = new Date('2025-09-16T11:00:00Z');
const tz = 'Europe/Istanbul';
const local = utcToZonedTime(utcDate, tz);
format(local, 'yyyy-MM-dd HH:mm:ssXXX', { timeZone: tz });
```

---

## 9️⃣ Timezone & GMT İşlemleri

```ts
const localDate = zonedTimeToUtc(new Date('2025-09-16T14:00:00'), 'Europe/Istanbul');
const backToLocal = utcToZonedTime(localDate, 'Europe/Istanbul');
```

---

## 10️⃣ Immutable & Tree-Shakeable

- Date-fns fonksiyonları **immutable** → orijinal Date değişmez
    
- **Tree-shakeable** → sadece import edilen fonksiyon bundle’a eklenir
    

```ts
const newDate = addHours(now, 2);
```

```

---

✅ Bu Markdown’u Obsidian’a yapıştırdığında:  

- TOC kısmındaki linkler sayfa içi anchor linkleri gibi çalışır.  
- Her başlığa tek tıkla hızlıca geçebilirsin.  
- İstersen bu şemayı **obsidian panelinde pinleyip hızlı erişim menüsü** gibi kullanabilirsin.  

---

TkMatE, istersen ben bunu biraz daha **daha kısa, tek sayfa “mini cheat sheet” tarzı** hâle getirip, bütün fonksiyonları bir tabloya da dökebilirim.  

Bunu yapayım mı?
```