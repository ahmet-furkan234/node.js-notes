
👉 `url` modülü, URL’leri **parçalamak**, **birleştirmek**, **çözümlemek** ve **biçimlendirmek** için kullanılan **yerleşik (built-in)** bir Node.js modülüdür.  
👉 Web sunucusu yaparken URL’den bilgi almak için çok kullanılır.

---

## 📌 **`url` Modülünü Kullanmak**

```js
const url = require('url');
```

---

## ⚡ **En Sık Kullanılan Yöntemler ve Özellikler**

---

### 1️⃣ `url.parse(urlStr[, parseQueryString, slashesDenoteHost])`

👉 URL string'ini parçalar ve bir obje döner.

#### Örnek:

```js
const url = require('url');

const adres = 'http://example.com:8080/yol/alt?name=Ahmet&yas=25#bolum1';

const cozulmusUrl = url.parse(adres, true);
console.log(cozulmusUrl);
```

✅ Çıktı:

```js
Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'example.com:8080',
  port: '8080',
  hostname: 'example.com',
  hash: '#bolum1',
  search: '?name=Ahmet&yas=25',
  query: { name: 'Ahmet', yas: '25' },
  pathname: '/yol/alt',
  path: '/yol/alt?name=Ahmet&yas=25',
  href: 'http://example.com:8080/yol/alt?name=Ahmet&yas=25#bolum1'
}
```

> **true parametresi:** `query`'yi obje olarak döner, aksi halde sadece string olur.

---

### 2️⃣ `url.format(urlObj)`

👉 Parçalanmış bir URL objesini tekrar string’e çevirir.

#### Örnek:

```js
const urlObj = {
  protocol: 'http:',
  hostname: 'example.com',
  pathname: '/ornek',
  query: { ad: 'Ali', yas: '30' }
};

const urlStr = url.format(urlObj);
console.log(urlStr);
```

✅ Çıktı:

```http
http://example.com/ornek?ad=Ali&yas=30
```

---

### 3️⃣ `url.resolve(from, to)`

👉 İki URL parçasını birleştirir.

#### Örnek:

```js
console.log(url.resolve('http://example.com/dir/', 'alt')); 
// http://example.com/dir/alt
console.log(url.resolve('http://example.com/dir/', '/alt')); 
// http://example.com/alt
```

---

## ⚠️ **Dikkat**

- `url.parse`, `url.format`, `url.resolve` eski (legacy) API’dendir. Yine çalışır ama **yeni projelerde `URL` sınıfı** kullanılır.
- URL sınıfı daha modern ve ES6 uyumludur.

---

## 🚀 **Modern `URL` sınıfı**

Node.js 7.0+ ile geldi ve önerilir.

#### Örnek:

```js
const myURL = new URL('http://example.com:8080/yol/alt?name=Ahmet&yas=25#bolum1');

console.log(myURL.hostname);   // example.com
console.log(myURL.port);       // 8080
console.log(myURL.pathname);   // /yol/alt
console.log(myURL.searchParams.get('name')); // Ahmet
```

---

## 📝 **Kısa Özet**

|Yöntem|Açıklama|
|---|---|
|`url.parse`|URL’i parçalara ayırır (legacy)|
|`url.format`|URL objesini string’e çevirir|
|`url.resolve`|URL parçalarını birleştirir|
|`URL` sınıfı|Modern, güçlü URL işleme aracı|

---

## 🎁 **Sonuç**

✅ `url` modülü, URL çözümleme ve oluşturma işini kolaylaştırır.  
✅ Yeni projelerde `URL` sınıfını kullanmak en doğrusudur.  
✅ Sunucu yaparken route çözümlemede, query string okumada sık kullanılır.