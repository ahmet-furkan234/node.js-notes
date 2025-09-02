
## 1. **Event Loop’un Amacı**

Node.js, tek iş parçacıklı (single-threaded) çalışır ama aynı anda binlerce işlemi asenkron yapabilir. Bunu sağlayan şey **Event Loop**’dur.  
Event Loop, işlemleri kuyruklar halinde yönetip, asenkron callback’leri sırayla çalıştırır.

---

## 2. **Node.js’de Event Loop’un Genel İşleyişi**

- **Call Stack (Çağrı Yığını)**: Senin senkron kodların burada çalışır.
- **Node APIs**: Asenkron işlemler (dosya okuma, ağ, timer vs) burada çalışır, tamamlanınca callback’ler event loop’a gönderilir.
- **Callback Queue (Kuyruk)**: Asenkron işlemlerin callback’leri burada sıraya girer.
- **Event Loop**: Callback Queue’yu takip eder, Call Stack boşsa sıradaki callback’i alıp çalıştırır.

---

## 3. **Basit Örnek**

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

console.log("3");
```

Çıktı:

```
1
3
2
```

Çünkü:

- `console.log("1")` ve `console.log("3")` senkron, hemen çalışır.
- `setTimeout` callback’i timer fazında çalışır, event loop’un sonraki turuna kalır.

---

## 4. **Event Loop Fazları (Phases)**

Event Loop, belirli fazlardan oluşur. Her fazda belirli tip callback’leri işler:

| Faz (Phase)       | Açıklama                                       |
| ----------------- | ---------------------------------------------- |
| timers            | `setTimeout` ve `setInterval` callback’leri    |
| pending callbacks | Sistem tarafından tamamlanan I/O callback’leri |
| idle, prepare     | Node.js dahili kullanımı                       |
| poll              | Yeni I/O olaylarını bekler ve çalıştırır       |
| check             | `setImmediate` callback’leri                   |
| close callbacks   | Kapanan bağlantıların close event’leri         |

---

## 5. **Önemli Notlar**

- `process.nextTick()` callback’leri event loop fazlarından bağımsızdır; mevcut operasyon tamamlanınca, event loop devam etmeden hemen çalışırlar.
- `setImmediate()` callback’leri check fazında çalışır, I/O sonrası hemen tetiklenir.
- `setTimeout(fn, 0)` timer fazında çalışır, minimum gecikme olabilir.

---

## 6. **Event Loop’un Görsel Örneği**

```
┌─────────────┐
│ Call Stack  │
└─────┬───────┘
      │
      ▼
┌─────────────┐        ┌───────────────────┐
│ Node APIs   │<──────▶│ Event Loop Phases │
└─────────────┘        └───────────────────┘
      ▲
      │
┌─────┴───────┐
│ Callback Q. │
└─────────────┘
```
