
**EJS (Embedded JavaScript Templates)**, HTML içinde JavaScript kodlarını gömebildiğiniz bir şablon motorudur. Özellikle Express.js gibi frameworklerle birlikte HTML sayfaları dinamik olarak oluşturmak için sıkça kullanılır.

**Dosya uzantısı**: `.ejs`

---

### 🔹 2. Kurulum

```bash
npm install ejs
```

Express ile birlikte kullanıyorsan:

```js
app.set('view engine', 'ejs');
```

---

### 🔹 3. Basit Kullanım

#### 📁 `app.js`

```js
import express from 'express';

const app = express();

app.set('view engine', 'ejs'); // EJS aktif edilir

app.get('/', (req, res) => {
    res.render('index', { name: "TkMatE" });
});

app.listen(3000, () => {
    console.log("Server started on http://localhost:3000");
});
```

#### 📁 `views/index.ejs`

```html
<!DOCTYPE html>
<html>
<head>
  <title>Hoş Geldin</title>
</head>
<body>
  <h1>Merhaba <%= name %>!</h1>
</body>
</html>
```

---

### 🔹 4. EJS Söz Dizimi

|Söz Dizimi|Açıklama|
|---|---|
|`<%= value %>`|HTML olarak yazdırır|
|`<%- value %>`|HTML'yi escape etmeden yazdırır|
|`<% code %>`|JavaScript çalıştırır (yazdırmaz)|
|`<% if (true) { %> ... <% } %>`|Koşullu ifadeler|
|`<% for (let item of items) { %> ... <% } %>`|Döngü kullanımı|

---

### 🔹 5. Örnek: Liste Döngüsü

```js
res.render('list', { items: ["elma", "armut", "üzüm"] });
```

#### 📁 `views/list.ejs`

```html
<ul>
  <% items.forEach(function(item) { %>
    <li><%= item %></li>
  <% }); %>
</ul>
```
