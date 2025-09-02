
. Nunjucks
- **Geliştirici**: Mozilla
- **Mantık gücü**: Çok yüksek
- **Kullanım**: Django benzeri sözdizimi
- **Dosya uzantısı**: `.njk`

### ✅ Özellikler

- `if`, `for`, `include`, `macro`, `block`, `extends`, `filter` gibi tüm yapılar var
- HTML kalıtım (template inheritance)
- Layout ve reusable parçalar
- Express ile rahat entegre olur

### 🔸 Kod Örneği

```njk
{% extends "layout.njk" %}

{% block content %}
  {% for user in users %}
    <p>{{ user.name }}</p>
  {% endfor %}
{% endblock %}
```

---

## 🔶 2. Jade (şimdi: Pug)

- **Yeni adı**: Pug
- **Önceki adı**: Jade
- **Sözdizimi**: Girintiye dayalı, HTML yazılmaz
- **Dosya uzantısı**: `.pug`

### ✅ Özellikler

- Kod sade, kısa
- `if`, `each`, `extends`, `include` gibi yapılar
- Çok hızlı render

### 🔸 Kod Örneği

```pug
ul
  each item in items
    li= item

if user.isAdmin
  p Admin Paneline Hoşgeldiniz
```

---

## 🔶 3. Vash

- **C# Razor'a benzer**
- **Sözdizimi**: ASP.NET Razor tarzı
- **Dosya uzantısı**: `.vash`

### ✅ Özellikler

- Full JavaScript kullanılabilir
- Express.js ile uyumlu
- Daha az yaygın, niche kullanım

### 🔸 Kod Örneği

```vash
@html
<ul>
  @model.forEach(function(item) {
    <li>@item.name</li>
  });
</ul>
```

---

## 🔶 4. EJS (Embedded JavaScript)

- **En yaygınlardan biri**
- **Kullanımı çok kolay**
- **Dosya uzantısı**: `.ejs`

### ✅ Özellikler

- Saf JS ile tam kontrol
- `if`, `for`, include, partials
- Express ile çok uyumlu
- HTML içine JS gömülür

### 🔸 Kod Örneği

```ejs
<% if (user) { %>
  <p>Merhaba, <%= user.name %></p>
<% } %>
```

---

## 🔶 5. Handlebars

- **Mantıklı yapısı ve kolay sözdizimi ile çok kullanılır**
- **Logic seviyesi orta düzey**
- **Dosya uzantısı**: `.hbs`

### ✅ Özellikler

- `if`, `each`, `with`
- Kendi helper fonksiyonları yazılabilir
- Layout desteği: Ek modül ile

### 🔸 Kod Örneği

```hbs
{{#if isLoggedIn}}
  <p>Merhaba {{name}}</p>
{{else}}
  <p>Lütfen giriş yapın</p>
{{/if}}
```

---

## 🔶 6. HAML (HTML Abstraction Markup Language)

- **Ruby kökenli ama Node için de portları var**
- **Girintili, sade sözdizimi**
- **HTML yazılmaz, yapısal olarak yazılır**

### ✅ Özellikler

- Pug gibi girintili yapıda
- Ruby’ye benzer
- Daha çok Ruby tarafında popüler

### 🔸 Kod Örneği

```haml
%ul
  - items.each do |item|
    %li= item
```

---

## 🧾 Karşılaştırma Tablosu

|Engine|Logic Seviyesi|Syntax Tipi|HTML Yazar mısın?|Kapsam|
|---|---|---|---|---|
|Nunjucks|Çok Yüksek|Django-like|Evet|Express, Static|
|Pug (Jade)|Yüksek|Girintili|Hayır|Express|
|Vash|Yüksek|Razor-like|Evet|ASP-style|
|EJS|Orta/Yüksek|JavaScript|Evet|Express|
|Handlebars|Orta|Kendi DSL|Evet|Express, Ember|
|HAML|Orta/Yüksek|Girintili (Ruby)|Hayır|Ruby ağırlıklı|

---

## 🎯 Sonuç

- **Karmaşık yapı, layout ve kalıtım istiyorsan** → `Nunjucks`
- **Kısa ve okunaklı yazım istiyorsan** → `Pug`
- **HTML içine JS gömüp rahat yazayım diyorsan** → `EJS`
- **Sadece view logic basitçe yetiyorsa** → `Handlebars`
