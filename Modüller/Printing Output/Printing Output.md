
## 🖨️ 1. Temel `console` Komutları

|Komut|Açıklama|
|---|---|
|`console.log()`|Standart çıktı|
|`console.error()`|Hata çıktısı|
|`console.warn()`|Uyarı çıktısı|
|`console.info()`|Bilgilendirme çıktısı|
|`console.table()`|Nesne/dizi tablosal yazımı|

**Örnek:**

```js
console.log("Merhaba TkMatE!");
console.error("Bir hata oluştu!");
console.warn("Bu bir uyarıdır!");
console.table([
  { ad: "Ahmet", yas: 25 },
  { ad: "Mehmet", yas: 30 }
]);
```

---

## 🌈 2. Renkli Yazı: [`chalk`](https://www.npmjs.com/package/chalk)

**Kurulum:**

```bash
npm install chalk
```

**Kullanım:**

```js
import chalk from 'chalk';

console.log(chalk.green("✅ Başarılı işlem"));
console.log(chalk.red("❌ Hata oluştu"));
console.log(chalk.yellow.bold("⚠️ Dikkat!"));
console.log(chalk.blue.bgWhite("Bilgilendirme"));
```

### Stil Zincirleme:

```js
console.log(chalk.bgMagenta.white.bold.underline("Önemli mesaj"));
```

---

## ⏳ 3. Animasyonlu Yükleyici: [`ora`](https://www.npmjs.com/package/ora)

**Kurulum:**

```bash
npm install ora
```

**Kullanım:**

```js
import ora from 'ora';

const spinner = ora('Yükleniyor...').start();

setTimeout(() => {
  spinner.succeed('İşlem tamamlandı!');
}, 2000);
```

---

## 📊 4. Tablo Gösterimi: [`cli-table3`](https://www.npmjs.com/package/cli-table3)

**Kurulum:**

```bash
npm install cli-table3
```

**Kullanım:**

```js
import Table from 'cli-table3';

const table = new Table({
  head: ['Ad', 'Yaş'],
  colWidths: [15, 5]
});

table.push(
  ['Ahmet', 25],
  ['Mehmet', 30]
);

console.log(table.toString());
```

---

## 💡 5. Biçimli Yazı: [`figlet`](https://www.npmjs.com/package/figlet)

**Kurulum:**

```bash
npm install figlet
```

**Kullanım:**

```js
import figlet from 'figlet';

figlet('Merhaba!', (err, data) => {
  if (err) {
    console.log('Figlet hatası!');
    return;
  }
  console.log(data);
});
```

---

## 🔧 BONUS: Chalk + Ora + Figlet Kombinasyonu

```js
import ora from 'ora';
import chalk from 'chalk';
import figlet from 'figlet';

const spinner = ora('Hazırlanıyor...').start();

setTimeout(() => {
  spinner.stop();
  console.log(chalk.green(figlet.textSync('Hoşgeldin!')));
}, 1500);
```

---

## 🎯 Ne Zaman Hangi Araç?

| Amaç               | Modül         |
| ------------------ | ------------- |
| Basit çıktı        | `console.log` |
| Renkli çıktı       | `chalk`       |
| Yükleme animasyonu | `ora`         |
| ASCII başlık yazı  | `figlet`      |
| Tablo              | `cli-table3`  |
