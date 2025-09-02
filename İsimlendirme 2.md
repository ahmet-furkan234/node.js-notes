
## Controller Method İsimlendirme Önerisi

| İşlem                             | Örnek Method Adı    | Açıklama                      |
| --------------------------------- | ------------------- | ----------------------------- |
| Tüm kullanıcıları getir           | `getAllUsers`       | Route: `GET /users`           |
| Kullanıcıyı userName’e göre getir | `getUserByUserName` | Route: `GET /users/:userName` |
| Yeni kullanıcı oluştur            | `createUser`        | Route: `POST /users`          |
| Kullanıcı güncelle                | `updateUser`        | Route: `PUT /users/:id`       |
| Kullanıcı sil                     | `deleteUser`        | Route: `DELETE /users/:id`    |

---

## Örnek Controller Sınıfı (Express tarzı)

```ts
export class UserController {
  async getAllUsers(req, res) {
    const users = await this.userService.getAllUser();
    res.json(users);
  }

  async getUserByUserName(req, res) {
    const userName = req.params.userName;
    const user = await this.userService.getUserByUserName(userName);
    res.json(user);
  }

  async createUser(req, res) {
    const newUserData = req.body;
    const newUser = await this.userService.createUser(newUserData);
    res.status(201).json(newUser);
  }

  async updateUser(req, res) {
    const id = req.params.id;
    const updateData = req.body;
    const updatedUser = await this.userService.updateUser(id, updateData);
    res.json(updatedUser);
  }

  async deleteUser(req, res) {
    const id = req.params.id;
    await this.userService.deleteUser(id);
    res.status(204).send();
  }
}
```

---

## Özet

- Controller methodları **Service metodlarını çağırır** ve HTTP request/response yönetir.
- İsimlendirme **getAllUsers**, **getUserByUserName**, **createUser**, **updateUser**, **deleteUser** gibi açık ve standart olmalı.
- Route URL’leri RESTful olmalı (`/users`, `/users/:id` veya `/users/:userName`).
