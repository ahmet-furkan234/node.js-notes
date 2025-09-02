
- Metni büyük ASCII karakterleriyle gösterir.
- Terminalde başlık, logo, dikkat çekmek için kullanılır.
- Çok sayıda farklı yazı fontu (font) destekler.
- Kullanımı çok kolaydır.

---

# 🚀 Kurulum

```bash
npm install figlet
```

---

# 🛠️ Temel Kullanım

```js
import figlet from 'figlet';

figlet('Merhaba TkMatE!', (err, data) => {
  if (err) {
    console.log('Figlet hatası:', err);
    return;
  }
  console.log(data);
});
```

---

# 🎨 Font Değiştirme

```js
figlet.text('TkMatE', {
  font: 'Ghost',
  horizontalLayout: 'default',
  verticalLayout: 'default'
}, (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

---

# 📜 Mevcut Fontları Listeleme

```js
figlet.fonts((err, fonts) => {
  if (err) throw err;
  console.log(fonts);
});
```

---

# 🔄 Synchronous Kullanım (Senkrondur, basit scriptler için uygun)

```js
import figlet from 'figlet';

const text = figlet.textSync('TkMatE', {
  font: 'Standard',
  horizontalLayout: 'default',
  verticalLayout: 'default'
});

console.log(text);
```

---

# 🧩 İleri Seviye Örnek — `chalk` ile Kombinasyon

```js
import figlet from 'figlet';
import chalk from 'chalk';

figlet('TkMatE!', (err, data) => {
  if (err) {
    console.error('Figlet hatası:', err);
    return;
  }
  console.log(chalk.green(data));
});
```

---

# 🎯 Figlet Kullanım Alanları

- CLI uygulamalarda başlık ve logo
- Hoş geldiniz mesajları
- Hata veya başarı mesajlarını vurgulama
