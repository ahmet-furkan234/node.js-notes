
## 1. **`readline` Modülü ile Input Alma**

Node.js’in standart modülü `readline` kullanıcıdan interaktif olarak veri almak için kullanılır.

---

### Örnek: Tek Satır Input Alma

```js
import readline from 'readline';

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('Adınızı girin: ', (answer) => {
  console.log(`Merhaba, ${answer}!`);
  rl.close();
});
```

---

### Açıklama

- `readline.createInterface()` ile input/output arayüzü oluşturulur.
- `rl.question()` ile kullanıcıya soru sorulur ve callback ile cevap alınır.
- İşlem bitince `rl.close()` çağrılır.

---

## 2. **Promise / Async-Await ile Input Alma**

`readline` modülünü Promise yapısıyla kullanarak `async/await` ile daha temiz kod yazabilirsin.

```js
import readline from 'readline';

function askQuestion(query) {
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
  });
  
  return new Promise(resolve => rl.question(query, ans => {
    rl.close();
    resolve(ans);
  }));
}

(async () => {
  const name = await askQuestion('Adınızı girin: ');
  console.log(`Merhaba, ${name}!`);
})();
```

---

## 3. **Birden Fazla Soru Sorma**

```js
import readline from 'readline';

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('Adınız: ', (name) => {
  rl.question('Yaşınız: ', (age) => {
    console.log(`Merhaba ${name}, yaşınız ${age}.`);
    rl.close();
  });
});
```

---

## 4. **`prompt-sync` ile Senkron Input Alma**

Alternatif olarak, senkron input almak için `prompt-sync` modülünü kullanabilirsin.

### Kurulum

```bash
npm install prompt-sync
```

### Kullanım

```js
import promptSync from 'prompt-sync';

const prompt = promptSync();

const name = prompt('Adınızı girin: ');
console.log(`Merhaba, ${name}!`);
```

---

## ⚠️ Notlar

- `readline` asenkron olduğu için büyük uygulamalarda tercih edilir.
- `prompt-sync` daha basit ve küçük scriptlerde hızlı senkron input için kullanışlıdır.
- Tarayıcıda farklı, Node.js’de farklı yöntemler kullanılır.
