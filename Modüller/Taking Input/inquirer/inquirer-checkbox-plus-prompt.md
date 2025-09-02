
## ✅ 1. Kurulum

Aşağıdaki komutları çalıştır:

```bash
npm install inquirer inquirer-checkbox-plus-prompt
npm install --save-dev @types/node
```

---

## ✅ 2. TypeScript Uyumlu Kod

> Aşağıdaki örnek: şehir listesinden **birden fazla seçim yapılabilen** ve **arama destekli** konsol uygulamasıdır.

📁 **`multi-autocomplete.ts`**:

```ts
import inquirer from 'inquirer';
import checkboxPlusPrompt from 'inquirer-checkbox-plus-prompt';

// Harici prompt'u kaydet (as any ile TypeScript hatasını geçiyoruz)
inquirer.registerPrompt('checkbox-plus', checkboxPlusPrompt as any);

// Şehir listesi
const cities = [
  'Istanbul', 'Izmir', 'Ankara', 'Antalya', 'Bursa',
  'Mersin', 'Konya', 'Kayseri', 'Adana', 'Trabzon',
  'Eskişehir', 'Erzurum', 'Gaziantep', 'Samsun', 'Van'
];

// Otomatik tamamlama yapan kaynak fonksiyonu
function searchCities(_: any, input?: string): Promise<{ name: string; value: string }[]> {
  input = input || '';
  return new Promise((resolve) => {
    const filtered = cities
      .filter(city => city.toLowerCase().includes(input.toLowerCase()))
      .map(city => ({ name: city, value: city }));
    resolve(filtered);
  });
}

// Ana fonksiyon
async function main() {
  const answers = await inquirer.prompt(
    [
      {
        type: 'checkbox-plus',
        name: 'selectedCities',
        message: 'Birden fazla şehir seçin:',
        pageSize: 8,
        highlight: true,
        searchable: true,
        source: searchCities
      }
    ] as any // prompt array'ine as any diyerek tip uyuşmazlığını çözüyoruz
  );

  console.log('\n✅ Seçilen şehirler:', answers.selectedCities);
}

main();
```

---

## 🧠 Açıklamalar

|Özellik|Açıklama|
|---|---|
|`checkbox-plus`|Birden fazla seçim yapılmasına izin verir.|
|`searchable: true`|Kullanıcı yazdıkça listeyi filtreler.|
|`source`|Dinamik olarak arama sonuçlarını döner.|
|`highlight`|Seçilen öğeyi vurgular.|
|`pageSize`|Terminalde aynı anda kaç seçenek gösterileceğini ayarlar.|

---

## ✅ `tsconfig.json` (Gerekirse)

Eğer ESM mod kullanıyorsan aşağıdaki gibi:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "moduleResolution": "node",
    "esModuleInterop": true,
    "strict": true,
    "types": ["node"]
  }
}
```

---

## 🚀 Sonuç

Bu yapı ile terminalde:

- ✅ Otomatik arama yaparak filtreleme
    
- ✅ Aynı anda birden fazla seçenek seçme
    
- ✅ CLI tool'ları için ideal kullanıcı deneyimi
    

elde etmiş oluyorsun.

---

İstersen bir sonraki adımda:

- 🔌 Bu verileri bir API'den çekmek
    
- 🧠 Seçime göre başka bir prompt açmak
    
- 🗂️ Kategorilere göre grup grup gösterim
    

gibi ileri düzey özellikleri de anlatabilirim.

Devam edelim mi?