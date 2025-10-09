
### 🔑 Anahtar Kavram: Göreceli Değil, Mutlak

`node-cron` paketindeki tüm zamanlanmış görevler (cron job), bir `setTimeout` veya `setInterval` gibi **göreceli (relative)** bir periyotla çalışmaz. Bunun yerine, sistem saatinin **mutlak (absolute)** değerlerine kilitlenirler.

|Prensip|Açıklama|
|---|---|
|**Mutlak Değer**|Cron işi, uygulama **ne zaman başlarsa başlasın**, sadece sistem saati cron ifadesindeki değere **tam olarak ulaştığında** tetiklenir.|
|**Göreceli Değil**|"Uygulama başladıktan 10 saniye sonra" diye saymaya başlamaz. "Saniye **10, 20, 30, 40, 50 veya 00** olduğunda" çalışır.|
|**Örtüşme (Çakışma)**|Birden fazla cron ifadesi aynı mutlak zaman noktasını paylaşıyorsa, **hepsi aynı anda** (aynı Event Loop döngüsünde) tetiklenir ve çalışır.|

### Örnek Senaryo Özeti

| Cron İfadesi           | Çalışma Anları                  | Çakışma Anı              |
| ---------------------- | ------------------------------- | ------------------------ |
| `*/10 * * * * *` (10s) | 10,20,30,40,50,00 saniyeler     |                          |
| `*/30 * * * * *` (30s) | 30,00 saniyeler                 | 00. Saniye (Yeni Dakika) |
| `*/1 * * * *` (60s)    | 00 saniyesi (Dakika Başlangıcı) |                          |

**Not:** Uygulama ister 03. saniyede ister 57. saniyede başlasın; 00. saniyeye ulaşıldığı an, bu üç görev de **aynı anda** tetiklenir. İlk çalıştırmadan sonra ise her görev kendi mutlak zamanlamasına göre düzenli çalışmaya devam eder.