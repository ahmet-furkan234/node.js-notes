
Date-fns’in diğer büyük tarih kütüphanelerinden ayrıldığı en önemli özellikler:

1. **Immutable (Değişmez)**
2. **Tree-shakeable (Ağaç silinebilir)**

Bu özellikler özellikle performans ve bundle boyutu açısından kritik.

---

## **10.1 Immutable (Değişmez) Yapı**

- Date-fns fonksiyonları **orijinal Date objesini değiştirmez**, yeni bir Date objesi döner.
- Böylece yan etki (side-effect) riski olmaz.

### Örnek:

```ts
import { addHours, startOfDay } from 'date-fns';

const now = new Date('2025-09-16T14:30:00');
const newDate = addHours(now, 2);

console.log(now.toISOString());     // 2025-09-16T14:30:00.000Z → orijinal değişmedi
console.log(newDate.toISOString()); // 2025-09-16T16:30:00.000Z → yeni Date
```

✅ Avantaj:

- Fonksiyonları zincirleyebilirsin
- Orijinal tarih verisi bozulmaz
- Rezervasyon sistemlerinde güvenli

---

## **10.2 Tree-Shakeable (Ağaç Silinebilir)**

- Modüler import sayesinde, **sadece kullandığın fonksiyonlar bundle’a eklenir**
- Moment.js gibi kütüphanelerde tüm fonksiyonlar dahil edilir → büyük bundle

### Örnek:

```ts
// İhtiyacın olan sadece addHours ve format
import { addHours, format } from 'date-fns';
```

- `differenceInMinutes`, `startOfDay` kullanmıyorsan bundle’a dahil edilmez.
- Sonuç: Daha küçük frontend bundle → hızlı yükleme

---

## **10.3 Immutable + Tree-shakeable Kullanım Örneği**

```ts
import { addHours, differenceInMinutes, format, startOfDay } from 'date-fns';

const now = new Date();
const sessionStart = addHours(now, 3); // Immutable
const minutesLeft = differenceInMinutes(sessionStart, now);

console.log(format(startOfDay(sessionStart), 'yyyy-MM-dd HH:mm:ss'));
// 2025-09-16 00:00:00
```

- Orijinal `now` değişmedi
- Sadece kullandığın fonksiyonlar bundle’a eklendi

---

## **10.4 Özet Avantajlar**

|Özellik|Faydası|
|---|---|
|Immutable|Yan etkileri önler, güvenli ve tahmin edilebilir kod|
|Tree-shakeable|Bundle küçülür, frontend hızlı yüklenir|
|Modüler|İhtiyacın olan fonksiyonları import et, gereksiz kod ekleme|
