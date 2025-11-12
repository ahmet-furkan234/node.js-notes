
> **Tanım:**  
> `npm ci`, _clean install_ (temiz kurulum) anlamına gelir.  
> Mevcut `node_modules` klasörünü tamamen siler ve **`package-lock.json`** dosyasına _birebir sadık kalarak_ bağımlılıkları yeniden kurar.  
> Bu sayede kurulumlar **hızlı**, **tutarlı** ve **tekrarlanabilir (deterministik)** olur.

---

#### 💡 Kullanımı:

```bash
npm ci
```

Bu komut:  
1️⃣ Var olan `node_modules` klasörünü **tamamen siler**,  
2️⃣ `package-lock.json` dosyasına göre **birebir aynı sürümleri** kurar.

---

#### 🧱 Ne işe yarar:

|Amaç|Açıklama|
|---|---|
|⚡ **Hızlı kurulum**|`npm install`’dan daha hızlıdır çünkü dependency çözümlemesi yapmaz.|
|🧩 **Deterministik build**|`package-lock.json`’daki versiyonları birebir kurar.|
|🧹 **Temiz ortam sağlar**|Her çalıştırmada node_modules sıfırdan oluşturulur.|
|🧱 **CI/CD uyumludur**|Build pipeline’larda “aynı bağımlılıklar” garantisi verir.|

---

#### 🧰 Kullanım Senaryoları

|Senaryo|Açıklama|
|---|---|
|🐳 **Docker build’lerde**|`npm ci` → cache-friendly + hızlı + güvenli|
|🔧 **CI/CD (GitHub Actions, Jenkins)**|Kodun her build’de aynı şekilde kurulmasını sağlar|
|🚀 **Prod deployment öncesi**|Gereksiz bağımlılık farklılıklarını önler|

---

#### ⚙️ Docker Örneği:

```dockerfile
FROM node:20-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build
```

> ✅ `npm ci` her build’de aynı bağımlılık versiyonlarını kurar → reproducible builds.  
> `npm install` yerine `npm ci` kullanmak, Docker cache mekanizmasıyla da uyumludur.

---

#### ⚡ Fark: `npm ci` vs `npm install`

|Özellik|`npm install`|`npm ci`|
|---|---|---|
|`node_modules` siler mi?|❌ Hayır|✅ Evet|
|Hız|Orta|⚡ Daha hızlı|
|package-lock’a göre mi yükler?|🔸 Evet ama toleranslı|✅ Evet, _birebir aynısını_|
|CI/CD için önerilir mi?|❌ Hayır|✅ Evet|
|package.json değişirse davranış|Yeniden çözümleme yapar|❌ Hata verir|
|Kullanım amacı|Geliştirme ortamı|Otomatik build ve production|

---

#### 🧩 Paket dosyalarıyla ilişkisi

- **`package.json`** → hangi bağımlılıklar (ve türü: `dependencies`, `devDependencies`)
    
- **`package-lock.json`** → her bağımlılığın tam sürümü (npm ci buna sadık kalır)
    

> 🔒 `npm ci`, lock dosyası yoksa hata verir.  
> Bu sayede build’ler “lock dosyasız” çalışamaz (bu bir güvenlik ve tutarlılık garantisidir).

---

#### 🧠 Avantajları

✅ Deterministik kurulum (her ortamda birebir aynı)  
✅ Daha hızlı (çözümleme yok, direkt lock dosyasına göre kurulum)  
✅ CI/CD sistemlerinde cache dostu  
✅ Build hatalarını minimize eder

---

#### ⚠️ Dikkat Edilmesi Gerekenler

- `package-lock.json` **olmazsa** `npm ci` hata verir.
    
- `package.json` değişip lock dosyası güncellenmezse yine hata verir.
    
- Lokal geliştirme sırasında her seferinde `npm ci` kullanmak gerekmez (sadece clean build durumlarında).
    

---

#### 🧾 Örnek: Build Pipeline Script

```bash
rm -rf node_modules
npm ci
npm run build
npm prune --omit=dev
```

> 1️⃣ Eski node_modules silinir  
> 2️⃣ Lock dosyasına göre yeniden kurulum yapılır  
> 3️⃣ Build edilir  
> 4️⃣ Dev bağımlılıkları temizlenir

---

#### 💬 Kısaca:

> **`npm ci` = deterministik, hızlı ve güvenli kurulum yöntemi.**  
> Özellikle **Docker**, **CI/CD**, ve **production** ortamlarında önerilir.

---

İstersen sıradaki komut olarak **`npm dedupe`** (bağımlılık tekilleştirme) veya **`npm audit`** (güvenlik taraması) ile devam edebilirim.  
Hangisiyle ilerleyelim?