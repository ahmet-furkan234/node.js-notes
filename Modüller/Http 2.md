
👉 Sunucu oluşturunca 2 ana obje ile çalışırsın:

- **`req` (IncomingMessage)** → İstekle ilgili bilgiler
- **`res` (ServerResponse)** → Cevabı oluşturmak için kullanırsın

---

## 🔹 **http.createServer(callback)**

Yeni bir HTTP sunucusu oluşturur.

```js
const http = require('http');

const server = http.createServer((req, res) => {
    // İstek ve yanıtı burada işleriz
});

server.listen(3000, () => {
    console.log('Sunucu çalışıyor: http://localhost:3000');
});
```

---

# 💻 **req (IncomingMessage) Özellikleri ve Kullanımı**

### 📌 **req.url**

👉 İsteğin URL yolunu verir.

```js
console.log(req.url); 
// Örnek: /, /hakkinda, /api/data
```

---

### 📌 **req.method**

👉 HTTP metodunu verir (GET, POST, PUT, DELETE gibi)

```js
console.log(req.method); 
// Örnek: GET
```

---

### 📌 **req.headers**

👉 İstek başlıklarını verir (object)

```js
console.log(req.headers); 
// Örnek: { host: 'localhost:3000', connection: 'keep-alive', ... }
```

---

### 📌 **req.on('data', callback)** ve **req.on('end', callback)**

👉 POST gibi gövde içeren isteklerde gelen veriyi parçalar halinde okur.

```js
let body = '';

req.on('data', chunk => {
    body += chunk.toString();  // Buffer'ı stringe çevir
});

req.on('end', () => {
    console.log('Gelen veri:', body);
    res.end('Veri alındı');
});
```

---

# 💻 **res (ServerResponse) Method ve Kullanımı**

### 📌 **res.statusCode**

👉 Yanıtın HTTP durum kodunu belirler.

```js
res.statusCode = 200;  // Başarılı
res.statusCode = 404;  // Bulunamadı
res.statusCode = 500;  // Sunucu hatası
```

---

### 📌 **res.setHeader(name, value)**

👉 Yanıt başlığı ekler.

```js
res.setHeader('Content-Type', 'text/plain'); 
res.setHeader('X-Custom-Header', 'deger');
```


---

### 📌 **res.write(data)**

👉 Yanıt gövdesine veri yazar (end çağrılmadan birden fazla yazabilirsin).

```js
res.write('Merhaba ');
res.write('Dünya!');
```

---

### 📌 **res.end([data])**

👉 Yanıtı sonlandırır ve tarayıcıya gönderir.

```js
res.end('Tamamlandı');
```

`res.write` + `res.end` birlikte kullanılır ya da doğrudan `res.end('Tüm veri')` yazabilirsin.

---

# 💡 **Tüm Methodların Kullanıldığı Örnek**

```js
const http = require('http');

const server = http.createServer((req, res) => {
    console.log('URL:', req.url);
    console.log('Method:', req.method);
    console.log('Headers:', req.headers);

    if (req.method === 'GET' && req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.write('<h1>Ana Sayfa</h1>');
        res.end('<p>Hoş geldin!</p>');
    }
    else if (req.method === 'POST' && req.url === '/veri') {
        let body = '';

        req.on('data', chunk => {
            body += chunk.toString();
        });

        req.on('end', () => {
            console.log('POST verisi:', body);
            res.statusCode = 200;
            res.setHeader('Content-Type', 'application/json');
            res.end(JSON.stringify({ mesaj: 'Veri alındı', veri: body }));
        });
    }
    else {
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Sayfa bulunamadı');
    }
});

server.listen(3000, () => {
    console.log('Sunucu çalışıyor: http://localhost:3000');
});
```

---

# 🚀 **http Modülü Method + Özellik Tablosu**

|Özellik / Method|Açıklama|
|---|---|
|`http.createServer(cb)`|Sunucu oluşturur|
|`server.listen(port, cb)`|Sunucuyu başlatır|
|`req.url`|İstek URL’i|
|`req.method`|HTTP methodu (GET, POST, vs)|
|`req.headers`|İstek başlıkları|
|`req.on('data', cb)`|İstek verisi geldikçe çalışır (POST vb.)|
|`req.on('end', cb)`|Veri bittiğinde çalışır|
|`res.statusCode = ...`|Yanıt kodu ayarla|
|`res.setHeader(name, val)`|Header ayarla|
|`res.write(data)`|Yanıt gövdesine veri yaz|
|`res.end(data)`|Yanıtı bitir|

---

## ⚠ **Notlar**

✅ Sunucu dinlenmeye başladıktan sonra `CTRL + C` ile durdurabilirsin.  
✅ Tarayıcıdan ya da `curl`, Postman gibi araçlarla test edebilirsin.