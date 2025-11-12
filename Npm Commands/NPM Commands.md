
> **NPM**, Node.js projelerinde paket (bağımlılık) yönetimi için kullanılır.  
> Aşağıdaki komutlar, hem geliştirme sürecinde hem de üretim (production) ortamında en çok kullanılan NPM işlemlerini kapsar.

---

## 🧱 1️⃣ Proje Başlatma ve Paket Yönetimi

| Komut                                | Açıklama                                                                | Örnek                                              |
| ------------------------------------ | ----------------------------------------------------------------------- | -------------------------------------------------- |
| **`npm init`**                       | Yeni bir Node.js projesi oluşturur ve `package.json` dosyası oluşturur. | `npm init -y` _(tüm soruları otomatik kabul eder)_ |
| **`npm install <paket>`**            | Belirtilen paketi indirir ve `package.json`’a ekler.                    | `npm install express`                              |
| **`npm install <paket> --save-dev`** | Sadece geliştirme sırasında kullanılacak bağımlılığı ekler.             | `npm install typescript --save-dev`                |
| **`npm uninstall <paket>`**          | Paketi kaldırır.                                                        | `npm uninstall lodash`                             |
| **`npm update`**                     | Tüm bağımlılıkları semver aralığına göre günceller.                     | `npm update`                                       |

---

## ⚙️ 2️⃣ Kurulum ve Derleme

| Komut             | Açıklama                                                           | Ne Yapar                                                |
| ----------------- | ------------------------------------------------------------------ | ------------------------------------------------------- |
| **`npm install`** | `package.json`’daki tüm bağımlılıkları kurar.                      | `node_modules` klasörünü oluşturur.                     |
| **`npm ci`**      | `package-lock.json`’a göre _temiz ve deterministik_ kurulum yapar. | CI/CD ve Docker ortamları için önerilir.                |
| **`npm rebuild`** | Native modülleri (ör. `bcrypt`, `sharp`) yeniden derler.           | Node versiyonu değiştiğinde kullanılır.                 |
| **`npm prune`**   | Gereksiz bağımlılıkları siler.                                     | `npm prune --omit=dev` → prod bağımlılıklarını bırakır. |

---

## 🧹 3️⃣ Temizlik ve Optimizasyon

| Komut                         | Açıklama                                               | Örnek                     |
| ----------------------------- | ------------------------------------------------------ | ------------------------- |
| **`npm dedupe`**              | Yinelenen bağımlılıkları tekilleştirir.                | `npm dedupe`              |
| **`npm cache clean --force`** | NPM önbelleğini tamamen temizler.                      | `npm cache clean --force` |
| **`npm doctor`**              | Ortam yapılandırmasını kontrol eder (diagnostic tool). | `npm doctor`              |
| **`npm audit`**               | Güvenlik açıklarını analiz eder.                       | `npm audit`               |
| **`npm audit fix`**           | Güvenlik açıklarını otomatik olarak düzeltir.          | `npm audit fix`           |

---

## 🧰 4️⃣ Script ve Çalıştırma Komutları

|Komut|Açıklama|Örnek|
|---|---|---|
|**`npm run <script>`**|`package.json`’daki script’i çalıştırır.|`npm run start`|
|**`npm test`**|`scripts.test` alanındaki komutu çalıştırır.|`npm test`|
|**`npm start`**|`scripts.start` komutunu çalıştırır (kısayol).|`npm start`|
|**`npm run build`**|`scripts.build` içeriğini çalıştırır (ör. TS derlemesi).|`npm run build`|

> 💡 Not: `npm run` kullanırken komut ismi `package.json`’daki `"scripts"` kısmında olmalıdır.

---

## 🧩 5️⃣ Bağımlılık İnceleme ve Sürüm Yönetimi

|Komut|Açıklama|Örnek|
|---|---|---|
|**`npm list`**|Kurulu paketlerin listesini gösterir.|`npm list --depth=0`|
|**`npm outdated`**|Güncel olmayan bağımlılıkları listeler.|`npm outdated`|
|**`npm view <paket>`**|Paket hakkında meta bilgi verir (versiyon, lisans, vb.).|`npm view express`|
|**`npm info <paket>`**|Aynı işlev, ancak daha detaylı çıktı üretir.|`npm info mongoose`|
|**`npm version <patch/minor/major>`**|Paket versiyonunu artırır ve `package.json`’ı günceller.|`npm version patch`|

---

## 🔐 6️⃣ Güvenlik, Yetkilendirme ve Hesap Yönetimi

|Komut|Açıklama|Örnek|
|---|---|---|
|**`npm login`**|NPM hesabına giriş yapar.|`npm login`|
|**`npm logout`**|Oturumu kapatır.|`npm logout`|
|**`npm whoami`**|Aktif kullanıcıyı gösterir.|`npm whoami`|
|**`npm token list`**|Kullanıcı erişim tokenlarını listeler.|`npm token list`|

---

## 📦 7️⃣ Paket Yayınlama (Publish & Unpublish)

|Komut|Açıklama|Örnek|
|---|---|---|
|**`npm publish`**|Paketi NPM Registry’ye yükler.|`npm publish --access public`|
|**`npm unpublish`**|Paketi NPM’den kaldırır.|`npm unpublish <paket>@<sürüm>`|
|**`npm pack`**|Paketi `.tgz` arşivine dönüştürür (lokal test için).|`npm pack`|

> ⚠️ **Uyarı:** `npm unpublish` işlemi dikkatli yapılmalıdır; yayınlanan sürümler geri alınamaz.

---

## ⚡ 8️⃣ Faydalı Ek Komutlar

|Komut|Açıklama|Örnek|
|---|---|---|
|**`npm help`**|Yardım menüsünü gösterir.|`npm help install`|
|**`npm config get <key>`**|NPM konfigürasyon ayarlarını gösterir.|`npm config get prefix`|
|**`npm config set <key> <value>`**|Ayar değiştirir (örneğin proxy).|`npm config set proxy http://proxy:8080`|
|**`npm root -g`**|Global paketlerin kurulduğu dizini gösterir.|`npm root -g`|
|**`npm prefix`**|Mevcut proje kök dizinini döndürür.|`npm prefix`|

---

## 🧠 9️⃣ En Çok Kullanılan Kombinasyonlar

|Amaç|Komut|
|---|---|
|Temiz, güvenli kurulum|`npm ci`|
|Gereksiz modülleri sil|`npm prune`|
|Geliştirme bağımlılıklarını kaldır|`npm prune --omit=dev`|
|Güvenlik açığı kontrolü|`npm audit fix`|
|Native modül yeniden derleme|`npm rebuild`|
|Paket versiyon artırma|`npm version patch`|
|Projeyi başlatma|`npm init -y`|
|Hızlı çalıştırma|`npm run start`|

---

## 🧾 🔍 10️⃣ Kısa Özet

| Kategori                   | Komutlar                                  |
| -------------------------- | ----------------------------------------- |
| 📦 **Kurulum & Başlatma**  | `init`, `install`, `uninstall`, `update`  |
| ⚙️ **Build & CI/CD**       | `ci`, `prune`, `rebuild`                  |
| 🧹 **Temizlik & Güvenlik** | `dedupe`, `audit`, `cache clean`          |
| 🧠 **Analiz & Bilgi**      | `list`, `outdated`, `view`, `info`        |
| 🚀 **Çalıştırma**          | `run`, `start`, `test`, `build`           |
| 🔐 **Yayın & Hesap**       | `publish`, `unpublish`, `login`, `whoami` |
