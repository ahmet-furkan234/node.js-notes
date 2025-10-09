
Bu örneklerin tamamı için öncelikle `node-cron` paketini kurmuş ve projenize dahil etmiş olmalısınız:


```JavaScript
// Başlangıç yapısı
const cron = require('node-cron');
```

### 1. `cron.schedule(expression, callback, options)`

Bu, bir cron işini tanımlayan ve başlatan **ana fonksiyondur**. Verilen cron ifadesine göre geri çağırım (`callback`) fonksiyonunu çalıştırır.

|Parametre|Açıklama|
|---|---|
|`expression`|Cron ifadesi (Örn: `* * * * *`).|
|`callback`|Cron işi tetiklendiğinde çalışacak fonksiyon.|
|`options`|İsteğe bağlı konfigürasyon (Örn: `scheduled: false`).|

**Örnek:** Her dakikanın ilk saniyesinde bir mesaj yazdırma.


```JavaScript
// Her dakikada bir (*/1 * * * *) çalışır.
cron.schedule('*/1 * * * *', () => {
  console.log('1. [SCHEDULE]: Her dakika başı çalıştı.');
});

// Her gün sabah 08:00'de (0 8 * * *) çalışır.
cron.schedule('0 8 * * *', () => {
  console.log('2. [SCHEDULE]: Günaydın! Günlük başlangıç görevi.');
});
```

---

### 2. `task.start()`

`scheduled: false` seçeneği ile oluşturulmuş veya daha önce `task.stop()` ile durdurulmuş bir görevi **başlatmak** için kullanılır. Cron işi oluşturulduğunda otomatik olarak dönen `task` nesnesi üzerinden çağrılır.

**Örnek:** Görevi oluştur, otomatik başlatma, sonra manuel başlat.

```JavaScript
const manuelGorev = cron.schedule('*/2 * * * *', () => {
  console.log('3. [START]: Manuel olarak başlatılan görev çalışıyor.');
}, {
  // Görevin hemen başlamamasını söyler.
  scheduled: false 
});

console.log('Manuel görev oluşturuldu ancak beklemede.');

// 5 saniye sonra görevi başlat
setTimeout(() => {
  manuelGorev.start();
  console.log('Görevi manuel olarak başlattık!');
}, 5000);
```

---

### 3. `task.stop()`

Çalışan bir cron işini **durdurmak** için kullanılır. Görev durdurulduktan sonra tekrar `task.start()` ile başlatılabilir.

**Örnek:** Bir görevi başlat, 15 saniye sonra durdur.

```JavaScript
const durdurulabilirGorev = cron.schedule('*/5 * * * * *', () => {
  const an = new Date().toLocaleTimeString();
  console.log(`4. [STOP]: Durdurulacak görev çalışıyor... (${an})`);
});

// 15 saniye sonra görevi durdur
setTimeout(() => {
  durdurulabilirGorev.stop();
  console.log('Durdurulabilir görev başarıyla durduruldu.');
}, 15000);
```

---

### 4. `task.destroy()`

Çalışan veya durdurulmuş bir cron işini **bellekten tamamen kaldırmak** için kullanılır. Bu, işin bir daha asla çalışmayacağı anlamına gelir ve geri alınamaz.

**Örnek:** Bir görevi başlat ve 30 saniye sonra tamamen yok et.

```JavaScript
const yokEdilebilirGorev = cron.schedule('*/10 * * * * *', () => {
  console.log('5. [DESTROY]: Yok edilebilir görev çalışıyor.');
});

// 30 saniye sonra görevi tamamen yok et
setTimeout(() => {
  yokEdilebilirGorev.destroy();
  console.log('Yok edilebilir görev sistemden tamamen kaldırıldı (destroy).');
}, 30000);
```

---

### 5. `cron.validate(expression)`

Verilen cron ifadesinin **geçerli bir format** olup olmadığını kontrol eder. Hata ayıklama (debugging) ve kullanıcıdan gelen ifadeleri doğrulamak için çok kullanışlıdır.

|Dönüş Değeri|Açıklama|
|---|---|
|`true`|İfade geçerlidir.|
|`false`|İfade geçersizdir.|

**Örnek:** İfade doğrulama.

```JavaScript
const gecerliIfade = '0 0 1 * *';    // Her ayın 1. günü, saat 00:00
const gecersizIfade = '99 99 * * *'; // Dakika ve saat aralığı hatalı

console.log(`6. [VALIDATE]: Geçerli ifade sonucu: ${cron.validate(gecerliIfade)}`); // true
console.log(`7. [VALIDATE]: Geçersiz ifade sonucu: ${cron.validate(gecersizIfade)}`); // false
```