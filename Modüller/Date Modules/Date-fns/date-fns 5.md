
## 🔹 Amaç

- Date objesini **okunabilir string hâline getirmek**    
- Raporlama, kullanıcıya gösterim, loglama gibi durumlar için kritik

---

## 🔹 Temel Fonksiyon

|Fonksiyon|Açıklama|
|---|---|
|`format(date, formatString)`|Verilen tarihi, istediğin formatta string olarak döner|

---

## 🔹 Format Stringleri (En Çok Kullanılanlar)

|Format|Açıklama|Örnek Çıktı|
|---|---|---|
|`yyyy`|Yıl (4 haneli)|2025|
|`MM`|Ay (01–12)|09|
|`dd`|Gün (01–31)|16|
|`HH`|Saat (24 saat formatı)|14|
|`mm`|Dakika|05|
|`ss`|Saniye|30|
|`eeee`|Haftanın günü adı|Tuesday|
|`do`|Ayın günü (ordinal)|16th|
|`MMMM`|Ayın adı|September|

---

## 🔹 Örnek Kullanım

```ts
import { format } from 'date-fns';

const now = new Date(); // 2025-09-16T10:45:30

console.log(format(now, 'yyyy-MM-dd HH:mm:ss')); // 2025-09-16 10:45:30
console.log(format(now, 'eeee, MMMM do yyyy'));  // Tuesday, September 16th 2025
console.log(format(now, 'dd/MM/yyyy'));          // 16/09/2025
```

---

## 🔹 Detaylı Açıklama

1. **Immutable**
    - format() fonksiyonu **Date objesini değiştirmez**, sadece string döner.
2. **Local Time Üzerinden Çalışır**
    - Sistem saat dilimine göre formatlar.
    - Eğer UTC formatı gerekiyorsa, UTC Date objesi kullan veya `date-fns-tz` ile timezone dönüşümü yap.
3. **Kullanım Senaryoları**
	- Rezervasyon ekranında kullanıcıya tarih göstermek
	- Loglama: API çağrılarında tarih string’i
	- Raporlama: PDF / CSV / ekran raporu

---

## 🔹 Örnek Rezervasyon Gösterimi

```ts
import { format } from 'date-fns';

const sessionDate = new Date('2025-09-16T14:00:00');
const formattedDate = format(sessionDate, 'dd/MM/yyyy HH:mm');

console.log("Rezervasyon tarihi:", formattedDate); // Rezervasyon tarihi: 16/09/2025 14:00
```

---

💡 **İpucu:**

- Format stringleri **Moment.js ile benzerdir** ama date-fns küçük ve tree-shakeable.
- Özellikle kullanıcıya gösterim veya export için çok sık kullanılır.
