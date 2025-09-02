
İşte `inversify-express-utils` paketinde bulunan tüm önemli **dekoratörler** ve **örnek kullanımlarıyla** detaylı açıklamaları:

---

## 📦 1. `@controller(path: string, ...middleware: any[])`

> Belirli bir route altında controller tanımlamak için kullanılır.

### ✅ Örnek:

```ts
import { controller, httpGet } from 'inversify-express-utils';

@controller('/users')
export class UserController {
  @httpGet('/')
  getAll() {
    return 'Tüm kullanıcılar';
  }
}
```

---

## 🛣️ 2. `@httpGet(path: string, ...middleware: any[])`

> GET isteğini yakalar.

### ✅ Örnek:

```ts
@httpGet('/:id')
getById(@requestParam('id') id: string) {
  return `ID: ${id}`;
}
```

---

## 🔽 3. `@httpPost(path: string, ...middleware: any[])`

> POST isteğini yakalar.

### ✅ Örnek:

```ts
@httpPost('/')
create(@requestBody() body: any) {
  return { message: 'Kullanıcı oluşturuldu', user: body };
}
```

---

## 🔼 4. `@httpPut(path: string, ...middleware: any[])`

> PUT isteğini yakalar.

### ✅ Örnek:

```ts
@httpPut('/:id')
update(@requestParam('id') id: string, @requestBody() body: any) {
  return { id, updated: body };
}
```

---

## 🔁 5. `@httpPatch(path: string, ...middleware: any[])`

> PATCH isteğini yakalar.

### ✅ Örnek:

```ts
@httpPatch('/:id')
patch(@requestParam('id') id: string, @requestBody() body: any) {
  return { id, patch: body };
}
```

---

## ❌ 6. `@httpDelete(path: string, ...middleware: any[])`

> DELETE isteğini yakalar.

### ✅ Örnek:

```ts
@httpDelete('/:id')
delete(@requestParam('id') id: string) {
  return { message: `Kullanıcı ${id} silindi` };
}
```

---

## 🧷 7. `@request()`

> Tüm `req` nesnesini alır.

### ✅ Örnek:

```ts
@httpGet('/headers')
headers(@request() req: Request) {
  return req.headers;
}
```

---

## 📤 8. `@response()`

> `res` nesnesini doğrudan elde etmek için.

### ✅ Örnek:

```ts
@httpGet('/res')
resSample(@response() res: Response) {
  return res.status(200).json({ message: 'OK' });
}
```

---

## 🔢 9. `@requestParam(name?: string)`

> URL parametrelerini almak için.

### ✅ Örnek:

```ts
@httpGet('/:id')
getById(@requestParam('id') id: string) {
  return `User ID: ${id}`;
}
```

---

## 📦 10. `@requestBody()`

> Body'den gelen veriyi almak için.

### ✅ Örnek:

```ts
@httpPost('/')
create(@requestBody() user: any) {
  return user;
}
```

---

## 🔎 11. `@queryParam(name: string)`

> Query string verilerini alır.

### ✅ Örnek:

```ts
@httpGet('/search')
search(@queryParam('q') q: string) {
  return `Arama: ${q}`;
}
```

---

## ⛔ 12. `@next()`

> Middleware zincirinde `next()` fonksiyonuna erişmek için.

### ✅ Örnek:

```ts
@httpGet('/next')
testNext(@request() req, @response() res, @next() nextFn) {
  console.log('Orta katman');
  nextFn();
}
```

---

## ⚙️ 13. `@httpMethod(method: string, path: string, ...middleware: any[])`

> Özel HTTP metodu kullanımı (örneğin: `OPTIONS`, `HEAD` vs.)

### ✅ Örnek:

```ts
import { httpMethod } from 'inversify-express-utils';

@httpMethod('options', '/')
optionsRoute() {
  return {};
}
```

---

## Özet Tablo

|Dekoratör|Açıklama|
|---|---|
|`@controller()`|Route ve middleware tanımlar|
|`@httpGet()`|GET isteğini işler|
|`@httpPost()`|POST isteğini işler|
|`@httpPut()`|PUT isteğini işler|
|`@httpPatch()`|PATCH isteğini işler|
|`@httpDelete()`|DELETE isteğini işler|
|`@request()`|`req` nesnesini alır|
|`@response()`|`res` nesnesini alır|
|`@requestParam()`|URL parametrelerini alır|
|`@requestBody()`|Body verisini alır|
|`@queryParam()`|Query verisini alır|
|`@next()`|Middleware geçişi için `next()`|
|`@httpMethod()`|Özel HTTP metotları için|

---

İstersen bir örnek proje yapısı da gösterebilirim veya bu dekoratörlerin nasıl birlikte kullanılacağını içeren bir `controller` örneği de verebilirim. Devam edeyim mi TkMatE?