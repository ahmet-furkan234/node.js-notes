
## 📌 1. UUID v1 – Zaman damgası tabanlı (timestamp + MAC adresi içerir)

```ts
import { v1 as uuidv1 } from 'uuid';

const id = uuidv1();
console.log('UUID v1:', id);
```

> ⚠️ Zaman bazlıdır, sıralı olabilir. Genelde sistemler arası zaman tabanlı eşleştirmelerde kullanılır.

---

## 📌 2. UUID v3 – Namespace + name (deterministik, MD5)

```ts
import { v3 as uuidv3 } from 'uuid';

const MY_NAMESPACE = uuidv3.DNS; // veya kendi özel namespace UUID'in
const id = uuidv3('example.com', MY_NAMESPACE);
console.log('UUID v3:', id);
```

> Aynı isim + namespace kombinasyonu daima aynı UUID’yi üretir.

---

## 📌 3. UUID v4 – Rastgele (GENELLİKLE EN ÇOK KULLANILAN)

```ts
import { v4 as uuidv4 } from 'uuid';

const id = uuidv4();
console.log('UUID v4:', id);
```

> Rastgele olduğu için çakışma ihtimali düşüktür, çoğu uygulamada tercih edilir.

---

## 📌 4. UUID v5 – Namespace + name (deterministik, SHA-1)

```ts
import { v5 as uuidv5 } from 'uuid';

const MY_NAMESPACE = uuidv5.URL;
const id = uuidv5('https://example.com', MY_NAMESPACE);
console.log('UUID v5:', id);
```

> v3 ile aynıdır, ama daha güvenli SHA-1 kullanır.

---

## 🎯 Namespace Kullanımı

Eğer özel bir namespace kullanmak istersen bir v4 UUID üreterek kullanabilirsin:

```ts
import { v4 as uuidv4, v5 as uuidv5 } from 'uuid';

const customNamespace = uuidv4(); // özel namespace üret
const id = uuidv5('my-resource-name', customNamespace);
console.log('Custom v5 UUID:', id);
```

---

## 🔍 Bonus – UUID doğrulama

```ts
import { validate as uuidValidate } from 'uuid';

const isValid = uuidValidate('110ec58a-a0f2-4ac4-8393-c866d813b8d1');
console.log('Is valid UUID?', isValid);
```

---

İstersen bu örneklerin hepsini tek bir `.ts` dosyasında birleştirilmiş halde de sunabilirim. Hazır hale getireyim mi?