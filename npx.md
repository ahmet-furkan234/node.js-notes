
> **Sistemde yüklü olmayan bir npm paketini**:

1. **Geçici olarak indirir**
2. **Çalıştırır**
3. **İş bitince siler (genellikle)**

Yani senin sistemine yükleme zahmeti olmadan doğrudan komutu çalıştırır.

---

## 🔍 Örnekle Açalım

Diyelim ki sisteminde `typescript` yüklü değil ama `tsconfig.json` oluşturmak istiyorsun:

### Bu çalışmaz:

```bash
tsc --init
# ❌ tsc: komutu bulunamadı
```

### Bu çalışır:

```bash
npx tsc --init
# ✅ npx typescript paketini indirir, tsc komutunu çalıştırır
```

---

## 🔁 `npx` Ne Zaman Kullanılır?

|Durum|`npx` Kullanımı|
|---|---|
|CLI aracıyla bir proje başlatmak|`npx create-react-app my-app`|
|Geçici araç denemek|`npx cowsay "TkMatE yazdı"`|
|Kodları test etmek, derlemek|`npx tsc`, `npx eslint`, `npx jest`|
|Global paket yüklemek istemiyorsan|`npx` ile çözüm ✅|

---

## 📂 Nerede Yükler?

- `npx`, paketi genellikle `~/.npm/_npx` gibi bir geçici klasöre indirir.
- Bu yüzden sistemde kalıcı yer kaplamaz.

---

## 🧠 Unutma!

> Eğer `npx` ile kullandığın paket **zaten local olarak yüklüyse**, onu kullanır.  
> Ama hiç yoksa `npm registry` üzerinden indirir ve çalıştırır.
