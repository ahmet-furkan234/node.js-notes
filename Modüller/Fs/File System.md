
👉 `fs` (file system) modülü Node.js’in yerleşik (built-in) modülüdür.  
👉 Dosya ve klasörlerle çalışmak için kullanılır:  
✔ Dosya okuma  
✔ Dosya yazma  
✔ Dosya silme  
✔ Klasör oluşturma/silme  
✔ Dosya bilgilerini alma

`fs` modülünü kullanmak için:

```js
const fs = require('fs');
```

---

## ⚡ **En Sık Kullanılan `fs` Yöntemleri**

### 📝 **Not:**

- `fs` yöntemlerinin çoğu hem **senkron (Sync)** hem **asenkron (Async)** versiyona sahiptir.
- Async versiyonları tercih edilir çünkü non-blocking (engellemez).

---

### 1️⃣ **Dosya Okuma**

#### Asenkron:

```js
fs.readFile('ornek.txt', 'utf-8', (err, data) => {
    if (err) {
        console.error('Okuma hatası:', err);
        return;
    }
    console.log('Dosya içeriği:', data);
});
```

#### Senkron:

```js
const data = fs.readFileSync('ornek.txt', 'utf-8');
console.log('Dosya içeriği:', data);
```

---

### 2️⃣ **Dosya Yazma**

#### Asenkron:

```js
fs.writeFile('ornek.txt', 'Merhaba Node.js!', (err) => {
    if (err) {
        console.error('Yazma hatası:', err);
        return;
    }
    console.log('Dosya başarıyla yazıldı.');
});
```

#### Senkron:

```js
fs.writeFileSync('ornek.txt', 'Merhaba Node.js!');
console.log('Dosya başarıyla yazıldı.');
```

---

### 3️⃣ **Dosya Eklemek (append)**

```js
fs.appendFile('ornek.txt', '\nYeni satır', (err) => {
    if (err) throw err;
    console.log('Veri eklendi.');
});
```

---

### 4️⃣ **Dosya Silmek**

```js
fs.unlink('ornek.txt', (err) => {
    if (err) throw err;
    console.log('Dosya silindi.');
});
```

---

### 5️⃣ **Klasör Oluşturmak**

```js
fs.mkdir('yeniklasor', (err) => {
    if (err) throw err;
    console.log('Klasör oluşturuldu.');
});
```

---

### 6️⃣ **Klasör Silmek**

```js
fs.rmdir('yeniklasor', (err) => {
    if (err) throw err;
    console.log('Klasör silindi.');
});
```

> ⚠️ `rmdir` sadece boş klasörler için çalışır.

---

### 7️⃣ **Dosya Varlığını Kontrol Etmek**

```js
	fs.access('ornek.txt', fs.constants.F_OK, (err) => {
    if (err) {
        console.log('Dosya yok');
    } else {
        console.log('Dosya mevcut');
    }
});
```

## 📘 `fs.constants` Sabitleri (Erişim İçin Kullanılanlar)

|Sabit|Anlamı|Açıklama|
|---|---|---|
|`fs.constants.F_OK`|File OK|Dosyanın var olup olmadığını kontrol eder.|
|`fs.constants.R_OK`|Read OK|Dosyanın okunabilir olup olmadığını kontrol eder.|
|`fs.constants.W_OK`|Write OK|Dosyanın yazılabilir olup olmadığını kontrol eder.|
|`fs.constants.X_OK`|Execute OK|Dosyanın çalıştırılabilir olup olmadığını kontrol eder. (Sadece Unix/Linux)|
### 🎯 Örnekler

#### 🔹 Sadece dosyanın var olup olmadığını kontrol et

```js
fs.access('deneme.txt', fs.constants.F_OK, (err) => {
    console.log(err ? 'Dosya yok' : 'Dosya mevcut');
});
```

#### 🔹 Dosya okunabilir mi?

```js
fs.access('deneme.txt', fs.constants.R_OK, (err) => {
    console.log(err ? 'Okuma izni yok' : 'Okunabilir');
});
```

#### 🔹 Dosya yazılabilir mi?

```js
fs.access('deneme.txt', fs.constants.W_OK, (err) => {
    console.log(err ? 'Yazma izni yok' : 'Yazılabilir');
});
```

#### 🔹 Hem okunabilir hem yazılabilir mi?

```js
fs.access('deneme.txt', fs.constants.R_OK | fs.constants.W_OK, (err) => {
    console.log(err ? 'Okuma veya yazma izni yok' : 'Hem okunabilir hem yazılabilir');
});
```

---

### 8️⃣ **Dosya İstatistiklerini Almak**

```js
fs.stat('ornek.txt', (err, stats) => {
    if (err) throw err;
    console.log(stats);
    console.log('Boyut:', stats.size, 'byte');
    console.log('Oluşturulma:', stats.birthtime);
});
```

---

## 💡 **Neden Asenkron Kullanılır?**

👉 Asenkron yöntemler Node.js’in non-blocking doğasına uygundur.  
👉 Büyük dosyalarla çalışırken diğer işlemler beklemez.

---

## 🎁 **Küçük Proje Örneği: Dosya Yaz, Oku ve Sil**

```js
const fs = require('fs');
const path = require('path');

const dosyaYolu = path.join(__dirname, 'deneme.txt');

// Yaz
fs.writeFile(dosyaYolu, 'İlk satır', (err) => {
    if (err) throw err;
    console.log('Dosya yazıldı.');

    // Oku
    fs.readFile(dosyaYolu, 'utf-8', (err, data) => {
        if (err) throw err;
        console.log('Okunan veri:', data);

        // Sil
        fs.unlink(dosyaYolu, (err) => {
            if (err) throw err;
            console.log('Dosya silindi.');
        });
    });
});
```

---

## 📝 **Özet**

| Yöntem                      | Görevi                    |
| --------------------------- | ------------------------- |
| `readFile / readFileSync`   | Dosya okur                |
| `writeFile / writeFileSync` | Dosya yazar               |
| `appendFile`                | Dosyaya veri ekler        |
| `unlink`                    | Dosya siler               |
| `mkdir` / `rmdir`           | Klasör oluşturur / siler  |
| `stat`                      | Dosya bilgisi getirir     |
| `access`                    | Dosya var mı kontrol eder |
