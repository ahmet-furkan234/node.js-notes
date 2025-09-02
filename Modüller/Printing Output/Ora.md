
- Terminalde **yükleniyor animasyonu (spinner)** gösterir.
- İşlem devam ederken kullanıcıya görsel geri bildirim verir.
- İşlem tamamlandığında başarı, hata, uyarı mesajları ile spinner durdurulur.
- Çok hafif, kolay kullanılır.

---

# 🚀 Kurulum

```bash
npm install ora
```

---

# 🛠️ Temel Kullanım

```js
import ora from 'ora';

const spinner = ora('Yükleniyor...').start();

setTimeout(() => {
  spinner.succeed('İşlem tamamlandı!');
}, 3000);
```

---

# 🌀 Spinner Kontrol Metodları

| Metot           | Açıklama                           |
| --------------- | ---------------------------------- |
| `.start()`      | Spinner'ı başlatır                 |
| `.stop()`       | Spinner'ı durdurur (mesaj olmadan) |
| `.succeed(msg)` | Başarı ile durdurup mesaj gösterir |
| `.fail(msg)`    | Hata ile durdurup mesaj gösterir   |
| `.warn(msg)`    | Uyarı ile durdurup mesaj gösterir  |
| `.info(msg)`    | Bilgi ile durdurup mesaj gösterir  |
| `.clear()`      | Spinnerı temizler (terminal temiz) |

---

# 🌈 Özelleştirme

- Spinner tipi değiştirilebilir.
- Renk, text değiştirilebilir.

```js
const spinner = ora({
  text: 'Yükleniyor...',
  spinner: 'dots',  // default: 'dots'
  color: 'cyan'
}).start();
```

---

# 🔄 Spinner Tipleri (Bazı Popülerler)

- `dots`
- `dots2`
- `dots3`
- `dots4`
- `dots5`
- `dots6`
- `dots7`
- `dots8`
- `dots9`
- `line`
- `line2`
- `pipe`
- `simpleDots`
- `star`
- `flip`
- `hamburger`
- `growVertical`
- `moon`
- `pong`
- `shark`
- `weather`

---

# 🧩 Tam Örnek

```js
import ora from 'ora';

async function uzunIslem() {
  const spinner = ora('İşlem başlatıldı...').start();

  await new Promise(resolve => setTimeout(resolve, 4000));

  spinner.succeed('İşlem başarıyla tamamlandı!');
}

uzunIslem();
```

---

# 🔧 `chalk` + `ora` Kombinasyonu

```js
import ora from 'ora';
import chalk from 'chalk';

const spinner = ora({
  text: chalk.cyan('Yükleniyor...'),
  spinner: 'star'
}).start();

setTimeout(() => {
  spinner.succeed(chalk.green('İşlem tamamlandı!'));
}, 3000);
```

---

# 📌 Özet

|Özellik|Açıklama|
|---|---|
|Terminalde spinner|Yükleniyor, bekleniyor animasyonu|
|Kolay kullanım|`ora().start()`|
|Spinner durdurma|`succeed`, `fail`, `warn`, `stop`|
|Spinner türü değiştirme|`spinner` opsiyonu ile|
|Renklendirme|`color` veya `chalk` ile|
