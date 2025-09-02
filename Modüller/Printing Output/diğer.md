
### 🧩 1. **Enquirer**

- **Modern**, **gelişmiş**, **çok özelleştirilebilir** bir CLI prompt kütüphanesidir.
- `inquirer`’a çok benzer, ama **daha hızlı**, **daha hafif** ve **plugin desteklidir**.

**Kurulum:**

```bash
npm install enquirer
```

**Örnek:**

```js
import { prompt } from 'enquirer';

const response = await prompt({
  type: 'input',
  name: 'username',
  message: 'Kullanıcı adınız nedir?'
});

console.log(response.username);
```

---

### 🧩 2. **Clack** (eski adıyla `cliffy`)

- **Sade**, **tip güvenli**, **modern** ve `TypeScript` ile çok iyi çalışan bir CLI aracı.
- Özellikle interaktif terminal deneyimleri için güzel seçenekler sunar.

**Kurulum:**

```bash
npm install clack
```

**Örnek:**

```js
import { intro, text, outro } from '@clack/prompts';

intro("Kullanıcı Bilgisi");

const name = await text({
  message: 'Adınız nedir?'
});

outro(`Teşekkürler, ${name}`);
```

---

### 🧩 3. **Zx** (Google tarafından geliştirilmiştir)

- Node.js için yazılmış **shell scripting** odaklı bir araç, ancak input da alabilir.
- `readline` ile uğraşmak yerine daha modern bir yapı sunar.

**Kurulum:**

```bash
npm install zx
```

**Örnek:**

```js
#!/usr/bin/env zx

const name = await question('Adınız nedir? ');
console.log(`Merhaba, ${name}`);
```

---

### 🧩 4. **vorpal**

- CLI uygulamaları için **komut destekli** yapılar sunar.
- Oturum içinde komut tanımlamaya izin verir.

**Kurulum:**

```bash
npm install vorpal
```

**Örnek:**

```js
import vorpal from 'vorpal';

const cli = vorpal();

cli
  .command('selam', 'Selam verir')
  .action(function(args, callback) {
    this.log('Merhaba!');
    callback();
  });

cli.show();
```

---

### 🔍 Kıyaslama Tablosu

| Modül    | Prompt Türleri | Ağırlık | Promise Desteği | Gelişmiş UI | Açıklama                      |
| -------- | -------------- | ------- | --------------- | ----------- | ----------------------------- |
| readline | Basit          | Hafif   | ❌ (Callback)    | ❌           | En temel yapı                 |
| inquirer | Gelişmiş       | Orta    | ✅               | ✅           | Çok kullanılan klasik seçenek |
| prompts  | Gelişmiş       | Hafif   | ✅               | ✅           | Daha sade, kullanıcı dostu    |
| enquirer | Çok gelişmiş   | Hafif   | ✅               | ✅           | Daha özelleştirilebilir       |
| clack    | Modern         | Hafif   | ✅               | ✅           | Tip güvenli, yeni nesil       |
| zx       | Shell odaklı   | Hafif   | ✅               | ❌           | Script odaklı projeler için   |
| vorpal   | Komut bazlı    | Orta    | ✅               | Orta        | CLI içi komut tanımlamaları   |
