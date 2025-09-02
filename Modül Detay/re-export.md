
`re-export`, başka bir dosyadan içe aktardığın şeyi **kendin dışa aktarman** anlamına gelir.

Kullanım amacı:

- Modülleri merkezileştirmek (tek dosyadan erişmek).
- Kodun okunabilirliğini artırmak.
- İsim çakışmalarını yönetmek.

---

## ✅ 1. Temel Re-export

### 📁 math.ts

```ts
export function topla(a: number, b: number): number {
  return a + b;
}
```

### 📁 index.ts (re-export burada)

```ts
export { topla } from "./math"; // re-export işlemi
```

### 📁 main.ts

```ts
import { topla } from "./index"; // math değil, index'ten geldi!
```

---

## ✅ 2. Re-export All (`export * from`)

Bir dosyadaki tüm dışa aktarımları tekrar dışa aktarmak.

### 📁 math.ts

```ts
export function topla(a: number, b: number): number {
  return a + b;
}

export function cikar(a: number, b: number): number {
  return a - b;
}
```

### 📁 index.ts

```ts
export * from "./math"; // tüm fonksiyonları dışa aktar
```

### 📁 main.ts

```ts
import { topla, cikar } from "./index";
```

> ⚠️ `export *` ile gelen öğeleri **yeniden adlandıramazsın**, sadece olduğu gibi dışa aktarırsın.

---

## ✅ 3. Re-export with Rename

```ts
export { topla as add } from "./math";
```

Bu şekilde hem re-export hem de isim değişimi yapabilirsin.

---

## ✅ 4. Re-export Default

Varsayılan export'u yeniden dışa aktarmak için:

### 📁 logger.ts

```ts
export default function log(msg: string) {
  console.log("Log:", msg);
}
```

### 📁 index.ts

```ts
export { default as log } from "./logger"; // default'u ad vererek re-export
```

### 📁 main.ts

```ts
import { log } from "./index";
log("Merhaba");
```

---

## 🎯 Ne Zaman Kullanılır?

- 📁 `index.ts` dosyasında tüm modülleri toplayıp dışa aktarmak istediğinde.    
- 📦 Bir `utility`, `api`, veya `components` klasöründeki tüm dosyaları tek bir yerden erişilebilir yapmak için.
- 📚 Büyük projelerde daha düzenli içe aktarma yolları sunmak için.

---

## 📌 Örnek Yapı

```
/utils
  - math.ts
  - string.ts
  - index.ts  ← Re-export burada
```

### index.ts

```ts
export * from "./math";
export * from "./string";
```

Artık `main.ts` içinde:

```ts
import { topla, capitalize } from "./utils";
```

---
## ✅ 1. **Merkezi Kontrol ve Bakım Kolaylığı**

**Sorun:** Her modülü ayrı ayrı import etmek kodu karmaşıklaştırır.

**Çözüm:** Tüm modülleri tek bir dosyada toplarsan, bir dosyanın yeri değiştiğinde sadece `index.ts`'teki yolu güncelleyerek projeyi düzeltirsin.

### Örnek:

#### Eskisi:

```ts
import { topla } from "./utils/math";
import { capitalize } from "./utils/string";
import { log } from "./helpers/logger";
```

#### Re-export ile:

```ts
import { topla, capitalize, log } from "./core"; // tek yerden geldi
```

---

## ✅ 2. **Modülerlik ve Soyutlama (Abstraction)**

Dışa yalnızca ihtiyaç olanı aktarabilirsin. Modül içinde ne olursa olsun dış dünya sadece senin sunduğun arayüzü görür.

> 👁️‍🗨️ Böylece içerideki yapıyı değiştirmek dışarıyı etkilemez.

---

## ✅ 3. **İsim Çakışmalarını Önleme**

Farklı dosyalarda aynı isimde fonksiyonlar olabilir. `re-export` ile onları yeniden adlandırabilir, çakışmaları engellersin.

### Örnek:

```ts
// math.ts
export function validate() { }

// string.ts
export function validate() { }

// core.ts
export { validate as validateMath } from "./math";
export { validate as validateString } from "./string";
```

---

## ✅ 4. **Auto-import (VSCode gibi editörlerde)** daha iyi çalışır

Bir modülün tek merkezden dışa aktarıldığını bilen editörler, otomatik içe aktarma (`auto import`) yaparken **doğru ve düzenli yolu** kullanır.

---

## ✅ 5. **Yaygın Bir Proje Standartı (Barrel Files)**

Profesyonel projelerde genellikle her klasörde bir `index.ts` bulunur. Bu, o klasörün **genel API’si** gibi çalışır.

```txt
/components
  Button.tsx
  Input.tsx
  index.ts ← buradan her şey re-export edilir
```

Kullanım:

```ts
import { Button, Input } from "./components";
```

---

## ✅ 6. **Dış kütüphanelerle uyum**

Bazı durumlarda re-export sayesinde özel API tasarımı sunabilirsin. Örneğin bir SDK oluşturuyorsan kullanıcıya sadece bazı metotları sunmak isteyebilirsin.

---

## 📌 Özetle Sana Ne Katıyor?

|Fayda|Açıklama|
|---|---|
|✅ Daha temiz import'lar|Her yerde uzun yollar yerine tek merkez|
|✅ Kod organizasyonu|Tüm API'yi düzenli olarak dışa açabilirsin|
|✅ Değişiklik yönetimi|Dosya yolu değişse bile tek yerden çözülür|
|✅ Proje büyüklüğüyle baş etme|Modüler yapı büyük kod tabanlarında şart|
|✅ Tip güvenliği|TypeScript ile birlikte harika çalışır|
