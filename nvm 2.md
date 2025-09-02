
|Komut|Açıklama|
|---|---|
|`nvm install <sürüm>`|Belirtilen Node.js sürümünü indirip kurar. Örn: `nvm install 18`|
|`nvm use <sürüm>`|Belirtilen sürümü aktif hale getirir. Örn: `nvm use 18`|
|`nvm list` veya `nvm ls`|Tüm kurulu Node sürümlerini listeler|
|`nvm current`|Şu an aktif olan Node sürümünü gösterir|
|`nvm uninstall <sürüm>`|Belirtilen Node.js sürümünü kaldırır|
|`node -v`|Aktif Node sürümünü terminalde gösterir|
|`npm -v`|Aktif npm sürümünü gösterir|

---

## ⚙️ İLERİ SEVİYE NVM KOMUTLARI

|Komut|Açıklama|
|---|---|
|`nvm install <sürüm> <arch>`|Belirli mimaride (32/64 bit) sürüm kurar. Örn: `nvm install 18 64`|
|`nvm use <sürüm> <arch>`|Mimariye göre sürüm etkinleştirir|
|`nvm root`|NVM dizinini gösterir (örn: `C:\nvm`)|
|`nvm version`|NVM'nin kendi sürümünü gösterir|
|`nvm proxy <url>`|Proxy ayarlar (nadiren kullanılır)|
|`nvm node_mirror <url>`|Node indirilecek adresi değiştirir (gelişmiş)|
|`nvm npm_mirror <url>`|NPM indirilecek adresi değiştirir|

---

## 🔄 VARSAYILAN NODE SÜRÜMÜ AYARLAMA

```bash
nvm alias default 18
```

Bilgisayar açıldığında veya terminal her açıldığında **otomatik olarak Node 18** kullanılır.

---

## 🧪 Örnek Kullanım Akışı:

```bash
nvm install 14
nvm install 18
nvm list

nvm use 14
node -v     # v14...

nvm use 18
node -v     # v18...

nvm uninstall 14
```

---

## 🔍 Bonus: Mevcut Node ve NPM Nereden Geliyor?

```bash
where node
where npm
```

> Windows’ta bu komutlar Node ve npm’nin nerede yüklü olduğunu gösterir.  
> `C:\nvm\v18.x.x\` gibi görünmeli. Aksi halde eski kurulum kalmış olabilir.

---

İstersen sana özel olarak tüm bu komutları açıklayan bir `.md` (markdown) belge bile hazırlayabilirim.  
Devam edelim mi TkMatE?