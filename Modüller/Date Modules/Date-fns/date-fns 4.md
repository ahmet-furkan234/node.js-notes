
## 🔹 Amaç

- İki tarih arasındaki farkı **gün, saat, dakika, saniye, ay veya yıl cinsinden** hesaplamak
- Rezervasyon süresi, deadline kontrolü, raporlama ve istatistikler için kritik

---

## 🔹 Temel Fonksiyonlar

| Fonksiyon                                  | Açıklama                          |
| ------------------------------------------ | --------------------------------- |
| `differenceInDays(dateLeft, dateRight)`    | İki tarih arasındaki gün farkı    |
| `differenceInHours(dateLeft, dateRight)`   | İki tarih arasındaki saat farkı   |
| `differenceInMinutes(dateLeft, dateRight)` | İki tarih arasındaki dakika farkı |
| `differenceInSeconds(dateLeft, dateRight)` | İki tarih arasındaki saniye farkı |
| `differenceInMonths(dateLeft, dateRight)`  | İki tarih arasındaki ay farkı     |
| `differenceInYears(dateLeft, dateRight)`   | İki tarih arasındaki yıl farkı    |

> dateLeft - dateRight olarak hesaplanır, negatif veya pozitif değer dönebilir.

---

## 🔹 Örnek Kullanım

```ts
import { differenceInDays, differenceInHours, differenceInMinutes } from 'date-fns';

const start = new Date('2025-09-15T10:00:00');
const end = new Date('2025-09-16T12:00:00');

console.log("Gün farkı:", differenceInDays(end, start));       // 1
console.log("Saat farkı:", differenceInHours(end, start));     // 26
console.log("Dakika farkı:", differenceInMinutes(end, start)); // 1560
```

---

## 🔹 Detaylı Açıklama

1. **Pozitif veya Negatif Değer**

```ts
differenceInDays(start, end); // -1
```

- dateLeft < dateRight → negatif
- dateLeft > dateRight → pozitif

2. **Local Time Üzerinden Çalışır**
	- Sistem saat dilimine göre hesaplar
	- Eğer UTC bazlı fark lazım ise, tarihleri UTC olarak oluştur

3. **Kullanım Senaryoları**    
	- Rezervasyon süresi kontrolü (örn: maksimum 24 saat)
	- Deadline kontrolü (bugün ile teslim tarihi farkı)
	- Raporlama: günlük, haftalık, aylık farklar

---

## 🔹 Örnek Rezervasyon Kontrolü

```ts
import { differenceInHours } from 'date-fns';

const now = new Date();
const sessionDate = new Date('2025-09-16T14:00:00');

const hoursDiff = differenceInHours(sessionDate, now);

if (hoursDiff < 2) {
  console.log("Rezervasyon en az 2 saat sonrası olmalı");
} else {
  console.log("Rezervasyon geçerli");
}
```

- Bu yöntem **addHours ile karşılaştırmaya alternatif** olarak kullanılabilir.
- Hangisi daha okunaklı gelirse onu tercih edebilirsin.
