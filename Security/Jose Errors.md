
## 🔎 `jwtVerify` Hata Türleri

|Hata Sınıfı|Ne Zaman Çıkar?|Örnek Mesaj|Kullanıcıya Ne Denmeli?|
|---|---|---|---|
|**JWTExpired**|Token’ın `exp` süresi geçmişse|`JWTExpired: JWT has expired`|"Oturum süresi doldu, lütfen tekrar giriş yapın."|
|**JWTInvalid**|JWT formatı bozuksa (ör. header.payload.signature formatında değilse)|`JWTInvalid: JWT malformed`|"Geçersiz token, lütfen tekrar giriş yapın."|
|**JWSInvalid**|İmza doğrulanamazsa (yanlış secret key, değiştirilmiş token)|`JWSInvalid: signature verification failed`|"Token doğrulanamadı."|
|**JWSSignatureVerificationFailed**|Token imzası geçersizse|`JWSSignatureVerificationFailed`|"Geçersiz imza, lütfen tekrar giriş yapın."|
|**JWTClaimValidationFailed**|Payload içindeki `aud`, `iss`, `nbf` gibi claim’ler beklenenle uyuşmazsa|`JWTClaimValidationFailed: unexpected "aud" claim value`|"Token doğrulama hatası."|

---

## 🔧 Önerilen Kullanım

Eğer **daha kullanıcı dostu hata mesajları** vermek istiyorsan `try/catch` ile spesifik sınıfları kontrol edebilirsin:

```ts
try {
    const { payload } = await jwtVerify(refreshToken, secret);
    // token geçerliyse devam et
} catch (err: any) {
    if (err.name === "JWTExpired") {
        throw new AuthorizationException("Refresh token süresi dolmuş, lütfen tekrar giriş yapın.");
    }
    if (err.name === "JWSInvalid" || err.name === "JWSSignatureVerificationFailed") {
        throw new AuthorizationException("Geçersiz token, lütfen tekrar giriş yapın.");
    }
    throw new AuthorizationException("Token doğrulama hatası.");
}
```

---

👉 Eğer `try/catch` kullanmazsan, global error handler **orijinal jose hatasını** (ör. `"JWTExpired: JWT has expired"`) döner.
