
# 📚 `fs-extra` Tüm Metotlar Listesi (Alfabetik + Gruplu)

## 🔁 Genel Bilgi

Tüm metotlar hem **callback** destekler, hem de **Promise** tabanlı çalışır (yani `async/await` uyumludur).

---

## 🔧 1. Gelişmiş (fs-extra’ya özel) Metotlar

|Metot|Açıklama|
|---|---|
|`copy(src, dest)`|Dosya veya klasörü kopyalar.|
|`copySync(src, dest)`|Aynı işlem sync (bloklayıcı) olarak.|
|`move(src, dest)`|Dosya veya klasörü taşır.|
|`moveSync(src, dest)`|Sync versiyonu.|
|`remove(path)`|Dosya ya da klasörü siler.|
|`removeSync(path)`|Sync versiyonu.|
|`ensureFile(path)`|Dosya yoksa oluşturur, varsa bir şey yapmaz.|
|`ensureFileSync(path)`|Sync versiyonu.|
|`ensureDir(path)`|Klasör yoksa oluşturur.|
|`ensureDirSync(path)`|Sync versiyonu.|
|`ensureLink(src, dest)`|Hard link oluşturur (varsa bir şey yapmaz).|
|`ensureLinkSync(src, dest)`|Sync versiyonu.|
|`ensureSymlink(src, dest)`|Sembolik link oluşturur.|
|`ensureSymlinkSync(...)`|Sync versiyonu.|
|`emptyDir(dir)`|Klasörü boşaltır ama silmez.|
|`emptyDirSync(dir)`|Sync versiyonu.|
|`pathExists(path)`|Dosya/klasör var mı kontrol eder.|
|`pathExistsSync(path)`|Sync versiyonu.|
|`readJson(path)`|JSON dosyasını okur (otomatik `JSON.parse`).|
|`readJsonSync(path)`|Sync versiyonu.|
|`writeJson(path, obj)`|Nesneyi JSON dosyasına yazar.|
|`writeJsonSync(...)`|Sync versiyonu.|
|`outputFile(file, data)`|Dosyayı ve gerekli klasörleri oluşturup veri yazar.|
|`outputFileSync(...)`|Sync versiyonu.|
|`outputJson(file, obj)`|`writeJson` + `ensureFile` birleşimi.|
|`outputJsonSync(...)`|Sync versiyonu.|
|`outputFileSync(path, data)`|Dosya ve klasörleri otomatik oluşturup yazar.|
|`outputJsonSync(path, obj)`|JSON objesini otomatik yazar.|

---

## 📁 2. Dosya/klasör işlemleri (fs'den miras)

Bu metotlar `fs.promises` içeriğiyle aynı şekilde çalışır ama `fs-extra` ile otomatik promise desteklidir:

|Metot|Açıklama|
|---|---|
|`access(path)`|Dosya izin kontrolü.|
|`appendFile(path, data)`|Dosyaya veri ekler.|
|`chmod(path, mode)`|İzinleri değiştirir.|
|`chown(path, uid, gid)`|Sahipliğini değiştirir.|
|`close(fd)`|Dosya tanıtıcısını kapatır.|
|`copyFile(src, dest)`|Basit dosya kopyalama.|
|`createReadStream(path)`|Okuma akışı oluşturur.|
|`createWriteStream(path)`|Yazma akışı oluşturur.|
|`lchmod(path, mode)`|Linke chmod (Unix).|
|`lchown(path, uid, gid)`|Linke chown.|
|`link(src, dest)`|Hard link oluşturur.|
|`lstat(path)`|Symbolic link dahil detaylı bilgi verir.|
|`mkdir(path)`|Klasör oluşturur.|
|`mkdtemp(prefix)`|Geçici klasör oluşturur.|
|`open(path, flags)`|Dosya açar.|
|`read(fd, buffer, ...)`|Dosya tanıtıcısından veri okur.|
|`readFile(path)`|Dosyayı tümüyle okur.|
|`readdir(path)`|Klasör içeriğini listeler.|
|`readlink(path)`|Symbolic link hedefini verir.|
|`realpath(path)`|Gerçek yolu verir (linkleri çözer).|
|`rename(oldPath, newPath)`|Yeniden adlandırır/taşır.|
|`rmdir(path)`|Klasör siler (boş olmalı).|
|`stat(path)`|Dosya bilgisi verir.|
|`symlink(target, path)`|Symbolic link oluşturur.|
|`truncate(path, len)`|Dosyayı belirtilen uzunluğa kısaltır.|
|`unlink(path)`|Dosya siler.|
|`utimes(path, atime, mtime)`|Erişim ve modifiye zamanını değiştirir.|
|`write(fd, buffer, ...)`|Dosya tanıtıcısına veri yazar.|
|`writeFile(path, data)`|Dosyaya veri yazar (varsa üstüne).|

> ✅ Not: Bu metotların `.Sync` versiyonları da mevcuttur (örn: `writeFileSync`, `statSync`).

---

## ✅ Kısayol Özet Tablosu

|Kullanım Amacı|Fonksiyon|
|---|---|
|Dosya varsa oluşturma|`ensureFile()`|
|Klasör varsa oluşturma|`ensureDir()`|
|JSON okuma/yazma|`readJson()`, `writeJson()`|
|Dosya kopyalama/taşıma|`copy()`, `move()`|
|Dosya/klasör silme|`remove()`, `emptyDir()`|
|Dosya/klasör var mı|`pathExists()`|
|Kapsamlı yazma|`outputFile()`, `outputJson()`|
