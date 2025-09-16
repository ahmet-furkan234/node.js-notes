
## 🔹 Amaç

- Bir tarihin **günün başlangıcını (00:00:00.000)** ve **günün sonunu (23:59:59.999)** hesaplamak
- Rezervasyon, raporlama, günlük filtreleme gibi işlemler için kritik

---

## 🔹 Temel Fonksiyonlar

|Fonksiyon|Açıklama|
|---|---|
|`startOfDay(date)`|Verilen tarihin günün başlangıcını döner|
|`endOfDay(date)`|Verilen tarihin günün sonunu döner|

---

## 🔹 Örnek Kullanım

```ts
import { startOfDay, endOfDay } from 'date-fns';

const now = new Date(); // Örn: 2025-09-16 10:45:30
const start = startOfDay(now); // 2025-09-16 00:00:00.000
const end = endOfDay(now);     // 2025-09-16 23:59:59.999

console.log("Şu an:", now);
console.log("Günün başı:", start);
console.log("Günün sonu:", end);
```

**Çıktı Örneği:**

```
Şu an: 2025-09-16T10:45:30.000Z
Günün başı: 2025-09-16T00:00:00.000Z
Günün sonu: 2025-09-16T23:59:59.999Z
```

---

## 🔹 Detaylı Açıklama

1. **Local Time Üzerinden Çalışır**
    - startOfDay ve endOfDay fonksiyonları, sistem saat dilimine göre hesaplama yapar.
    - Örn: Türkiye’de GMT+3 ise gün başı saat 00:00 GMT+3 olur.
2. **Immutable**
    - Orijinal date değişmez, her fonksiyon yeni Date objesi döner.
3. **Kullanım Senaryoları**
    - **Rezervasyon filtresi:** Aynı gün içindeki session’ları listeleme
    - **Raporlama:** Günlük satış/aktivite raporları
    - **Validasyon:** Kullanıcının seçtiği tarih gün içi geçerli mi kontrolü

---

## 🔹 Örnek Rezervasyon Kontrolü

```ts
import { startOfDay, endOfDay, isWithinInterval } from 'date-fns';

const sessionDate = new Date('2025-09-16T14:00:00');
const today = new Date();

const start = startOfDay(today);
const end = endOfDay(today);

if (isWithinInterval(sessionDate, { start, end })) {
  console.log("Rezervasyon bugün için geçerli");
} else {
  console.log("Bugün dışında bir tarihe rezervasyon");
}
```

---

💡 **İpucu:**

- startOfDay / endOfDay genellikle **interval veya filtrelemelerle birlikte** kullanılır.
- Native JS ile manuel yapmak istersek:

```ts
const start = new Date(now);
start.setHours(0,0,0,0);
const end = new Date(now);
end.setHours(23,59,59,999);
```

Ama date-fns ile daha okunaklı ve güvenli.
