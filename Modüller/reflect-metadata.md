
## Amaç ve Kullanım

- **TypeScript dekoratörleriyle birlikte kullanılır.**
- Bir sınıfın, metodun, parametrenin veya property’nin üzerine ek bilgiler (tip, konfigürasyon vb.) koymaya yarar.
- Bu sayede kütüphaneler (örneğin InversifyJS) **runtime (çalışma zamanında) tip bilgisi** elde edip, ona göre işlem yapabilir.
- Özellikle **Dependency Injection (DI) container'larında bağımlılıkları otomatik çözmek için kullanılır.**

---

## Nasıl Çalışır?

- Bir dekoratör ile sınıfa veya metoda metadata eklenir.
- `reflect-metadata` API’si ile bu metadata runtime’da okunabilir.
- Örneğin, InversifyJS constructor parametrelerinin tiplerini `reflect-metadata` sayesinde öğrenir.

---

## Örnek Kullanım

```ts
import 'reflect-metadata';

class Example {
  method(param: string) {}
}

// Metadata'yı elde et
const paramTypes = Reflect.getMetadata('design:paramtypes', Example.prototype, 'method');

console.log(paramTypes); // [ [Function: String] ]
```

---

## InversifyJS’de Neden Gerekli?

- TypeScript, derleme sırasında tip bilgisini kaybeder, çalışma zamanında bu bilgi yoktur.
- `reflect-metadata` sayesinde tip bilgisi çalışma zamanında elde edilir.
- Bu bilgi ile InversifyJS hangi tipin hangi bağımlılığa karşılık geldiğini otomatik anlayabilir.

---

## Özet

|Özellik|Açıklama|
|---|---|
|Kütüphane|`reflect-metadata`|
|Amaç|Runtime’da tip ve diğer metadata sağlamak|
|Kullanım alanı|Dekoratör, DI, ORM, validation kütüphaneleri|
|Zorunluluk|Dekoratör ve DI kullanan TS projelerinde|

---

## Dikkat

- `reflect-metadata`'yı projenin **en başında import etmelisin** (ör: `import 'reflect-metadata';`).
- `tsconfig.json` içinde mutlaka aşağıdaki ayarlar aktif olmalı:

```json
{
  "experimentalDecorators": true,
  "emitDecoratorMetadata": true
}
```
