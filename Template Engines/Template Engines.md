
Template Engine, HTML dosyalarını dinamik hale getiren araçlardır.  
Statik HTML yerine, içine **veri gömülebilen** dosyalar kullanırız.

> HTML dosyasında:

```html
<h1>Merhaba <%= name %>!</h1>
```

> JS tarafında:

```js
res.render("index", { name: "TkMatE" });
```

Tarayıcıya dönen:

```html
<h1>Merhaba TkMatE!</h1>
```

---

## 🧠 Ne İşe Yarar?

- HTML dosyalarına **dinamik veri** eklemek
- Kod tekrarını azaltmak (**partial**, **layout**)
- MVC mimarisine uyum sağlar (özellikle Express.js içinde `res.render` ile)
- Şablonlar oluşturulabilir: başlık, menü, footer vs.

---

## 💡 Yaygın Template Engine’ler

|Adı|Sözdizimi|Özellikler|
|---|---|---|
|**EJS**|`<%= %>`|Basit, JS benzeri sözdizimi, çok kullanılır|
|**Pug**|Girintili|Daha kısa kod, HTML yazımı yok|
|**Handlebars**|`{{ }}`|Daha temiz, mantıksal kontroller güçlü|
|**Mustache**|`{{ }}`|Minimal, mantık içermez, veri odaklı|
|**Nunjucks**|`{% %}`|Django benzeri, kapsamlı|

---

## 🔄 Express ile Kullanımı (EJS Örneği)

### 1. EJS Kurulumu

```bash
npm install ejs
```

### 2. Express'e EJS Ayarı

```js
import express from "express";

const app = express();
app.set("view engine", "ejs");   // .ejs dosyaları render edilsin

app.get("/", (req, res) => {
    res.render("home", { name: "TkMatE" });
});

app.listen(3000);
```

### 3. `views/home.ejs` dosyası

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Merhaba <%= name %>!</h1>
  </body>
</html>
```

---

## ✨ Partial ve Layout Kullanımı (EJS)

### Ortak parça `views/partials/header.ejs`:

```html
<header><h1>Site Başlığı</h1></header>
```

### Ana dosyada çağırmak:

```html
<%- include("partials/header") %>
```

---

## 🔁 EJS Koşullar ve Döngüler

```ejs
<% if (loggedIn) { %>
  <p>Hoşgeldin <%= username %></p>
<% } else { %>
  <p>Lütfen giriş yap.</p>
<% } %>

<ul>
<% todos.forEach(todo => { %>
  <li><%= todo %></li>
<% }) %>
</ul>
```

---

## 📂 Klasör Yapısı Önerisi

```
project/
│
├── views/
│   ├── index.ejs
│   ├── layout.ejs
│   └── partials/
│       ├── header.ejs
│       └── footer.ejs
├── public/
│   └── style.css
├── app.js
```

---

## 🔥 Kıyaslama

|Engine|HTML benzeri|Öğrenme kolaylığı|Logic seviyesi|
|---|---|---|---|
|**EJS**|✅|✅ Kolay|Basit kontrol|
|**Pug**|❌ (yok)|Orta|Yüksek|
|**Handlebars**|✅|Kolay|Orta - güçlü|
|**Nunjucks**|✅|Orta|Güçlü|

---

## 🧪 Kullanım Alanı Örnekleri

- Admin panelleri
    
- Blog sistemleri
    
- Panel temaları
    
- Sunucu tarafı render (SSR)
    
- Express.js projeleri
    

---

Hazırsan bir sonraki adımda farklı template engine’lere örnek yapalım (örneğin: Pug veya Handlebars).  
Hangisini istiyorsan onunla devam edebilirim.  
Ne dersin TkMatE?