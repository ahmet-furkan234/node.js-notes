
Tabii TkMatE! Şimdi `inversify-express-utils` içindeki tüm dekoratörleri kapsayan detaylı, gerçek hayata yakın örneklerle beraber anlatayım. Kod örneklerini açıklamalarla birlikte adım adım vereceğim.

---

# 1. Setup (Temel Ayarlar)

```bash
npm install express inversify inversify-express-utils reflect-metadata
```

`tsconfig.json` içinde:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true,
    "strict": true
  }
}
```

En üst dosyada (örneğin `app.ts`):

```ts
import "reflect-metadata";
```

---

# 2. Types (Dependency Injection için)

```ts
// types.ts
export const TYPES = {
  UserService: Symbol.for("UserService"),
};
```

---

# 3. Service Sınıfı

```ts
// services/UserService.ts
import { injectable } from "inversify";

export interface IUserService {
  getAll(): string[];
  getById(id: string): string | null;
  create(name: string): string;
}

@injectable()
export class UserService implements IUserService {
  private users = ["Ahmet", "Mehmet", "Ayşe"];

  getAll(): string[] {
    return this.users;
  }

  getById(id: string): string | null {
    const index = parseInt(id);
    if (isNaN(index) || index < 0 || index >= this.users.length) return null;
    return this.users[index];
  }

  create(name: string): string {
    this.users.push(name);
    return name;
  }
}
```

---

# 4. Controller Sınıfı - Tüm Dekoratörlerle

```ts
// controllers/UserController.ts
import {
  controller,
  httpGet,
  httpPost,
  httpPut,
  httpDelete,
  httpPatch,
  request,
  response,
  requestParam,
  queryParam,
  requestBody,
  next,
} from "inversify-express-utils";
import { Request, Response, NextFunction } from "express";
import { inject } from "inversify";
import { TYPES } from "../types";
import { IUserService } from "../services/UserService";

@controller("/users")
export class UserController {
  constructor(@inject(TYPES.UserService) private userService: IUserService) {}

  // GET /users/
  @httpGet("/")
  public getAllUsers() {
    return this.userService.getAll();
  }

  // GET /users/:id
  @httpGet("/:id")
  public getUserById(@requestParam("id") id: string, @response() res: Response) {
    const user = this.userService.getById(id);
    if (!user) {
      return res.status(404).json({ error: "Kullanıcı bulunamadı" });
    }
    return res.json({ user });
  }

  // GET /users/search?q=name
  @httpGet("/search")
  public searchUser(@queryParam("q") q: string) {
    const all = this.userService.getAll();
    return all.filter((u) => u.toLowerCase().includes(q.toLowerCase()));
  }

  // POST /users/
  @httpPost("/")
  public createUser(@requestBody() body: { name: string }, @response() res: Response) {
    if (!body?.name) {
      return res.status(400).json({ error: "Ad alanı zorunlu" });
    }
    const newUser = this.userService.create(body.name);
    return res.status(201).json({ created: newUser });
  }

  // PUT /users/:id
  @httpPut("/:id")
  public updateUser(
    @requestParam("id") id: string,
    @requestBody() body: { name: string },
    @response() res: Response
  ) {
    const user = this.userService.getById(id);
    if (!user) {
      return res.status(404).json({ error: "Kullanıcı bulunamadı" });
    }
    if (!body?.name) {
      return res.status(400).json({ error: "Ad alanı zorunlu" });
    }
    // Basit update simülasyonu
    this.userService.create(body.name); // örnek amaçlı push ediyoruz
    return res.json({ updated: body.name });
  }

  // PATCH /users/:id
  @httpPatch("/:id")
  public patchUser(
    @requestParam("id") id: string,
    @requestBody() body: Partial<{ name: string }>,
    @response() res: Response
  ) {
    const user = this.userService.getById(id);
    if (!user) {
      return res.status(404).json({ error: "Kullanıcı bulunamadı" });
    }
    // Yalnızca isim varsa güncelle
    if (body.name) {
      this.userService.create(body.name);
      return res.json({ patched: body.name });
    }
    return res.status(400).json({ error: "Güncellenecek alan yok" });
  }

  // DELETE /users/:id
  @httpDelete("/:id")
  public deleteUser(@requestParam("id") id: string, @response() res: Response) {
    const user = this.userService.getById(id);
    if (!user) {
      return res.status(404).json({ error: "Kullanıcı bulunamadı" });
    }
    // Silme simülasyonu yapılmadı
    return res.json({ deleted: user });
  }

  // Örnek middleware ile next kullanımı
  @httpGet("/next/example")
  public withNext(@request() req: Request, @response() res: Response, @next() next: NextFunction) {
    console.log("Middleware öncesi");
    next();
  }
}
```

---

# 5. Container Setup

```ts
// inversify.config.ts
import { Container } from "inversify";
import { TYPES } from "./types";
import { IUserService, UserService } from "./services/UserService";

const container = new Container();
container.bind<IUserService>(TYPES.UserService).to(UserService);

export { container };
```

---

# 6. Server Başlatma

```ts
// app.ts
import "reflect-metadata";
import express from "express";
import { InversifyExpressServer } from "inversify-express-utils";
import { container } from "./inversify.config";

// Controller’lar import edilmeli ki decorator register olsun
import "./controllers/UserController";

const server = new InversifyExpressServer(container);

server.setConfig((app) => {
  app.use(express.json());
});

const app = server.build();

app.listen(3000, () => {
  console.log("Server 3000 portunda çalışıyor");
});
```

---

# 7. Test

- `GET http://localhost:3000/users/` → Tüm kullanıcılar
    
- `GET http://localhost:3000/users/0` → İlk kullanıcı
    
- `GET http://localhost:3000/users/search?q=ah` → Arama
    
- `POST http://localhost:3000/users/` `{ "name": "Ali" }` → Yeni kullanıcı oluştur
    
- `PUT http://localhost:3000/users/0` `{ "name": "Ayşe" }` → Güncelle
    
- `PATCH http://localhost:3000/users/0` `{ "name": "Mehmet" }` → Kısmi güncelle
    
- `DELETE http://localhost:3000/users/0` → Silme simülasyonu
    

---

Bu örnekle `inversify-express-utils` içindeki tüm önemli dekoratörleri **gerçek kullanım alanlarıyla** görmüş olduk. İstersen artık

- Middleware entegrasyonu,
    
- Authorization guard yapımı,
    
- DTO & validation ile zenginleştirme,
    

gibi ileri konulara geçebiliriz.  
Ne dersin?