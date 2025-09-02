
`inversify-express-utils`, `InversifyJS` ile Express uygulamaları geliştirmek için kullanılan bir yardımcı kütüphanedir.  
Şunları sağlar:

- Controller tabanlı yapı
- Express route’larının dekoratörlerle tanımlanması (`@controller`, `@httpGet` gibi)
- Otomatik dependency injection (DI)
- Middleware desteği
- Express instance’ını otomatik oluşturma

---

## 📦 2. Kurulum

```bash
npm install inversify inversify-express-utils reflect-metadata
```

`tsconfig.json` içinde şu ayarları yapman **şart**:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

Ve `reflect-metadata`'ı uygulamanın en başında import etmelisin:

```ts
import 'reflect-metadata';
```

---

## 🧩 3. Yapı Taşları

### 3.1. `@controller` Dekoratörü

Bir sınıfı Express route'u olarak tanımlar:

```ts
import { controller, httpGet } from 'inversify-express-utils';

@controller('/users')
export class UserController {
    @httpGet('/')
    getAllUsers() {
        return ['Ahmet', 'Zeynep', 'Ayşe'];
    }
}
```

### 3.2. `httpGet`, `httpPost`, `httpPut`, `httpDelete`

Bunlar route handler tanımlar. Express’teki `app.get`, `app.post` yerine geçer.

```ts
@httpGet('/:id')
getUserById(@requestParam('id') id: string) {
    return `Kullanıcı ID: ${id}`;
}
```

### 3.3. `@request`, `@response`, `@requestParam`, `@queryParam`, `@requestBody`

Bunlar parametre dekoratörleridir, Express objelerini metoda enjekte eder:

```ts
@httpPost('/')
createUser(@requestBody() body: any) {
    return { success: true, user: body };
}
```

---

## 🔄 4. IoC Container Yapısı

Bir DI konteyneri tanımlarsın:

```ts
import { Container } from 'inversify';
import { InversifyExpressServer } from 'inversify-express-utils';

const container = new Container();
// binding'ler burada yapılır (örneğin UserService)
```

---

## 🚀 5. Sunucuyu Başlatma (`app.ts`)

```ts
import 'reflect-metadata';
import './controllers/UserController'; // controller'ı import et
import { Container } from 'inversify';
import { InversifyExpressServer } from 'inversify-express-utils';

const container = new Container();
// service injection'larını burada yap
// örneğin: container.bind<UserService>(TYPES.UserService).to(UserServiceImpl)

const server = new InversifyExpressServer(container);
const app = server.build();

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

---

## 🔒 6. Middleware Kullanımı

### 6.1. Route seviyesinde:

```ts
@httpGet('/', someAuthMiddleware)
getAll() {
    return ['A', 'B'];
}
```

### 6.2. Global middleware:

```ts
const server = new InversifyExpressServer(container);
server.setConfig((app) => {
    app.use(express.json());
    app.use(someLoggerMiddleware);
});
```

---

## 📁 7. Klasör Yapısı Önerisi

```
src/
├── controllers/
│   └── UserController.ts
├── services/
│   └── UserService.ts
├── interfaces/
│   └── IUserService.ts
├── inversify.config.ts
├── types.ts
└── app.ts
```

---

## ✅ Avantajlar

- ASP.NET Core’a benzer düzenli bir yapı
    
- Yüksek modülerlik ve test edilebilirlik
    
- Decorator tabanlı okunabilir kod
    
- Servisleri kolayca değiştirme/test etme (mocking)
    

---

## ⚠️ Dikkat Edilecekler

- Runtime'da tip bilgisi için `reflect-metadata` zorunlu
    
- DI kullanımı için `@inject()` ile manuel binding gerekebilir
    
- Dinamik route, parametre validasyonu gibi işlemleri ekstra kütüphanelerle yapman gerekebilir (`class-validator`, `joi`, vs.)
    

---

İstersen bir sonraki adımda **service injection** ya da **middleware**, **auth guard** gibi konularla devam edebilirim.  
Hangisinden devam edelim?