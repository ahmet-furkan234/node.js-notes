
## 1️⃣ ObjectId (en yaygın)

```ts
roleId: { type: Schema.Types.ObjectId, ref: "Role" }
```

- Bu en doğal kullanım ve **varsayılan Mongoose davranışı**.
- `.populate("roleId")` sorunsuz çalışır.

---

## 2️⃣ String ID (örn. UUID v4)

```ts
roleId: { type: String, ref: "Role" }
```

- UUID v4 gibi string ifadeler de **ref** ile kullanılabilir.
- Önemli nokta: `ref` modeli aynı tipteki değerleri bekler.
    - Eğer Role tablosunda `_id` String ise, user.roleId da string olmalı.
    - Tipler uyuşmazsa populate çalışmaz.

Örnek:

```ts
// Role
const roleSchema = new Schema({
  _id: { type: String, default: () => uuidv4() },
  name: String
});

// User
const userSchema = new Schema({
  email: String,
  roleId: { type: String, ref: "Role" } // string referans
});
```

```ts
const user = await userModel.findOne({ email: "a@b.com" }).populate("roleId");
console.log(user.roleId.name); // works
```

---

## 3️⃣ Özet

|ID Tipi|populate ile uyum|
|---|---|
|ObjectId|✅ Tam uyum, varsayılan|
|String / UUID|✅ Çalışır ama hem referans hem target field aynı tip olmalı|
|Number|✅ Çalışır, aynı tip olmalı|
|Mixed / Array|⚠️ Karmaşık, genellikle tek ID için kullanılmaz|

---

💡 **Not:**

- MongoDB’de `_id` default olarak ObjectId olduğu için ObjectId kullanmak genellikle daha kolaydır.
- UUID gibi string ID kullanmak istiyorsan, **hem parent hem child tabloda tiplerin eşleştiğinden** emin olmalısın.
