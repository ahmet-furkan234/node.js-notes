
## 1. **Process Çıkışı Nedir?**

Node.js uygulaması çalışmayı tamamlayıp sonlandığında işletim sistemine bir çıkış kodu (exit code) gönderir.  
Bu kod, programın başarıyla mı yoksa hata ile mi bittiğini belirtir.

---

## 2. **Exit Code Nedir?**

- `0`: Başarılı çıkış (No error)
- `0` dışındaki sayılar: Hata veya özel durum kodları
- Örneğin:
    - `1`: Genel hata
    - `130`: Ctrl+C ile sonlandırma
    - `143`: SIGTERM sinyaliyle sonlandırma

---

## 3. **Programı Manuel Sonlandırma**

- `process.exit(code)` ile programı istediğin exit kodu ile sonlandırabilirsin.

```js
console.log("Program bitiyor...");
process.exit(0); // Başarılı çıkış
```

---

## 4. **Exit Event’i**

- `process` objesi `"exit"` eventi yayınlar.
- Bu event, program kapanmadan hemen önce çalışır.

```js
process.on('exit', (code) => {
  console.log(`Process exit kodu: ${code}`);
});
```

---

## 5. **Örnek: Başarılı ve Hata ile Çıkış**

```js
function runApp() {
  try {
    // İşlem
    console.log("İşlem başarılı");
    process.exit(0);
  } catch (err) {
    console.error("Hata oluştu:", err);
    process.exit(1);
  }
}

runApp();
```

---

## 6. **Exit Kodlarının Anlamları (Bazıları)**

|Kod|Anlamı|
|---|---|
|0|Başarılı|
|1|Genel hata|
|2|Yanlış komut satırı kullanımı|
|3|Dosya bulunamadı|
|130|Ctrl+C (SIGINT) ile çıkış|
|143|SIGTERM ile çıkış|

---

## 7. **Notlar**

- `process.exit()` çağrıldığında Node.js event loop'u hemen durdurur.
- Eğer asenkron işlemler devam ediyorsa tamamlanmayabilir.
- Bu yüzden `process.exit()`’i dikkatli kullanmalı, mümkünse önce temizleme (cleanup) yapmalısın.

---

# Özet

|Konu|Açıklama|
|---|---|
|Exit kodu (0)|Başarılı program çıkışı|
|Exit kodu (!= 0)|Hata ya da özel durum|
|`process.exit()`|Programı manuel sonlandırma|
|`exit` event|Program kapanmadan önce tetiklenir|
