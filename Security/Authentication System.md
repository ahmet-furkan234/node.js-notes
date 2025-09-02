Harika soru TkMatE 👌

JWT tabanlı kimlik doğrulamada modern yaklaşım **2 token mekanizmasıdır**:

- **Access Token** → kısa ömürlü (ör. 15dk – 2h). Her request’te client bunu gönderir.
- **Refresh Token** → uzun ömürlü (ör. 7–30 gün). DB’de saklanır, sadece yeni access token almak için kullanılır.

---

## 🔄 Refresh Token Mekanizması Akışı

1. **Login**
    - Kullanıcı email & şifre ile giriş yapar.
    - Server hem **access token** hem de **refresh token** üretir.
    - Access token client’a `Authorization: Bearer` header ile kullanması için gönderilir.
    - Refresh token DB’de saklanır (kullanıcıya HTTP-only cookie veya response body’de verilebilir).
2. **Request**
    - Client API çağırırken sadece **access token** kullanır.
3. **Access Token Expire Olunca**
    - Client **refresh token** ile `/auth/refresh` endpoint’ine gider.
    - Server refresh token’ın geçerli olup olmadığını kontrol eder.
    - Geçerliyse yeni bir access token üretir.
4. **Logout**
    - Refresh token DB’den silinir → kullanıcı artık yeni token alamaz.

---

## 🔧 Kod Örneği (Senin Yapıya Göre)

### 1. Login içinde hem Access hem Refresh token üret

```ts
const secret = new TextEncoder().encode(process.env.SECRET_KEY);

// Access Token (kısa süreli)
const accessToken = await new SignJWT({
    sub: userRole[0]._id.toString(),
    role: userRole[0].roles.name
})
.setProtectedHeader({ alg: 'HS256' })
.setIssuedAt()
.setExpirationTime('15m') // 15 dakika
.sign(secret);

// Refresh Token (uzun süreli)
const refreshToken = await new SignJWT({
    sub: userRole[0]._id.toString()
})
.setProtectedHeader({ alg: 'HS256' })
.setIssuedAt()
.setExpirationTime('7d') // 7 gün
.sign(secret);

// refresh token'ı DB'ye kaydet
await this.userModel.updateOne(
    { _id: userRole[0]._id },
    { $set: { refreshToken } }
);

return {
    message: "Giriş başarılı",
    result: { accessToken, refreshToken },
    success: true
};
```

---

### 2. Refresh Endpoint

```ts
async refresh(refreshToken: string): Promise<IGenericResponse<{ accessToken: string }>> {
    const secret = new TextEncoder().encode(process.env.SECRET_KEY);

    // Refresh token DB’de var mı kontrol et
    const user = await this.userModel.findOne({ refreshToken });
    if (!user) throw new AuthorizationException("Geçersiz refresh token");

    try {
        // Token doğrula
        const { payload } = await jwtVerify(refreshToken, secret);

        // Yeni access token üret
        const newAccessToken = await new SignJWT({
            sub: user._id.toString(),
            role: user.roleName
        })
        .setProtectedHeader({ alg: 'HS256' })
        .setIssuedAt()
        .setExpirationTime('15m')
        .sign(secret);

        return {
            message: "Yeni access token üretildi",
            result: { accessToken: newAccessToken },
            success: true
        }
    } catch (err) {
        throw new AuthorizationException("Refresh token süresi dolmuş");
    }
}
```

---

### 3. Logout

```ts
async logout(userId: string): Promise<IGenericResponse<null>> {
    await this.userModel.updateOne(
        { _id: userId },
        { $unset: { refreshToken: "" } }
    );
    return {
        message: "Çıkış başarılı",
        result: null,
        success: true
    }
}
```

---

## 🔐 Dikkat Edilmesi Gerekenler

- **Refresh token saklama** → HTTP-only cookie önerilir. (XSS saldırılarından korunur).
- **Token rotation** → Yeni refresh token her kullanımda yenilenmeli.
- **Blacklist** → Çalınan refresh token’ları engellemek için DB tarafında tutmak şart.
- **Kısa access token + uzun refresh token** → güvenlik ve performans dengesi sağlar.
