
## 📦 Kurulum

```bash
npm install commander
```

ESM modülü kullanıyorsan:

```js
import { Command } from 'commander';
```

CommonJS için:

```js
const { Command } = require('commander');
```

---

## 🧪 Basit Kullanım

```js
// app.js
import { Command } from 'commander';
const program = new Command();

program
  .name('uygulama')
  .description('Basit bir CLI örneği')
  .version('1.0.0');

program
  .option('-n, --name <string>', 'İsminizi girin')
  .option('-a, --age <number>', 'Yaşınızı girin');

program.parse(); // CLI argümanlarını ayrıştır

const options = program.opts();

console.log(`Merhaba ${options.name}, yaşın ${options.age}`);
```

### 🧪 Çalıştır:

```bash
node app.js --name=tkmate --age=25
```

---

## ⚙️ `Command` ile Komut Oluşturma

CLI uygulamaları sadece seçenek değil, **alt komut** (subcommand) da içerir.

### Örnek: `add`, `remove` komutları

```js
// cli.js
import { Command } from 'commander';
const program = new Command();

program
  .name('todo')
  .description('Yapılacaklar uygulaması')
  .version('1.0.0');

program
  .command('add')
  .description('Yeni bir görev ekle')
  .argument('<task>', 'Görev açıklaması')
  .action((task) => {
    console.log(`✅ Görev eklendi: ${task}`);
  });

program
  .command('remove')
  .description('Görev sil')
  .argument('<id>', 'Görev ID')
  .action((id) => {
    console.log(`🗑️ Görev silindi: ${id}`);
  });

program.parse();
```

### 🧪 Çalıştır:

```bash
node cli.js add "Alışveriş yap"
node cli.js remove 1
```

---

## 🔧 Options ve Arguments Karşılaştırması

|Özellik|Açıklama|Örnek|
|---|---|---|
|`.option()`|İsteğe bağlı parametre|`--verbose`|
|`.argument()`|Zorunlu parametre|`<filename>`|
|`.action()`|Komut çalışınca tetiklenir|`action((name) => { ... })`|

---

## 📁 Alt Komutları Harici Dosyalara Bölme

### `cli.js`

```js
import { Command } from 'commander';
import { addTask } from './commands/add.js';

const program = new Command();

program
  .command('add <task>')
  .description('Görev ekle')
  .action(addTask);

program.parse();
```

### `commands/add.js`

```js
export function addTask(task) {
  console.log(`Yeni görev eklendi: ${task}`);
}
```

---

## 🧠 Ek Özellikler

|Özellik|Açıklama|
|---|---|
|`.requiredOption()`|Zorunlu seçenek (opsiyon girilmezse hata)|
|`.alias('a')`|Kısa yol (`add` yerine `a`)|
|`.default()`|Varsayılan değer belirleme|
|`.help()`|Yardım metni|
|`program.help()`|Manuel yardım gösterimi|

---

## 🎯 Örnek: Gerçekçi Kullanım

```js
program
  .command('convert')
  .description('Resmi başka formata çevir')
  .requiredOption('-i, --input <path>', 'Girdi dosyası')
  .option('-o, --output <path>', 'Çıktı dosyası', 'output.png')
  .action((options) => {
    console.log(`Dönüştürülüyor: ${options.input} -> ${options.output}`);
  });
```

---

## 📚 Yardım Mesajı Otomatik

```bash
node cli.js --help
```

Commander, komutların ve argümanların açıklamalarıyla detaylı yardım ekranı üretir.
