
`process.stdout` → Node.js’in **standart çıktı (standard output)** akışıdır. Genellikle terminal ekranına veri yazdırmak için kullanılır.

Temel olarak:

- `stdout` = "standard output" yani çıktı
- `stdin` = "standard input" yani giriş
- `stderr` = "standard error" yani hata çıktısı

---

## 📌 Basit Kullanım

```js
process.stdout.write("Merhaba TkMatE!\n");
```

> `\n` yazmazsan, alt satıra geçmez!

**Farkı:**  
`console.log("selam")` → otomatik `\n` (satır atlatır)  
`process.stdout.write("selam")` → sadece yazdırır

---

## 🧠 Neden `stdout.write()` Kullanılır?

|Durum|Neden `stdout`?|
|---|---|
|**Canlı yazı** (yükleniyor gibi)|`console.log` her seferinde satır atlar|
|**Gelişmiş kontrol**|Renk, silme, ilerletme gibi özelliklerde esneklik sağlar|
|**Stream mantığı** (pipe vs)|`stdout` bir stream (akış) olduğu için `pipe()` gibi fonksiyonlarla uyumludur|

---

## 🌀 Örnek: Yükleniyor animasyonu

```js
let i = 0;
const frames = ['-', '\\', '|', '/'];

setInterval(() => {
  process.stdout.write(`\r${frames[i++ % frames.length]} Yükleniyor...`);
}, 100);
```

**Açıklama:**

- `\r`: imleci satır başına alır (eski çıktıyı silmek için)
- Tek satırda sürekli karakter değiştirerek animasyon yapar

---

## 🧼 Çıktıyı Temizlemek

```js
process.stdout.write('\r');
process.stdout.clearLine(0); // 0: current line
```

> Bunu bir terminal tabanlı oyun ya da uygulama yaparken kullanabilirsin (mesela sayaç, terminal UI, loader vs.).

---

## 📥 `stdin` + `stdout`: CLI Etkileşimi

```js
process.stdout.write("Adınızı girin: ");
process.stdin.on("data", (input) => {
  console.log(`Merhaba, ${input.toString().trim()}!`);
  process.exit();
});
```

Bu örnek `readline` kullanmadan basit etkileşimli CLI uygulamasıdır.

---

## 📚 Ek Özellikler (Output Stream olarak)

```js
console.log(process.stdout.isTTY); // true: terminale bağlı
console.log(process.stdout.columns); // terminal sütun sayısı
console.log(process.stdout.rows);    // terminal satır sayısı
```

---

## 🎯 Ne Zaman Kullanılır?

- Kendi `console.log` tarzı formatlayıcını yazarken
- Terminal animasyonu yaparken
- `stdin` ile kullanıcıdan veri alıp anlık yazı yazarken
- Terminal UI veya "CLI oyunları" geliştirirken