TypeScript (veya genel olarak Node.js) projelerinde benzersiz kimlikler (UUID) oluşturmak için en yaygın kullanılan paket `uuid` modülüdür. Bu modül hem CommonJS hem de ECMAScript Module (ESM) projelerinde sorunsuz çalışır.

---

## 🔧 Kurulum

### NPM:

```bash
npm install uuid
```

### Yarn:

```bash
yarn add uuid
```

---

## 📘 TypeScript ile Kullanımı

### ESM (ECMAScript Modules) ile (senin tercih ettiğin yapı):

```ts
import { v4 as uuidv4 } from 'uuid';

const id = uuidv4();
console.log(id); // Örn: '110ec58a-a0f2-4ac4-8393-c866d813b8d1'
```

> Eğer TypeScript `module` olarak `"ESNext"` ya da `"ESModule"` kullanıyorsan, bu yapı doğrudur.

---

### CommonJS ile (require kullanıyorsan):

```ts
const { v4: uuidv4 } = require('uuid');

const id = uuidv4();
console.log(id);
```

---

## 🔍 UUID Versiyonları

- `v1()` – Timestamp tabanlı
- `v3()` – Namespace (MD5)
- `v4()` – Rastgele (GENELLİKLE EN ÇOK KULLANILAN)
- `v5()` – Namespace (SHA-1)

### Örnek (v1 kullanımı):

```ts
import { v1 as uuidv1 } from 'uuid';

const id = uuidv1();
console.log(id);
```

---

## 📦 Tip Tanımlamaları

`uuid` modülünün TypeScript tipleri kutudan çıktığı gibi gelir, ayrıca `@types/uuid` yüklemen gerekmez.

---

## 🧪 UUID Doğrulama

Eğer bir string'in UUID olup olmadığını kontrol etmek istersen:

```ts
import { validate as uuidValidate } from 'uuid';

console.log(uuidValidate('110ec58a-a0f2-4ac4-8393-c866d813b8d1')); // true
```

---

## ⚠️ Not

Eğer bu hatayı alırsan:

```bash
SyntaxError: Cannot use import statement outside a module
```

Şunları kontrol et:

- `tsconfig.json` dosyanda `"module": "ESNext"` veya `"ESModule"` olmalı.
- Dosya uzantıların `.ts` yerine `.mts` olabilir (bazı ESM projelerinde önerilir).
- ESM'de çalışıyorsan Node.js 14+ sürümde `.ts` dosyalarını çalıştırmak için `--loader ts-node/esm` kullanmalısın.

