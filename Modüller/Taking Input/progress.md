
### 🔧 Kurulum

```bash
npm install progress
```

---

### 📦 Kullanımı

Aşağıda temel bir örnek var:

```js
import ProgressBar from 'progress';

// toplam 20 birimlik bir progress bar
const bar = new ProgressBar(':bar :percent :etas', { total: 20 });

// her 100ms'de bir ilerlet
const timer = setInterval(() => {
  bar.tick(); // ilerlet

  if (bar.complete) {
    clearInterval(timer);
    console.log('✅ İşlem tamamlandı.');
  }
}, 100);
```

---

### 🔍 Seçenekler Açıklaması

```js
new ProgressBar(format, options)
```

#### `format` alanı:

Metin içinde şu kısımlar kullanılabilir:

| Yer Tutucu | Açıklama                    |
| ---------- | --------------------------- |
| `:bar`     | Yatay bar (örnek: `====` )  |
| `:current` | Şu anki adım                |
| `:total`   | Toplam adım                 |
| `:elapsed` | Geçen süre (saniye)         |
| `:percent` | Tamamlanma yüzdesi          |
| `:eta`     | Tahmini kalan süre (saniye) |

#### `options` alanı:

|Özellik|Açıklama|Varsayılan|
|---|---|---|
|`total`|Toplam işlem sayısı|zorunlu|
|`width`|Bar uzunluğu (karakter olarak)|40|
|`complete`|Tamamlanan kısım için karakter|`=`|
|`incomplete`|Eksik kısım için karakter|`-`|
|`renderThrottle`|Yenileme sıklığı (ms)|16|
|`clear`|Tamamlandığında barı siler (true/false)|false|

---

### 🎯 Örnek: Dosya Kopyalama Simülasyonu

```js
import ProgressBar from 'progress';
import fs from 'fs';

const total = 50;
const bar = new ProgressBar('Yükleniyor [:bar] :percent :etas', { total });

let completed = 0;
const timer = setInterval(() => {
  bar.tick(); // bar ilerlet
  completed++;

  if (completed >= total) {
    clearInterval(timer);
    console.log('📦 Yükleme tamamlandı.');
  }
}, 100);
```

---

### 🧠 Ekstra: `tick(n)` ile birden fazla adımda ilerleme

```js
bar.tick(5); // 5 adım birden ilerlet
```

---

İstersen bu progress bar'ı bir dosya indirirken, API'den veri çekerken veya çok aşamalı bir işlemde nasıl kullanabileceğini de gösterebilirim. Devam etmek ister misin?