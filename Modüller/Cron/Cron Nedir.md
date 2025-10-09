
Cron, Unix benzeri işletim sistemlerinde belirli zamanlarda, otomatik olarak komutları veya betikleri çalıştırmak için kullanılan zaman tabanlı bir iş planlayıcısıdır. Node.js uygulamalarında ise, bu işlevselliği taklit eden ve yöneten **`node-cron`** gibi paketler kullanılır.

**Temel amaçları:**

- **Tekrarlayan Görevleri Otomatikleştirmek:** Veritabanı yedeklemesi, haftalık e-posta bültenleri gönderme, sistem loglarını temizleme gibi periyodik işleri el değmeden çalıştırmak.
- **Belirli Zamanlarda İşlem Yapmak:** Her gün saat 02:00'da envanter güncellemesi yapmak gibi zamanı kritik görevleri tetiklemek.

### 2. Cron İfadeleri (Cron Expressions)

Cron işlerinin ne zaman çalışacağını belirleyen en kritik kısım, Cron İfadeleridir. Bu ifadeler, beş veya altı alandan oluşur ve her alan bir zaman birimini temsil eder.

| Alan | Anlamı        | İzin Verilen Değerler                                           |
| ---- | ------------- | --------------------------------------------------------------- |
| 1    | Dakika        | 0-59                                                            |
| 2    | Saat          | 0-23                                                            |
| 3    | Ayın Günü     | 1-31                                                            |
| 4    | Ay            | 1-12 (veya İsimler: JAN, FEB, vb.)                              |
| 5    | Haftanın Günü | 0-7 (0 veya 7 Pazar, 1 Pazartesi) (veya İsimler: SUN, MON, vb.) |

**Özel Karakterler:**

| Karakter | Anlamı                                | Örnek Kullanım                                                |
| -------- | ------------------------------------- | ------------------------------------------------------------- |
| `*`      | Tüm değerler (Her ... )               | `* * * * *` (Her dakika çalışır)                              |
| `,`      | Birden çok değer                      | `1,5 * * * *` (Dakika 1 ve 5'te çalışır)                      |
| `-`      | Aralık belirtme                       | `0 9-17 * * *` (Saat 9 ile 17 arası her saat başında çalışır) |
| `/`      | Adım değeri                           | `*/15 * * * *` (Her 15 dakikada bir çalışır)                  |
| `L`      | Son (Ayın son günü/Haftanın son günü) | `0 0 L * *` (Her ayın son günü çalışır)                       |

### 3. Node.js'de Kullanılan Temel Yöntem (`node-cron` Paketi)

Node.js ortamında cron işlerini yönetmek için en popüler paket **`node-cron`**'dur.

#### A. Kurulum

```bash
npm install node-cron
```

#### B. Temel Metotlar

|Metot|Açıklama|
|---|---|
|`cron.schedule(expression, callback)`|Yeni bir cron işi oluşturur ve zamanlar. `expression` ile belirtilen zamanda `callback` fonksiyonunu çalıştırır.|
|`task.start()`|Durdurulmuş bir işi yeniden başlatır.|
|`task.stop()`|Halihazırda çalışan bir işi durdurur.|
|`task.destroy()`|Cron işini bellekten tamamen kaldırır.|
|`task.validate(expression)`|Cron ifadesinin geçerli olup olmadığını kontrol eder.|

#### C. Basit Proje Örneği: Loglama

Her 5 saniyede bir konsola mesaj yazdıran bir görev oluşturalım.


```ts
// schedules.js

const cron = require('node-cron');
const path = require('path');

// Her 5 saniyede bir çalışacak cron ifadesi: */5 * * * * *
// Not: 6. alan saniyeyi temsil eder ve node-cron'da isteğe bağlıdır.

const gorev = cron.schedule('*/5 * * * * *', () => {
  const tarih = new Date().toLocaleTimeString();
  console.log(`[${tarih}] Cron işi çalışıyor! Veritabanı kontrolü yapıldı.`);
});

console.log('Cron işi başlatıldı. Her 5 saniyede bir çalışacak.');

// 30 saniye sonra görevi durduralım
setTimeout(() => {
    gorev.stop();
    console.log('30 saniye geçti. Cron işi durduruldu.');
}, 30000);
```

### 4. Gelişmiş Proje Senaryoları

|Proje Senaryosu|Cron İfadesi|Amaç|
|---|---|---|
|**Veritabanı Yedekleme**|`0 2 * * *`|Her gün saat 02:00'da (gece) çalışır. Yedekleme scriptini tetikler.|
|**Haftalık Bülten**|`0 10 * * 1`|Her Pazartesi saat 10:00'da çalışır. Tüm kullanıcılara bülten e-postası gönderir.|
|**Eski Oturumları Temizleme**|`*/30 * * * *`|Her 30 dakikada bir çalışır. Süresi dolmuş kullanıcı oturumlarını (session) siler.|
|**API İstatistik Güncellemesi**|`*/1 * * * *`|Her dakikada bir çalışır. Uygulama istatistiklerini hesaplayıp önbelleği (cache) günceller.|

---

## Konu Ana Hatları (Not Tutmalık Özet)

|Bölüm|Başlık|Önemli Noktalar / Metotlar|
|---|---|---|
|**Giriş**|Cron Nedir?|Tekrarlayan görevleri otomatikleştiren zaman tabanlı iş planlayıcı.|
|**Node.js Paketi**|`node-cron`|Node.js'de en çok kullanılan kütüphane.|
|**Zamanlama**|Cron İfadeleri (5-6 Alan)|`* * * * *` (Dakika Saat AyGünü Ay HaftanınGünü)|
|**Karakterler**|Özel Karakterler|`*` (Hepsi), `/` (Adım), `-` (Aralık), `,` (Çoklu).|
|**Kullanım**|Temel Metotlar|`cron.schedule()`: Görevi oluşturur. `task.stop()`: Görevi durdurur. `task.start()`: Görevi başlatır.|
|**Senaryolar**|Basit Projeler|DB Yedekleme (`0 2 * * *`), E-posta Gönderimi, Log/Önbellek Temizleme.|