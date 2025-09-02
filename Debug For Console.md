Tabii TkMatE! **CMD (Command Prompt) üzerinde Node.js debug yapmak** için birkaç farklı yöntem var. Aşağıda en pratik ve yaygın kullanılan yöntemleri adım adım anlatıyorum.

---

# CMD Üzerinde Node.js Debug Nasıl Yapılır?

---

## 1. **Node.js Komut Satırı Debugger Kullanmak (`node inspect`)**

Node.js kendi içinde basit bir komut satırı debugger sağlar.

### Adımlar:

1. CMD aç.
2. Debug yapmak istediğin dosyayı şu komutla çalıştır:

```bash
node inspect app.js
```

3. Program çalışmaya başlar, ilk satıra gelir ve komut satırı debugger aktif olur.

---

### Temel Komutlar:

|Komut|Açıklama|
|---|---|
|`c`|Devam et, breakpoint’e kadar gider|
|`n`|Sonraki satıra geç (step over)|
|`s`|Fonksiyon içine gir (step into)|
|`o`|Fonksiyondan çık (step out)|
|`repl`|Debug konsolu aç, interaktif kod yaz|
|`watch(expr)`|Belirli bir ifadeyi izle|
|`setBreakpoint()`|Breakpoint koy|

---

### Örnek:

```bash
> node inspect app.js
```

Çıktı şöyle olur:

```
< Debugger listening on ws://127.0.0.1:9229/...
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in app.js:1
> 1 (function() {
```

Burada:

- `n` yazarak satır satır ilerlersin
- `c` yazarak devam edersin
- `repl` ile anlık JS kodu çalıştırabilirsin

---

## 2. **`debugger;` Satırı Koyup `--inspect-brk` ile Başlatmak**

Kodunun istediğin satırına `debugger;` koy.

CMD’den şu komutla başlat:

```bash
node --inspect-brk app.js
```

Bu komut programı başlatır ve `debugger;` satırında durur.

---

## 3. **Chrome DevTools ile Debug (CMD’den Başlatılır)**

CMD’de şunu yaz:

```bash
node --inspect app.js
```

Sonra Chrome tarayıcıda:

```
chrome://inspect
```

adresine git ve “Open dedicated DevTools for Node” tıkla.

Buradan kodu adım adım debug edebilirsin.

---

## 4. **Örnek Basit Debug Komutları**

CMD’de çalıştırdın:

```bash
node inspect app.js
```

Terminale şu komutları yazabilirsin:

```bash
n      # Next - sonraki satır
c      # Continue - devam et
s      # Step into - fonksiyon içine gir
o      # Step out - fonksiyondan çık
repl   # Konsol aç, JS yaz çalıştır
watch('a + b') # İfadeyi izle
```

---

## Özet

|Yöntem|Komut / Açıklama|
|---|---|
|Komut Satırı Debugger|`node inspect app.js`|
|Debugger ile durma (breakpoint)|Kod içine `debugger;` koy, `node --inspect-brk app.js`|
|Chrome DevTools ile Debug|`node --inspect app.js` + `chrome://inspect`|
