`process.cwd()` Node.js'de çalışan programın **şu anki çalışma dizinini (current working directory)** döndürmek için kullanılan bir metottur. Bu dizin, terminalde Node.js uygulamasını çalıştırdığınız yerdir.

---

## 📘 Söz Dizimi (Syntax)

```js
process.cwd()
```

- Parametre almaz.
- `string` türünde mutlak (absolute) yol döner.

---

## 📂 `__dirname` ile Farkı Nedir?

| Özellik          | `process.cwd()`                               | `__dirname`                                         |
| ---------------- | --------------------------------------------- | --------------------------------------------------- |
| Döndürdüğü yol   | Uygulamanın çalıştırıldığı dizin              | Bulunduğu dosyanın dizini                           |
| Ne zaman değişir | Terminalden farklı klasörde çalıştırıldığında | Sabittir, dosya nereye taşınırsa oraya göre değişir |
| Kullanım alanı   | Dosya/klasör işlemleri, path ayarlamaları     | Modül ve kaynak yolu ayarlamaları                   |

---

## 📌 Örnek:

### Dosya yapısı:

```
my-app/
│
├── index.js
└── subfolder/
    └── test.js
```

### `index.js`

```js
console.log('process.cwd():', process.cwd());
console.log('__dirname:', __dirname);
```

Bu dosya terminalde `my-app` klasöründe şu komutla çalıştırılırsa:

```bash
node index.js
```

### Çıktı:

```
process.cwd(): /Users/ahmet/Desktop/my-app
__dirname: /Users/ahmet/Desktop/my-app
```

Ama `subfolder/test.js` dosyasını çalıştırırsak:

### `subfolder/test.js`

```js
console.log('process.cwd():', process.cwd());
console.log('__dirname:', __dirname);
```

Ve terminalden şunu yazarsak:

```bash
node subfolder/test.js
```

### Çıktı:

```
process.cwd(): /Users/ahmet/Desktop/my-app
__dirname: /Users/ahmet/Desktop/my-app/subfolder
```

> **Görüldüğü gibi:**
> 
> - `process.cwd()` = terminalin çalıştırıldığı yer
> - `__dirname` = dosyanın bulunduğu klasör

---

## ✅ Ne zaman kullanılır?

- Dosya yollarını dinamik oluşturmak için:

```js
const path = require('path');
const filePath = path.join(process.cwd(), 'data', 'users.json');
```

- Çalışma dizinine göre yapılandırma dosyası veya log dosyası ayarlamak için.

---

İstersen bir `fs` (file system) örneğiyle göstererek `process.cwd()` kullanarak dosya okuma işlemi de yapabiliriz. İlgini çeker mi?