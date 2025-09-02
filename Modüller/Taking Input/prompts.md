  [`prompts`](https://www.npmjs.com/package/prompts) modülüne geçelim. `prompts`, komut satırında **kullanıcıdan etkileşimli giriş almak** için kullanılan minimal ve çok esnek bir Node.js kütüphanesidir. Özellikle TypeScript uyumluluğu, async/await ile sorunsuz çalışması ve küçük boyutlu olmasıyla dikkat çeker.

---

## 🔧 Kurulum

```bash
npm install prompts
```

---

## 📦 Temel Kullanım

```ts
// prompts-example.ts
import prompts from 'prompts';

const main = async () => {
  const response = await prompts({
    type: 'text',
    name: 'username',
    message: 'Kullanıcı adınızı girin:'
  });

  console.log(`Merhaba, ${response.username}`);
};

main();
```

> 🧠 `prompts` her zaman bir `Promise` döndürür.

---

## 📌 Desteklediği Tipler

|Type|Açıklama|
|---|---|
|`text`|Metin girdisi alır|
|`password`|Şifre gibi gizli veri alır|
|`number`|Sayısal giriş|
|`confirm`|Evet/Hayır seçimi|
|`list`|Virgülle ayrılmış değer listesi|
|`select`|Menüden seçim (tek seçenek)|
|`multiselect`|Menüden çoklu seçim|
|`autocomplete`|Otomatik tamamlama (async destekler)|
|`date`|Tarih seçimi|

---

## 🎯 Çoklu Soru

```ts
const responses = await prompts([
  {
    type: 'text',
    name: 'email',
    message: 'Email adresinizi girin:'
  },
  {
    type: 'password',
    name: 'password',
    message: 'Şifrenizi girin:'
  },
  {
    type: 'confirm',
    name: 'remember',
    message: 'Beni hatırla?'
  }
]);

console.log(responses);
```

---

## 🛑 İptal Edilebilirlik

Kullanıcı `Ctrl+C` yaparsa `prompts` varsayılan olarak süreci durdurmaz ama istersen bu kontrolü sen yapabilirsin:

```ts
const response = await prompts({
  type: 'text',
  name: 'name',
  message: 'İsminiz?'
}, {
  onCancel: () => {
    console.log('Kullanıcı iptal etti');
    process.exit(0);
  }
});
```

---

## ✅ Avantajları

- ✔ Async/await uyumlu
- ✔ Küçük boyutlu (~20 KB)
- ✔ Validasyon destekler
- ✔ Dinamik soru üretimi
- ✔ TypeScript ile tam uyum

---

## 🆚 `inquirer` vs `prompts`

| Özellik            | `inquirer`          | `prompts`           |
| ------------------ | ------------------- | ------------------- |
| Boyut              | Büyük               | Küçük               |
| Performans         | Daha yavaş          | Hızlı ve hafif      |
| Kullanımı          | Detaylı             | Minimal ve sade     |
| TypeScript desteği | Dışarıdan tip gerek | Yerleşik destek var |
| Async kullanımı    | Orta                | Doğrudan await      |
