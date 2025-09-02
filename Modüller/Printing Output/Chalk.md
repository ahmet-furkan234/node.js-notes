
- Terminalde **renkli, vurgulu, arka plan renkli, altı çizgili** gibi çeşitli stillerde yazı yazmanı sağlar.
- Hem sade hem güçlü bir API’si vardır.
- **Sürekli güncellenir ve aktif olarak kullanılır.**

---

# 🚀 Kurulum

```bash
npm install chalk
```

---

# 🛠️ Temel Kullanım

```js
import chalk from 'chalk';

console.log(chalk.red('Bu kırmızı yazı!'));
console.log(chalk.green('Başarılı!'));
console.log(chalk.blue.bgYellow('Mavi yazı sarı arka plan!'));
console.log(chalk.bold('Kalın yazı'));
console.log(chalk.underline('Altı çizili yazı'));
console.log(chalk.strikethrough('Üstü çizili yazı'));
```

---

# 🎨 Stil Zincirleme

Birden fazla stil aynı anda uygulanabilir:

```js
console.log(chalk.red.bgWhite.bold.underline('Önemli ve vurgulu yazı'));
```

---

# 🧑‍💻 Renkler ve Stiller

|Renkler|Stil Özellikleri|
|---|---|
|red, green, blue|bold, dim, italic|
|cyan, magenta|underline, inverse|
|yellow, white|strikethrough, reset|
|black|visible, hidden|

---

# 📦 Örnek: Hata, Uyarı ve Bilgi Mesajları

```js
console.log(chalk.green('✅ İşlem başarılı!'));
console.log(chalk.yellow('⚠️ Uyarı: Dikkatli olun!'));
console.log(chalk.red('❌ Hata: Bir şeyler yanlış gitti!'));
```

---

# 🔄 Koşullu Stil Kullanımı

```js
const hataVar = true;
console.log(
  hataVar ? chalk.red('Hata var!') : chalk.green('Her şey yolunda.')
);
```

---

# 🔥 İleri Seviye: Template Literals ile Kullanım

```js
const name = 'TkMatE';
console.log(chalk`Merhaba {bold.green ${name}}!`);
```

---

# 📌 Neden `chalk`?

- **Basit:** Az kodla çok şey yaparsın.
- **Taşınabilir:** Windows, Linux, Mac uyumlu.
- **Popüler:** Binlerce projede kullanılıyor.
- **ESM uyumlu:** Modern projelerde kolayca import edilir.

---

# 🔧 `chalk` + `ora` Örnek Kombinasyon

```js
import ora from 'ora';
import chalk from 'chalk';

const spinner = ora('İşlem yapılıyor...').start();

setTimeout(() => {
  spinner.succeed(chalk.green('İşlem başarıyla tamamlandı!'));
}, 3000);
```
