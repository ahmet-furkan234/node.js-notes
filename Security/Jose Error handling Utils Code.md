
### 🔧 `verifyToken.ts`

```ts
import { jwtVerify, JWTPayload } from "jose";
import { AuthorizationException } from "../utils/appError";

/**
 * JWT doğrulama fonksiyonu
 * @param token JWT string
 * @param secret Secret key (TextEncoder ile encode edilmiş)
 * @returns payload (JWTPayload)
 */
export async function verifyToken(token: string, secret: Uint8Array): Promise<JWTPayload> {
    try {
        const { payload } = await jwtVerify(token, secret);
        return payload;
    } catch (err: any) {
        switch (err.name) {
            case "JWTExpired":
                throw new AuthorizationException("Token süresi dolmuş, lütfen tekrar giriş yapın.");
            case "JWTInvalid":
            case "JWSInvalid":
            case "JWSSignatureVerificationFailed":
                throw new AuthorizationException("Geçersiz token, lütfen tekrar giriş yapın.");
            case "JWTClaimValidationFailed":
                throw new AuthorizationException("Token doğrulama hatası.");
            default:
                throw new AuthorizationException("Token doğrulama sırasında bilinmeyen bir hata oluştu.");
        }
    }
}
```

---

### 🔹 Kullanımı AuthService içinde

```ts
import { verifyToken } from "../utils/verifyToken";

const secret = new TextEncoder().encode(process.env.SECRET_KEY);
const payload = await verifyToken(refreshToken, secret);

// payload geçerli ise devam et
const user = await this.userModel.findById(payload.sub);
```

---

### ✅ Avantajları

1. Tek noktadan **tüm JWT hatalarını yönetebilirsin**.
2. Kod tekrarını önler, her endpoint’te try/catch yazmana gerek yok.
3. Global error handler ile entegre çalışır, kullanıcıya anlamlı mesaj döner.
4. Refresh token veya access token fark etmez, aynı fonksiyon kullanılabilir.
