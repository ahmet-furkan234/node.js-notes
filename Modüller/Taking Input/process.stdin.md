
Node.js’de `process.stdin`, standart giriş (standard input) akışını temsil eder. Konsoldan veri okumak için kullanılabilir.

---

## 1. Basit Örnek: `data` event ile okuma

```js
process.stdin.on('data', (data) => {
  const input = data.toString().trim();
  console.log(`Girdi: ${input}`);

  if (input === 'exit') {
    console.log('Çıkılıyor...');
    process.exit();
  }
});
```

- Burada, kullanıcı Enter’a bastığında `data` eventi tetiklenir.
- `data` Buffer türündedir, `.toString()` ile metne çevrilir.
- `trim()` ile baştaki/sondaki boşluklar silinir.

---

## 2. `process.stdin` Ayarları

Önce `process.stdin`'in akış modunu **"resume"** yapmak gerekir ki dinlemeye başlasın:

```js
process.stdin.resume();
```

---

## 3. Satır satır okuma için

`process.stdin` doğrudan satır satır okumaz, satır sonlarını takip etmek gerekir:

```js
process.stdin.setEncoding('utf-8');
process.stdin.resume();

process.stdin.on('data', (data) => {
  const input = data.trim();
  console.log(`Girdi: ${input}`);

  if (input === 'exit') {
    console.log('Çıkılıyor...');
    process.exit();
  }
});
```

---

## 4. Örnek: Basit Komut Satırı Döngüsü

```js
console.log('Bir şeyler yazın (Çıkmak için "exit" yazın):');

process.stdin.setEncoding('utf-8');
process.stdin.resume();

process.stdin.on('data', (data) => {
  const input = data.trim();

  if (input === 'exit') {
    console.log('Çıkılıyor...');
    process.exit();
  } else {
    console.log(`Yazdınız: ${input}`);
  }
});
```

---

## 5. `readline` vs `process.stdin`

- `process.stdin` düşük seviyede veri akışı sağlar, kendi başına satır satır okumak için biraz ekstra iş yapman gerekir.
- `readline` ise `process.stdin` ve `process.stdout`’u kullanarak satır satır ve daha kolay etkileşim sağlar.
