
Node.js'in yerleşik (`built-in`) bir modülüdür. Yani **harici olarak yüklemen gerekmez**.  
Konsoldan satır satır veri okumak için kullanılır.

📌 Genellikle `input` ve `output` akışları (`process.stdin`, `process.stdout`) üzerinden çalışır.

---

## 🔹 2. Basit Kullanım – `readline.createInterface`

```ts
import readline from 'readline';

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('Adınız nedir? ', (cevap) => {
  console.log(`Merhaba, ${cevap}!`);
  rl.close(); // Konsol oturumunu kapat
});
```

### Açıklama:

- `createInterface()` ile kullanıcıya soru soran bir arayüz oluşturulur.
- `rl.question()` ile kullanıcıya bir soru sorulur.
- Cevap geldikten sonra `callback` içinde işlenir ve `rl.close()` ile oturum kapatılır.

---

## 🔹 3. `rl.on()` ile Çoklu Soru Sorma (Senkron değil, olay tabanlı)

```ts
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const cevaplar: string[] = [];

rl.question("Adınız nedir? ", (ad) => {
  cevaplar.push(ad);
  rl.question("Yaşınız kaç? ", (yas) => {
    cevaplar.push(yas);
    console.log(`Hoş geldin ${cevaplar[0]}, ${cevaplar[1]} yaşındasın.`);
    rl.close();
  });
});
```

---

## 🔹 4. `async/await` ile readline kullanımı

`readline` klasik olarak `callback` yapısıyla çalışsa da, `Promise` kullanarak `await` destekli hale getirebiliriz:

```ts
import readline from 'readline';

function soruSor(soru: string): Promise<string> {
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
  });

  return new Promise((resolve) => {
    rl.question(soru, (cevap) => {
      rl.close();
      resolve(cevap);
    });
  });
}

async function basla() {
  const ad = await soruSor('Adınız nedir? ');
  const sehir = await soruSor('Hangi şehirde yaşıyorsunuz? ');
  console.log(`Adınız: ${ad}, Şehir: ${sehir}`);
}

basla();
```

---

## 🔹 5. `rl.on("line")` – Satır Satır Veri Dinleme

Özellikle terminalden **çok satırlı giriş** almak için kullanılır:

```ts
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

console.log("Birden fazla satır yazın. Çıkmak için 'exit' yazın:");

rl.on("line", (line) => {
  if (line === "exit") {
    rl.close();
    return;
  }
  console.log(`Girdiğiniz: ${line}`);
});
```

---

## 🔹 6. Otomatik Tamamlama Özelliği (Auto-Completion)

```ts
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
  completer: (line) => {
    const commands = ['help', 'exit', 'version'];
    const hits = commands.filter(c => c.startsWith(line));
    return [hits.length ? hits : commands, line];
  }
});

rl.question('Komut girin: ', (cmd) => {
  console.log(`Komut: ${cmd}`);
  rl.close();
});
```

---

## 🔹 7. `SIGINT` – CTRL+C İle Özel Davranış

```ts
rl.on('SIGINT', () => {
  console.log('\nCTRL+C yakalandı. Güle güle!');
  rl.close();
});
```

---

## 🔸 Avantajları

✅ Yerleşik (extra kurulum gerekmez)  
✅ Küçük, hızlı, doğrudan terminalle etkileşim  
✅ Promise tabanlı yapılara kolayca adapte edilir  
✅ Çok satırlı veya sürekli dinleme için uygun

---

## 🔸 Dezavantajları

⚠️ `prompts`, `inquirer` gibi gelişmiş görsel özellikleri yok  
⚠️ Sadece satır tabanlı çalışır – çoklu seçimler, checkbox gibi öğeler desteklenmez  
⚠️ Callback yapısı fazla iç içe girerse okunabilirlik düşebilir

---

## 🔚 Özet

|Özellik|readline|
|---|---|
|Modül türü|Dahili (built-in) Node.js modülü|
|Kullanım tipi|Satır bazlı CLI input|
|Modern destek|Promise & async/await ile uyumlu|
|Alternatifleri|`prompts`, `inquirer`, `enquirer`|
