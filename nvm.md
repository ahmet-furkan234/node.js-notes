
- Farklı projelerde farklı Node.js sürümleri kullanmanı sağlar.
- Belirli bir Node sürümünü global değil, proje bazlı olarak kullanmana yardımcı olur.
- Node.js sürümünü kolayca yükseltip düşürebilirsin.
- Windows ya da Unix/Linux sistemlerinde kullanabilirsin (Windows için ayrı bir sürüm var: `nvm-windows`).

---

## 🧠 Neden NVM Kullanmalıyım?

Diyelim ki bir projen Node 14 ile çalışıyor, diğeri ise Node 18 gerektiriyor. Bilgisayarında sadece bir Node sürümü varsa sürekli kur/kaldır yapmak zorunda kalırsın.  
**NVM ile:**

```bash
nvm install 14
nvm install 18
nvm use 14   # aktif sürüm 14 olur
nvm use 18   # aktif sürüm 18 olur
```

---

## 🔍 Temel NVM Komutları

|Komut|Açıklama|
|---|---|
|`nvm install <versiyon>`|İlgili Node.js sürümünü indirir ve kurar|
|`nvm use <versiyon>`|Belirli bir Node sürümüne geçiş yapar|
|`nvm ls` veya `list`|Kurulu Node sürümlerini listeler|
|`nvm uninstall <versiyon>`|Belirli sürümü kaldırır|
|`nvm current`|Şu an kullanılan Node sürümünü gösterir|
|`nvm alias default <v>`|Varsayılan kullanılacak Node sürümünü ayarlar|

---

## 💻 Kurulum

### Windows:

1. `nvm-windows` sürümünü kurmalısın:  [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)
2. İndirdikten sonra kurulum sırasında Node.js kuruluysa onu kaldırman gerekebilir
3. Ardından terminalden aşağıdaki gibi çalıştırabilirsin:

```bash
nvm install 20
nvm use 20
```

### Linux / macOS:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

> Ardından `.bashrc`, `.zshrc` veya `.profile` dosyana eklenir ve aktif hale gelir.

---

## 🧪 Örnek Kullanım

```bash
nvm install 16
nvm install 18
nvm use 16
node -v     # v16.x.x
nvm use 18
node -v     # v18.x.x
```
