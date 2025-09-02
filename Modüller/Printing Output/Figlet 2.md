
## Figlet Özellikleri ve Opsiyonları

|Özellik|Açıklama|Değerler / Örnekler|
|---|---|---|
|`font`|Yazı tipi/font seçimi|`'Standard'`, `'Ghost'`, `'Slant'`, `'3-D'`, vb.|
|`horizontalLayout`|Yazının yatay hizalaması|`'default'`, `'full'`, `'fitted'`, `'controlled smushing'`|
|`verticalLayout`|Yazının dikey hizalaması|`'default'`, `'full'`, `'fitted'`|
|`width`|Satır genişliği sınırı (kelimelerin satır sığması için)|Sayısal değer, örn: `80`|
|`whitespaceBreak`|Boşluk karakterlerinde satır kırma|`true` veya `false`|

---

## Örneklerle Açıklama

```js
import figlet from 'figlet';

figlet.text('TkMatE', {
  font: 'Ghost',
  horizontalLayout: 'fitted',
  verticalLayout: 'fitted',
  width: 100,
  whitespaceBreak: true
}, (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

- `horizontalLayout: 'fitted'` yazının yatayda sıkışmasını sağlar.
- `verticalLayout: 'fitted'` dikey sıkıştırma.
- `width` parametresi çıktı genişliğini sınırlar, satır kaydırma yapılabilir.
- `whitespaceBreak` boşluklarda satır kırma kontrolü sağlar.

---

## Font Size (Boyut) Alternatifleri

Figlet'te doğrudan "font size" yok ama;

- **Farklı fontlar** farklı büyüklük ve tarzda ASCII oluşturur.
- Mesela `'Standard'` font daha sade ve büyük, `'Small'` font daha kompakt olabilir.

---

## Özet

| Özellik            | Font size etkisi?                                   |
| ------------------ | --------------------------------------------------- |
| Font seçimi        | Evet, farklı fontlar farklı boyutta/asciiler üretir |
| Layout seçenekleri | Yazının sıkışması/genişlemesi kontrolü sağlar       |
| Width parametresi  | Satır uzunluğunu sınırlandırır, kaydırma yapar      |
