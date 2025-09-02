
# 🔐 JSON Web Token (JWT) & JOSE Nedir?

---

## 1️⃣ JWT (JSON Web Token) Nedir?

- **JSON formatında, dijital olarak imzalanmış veya şifrelenmiş token’dır.**
- Kullanıcı kimliğini doğrulamak ve güvenli bilgi taşımak için kullanılır.
- Yapısı 3 parçadan oluşur: Header, Payload (Claims), Signature.

---

## 2️⃣ JWT’nin 3 Parçası

|Parça|İçerik|Format (Base64Url encoded)|
|---|---|---|
|Header|Token tipi ve algoritma bilgisi|`{ "alg": "HS256", "typ": "JWT" }`|
|Payload|Kullanıcı bilgisi ve claims|`{ "sub": "123", "name": "Ahmet", "iat": 1516239022 }`|
|Signature|Header + Payload + Secret ile imza|Güvenlik sağlar|

---

## 3️⃣ JOSE (JavaScript Object Signing and Encryption)

- JWT’yi oluşturmak, imzalamak, doğrulamak için kullanılan standart ve kütüphane ailesi.
- JOSE 4 temel standardı içerir:
    - **JWS** — JSON Web Signature (İmzalama)
    - **JWE** — JSON Web Encryption (Şifreleme)
    - **JWK** — JSON Web Key (Anahtar formatı)
    - **JWA** — JSON Web Algorithms (Algoritmalar)
- **`jose`** npm paketi modern ve güçlü bir JOSE/JWT kütüphanesidir.

---

## 4️⃣ Basit JWT Oluşturma ve Doğrulama (JOSE ile)

### Kurulum:

```bash
npm install jose
```

---

### Örnek: JWT Oluşturma (Sign) & Doğrulama (Verify)

```ts
import { SignJWT, jwtVerify } from 'jose';

// Gizli anahtar (secret key)
const secret = new TextEncoder().encode('supersecretkey123');

// JWT Oluşturma
async function createToken() {
  const token = await new SignJWT({ userId: '123', role: 'admin' })
    .setProtectedHeader({ alg: 'HS256' })
    .setIssuedAt()
    .setExpirationTime('2h')
    .sign(secret);

  return token;
}

// JWT Doğrulama
async function verifyToken(token: string) {
  try {
    const { payload } = await jwtVerify(token, secret);
    console.log('Doğrulandı, payload:', payload);
  } catch (err) {
    console.error('Geçersiz token:', err);
  }
}

(async () => {
  const myToken = await createToken();
  console.log('Token:', myToken);

  await verifyToken(myToken);
})();
```

---

## 5️⃣ Önemli Notlar:

- **Secret key** gizli tutulmalı, asla client tarafına verilmemeli.
- Algoritma olarak HS256, RS256, ES256 gibi seçenekler var.
- Token içinde `exp`, `iat`, `aud` gibi standart claim’ler kullanılabilir.
- JOSE, sadece JWT değil, JSON Web Encryption (JWE) ile veri şifrelemesi de sağlar.

---

## 6️⃣ JWT Kullanım Alanları

- Kullanıcı kimlik doğrulama (Login sonrası token üretip client’a gönderme)
- API erişim kontrolü (token ile istekleri doğrulama)
- Yetkilendirme (rol bazlı erişim yönetimi)
