
## 🔁 1. `copy(src, dest)`

Bir dosya veya klasörü başka bir konuma kopyalar.

```js
const fs = require('fs-extra');

async function exampleCopy() {
  await fs.copy('example.txt', 'backup/example.txt');
  console.log('Dosya başarıyla kopyalandı.');
}

exampleCopy();
```

---

## 🔁 2. `move(src, dest)`

Dosya veya klasörü taşır.

```js
async function exampleMove() {
  await fs.move('temp/note.txt', 'archive/note.txt');
  console.log('Dosya taşındı.');
}
exampleMove();
```

---

## 🗑️ 3. `remove(path)`

Belirtilen dosya veya klasörü (içindekilerle birlikte) siler.

```js
async function exampleRemove() {
  await fs.remove('old-backups');
  console.log('Klasör silindi.');
}
exampleRemove();
```

---

## 📁 4. `ensureDir(path)`

Klasör yoksa oluşturur, varsa hata vermez.

```js
async function exampleEnsureDir() {
  await fs.ensureDir('logs');
  console.log('Klasör oluşturuldu veya zaten vardı.');
}
exampleEnsureDir();
```

---

## 📄 5. `ensureFile(path)`

Dosya yoksa oluşturur.

```js
async function exampleEnsureFile() {
  await fs.ensureFile('data/info.txt');
  console.log('Dosya oluşturuldu veya zaten vardı.');
}
exampleEnsureFile();
```

---

## 🧹 6. `emptyDir(path)`

Klasör içindeki tüm dosyaları siler ama klasörü silmez.

```js
async function exampleEmptyDir() {
  await fs.emptyDir('temp');
  console.log('Klasör boşaltıldı.');
}
exampleEmptyDir();
```

---

## ✅ 7. `pathExists(path)`

Dosya veya klasör var mı diye kontrol eder (`fs.exists` alternatifi).

```js
async function examplePathExists() {
  const exists = await fs.pathExists('config.json');
  console.log(exists ? 'Var' : 'Yok');
}
examplePathExists();
```

---

## 📖 8. `readJson(path)`

Bir JSON dosyasını okuyup JS nesnesi olarak verir.

```js
async function exampleReadJson() {
  const data = await fs.readJson('user.json');
  console.log('Kullanıcı:', data);
}
exampleReadJson();
```

---

## ✍️ 9. `writeJson(path, object, options)`

Bir JS nesnesini JSON olarak dosyaya yazar.

```js
async function exampleWriteJson() {
  const user = { name: 'TkMatE', level: 'Pro' };
  await fs.writeJson('user.json', user, { spaces: 2 });
  console.log('JSON dosyaya yazıldı.');
}
exampleWriteJson();
```

---

## 📤 10. `outputFile(path, data)`

Dosyayı yazar, yoksa otomatik oluşturur (ara klasörlerle birlikte).

```js
async function exampleOutputFile() {
  await fs.outputFile('logs/2025/07/info.txt', 'Merhaba TkMatE!');
  console.log('Dosya oluşturuldu ve yazıldı.');
}
exampleOutputFile();
```

---

## 📤 11. `outputJson(path, data, options)`

JSON verisini dosyaya yazar, eksik klasörleri otomatik oluşturur.

```js
async function exampleOutputJson() {
  const log = { status: 'OK', time: Date.now() };
  await fs.outputJson('logs/2025/07/log.json', log, { spaces: 2 });
  console.log('JSON yazıldı.');
}
exampleOutputJson();
```

---

## 🔗 12. `ensureSymlink(src, dest)` & `ensureLink(src, dest)`

Link oluşturur, varsa bir şey yapmaz.

```js
async function exampleEnsureSymlink() {
  await fs.ensureSymlink('./data/file.txt', './link-to-file.txt');
  console.log('Sembolik link oluşturuldu.');
}
exampleEnsureSymlink();
```

---

## 🧪 13. `readFile()` / `writeFile()` / `appendFile()`

Aynı `fs.promises` gibi çalışır, ekstra kurulum gerekmez:

```js
async function exampleReadWrite() {
  await fs.writeFile('notes.txt', 'İlk satır.\n');
  await fs.appendFile('notes.txt', 'İkinci satır.\n');
  const content = await fs.readFile('notes.txt', 'utf8');
  console.log(content);
}
exampleReadWrite();
```

---

## 🚀 Ekstra İstek?

Bu metotları kullanarak:

- ✅ Mini bir **not defteri**
    
- ✅ Basit bir **yedekleme aracı**
    
- ✅ Otomatik **JSON loglama sistemi**
    

gibi gerçekçi uygulamalar yapabiliriz. Hangisini yapalım istersin? Yoksa daha az bilinen `fs-extra` fonksiyonlarıyla devam mı edelim?