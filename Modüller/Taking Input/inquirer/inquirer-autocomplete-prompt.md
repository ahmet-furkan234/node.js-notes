`inquirer-autocomplete-prompt`, [`inquirer`](https://www.npmjs.com/package/inquirer) kütüphanesiyle birlikte kullanılan bir eklentidir ve kullanıcıdan alınacak cevabın otomatik tamamlamalı (autocomplete) şekilde seçilmesini sağlar. Genelde büyük veri listelerinden hızlı şekilde seçim yapılması gerektiğinde kullanılır.

---

### 🔧 Kurulum

Öncelikle `inquirer` ve `inquirer-autocomplete-prompt` paketlerini yükle:

```bash
npm install inquirer inquirer-autocomplete-prompt
```

---

### 📌 Temel Kullanım

```js
import inquirer from 'inquirer';
import autocomplete from 'inquirer-autocomplete-prompt';

// autocomplete prompt'u kaydet
inquirer.registerPrompt('autocomplete', autocomplete);

// örnek veri listesi
const cities = ['Istanbul', 'Izmir', 'Ankara', 'Antalya', 'Bursa', 'Mersin', 'Konya', 'Kayseri'];

function searchCities(answersSoFar, input) {
  input = input || '';
  return new Promise((resolve) => {
    const result = cities.filter(city =>
      city.toLowerCase().includes(input.toLowerCase())
    );
    resolve(result);
  });
}

inquirer
  .prompt([
    {
      type: 'autocomplete',
      name: 'city',
      message: 'Bir şehir seçin:',
      source: searchCities
    }
  ])
  .then((answers) => {
    console.log('Seçilen şehir:', answers.city);
  });
```

---

### 📌 Açıklamalar

- **`type: 'autocomplete'`**: Otomatik tamamlamalı prompt türü.
    
- **`source`**: Seçenekleri getiren fonksiyon. `input`'a göre filtreleme yapılır.
    
- **`answersSoFar`**: Diğer cevapları temsil eder, genelde kullanılmaz ama bağımlı seçimlerde işine yarayabilir.
    

---

### ⚠️ Dikkat Edilecek Noktalar

- `source` fonksiyonu **Promise döndürmelidir**.
    
- Liste büyükse async sorgular (örneğin bir API veya DB üzerinden) ile uyumlu çalışabilir.
    

---

### 🌐 Uygulama Senaryoları

- 1000+ elemanlı şehir, ürün, ülke listeleri
    
- DB'den veya API'den dinamik veri çekmek
    
- Komut satırı tabanlı araçlar (CLI tool) geliştirirken kullanıcı deneyimini artırmak
    

---

İstersen bir de **dinamik veri (örneğin bir API'den çekilen JSON)** ile örnek gösterebilirim. Devam edeyim mi?