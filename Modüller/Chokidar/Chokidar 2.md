
## 🎯 Proje: `auto-runner`

**Amaç:**  
`src/` klasöründe bir `.js` dosyası değiştiğinde otomatik olarak çalışan bir script’i yeniden başlatalım. Bu sistem:

- Kod değişince script’i durdurur
- Yeniden başlatır  
- Yani bir çeşit `nodemon` gibi çalışır, ama biz manuel kuruyoruz.

---

## 📁 Proje Yapısı

```
auto-runner/
├── src/
│   └── app.js        👈 İzlenecek dosya
├── watcher.js        👈 Chokidar kodları burada
├── package.json
```

---

## 1️⃣ `src/app.js` (Örnek script)

```js
console.log("Script çalıştı.");
```

Her çalıştırıldığında bunu yazacak.

---

## 2️⃣ `watcher.js` (Chokidar ile izleme)

> ECMAScript modu ile yazıyoruz (`type: module` gerekir!)

```js
// watcher.js
import chokidar from 'chokidar';
import { spawn } from 'child_process';

let subprocess;

function startScript() {
  if (subprocess) {
    subprocess.kill();
    console.log("⛔️ Eski script durduruldu.");
  }

  subprocess = spawn('node', ['src/app.js'], {
    stdio: 'inherit', // çıktıyı direkt terminale bas
  });

  console.log("🚀 Yeni script başlatıldı.");
}

// Başta bir kere başlat
startScript();

// src klasörünü izle
const watcher = chokidar.watch('./src/*.js', {
  ignoreInitial: true
});

// Değişiklik olduğunda script'i yeniden başlat
watcher.on('change', (path) => {
  console.log(`🌀 Dosya değişti: ${path}`);
  startScript();
});
```

---

## 3️⃣ `package.json`

```json
{
  "name": "auto-runner",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "node watcher.js"
  },
  "dependencies": {
    "chokidar": "^3.5.3"
  }
}
```

---

## ▶️ Projeyi Çalıştırmak

```bash
npm install
npm run dev
```

> Şimdi `src/app.js` dosyasını değiştir ve kaydet — anında yeniden çalışacak! ✨

---

## 🧠 Ekstra Geliştirmeler

- `*.ts` dosyalarını da izleyebilirsin.
- Hata loglama veya bildirim sistemleri entegre edebilirsin.
- `.env` üzerinden script yolu tanımlayabilirsin.
