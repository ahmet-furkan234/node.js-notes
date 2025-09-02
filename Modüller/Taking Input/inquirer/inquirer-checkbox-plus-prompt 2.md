
`inquirer-checkbox-plus-prompt` paketi **kendi TypeScript tipi (d.ts)** dosyasını sağlamaz ve **DefinitelyTyped** deposunda da (`@types/`) bir tanımı yok. Yani bu modül **tip tanımsız (untyped third-party module)** olarak gelir.

---

## 🎯 Çözüm: Tip Tanımsız Modülü Kullanmak

### ✅ Seçenek 1: `as any` ile kullanmak (Kolay ve pratik)

Bunu zaten uyguladık:

```ts
inquirer.registerPrompt('checkbox-plus', checkboxPlusPrompt as any);
```

Ve `prompt([...])` kısmında da:

```ts
await inquirer.prompt([...]) as any;
```

> Bu yöntem küçük-orta projelerde gayet yeterlidir.

---

## 💡 Seçenek 2: Tipi Kendin Tanımla (Gelişmiş)

Eğer proje büyürse veya kesin tip güvenliği istiyorsan, pakete özel tip tanımı yazabilirsin:

### 📁 `/types/inquirer-checkbox-plus-prompt/index.d.ts`

```ts
declare module 'inquirer-checkbox-plus-prompt' {
  import { PromptConstructor } from 'inquirer';
  const CheckboxPlusPrompt: PromptConstructor;
  export default CheckboxPlusPrompt;
}
```

Sonra `tsconfig.json`'da bu `types` klasörünü tanıt:

```json
{
  "compilerOptions": {
    "typeRoots": ["./types", "./node_modules/@types"]
  }
}
```

Artık şu şekilde yazabilirsin:

```ts
import checkboxPlusPrompt from 'inquirer-checkbox-plus-prompt';
inquirer.registerPrompt('checkbox-plus', checkboxPlusPrompt); // `as any` gerekmez
```

---

## 🤓 Bonus: Derin Tip Tanımı Gerekirse

Paketi incelersen `source` fonksiyonunun tipini detaylandırmak da mümkündür ama çoğu durumda bu gerekli olmaz. Yine de örnek istersen şu şekilde ilerleyebiliriz.

---

## 🚀 Özet

|Yol|Açıklama|Uygunluk|
|---|---|---|
|`as any`|Kolay ve hızlı çözüm|Hobi/CLI projeleri için ideal|
|`declare module`|Kendi modül tipini tanımlamak|Daha büyük projeler için önerilir|
|Custom `interface`|Derin tip güvencesi|Gelişmiş kullanım senaryoları|
