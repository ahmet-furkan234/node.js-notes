
> **Tanım:**  
> `npm prune`, `node_modules` klasöründe bulunan ama `package.json` dosyasında yer almayan bağımlılıkları siler.  
> Ayrıca `--omit=dev` parametresiyle çalıştırıldığında, `devDependencies` içinde tanımlı geliştirme bağımlılıklarını da kaldırır.

---

#### 💡 Kullanımı:

```bash
npm prune
```

Tüm gereksiz bağımlılıkları kaldırır.

```bash
npm prune --omit=dev
```

Sadece **production bağımlılıklarını** bırakır, `devDependencies` kısmındakileri siler.  
(Eski npm sürümlerinde bu, `npm prune --production` olarak geçer.)

---

#### 🧱 Ne işe yarar:

- Build veya deploy aşamasında **gereksiz paketleri temizler**.
- Özellikle Docker imajlarında **boyutu küçültmek** için kullanılır.
- `npm install` sonrasında sadece `prod` bağımlılıklarını koruyarak,  
    final ortama en az dosya ile geçiş sağlar.

---

#### ⚙️ Örnek (Docker ortamında):

```dockerfile
RUN npm install && npm run build && npm prune --omit=dev
```

> Bu sırayla:  
> 1️⃣ Tüm bağımlılıkları yükler  
> 2️⃣ Uygulamayı derler  
> 3️⃣ Geliştirme bağımlılıklarını (TypeScript, eslint, nodemon vs.) siler

---

#### 🧠 Kısaca:

- `npm prune` = gereksiz bağımlılıkları siler
- `npm prune --omit=dev` = **sadece prod bağımlılıklarını bırakır**
- `npm prune --production` = eski eşdeğer
