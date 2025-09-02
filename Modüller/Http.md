
`http` modülü Node.js’in içinde gelen bir modüldür ve **web sunucusu** oluşturmak için kullanılır.  
Yani **bir web tarayıcısından gelen isteklere cevap vermeni sağlar.**

👉 Örneğin tarayıcıda `http://localhost:3000` yazarsın, Node sunucun bu isteği alır ve bir yanıt döner.

---

## 📌 **http modülünü kullanarak basit bir sunucu**

```js
const http = require('http');

const server = http.createServer((req, res) => {
    // İstek (req) ve yanıt (res) objeleri
    console.log(`İstek alındı: ${req.url}`);

    res.statusCode = 200; // HTTP durum kodu
    res.setHeader('Content-Type', 'text/plain'); // Yanıtın tipi
    res.end('Merhaba, bu benim Node.js sunucum!'); // Yanıt ver ve kapat
});

// Sunucuyu dinlemeye başla
server.listen(3000, () => {
    console.log('Sunucu çalışıyor: http://localhost:3000');
});
```

### ⚡ Açıklama:

✅ `http.createServer(callback)` → Sunucu oluşturur, her gelen istekte callback çalışır.  
✅ `req` → Gelen isteği temsil eder (ör. istek URL’si, methodu).  
✅ `res` → Yanıtı temsil eder (ör. ne yazdıracağın, durum kodu).  
✅ `server.listen(port, callback)` → Sunucuyu başlatır.

---

## 📌 **İstek URL'sine göre farklı yanıtlar**

```js
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('<h1>Ana Sayfa</h1>');
    } else if (req.url === '/hakkinda') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('<h1>Hakkında Sayfası</h1>');
    } else {
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/html');
        res.end('<h1>404 - Sayfa Bulunamadı</h1>');
    }
});

server.listen(3000, () => {
    console.log('Sunucu çalışıyor: http://localhost:3000');
});
```

💡 Tarayıcıdan:

- `http://localhost:3000/` → Ana Sayfa
- `http://localhost:3000/hakkinda` → Hakkında Sayfası
- `http://localhost:3000/blabla` → 404

---

## 📌 **http modülünün bazı önemli özellikleri**

|Özellik|Açıklama|
|---|---|
|`req.method`|İstek türünü verir (GET, POST, vb.)|
|`req.url`|İstek URL’ini verir|
|`res.statusCode`|Yanıtın HTTP durum kodunu belirler|
|`res.setHeader(name, value)`|Header bilgisi ekler|
|`res.end(data)`|Yanıtı sonlandırır ve isteği kapatır|

---

## 💡 **Gerçek kullanımda**

Sen genelde `http` modülünü doğrudan değil, onun üstünde çalışan `express`, `koa`, `fastify` gibi frameworklerle kullanırsın. Ama temelini anlamak için `http` modülü çok önemli.