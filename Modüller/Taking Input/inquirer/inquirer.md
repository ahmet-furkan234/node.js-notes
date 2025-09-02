
`inquirer`; Node.js için geliştirilmiş, kullanıcıdan terminal (CLI) üzerinden **etkileşimli girişler almayı** kolaylaştıran bir modüldür.  
Komut satırında:

- Seçmeli listeler,
- Şifre kutuları,
- Onay (yes/no) pencereleri,
- Çoktan seçmeli kutular (checkbox),
- Koşullu sorular,
- Otomatik doldurma gibi gelişmiş özellikler sağlar.

---

## 📦 Kurulum

```bash
npm install inquirer
```

ESM modül olarak kullanacaksan:

```ts
import inquirer from 'inquirer';
```

---

## 🧱 Yapı Mantığı

Tüm yapı şu 2 parçadan oluşur:

```ts
const answers = await inquirer.prompt([
  {
    type: "input",         // Soru tipi
    name: "username",      // Cevabın tutulacağı anahtar
    message: "Kullanıcı adınız nedir?",  // Kullanıcıya gösterilecek soru
  }
]);
```

---

## 🧩 Soru Tipleri (`type`)

|Tip|Açıklama|
|---|---|
|`"input"`|Kullanıcıdan yazı alır (metin)|
|`"password"`|Girilen yazıyı maskeleyerek gizler|
|`"confirm"`|Evet/hayır sorusu (boolean döner)|
|`"list"`|Tek seçenekli seçim menüsü|
|`"rawlist"`|Numaralı listeden seçim (rakam tuşlarıyla)|
|`"checkbox"`|Birden fazla seçenekli seçim (çoklu işaretleme)|
|`"expand"`|Harf tuşlarıyla seçim (örnek: a/b/c/d)|
|`"number"`|Sayı girişi (inquirer-number-input eklentisi gerekir)|
|`"editor"`|Sistem editörünü açar, içine metin yazılır|

---

## 📌 Temel Örnekler

### 🎯 1. Basit metin girdisi (`input`)

```ts
const { name } = await inquirer.prompt([
  {
    type: "input",
    name: "name",
    message: "Adınız nedir?"
  }
]);
console.log(`Merhaba, ${name}!`);
```

---

### 🔐 2. Şifre giriş alanı (`password`)

```ts
const { password } = await inquirer.prompt([
  {
    type: "password",
    name: "password",
    message: "Şifrenizi girin:"
  }
]);
```

---

### ✅ 3. Onay sorusu (`confirm`)

```ts
const { isSure } = await inquirer.prompt([
  {
    type: "confirm",
    name: "isSure",
    message: "Devam etmek istiyor musunuz?"
  }
]);
```

---

### 🔽 4. Liste seçimi (`list`)

```ts
const { language } = await inquirer.prompt([
  {
    type: "list",
    name: "language",
    message: "Hangi dili öğrenmek istersiniz?",
    choices: ["JavaScript", "Python", "Go", "Rust"]
  }
]);
```

---

### ☑️ 5. Çoktan seçmeli (`checkbox`)

```ts
const { features } = await inquirer.prompt([
  {
    type: "checkbox",
    name: "features",
    message: "Hangi özellikleri kullanmak istersiniz?",
    choices: ["Login", "Signup", "Dark Mode", "API Access"]
  }
]);
```

---

## 🧠 Ek Özellikler

### 🎯 `validate`: Giriş doğrulama

```ts
{
  type: "input",
  name: "age",
  message: "Yaşınızı girin:",
  validate: input => isNaN(input) ? "Sayı girin!" : true
}
```

---

### 🧪 `default`: Varsayılan değer

```ts
{
  type: "input",
  name: "username",
  message: "Kullanıcı adınız:",
  default: "guest"
}
```

---

### 🧮 `filter`: Giriş üzerinde düzenleme

```ts
{
  type: "input",
  name: "filename",
  message: "Dosya adı girin:",
  filter: val => val.trim().toLowerCase()
}
```

---

### 🧨 `when`: Koşullu soru gösterme

```ts
{
  type: "confirm",
  name: "useDb",
  message: "Veritabanı kullanılsın mı?"
},
{
  type: "input",
  name: "dbUrl",
  message: "Veritabanı URL'si:",
  when: answers => answers.useDb === true
}
```

---

## 🧩 Plugin Desteği

`inquirer` plugin desteği de sunar:

- `inquirer-autocomplete-prompt` → arama destekli liste
- `inquirer-datepicker-prompt` → tarih seçici
- `inquirer-file-tree-selection-prompt` → dosya/dizin seçici

```bash
npm install inquirer-autocomplete-prompt
```

---

## 🏗️ Kullanım Senaryoları

|Senaryo|inquirer Kullanımı|
|---|---|
|CLI proje başlatıcı|✔️ liste + input + confirm|
|`create-env` gibi .env üretici script|✔️ input + password|
|Kullanıcıdan işlem parametresi alma|✔️ list / checkbox|
|Yapılandırma sihirbazı|✔️ when + filter + validate|
|Kod üreticiler (yeoman gibi)|✔️ tam destek|

---

## 🧪 Komple Örnek

```ts
const inquirer = require("inquirer");

const answers = await inquirer.prompt([
  {
    type: "input",
    name: "name",
    message: "Adınız?"
  },
  {
    type: "password",
    name: "password",
    message: "Şifreniz?",
    mask: "*"
  },
  {
    type: "list",
    name: "lang",
    message: "Hangi dili öğrenmek istiyorsunuz?",
    choices: ["JavaScript", "Python", "Go"]
  },
  {
    type: "confirm",
    name: "confirm",
    message: "Bilgiler doğru mu?"
  }
]);

console.log(answers);
```


### choices işlemi

```ts
const { rTags } = await inquirer.prompt([
  {
    type: "checkbox",
    name: "rTags",
    message: "Silmek istediğiniz etiketleri işaretleyin :",
    choices: list.map((x, index) => ({
      name: x.name,   // Kullanıcıya gösterilecek isim
      value: index        // Geri dönecek olan değer (index)
    }))
  }
]);
```