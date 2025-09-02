
- Dosya sistemi değişikliklerini gerçek zamanlı izlemeye yarar.
- Dosya veya klasör eklenince, silince, değişince seni haberdar eder.
- Çok hızlı ve platformlar arası uyumlu (Windows, macOS, Linux).
- `fs.watch` ve `fs.watchFile`’in eksiklerini giderir, daha güvenilir çalışır.
- Gelişmiş API ve filtreleme seçenekleri sunar.

---

## 🔧 Kurulum

```bash
npm install chokidar
```

---

## 📄 Basit Kullanım Örneği (ES Modules)

```js
import chokidar from 'chokidar';

// İzlemek istediğin dosya veya klasörleri belirt
const watcher = chokidar.watch('src', {
  ignored: /(^|[\/\\])\../,  // Gizli dosyalar (dotfiles) hariç
  persistent: true           // İzleme devam edecek
});

// Dosya eklendiğinde tetiklenir
watcher.on('add', path => {
  console.log(`Dosya eklendi: ${path}`);
});

// Dosya değiştiğinde tetiklenir
watcher.on('change', path => {
  console.log(`Dosya değişti: ${path}`);
});

// Dosya silindiğinde tetiklenir
watcher.on('unlink', path => {
  console.log(`Dosya silindi: ${path}`);
});

// Klasör eklendiğinde
watcher.on('addDir', path => {
  console.log(`Klasör eklendi: ${path}`);
});

// Klasör silindiğinde
watcher.on('unlinkDir', path => {
  console.log(`Klasör silindi: ${path}`);
});

console.log('Dosya izleme başladı...');
```

---

## 🔍 Chokidar Olayları (Events)

|Event|Ne Zaman Tetiklenir?|
|---|---|
|`add`|Yeni bir dosya eklendiğinde|
|`change`|Mevcut dosya değiştiğinde|
|`unlink`|Dosya silindiğinde|
|`addDir`|Yeni klasör eklendiğinde|
|`unlinkDir`|Klasör silindiğinde|
|`ready`|Başlangıç taraması tamamlandığında (hazır)|
|`error`|İzleme sırasında hata oluştuğunda|

---

## ⚙️ İleri Seviye Ayarlar

```js
const watcher = chokidar.watch('src', {
  ignored: ['node_modules', '**/*.test.js'], // Hariç tutulan dosya ve klasörler
  ignoreInitial: true,  // Başlangıçta tüm dosyaları "add" event’i tetiklemeden atlar
  persistent: true,
  usePolling: false,    // Performans için polling kapalı, gerekirse aç
  interval: 100,        // Polling interval ayarı
});
```

---

## 🧰 Pratik Kullanım Örneği: Otomatik Yeniden Başlatma

```js
import chokidar from 'chokidar';
import { exec } from 'child_process';

const watcher = chokidar.watch('src');

watcher.on('change', path => {
  console.log(`${path} değişti, sunucu yeniden başlatılıyor...`);
  exec('npm run start', (err, stdout, stderr) => {
    if (err) console.error(err);
    else console.log(stdout);
  });
});
```

---

## 🧩 Chokidar vs fs.watch

|Özellik|Chokidar|fs.watch / fs.watchFile|
|---|---|---|
|Performans|Daha stabil ve hızlı|Platforma göre değişken|
|Dosya değişiklikleri|Güvenilir algılar|Bazı durumlarda kaçırabilir|
|Platform Desteği|Windows, Linux, macOS uyumlu|Aynı|
|API Kolaylığı|Gelişmiş, event tabanlı|Basit, eksik özellikler|
