
## ✅ Doğru Kullanım (Gözden Geçirilmiş)

```ts
import { Container } from "inversify";
import "reflect-metadata"; // 💥 Bu çok önemli, unutulursa inject çalışmaz!

import { IUserRepository } from "./Repositories/Contracts/IUserRepository";
import { IUserService } from "./Services/Contracts/IUserService";
import { UserRepository } from "./Repositories/UserRepository";
import { UserService } from "./Services/UserService";

const container = new Container();

container.bind<IUserRepository>("IUserRepository").to(UserRepository);
container.bind<IUserService>("IUserService").to(UserService);

export { container };
```

---

## ⚠️ Dikkat Etmen Gerekenler

### 🔹 1. `reflect-metadata` kullanımı

InversifyJS çalışması için zorunludur:

- `import "reflect-metadata"` en üstte **bir kere çağrılmalı.**
- Ayrıca tsconfig.json içinde `"experimentalDecorators": true` ve `"emitDecoratorMetadata": true` olmalı:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

---

### 🔹 2. `bind<T>(IDENTIFIER).to(Class)` yapısı

- `bind<T>("string")` kısmında kullanılan string sabitler `Symbol` ile tanımlanabilir, bu daha güvenlidir.

Örneğin:

#### ✨ Daha iyi yol:

```ts
export const TYPES = {
  IUserRepository: Symbol.for("IUserRepository"),
  IUserService: Symbol.for("IUserService"),
};
```

Kullanım:

```ts
container.bind<IUserRepository>(TYPES.IUserRepository).to(UserRepository);
```

---

## ✅ Bonus: Dependency Injection Örneği

```ts
import { inject, injectable } from "inversify";
import { IUserRepository } from "./Repositories/Contracts/IUserRepository";
import { TYPES } from "./types";

@injectable()
export class UserService implements IUserService {
  constructor(
    @inject(TYPES.IUserRepository) private userRepository: IUserRepository
  ) {}

  async getUserById(id: string) {
    return this.userRepository.findById(id);
  }
}
```

---

## 📦 Paket Kurulumu Kontrolü

Eğer hâlâ kurmadıysan bu paketleri kurmalısın:

```bash
npm install inversify reflect-metadata
```

---

## 🟢 Özet

|Kontrol|Durum|
|---|---|
|`reflect-metadata` importu|✅ Gerekli|
|`tsconfig.json` ayarları|✅ Gerekli|
|`bind<>()` kullanımı|✅ Doğru|
|String identifier yerine `Symbol`|🔸 Tavsiye edilir|
|`@injectable`, `@inject` kullanımı|✅ Sınıflarda olmalı|
