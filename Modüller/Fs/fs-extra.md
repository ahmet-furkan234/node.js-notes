
`fs-extra`, `fs` modülünün tüm fonksiyonlarını içerir (yani `fs.readFile`, `fs.writeFile`, vs. çalışır), **artı olarak** şu ekstra fonksiyonları da sunar:

- `copy()`
- `move()`
- `ensureFile()`
- `ensureDir()`
- `readJson()` / `writeJson()`
- `remove()` (klasör ya da dosya siler)
- `emptyDir()` (klasörü boşaltır)

---

## 🔧 Kurulum

```bash
npm install fs-extra
```

---

## 🧠 Neden `fs` Yerine `fs-extra` Kullanmalı?

|Özellik|`fs`|`fs-extra`|
|---|---|---|
|Promise desteği|`fs.promises` altında|Doğrudan destekler|
|Ekstra fonksiyonlar|❌ Yok|✅ Var|
|JSON işlemleri|❌ Manuel|✅ `readJson`, `writeJson`|
|Otomatik klasör oluşturma|❌ Hata verir|✅ `ensureDir`, `ensureFile`|

---

## 📌 Kullanım Örnekleri

### 1. 📂 Dosya Kopyalama

```js
const fs = require('fs-extra');

fs.copy('source.txt', 'backup/source.txt')
  .then(() => console.log('Dosya kopyalandı'))
  .catch(err => console.error('Hata:', err));
```

---

### 2. 📁 Klasör Oluşturma (Varsa hata vermez)

```js
fs.ensureDir('./logs')
  .then(() => console.log('Klasör hazır!'))
  .catch(err => console.error(err));
```

---

### 3. 📄 JSON Dosyasını Okuma

```js
fs.readJson('./data/user.json')
  .then(data => {
    console.log('Veri:', data);
  })
  .catch(err => console.error('Okuma hatası:', err));
```

---

### 4. 📄 JSON Dosyasına Yazma

```js
const user = { name: 'TkMatE', level: 'Pro' };

fs.writeJson('./data/user.json', user, { spaces: 2 })
  .then(() => console.log('JSON dosyasına yazıldı'))
  .catch(err => console.error(err));
```

---

### 5. 🗑️ Klasörü veya Dosyayı Silme

```js
fs.remove('./logs')
  .then(() => console.log('Silindi'))
  .catch(err => console.error(err));
```

---

### 6. 🧹 Klasörü Temizleme (içini boşaltır)

```js
fs.emptyDir('./temp')
  .then(() => console.log('Klasör boşaltıldı'))
  .catch(err => console.error(err));
```

---

### 7. 📤 Dosya Taşıma

```js
fs.move('./temp/file.txt', './backup/file.txt')
  .then(() => console.log('Dosya taşındı'))
  .catch(err => console.error(err));
```

---

## 🧪 Önerilen Kullanım Biçimi: `async/await`

```js
const fs = require('fs-extra');

async function main() {
  try {
    await fs.ensureDir('./logs');
    await fs.writeJson('./logs/log.json', { message: 'Hello TkMatE' }, { spaces: 2 });
    const data = await fs.readJson('./logs/log.json');
    console.log('Log:', data);
  } catch (err) {
    console.error('Hata:', err);
  }
}

main();
```

---

## 🚀 Sonuç

`fs-extra` seni aşağıdaki işlemlerden kurtarır:

- JSON dosyasını elle `readFile` + `JSON.parse` ile okuma
    
- Dosya var mı yok mu kontrolü
    
- Klasör yoksa `mkdir` ile oluşturma
    

> Yani: **Daha az kodla, daha sağlam işlemler.**

---

İstersen şimdi küçük bir CRUD uygulaması yapalım: `fs-extra` ile dosya oluştur, oku, güncelle, sil. İlgini çeker mi?