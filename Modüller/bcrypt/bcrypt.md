
## 🔐 `bcrypt` Nedir?

`bcrypt`, kullanıcı şifrelerini **güvenli** bir şekilde saklamak için kullanılan bir **hashleme algoritmasıdır**. Amaç, gerçek şifreyi saklamamak, sadece "tek yönlü" bir temsilini (hash’ini) saklamaktır.

> ✅ Şifre veri tabanına asla düz yazı (plaintext) olarak kaydedilmez!

---

## ⚙️ Nasıl Çalışır?

1. **Kullanıcı şifresini girer** → örn: `admin123`
2. **bcrypt**, bu şifreyi önce bir "salt" ile birleştirir.
3. Sonra bir hash üretir → örn:  
    `$2b$10$yO4GbA7r0zWg6vDZF...`
4. Bu hash, veri tabanına kaydedilir.
5. Giriş yapılırken bcrypt, girilen şifreyi tekrar hash’ler ve veri tabanındakiyle karşılaştırır.

---

## 🧪 Güvenlik Özellikleri

- **Salt**: Her kullanıcı için **benzersiz bir karmaşık veri eklenir** (aynı şifre girilse bile hash farklı olur).
- **Zaman alıcıdır**: Brute force saldırılarına karşı dirençlidir.
- **Tek yönlüdür**: Hash’ten tekrar şifre üretilemez.

---

## ⚒️ Kurulum

```bash
npm install bcrypt
```

> `bcrypt` native modül içerdiğinden Node.js’in sisteminize uygun sürümde kurulu olması önemlidir.

---

## 💡 Kullanım – Adım Adım

### 🔸 1. Şifre Hashleme

```js
import bcrypt from 'bcrypt';

const password = 'admin123';
const saltRounds = 10; // güvenlik düzeyi

const hashedPassword = await bcrypt.hash(password, saltRounds);
console.log('Hash:', hashedPassword);
```

---

### 🔸 2. Şifre Karşılaştırma

```js
const isMatch = await bcrypt.compare('admin123', hashedPassword);
console.log('Eşleşiyor mu?', isMatch); // true
```

---

## 🧠 Salt Nedir? Neden Kullanılır?

Salt, her hash işlemine **benzersiz rastgele bir veri** ekler.

- Aynı şifreye sahip iki kullanıcı bile farklı hash değerlerine sahip olur.
- Rainbow Table saldırılarına karşı korur.

Örnek:

```js
await bcrypt.hash('admin123', 10); // farklı salt → farklı hash
await bcrypt.hash('admin123', 10); // yine farklı hash
```

---

## ❗ Sık Yapılan Hatalar

| Hata                                     | Açıklama          |
| ---------------------------------------- | ----------------- |
| Hash'lenmiş şifreyi tekrar hash'lemek    | Gereksiz ve bozar |
| Aynı salt'ı her kullanıcı için kullanmak | Güvenlik açığı    |
| Çok düşük saltRounds kullanmak           | Brute-force riski |
| Şifreyi düz olarak saklamak              | Felaket 🙀        |

---

## ✅ Best Practices

- `saltRounds = 10` iyi bir dengedir. Gerekirse 12 yap.
- Hash’lenmiş şifreyi her zaman `.env` dosyası gibi hassas yerlerden uzak tut.
- Girişlerde mutlaka `bcrypt.compare()` kullan.
- API dönerken hash’i asla istemciye gönderme.

---

## Bonus 🎁 TypeScript Servis Örneği

```ts
export class PasswordService {
  static async hashPassword(password: string): Promise<string> {
    const saltRounds = 10;
    return await bcrypt.hash(password, saltRounds);
  }

  static async comparePasswords(plain: string, hash: string): Promise<boolean> {
    return await bcrypt.compare(plain, hash);
  }
}
```
