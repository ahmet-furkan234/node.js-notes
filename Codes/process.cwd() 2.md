
## 🧠 Neden `__dirname` veya `__filename` Yetmez?

`__dirname` ve `__filename`:

- **bulundukları dosyaya özeldir**.
- Her dosyada kendi mutlak yolunu verir.
- Statiktir ve taşınsa bile dosyanın konumunu verir.

Ama bazı durumlarda, **"kullanıcının uygulamayı başlattığı dizin"** önemlidir. İşte `process.cwd()` burada devreye girer.

---

## 🔧 Ne zaman `process.cwd()` kullanırız?

### 1. ✅ **Global yol ihtiyaçlarında (örn: config, log, veritabanı dosyası)**

```js
// config.json dosyası projenin kök klasöründe
const configPath = path.join(process.cwd(), 'config.json');
```

Eğer bu kodu bir alt klasördeki bir dosyaya koyarsan, `__dirname` seni o alt klasöre götürür. Ama biz her zaman "uygulama başlatıldığında bulunduğumuz yerden" okumak isteriz.

---

### 2. ✅ **Command-line tool geliştirirken (CLI tool)**

Kullanıcılar terminalde CLI aracını farklı klasörlerden çalıştırır. O zaman senin kodunun:

```js
const workingDirectory = process.cwd();
```

demesi gerekir çünkü kullanıcının "şu anda bulunduğu dizin" önemlidir.

---

### 3. ✅ **Monorepo veya büyük projelerde kök dizin kontrolü**

Monorepo yapısında, birden çok alt modül olabilir. Her modülde `__dirname` farklı bir yer döner, ama sen her zaman proje kökünü bilmek istersin:

```js
// Örn: yarn workspace veya nx, turbo gibi sistemlerde
const projectRoot = process.cwd(); // çünkü uygulama oradan başlatılır
```

---

### 4. ✅ **Dinamik dosya yollarında (örn: script.js ile dışarıdan veri almak)**

```bash
node script.js ./input/data.txt
```

```js
const file = path.join(process.cwd(), process.argv[2]); // çalıştırılan klasöre göre yol oluşturulur
```

Burada `__dirname` işe yaramaz çünkü komut satırından verilen yol `cwd`'ye göredir.

---

## 🔍 Özet Karşılaştırma

|Özellik|`__dirname`|`process.cwd()`|
|---|---|---|
|Nereden alınır?|Dosyanın bulunduğu klasör|Terminalde uygulamanın çalıştığı dizin|
|Statik mi?|Evet|Hayır, terminale bağlıdır|
|Alt dizinlerde değişir mi?|Evet|Hayır|
|CLI/Tool yapımında uygun mu?|Hayır|Evet|

---

## 💡 Sonuç

- Eğer bir dosyanın **kendi konumuna göre** yol hesaplıyorsan → `__dirname`
- Eğer kullanıcı veya sistemin **çalıştırdığı klasöre göre** yol hesaplıyorsan → `process.cwd()`
