
`events` modülü ile kendi olay (event) sistemini yazabilir ve olaylara dinleyiciler (listener) ekleyip tetikleyebilirsin.  
Node.js’in içindeki `http`, `fs`, `stream` gibi modüller hep bu event sistemiyle çalışır.

---

## 📌 **Nasıl kullanılır?**

1️⃣ `events` modülünü çağır.  
2️⃣ `EventEmitter` sınıfından bir örnek oluştur.  
3️⃣ `.on()` ile olay dinleyicisi ekle.  
4️⃣ `.emit()` ile olayı tetikle.

---

## 💻 **Temel örnek**

```js
const EventEmitter = require('events');

// EventEmitter örneği
const myEmitter = new EventEmitter();

// Dinleyici ekle
myEmitter.on('selamla', (isim) => {
    console.log(`Merhaba ${isim}!`);
});

// Olayı tetikle
myEmitter.emit('selamla', 'TkMatE');
```

> 🔑 Çıktı: `Merhaba TkMatE!`

---

# ⚡ **EventEmitter Methodları ve Kullanımı**

| Method / Özellik                   | Açıklama                                       |
| ---------------------------------- | ---------------------------------------------- |
| `.on(event, listener)`             | Olay dinleyicisi ekler (birden fazla olabilir) |
| `.emit(event, [...args])`          | Olayı tetikler, dinleyicileri çalıştırır       |
| `.once(event, listener)`           | Sadece bir kere çalışacak dinleyici ekler      |
| `.removeListener(event, listener)` | Belirli bir dinleyiciyi kaldırır               |
| `.removeAllListeners(event)`       | Olayın tüm dinleyicilerini kaldırır            |
| `.listenerCount(event)`            | Olay için kaç dinleyici olduğunu döner         |
| `.listeners(event)`                | Dinleyicileri dizi olarak döner                |

---

## 📌 **once() örneği**

```js
myEmitter.once('tekSefer', () => {
    console.log('Bu sadece bir kez çalışır');
});

myEmitter.emit('tekSefer');
myEmitter.emit('tekSefer'); // Artık çalışmaz
```

---

## 📌 **Dinleyici silmek**

```js
function merhaba() {
    console.log('Merhaba Dünya');
}

myEmitter.on('selam', merhaba);

myEmitter.emit('selam'); // Merhaba Dünya
myEmitter.removeListener('selam', merhaba);
myEmitter.emit('selam'); // Artık bir şey yazmaz
```

---

## 📌 **Dinleyici sayısı ve listesi**

```js
console.log(myEmitter.listenerCount('selamla')); 
// Olay için kaç dinleyici var

console.log(myEmitter.listeners('selamla'));
// Dinleyici fonksiyonlarını listeler
```

---

# 🚀 **Biraz daha gerçekçi örnek**

Bir sipariş sistemi gibi düşün:

```js
const EventEmitter = require('events');
const siparisEmitter = new EventEmitter();

siparisEmitter.on('siparis-verildi', (siparisNo) => {
    console.log(`Sipariş alındı. Sipariş No: ${siparisNo}`);
});

siparisEmitter.on('siparis-verildi', (siparisNo) => {
    console.log(`Sipariş ${siparisNo} hazırlanıyor...`);
});

siparisEmitter.emit('siparis-verildi', 101);
```

> Çıktı:

```text
Sipariş alındı. Sipariş No: 101  
Sipariş 101 hazırlanıyor...
```

---

# 💡 **Kullanım alanları**

✅ **http sunucularında istek geldi olayları**  
✅ **socket uygulamaları (ör. chat)**  
✅ **akış (stream) sistemlerinde**  
✅ **kendi modüllerinde özelleştirilmiş eventler**

---

## 🎁 **Bonus — Kendi sınıfında EventEmitter**

```js
const EventEmitter = require('events');

class Siparis extends EventEmitter {
    ver(siparisNo) {
        console.log(`Sipariş verildi: ${siparisNo}`);
        this.emit('hazirla', siparisNo);
    }
}

const siparis = new Siparis();

siparis.on('hazirla', (siparisNo) => {
    console.log(`Sipariş hazırlanıyor: ${siparisNo}`);
});

siparis.ver(5001);
```

---

# ⚠ **Notlar**

✅ Dinleyici sayısı sınırını değiştirme:

```js
myEmitter.setMaxListeners(20);
```

(Default 10’dur, çok dinleyici ekleyince uyarı alırsın.)