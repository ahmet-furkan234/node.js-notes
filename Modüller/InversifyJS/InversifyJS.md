
**InversifyJS**, TypeScript için geliştirilmiş, güçlü ve **dekoratör destekli bir IoC/DI (Inversion of Control / Dependency Injection)** kütüphanesidir.

> "C#’ta kullandığın DI yapısını TypeScript dünyasında arıyorsan, doğru yerdesin."

---

## 🚀 2. InversifyJS Kurulumu

```bash
npm install inversify reflect-metadata
```

Ve `tsconfig.json` içinde şunları açmalısın:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

Ayrıca, uygulamanın en başında şunu **bir kez çağırmalısın**:

```ts
import "reflect-metadata";
```

---

## 🧪 3. Temel Kullanım Adımları

### 🎯 Amaç: `UserService`, `UserRepository`'yi kullanacak şekilde DI uygulanacak.

### 1. Interface Tanımı

```ts
// interfaces/IUserRepository.ts
export interface IUserRepository {
  getAll(): string[];
}
```

---

### 2. Repository Sınıfı

```ts
// repositories/UserRepository.ts
import { injectable } from "inversify";
import { IUserRepository } from "../interfaces/IUserRepository";

@injectable()
export class UserRepository implements IUserRepository {
  getAll(): string[] {
    return ["Ali", "Veli", "Ayşe"];
  }
}
```

---

### 3. Service Sınıfı (Injection ile)

```ts
// services/UserService.ts
import { inject, injectable } from "inversify";
import { IUserRepository } from "../interfaces/IUserRepository";

@injectable()
export class UserService {
  constructor(
    @inject("IUserRepository") private userRepository: IUserRepository
  ) {}

  getUsers() {
    return this.userRepository.getAll();
  }
}
```

---

### 4. IoC Container Kurulumu

```ts
// container.ts
import { Container } from "inversify";
import { IUserRepository } from "./interfaces/IUserRepository";
import { UserRepository } from "./repositories/UserRepository";
import { UserService } from "./services/UserService";

const container = new Container();

container.bind<IUserRepository>("IUserRepository").to(UserRepository);
container.bind<UserService>(UserService).toSelf();

export { container };
```

---

### 5. Kullanım (Main Dosyası)

```ts
// app.ts
import "reflect-metadata"; // !!! Olmazsa çalışmaz
import { container } from "./container";
import { UserService } from "./services/UserService";

const userService = container.get(UserService);
console.log(userService.getUsers()); // ["Ali", "Veli", "Ayşe"]
```

---

## 🧰 4. Inversify Terminolojisi

| Terim               | Açıklama                                                                  |
| ------------------- | ------------------------------------------------------------------------- |
| `@injectable()`     | Bir sınıfın container tarafından enjekte edilebilir olduğunu belirtir.    |
| `@inject("Token")`  | Enjekte edilecek bağımlılığı tanımlar (token-string veya sınıf olabilir). |
| `bind<T>(token)`    | Container'a bağımlılık kaydetme yöntemi                                   |
| `to()` / `toSelf()` | Bağımlılığı sınıfa bağlar                                                 |
| `get()`             | Bir sınıfı çözümleyip örneğini döner                                      |

---

## 📦 5. Bind Türleri

```ts
container.bind<UserRepository>("Repo").to(UserRepository);          // Transient (her çağrıda yeni)
container.bind<UserRepository>("Repo").to(UserRepository).inSingletonScope(); // Singleton
container.bind<UserRepository>("Repo").toConstantValue(new UserRepository()); // Tek instance
```

---

## 🧪 6. Test İçin Mock Repository

```ts
class MockUserRepo implements IUserRepository {
  getAll() {
    return ["TestUser1", "TestUser2"];
  }
}

container.unbind("IUserRepository");
container.bind<IUserRepository>("IUserRepository").to(MockUserRepo);

const service = container.get(UserService);
console.log(service.getUsers()); // ["TestUser1", "TestUser2"]
```

---

## 🧠 7. Ne Zaman Kullanılır?

InversifyJS şu durumlar için **mükemmel tercihtir**:

- TypeScript ile **büyük ölçekli** backend projeleri
    
- **SOLID prensiplerine uygun**, test edilebilir mimari kurmak
    
- C#'taki gibi **constructor tabanlı injection** isteniyorsa
    
- Genişletilebilir servis/middleware/controller yapıları varsa
    

---

## 🧩 Bonus: Otomatik Token Üretmek

Manuel string `"IUserRepository"` kullanmak yerine, **Symbol** ya da sabit tanım kullanabilirsin:

```ts
// types.ts
export const TYPES = {
  IUserRepository: Symbol.for("IUserRepository"),
};

// container.ts
container.bind<IUserRepository>(TYPES.IUserRepository).to(UserRepository);

// service.ts
@injectable()
export class UserService {
  constructor(
    @inject(TYPES.IUserRepository) private userRepository: IUserRepository
  ) {}
}
```

---

## ✨ Özet

|Özellik|InversifyJS|
|---|---|
|Dil|TypeScript|
|Dekoratör|✅ Desteklenir (`@inject`, `@injectable`)|
|Scope Desteği|Singleton, Transient, Constant|
|Test Desteği|Mükemmel – kolayca mock yapılabilir|
|Proje Boyutu|Orta ve Büyük projeler|

---

Devam etmek istersen şu konulara da geçebilirim:

- ✅ Middleware'lerde DI
    
- ✅ Controller yapısı ile REST mimarisi kurmak
    
- ✅ Express ile Inversify entegrasyonu
    
- ✅ Unit test örnekleri
    
- ✅ InversifyJS + class-validator + DTO mimarisi
    

Hangisini istersin `TkMatE`?