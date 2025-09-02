
## 🧩 1. `process.argv` ile Temel Kullanım

Node.js’in yerleşik bir özelliğidir.

```js
console.log(process.argv);
```

```bash
node app.js selam --name=tkmate --age=25
```

### 🔍 Çıktı örneği:

```js
[
  '/usr/local/bin/node',
  '/path/to/app.js',
  'selam',
  '--name=tkmate',
  '--age=25'
]
```

İlk iki eleman sırasıyla:

1. Node yolu
2. Çalıştırılan dosya yolu

Geri kalanlar kullanıcı argümanlarıdır.

---

## 🛠️ 2. Basit Parsing Örneği

```js
const args = process.argv.slice(2); // ilk 2 eleman atlanır

for (let i = 0; i < args.length; i++) {
  if (args[i] === '--name') {
    console.log('İsim:', args[i + 1]);
  }
}
```

```bash
node app.js --name tkMate
```

---

## 📦 3. Otomatik Parsing için Kütüphaneler

### ✅ **Option 1: minimist**

```bash
npm install minimist
```

```js
import minimist from 'minimist';

const args = minimist(process.argv.slice(2));
console.log(args);
```

```bash
node app.js --name=tkmate --age=25
```

Çıktı:

```js
{ _: [], name: 'tkmate', age: 25 }
```

---

### ✅ **Option 2: yargs (Daha gelişmiş)**

```bash
npm install yargs
```

```js
import yargs from 'yargs';

const args = yargs(process.argv.slice(2)).argv;

console.log(`Hoş geldin ${args.name}, yaşın ${args.age}`);
```

```bash
node app.js --name=tkmate --age=25
```

🧠 `yargs` ile:

- Argüman zorunlu olabilir
- Kısa/uzun versiyonlar desteklenir (`-n` ve `--name`)
- Komut tanımı yapılabilir (`add`, `remove` gibi)

---

### ✅ **Option 3: commander (çok popüler)**

```bash
npm install commander
```

```js
import { Command } from 'commander';
const program = new Command();

program
  .option('-n, --name <string>', 'İsminizi girin')
  .option('-a, --age <number>', 'Yaşınızı girin');

program.parse();

const options = program.opts();
console.log(`Ad: ${options.name}, Yaş: ${options.age}`);
```

```bash
node app.js --name=tkmate --age=25
```

---

## 🧠 Bonus: Argümanlarla Ne Yapılabilir?

|Kullanım Senaryosu|Örnek Komut|
|---|---|
|Dosya açma|`node app.js open myfile.txt`|
|Klasör oluşturma|`node app.js mkdir --name=docs`|
|Kullanıcı girişi|`node app.js login --username=ahmet`|
|Tema değiştirme|`node app.js --theme=dark`|
|Versiyon bilgisi|`node app.js --version`|
