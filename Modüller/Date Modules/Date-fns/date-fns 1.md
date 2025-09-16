
## 🔹 Amaç

- Yeni bir tarih (Date) oluşturmak    
- Var olan tarihi date-fns fonksiyonlarıyla manipulate etmek

## 🔹 Örnek Fonksiyonlar

- `addDays`, `subDays`, `addHours`, `subHours`
- Native `Date` ile birlikte kullanılır, immutable çalışır.

---

### 🔹 Örnekler

```ts
import { addDays, subDays, addHours, subHours } from 'date-fns';

const today = new Date();         // Bugünün tarihi
const tomorrow = addDays(today, 1); // Bugüne 1 gün ekler
const yesterday = subDays(today, 1); // Bugünden 1 gün çıkarır

const twoHoursLater = addHours(today, 2);
const oneHourAgo = subHours(today, 1);

console.log(today, tomorrow, yesterday, twoHoursLater, oneHourAgo);
```

---

### 🔹 Detaylı Açıklama

1. **Immutable Çalışır**
    - Orijinal `Date` objesi değişmez, her işlem yeni bir Date objesi döner.
    - Örn: `today` hâlâ aynı kalır, `tomorrow` farklı bir Date objesidir.
2. **Native Date ile Kullanılır**
    - date-fns, native JS Date objesi üzerine fonksiyon sağlar.
    - `new Date()` ile oluşturduğun herhangi bir tarih date-fns fonksiyonlarına direkt verilebilir.
3. **Avantajlar**
    - Karmaşık tarih hesaplamaları manuel set/get ile uğraşmadan yapılır.
    - Fonksiyon bazlı, tree-shakeable → sadece kullandığın fonksiyon bundle’a girer.

---

### 🔹 Kullanım Senaryoları

- Rezervasyon sistemi: bir gün sonrası için +1 gün kontrolü
- Deadline hesaplama: bugüne +2 saat veya +3 gün ekleme
- Tarih karşılaştırmaları için başlangıç tarihi oluşturma
