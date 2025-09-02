
`npm` (**Node Package Manager**), Node.js projelerinde kullanılan **paket yönetim sistemidir**.

- Paket (kütüphane) indirir, kaldırır, günceller.
- Bağımlılıkları yönetir.
- `package.json` dosyasını oluşturur ve günceller.

---

## 🔧 Temel `npm` Komutları

### 1. `npm init` → Projeyi Başlatır

```bash
npm init
```

- Sana birçok soru sorar ve `package.json` dosyası oluşturur.

### Hızlı versiyonu:

```bash
npm init -y
```

- Tüm sorulara otomatik `default` cevap verir.

---

### 2. `npm install` veya `npm i` → Paket Yükler

#### 📌 Yerel Paket (projeye özel)

```bash
npm install lodash
```

➡️ `node_modules/` klasörüne yüklenir  
➡️ `package.json` → `dependencies` bölümüne eklenir

#### 🌍 Global Paket (tüm sistemde geçerli)

```bash
npm install -g typescript
```

➡️ Tüm terminalde `tsc` gibi komutları doğrudan çalıştırırsın.

---

### 3. `npm uninstall` → Paket Sil

```bash
npm uninstall lodash
```

---

### 4. `npm install` (tek başına) → Bağımlılıkları Yeniden Kurar

```bash
npm install
```

> `package.json` ve `package-lock.json` dosyalarına bakarak tüm paketleri indirir.

---

### 5. `npm update` → Paketleri Günceller

```bash
npm update
```

---

## ⚙️ Ekstra Seçenekler

|Komut|Anlamı|
|---|---|
|`--save-dev`|Sadece geliştirme ortamı için yükle (örneğin: test araçları)|
|`--save`|(Varsayılan olarak yapılır, artık gerek yok)|

```bash
npm install typescript --save-dev
```

---

## 📁 `package.json` ve `node_modules`

|Dosya/Klasör|Ne işe yarar?|
|---|---|
|`package.json`|Projenin tüm bağımlılıklarını, sürümlerini ve metadata’sını tutar|
|`package-lock.json`|Yüklenen paketlerin kesin sürümlerini kilitler|
|`node_modules`|Tüm yüklenmiş paketler burada tutulur|

---

## 🔍 Faydalı Komutlar

|Komut|Açıklama|
|---|---|
|`npm list`|Yüklü paketleri gösterir|
|`npm list -g`|Global yüklü paketleri gösterir|
|`npm outdated`|Güncel olmayan paketleri gösterir|
|`npm cache clean --force`|Npm önbelleğini temizler|
|`npm run <script>`|`package.json` içindeki script’i çalıştırır|

---

## 🧪 Örnek Script Kullanımı

`package.json` içine şunu yaz:

```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

Sonra terminalde çalıştır:

```bash
npm run start
npm run dev
```

---

## 🎯 Özet

|Komut|İşlevi|
|---|---|
|`npm init -y`|Proje başlatır|
|`npm install <paket>`|Paket yükler|
|`npm install -g <paket>`|Global yükler|
|`npm uninstall <paket>`|Paketi siler|
|`npm run <script>`|Script çalıştırır|
