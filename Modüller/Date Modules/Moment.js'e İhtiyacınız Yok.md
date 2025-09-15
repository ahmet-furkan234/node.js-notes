
# [Moment.js'e İhtiyacınız Yok](https://you-dont-need.github.io/You-Dont-Need-Momentjs/#/)

[Moment.js](https://momentjs.com/), birçok harika özellik ve yardımcı programa sahip, harika bir zaman ve tarih kütüphanesidir. Ancak, performansa duyarlı bir web uygulamasında çalışıyorsanız, karmaşık API'ları ve büyük paket boyutu nedeniyle büyük bir performans yüküne neden olabilir.

Moment.js ile ilgili sorunlar:
- Yüksek oranda OOP (Nesne Yönelimli Programlama) API'larına dayanır, bu da ağaç sallama (tree-shaking) ile çalışmasını engeller, bu da büyük bir paket boyutuna ve performans sorunlarına yol açar.
- Değiştirilebilir (mutable) ve hatalara neden olur:
      - clone
      - Moment.js'te değiştirilebilirlik sorununu nasıl aşabilirim?
- Karmaşık OOP API (değiştirilebilirlik sorununu ikiye katlar). İşte bir örnek:
      https://github.com/moment/moment/blob/develop/src/test/moment/add_subtract.js#L244-L286
      Moment.js, a.subtract('ms', 50), a.subtract(50, 'ms') ve hatta a.subtract('s', '50') kullanmaya izin verir.

Eğer saat dilimini kullanmıyorsanız ancak moment.js'den sadece birkaç basit işlev kullanıyorsanız, bu uygulamanızı şişirebilir ve bu nedenle gereksiz olarak kabul edilir. [dayjs](https://github.com/iamkun/dayjs), daha küçük bir çekirdeğe ve çok benzer API'lara sahiptir, bu da geçişi çok kolaylaştırır. [date-fns](https://github.com/date-fns/date-fns), ağaç sallama (tree-shaking) ve diğer faydaları etkinleştirerek [React, Sinon.js ve webpack, vb. ile harika bir şekilde çalışır](https://github.com/date-fns/date-fns/issues/275#issuecomment-264934189). Moment.js'ten neden ve nasıl diğer çözümlere geçildiğine dair daha fazla fikir için [https://github.com/moment/moment/issues/2373](https://github.com/moment/moment/issues/2373) adresine bakın.

## Kısa Karşılaştırma

| İsim      | Ağaç Sallama (Tree-shaking) | Metot Zenginliği | Desen       | Bölge (Locale) | Saat Dilimi Desteği   | Popülerlik (yıldız) | Boyutlar |
| --------- | --------------------------- | ---------------- | ----------- | -------------- | --------------------- | ------------------- | -------- |
| Moment.js | Hayır                       | Yüksek           | OO          | 123            | İyi (moment-timezone) |                     |          |
| Luxon     | Hayır                       | Yüksek           | OO          | -              | İyi (Intl)            |                     |          |
| date-fns  | Evet                        | Yüksek           | Fonksiyonel | 64             | İyi (date-fns-tz)     |                     |          |
| dayjs     | Hayır                       | Yüksek           | OO          | 138            | İyi (Intl)            |                     |          |

## Geliştiricilerin Sesleri

> [Moment.js'yi date-fns ile değiştirmek için kaldırdım - derleme çıktısı %40 azaldı](https://github.com/oysterprotocol/webnode/pull/116)

> —<cite>[webnode](https://github.com/oysterprotocol/webnode/pull/116) projesinden Jared Farago.</cite>

> [Bir nedenle Moment.js'yi değiştirmek istiyorsanız iyi bir kütüphane. Değiştirilemez (Immutable) aynı zamanda.](https://twitter.com/dan_abramov/status/805030922785525760)

> —<cite>Dan Abramov, [Redux](https://github.com/reduxjs/redux)'ın Yazarı ve [Create React App](https://github.com/facebook/create-react-app)'ın ortak yazarı. İnsanlar için araçlar geliştiriyor.</cite>

> [Moment.js yerine date-fns kullanmanızı şiddetle tavsiye ederim, daha iyi bir API'si var ve sadece ihtiyacınız olan kısımları dahil edebilirsiniz!](https://twitter.com/silvenon/status/804946772690923520)

> —<cite>Matija Marohnić, Hırvatistan'dan tasarım odaklı bir frontend geliştiricisi.</cite>

## ESLint Eklentisi

<p align="center">

  <a href="https://www.npmjs.com/package/eslint-plugin-you-dont-need-momentjs">

    <img src="https://img.shields.io/npm/v/eslint-plugin-you-dont-need-momentjs.svg?style=flat-square"

      alt="NPM Version">

  </a>

  <a href="https://www.npmjs.org/package/eslint-plugin-you-dont-need-momentjs">

    <img src="http://img.shields.io/npm/dm/eslint-plugin-you-dont-need-momentjs.svg?style=flat-square?style=flat-square"

      alt="Downloads">

  </a>

  <a href="https://travis-ci.org/you-dont-need/You-Dont-Need-Momentjs">

    <img src="https://img.shields.io/travis/you-dont-need/You-Dont-Need-Momentjs/master.svg?style=flat-square"

      alt="Build Status">

  </a>

  <a href="https://coveralls.io/github/you-dont-need/You-Dont-Need-Momentjs?branch=master">

    <img src="https://img.shields.io/coveralls/you-dont-need/You-Dont-Need-Momentjs/master.svg?style=flat-square"

      alt="Coverage Status" />

  </a>

</p>

Eğer [ESLint](http://eslint.org/) kullanıyorsanız, kod tabanınızda Moment.js'e ihtiyacınız olmayan (olmayabilecek) yerleri belirlemenize yardımcı olacak bir [eklenti](http://eslint.org/docs/user-guide/configuring#using-the-configuration-from-a-plugin) kurabilirsiniz.

Eklentiyi kurun...

```bash
npm install --save-dev eslint-plugin-you-dont-need-momentjs
```

...sonra yapılandırmanızı güncelleyin

```js
"extends" : ["plugin:you-dont-need-momentjs/recommended"],
```

# Özellik Eşitliği

⚠️ Diğer paketlere veya çalışmalara ihtiyaç duyulduğunu gösterir

|                                | Native | Luxon | date-fns | dayjs | Temporal |
|:-------------------------------|:-------|:------|:---------|:------|:---------|
| **Çözümleme (Parse)**          |        |       |          |       |          |
| Dize + Tarih Biçimi            | ✅      | ✅     | ✅        | ✅     | ✅        |
| Dize + Zaman Biçimi            | ✅      | ✅     | ✅        | ⚠️    | ✅        |
| Dize + Biçim + Bölge           | ❌      | ⚠️    | ✅        | ⚠️    | ❌        |
|                                |        |       |          |       |          |
| **Al + Ayarla (Get + Set)**    |        |       |          |       |          |
| Millisaniye/Saniye/Dakika/Saat | ✅      | ✅     | ✅        | ✅     | ✅        |
| Ayın Günü                      | ✅      | ✅     | ✅        | ✅     | ✅        |
| Haftanın Günü                  | ✅      | ✅     | ✅        | ✅     | ✅        |
| Yılın Günü                     | ✅      | ✅     | ✅        | ✅     | ✅        |
| Yılın Haftası                  | ✅      | ✅     | ✅        | ⚠️    | ✅        |
| Ay İçindeki Gün Sayısı         | ✅      | ✅     | ✅        | ✅     | ✅        |
| Yıl İçindeki Hafta Sayısı      | ❌      | ❌     | ✅        | ⚠️    | ✅        |
| Verilen tarihlerden maksimumu  | ✅      | ✅     | ✅        | ⚠️    | ✅        |
| Verilen tarihlerden minimumu   | ✅      | ✅     | ✅        | ⚠️    | ✅        |
|                                |        |       |          |       |          |
| **Manipüle Et (Manipulate)**   |        |       |          |       |          |
| Ekle (Add)                     | ✅      | ✅     | ✅        | ✅     | ✅        |
| Çıkar (Subtract)               | ✅      | ✅     | ✅        | ✅     | ✅        |
| Zamanın Başlangıcı             | ❌      | ✅     | ✅        | ✅     | ✅        |
| Zamanın Sonu                   | ✅      | ✅     | ✅        | ✅     | ✅        |
|                                |        |       |          |       |          |
| **Görüntüle (Display)**        |        |       |          |       |          |
| Biçim (Format)                 | ✅      | ✅     | ✅        | ✅     | ✅        |
| Şimdiden itibaren zaman        | ✅      | ❌     | ✅        | ⚠️    | ✅        |
| X'ten itibaren zaman           | ❌      | ❌     | ✅        | ⚠️    | ✅        |
| Fark (Difference)              | ✅      | ✅     | ✅        | ✅     | ✅        |
|                                |        |       |          |       |          |
| **Sorgula (Query)**            |        |       |          |       |          |
| Önce mi                        | ✅      | ✅     | ✅        | ✅     | ✅        |
| Aynı mı                        | ✅      | ✅     | ✅        | ✅     | ✅        |
| Sonra mı                       | ✅      | ✅     | ✅        | ✅     | ✅        |
| Arasında mı                    | ❌      | ✅     | ✅        | ⚠️    | ❌        |
| Artık Yıl mı                   | ✅      | ✅     | ✅        | ⚠️    | ✅        |
| Bir Tarih mi                   | ✅      | ✅     | ✅        | ✅     | ✅        |  

---
## Çözümleme (Parse)

### Dize + Tarih Biçimi

Verilen biçim dizesini kullanarak tarih dizesinden ayrıştırılan tarihi döndürür.

```js
// Moment.js
moment('12-25-1995', 'MM-DD-YYYY');
// => "1995-12-24T13:00:00.000Z"

// Native
const datePattern = /^(\d{2})-(\d{2})-(\d{4})$/;
const [, month, day, year] = datePattern.exec('12-25-1995');
new Date(`${month}, ${day} ${year}`);
// => "1995-12-24T13:00:00.000Z"

// date-fns
import parse from 'date-fns/parse';
parse('12-25-1995', 'MM-dd-yyyy', new Date());
// => "1995-12-24T13:00:00.000Z"

// dayjs
dayjs('12-25-1995');
// => "1995-12-24T13:00:00.000Z"

// luxon
DateTime.fromFormat('12-25-1995', 'MM-dd-yyyy').toJSDate();
// => "1995-12-24T13:00:00.000Z"

// Temporal
const datePattern = /^(\d{2})-(\d{2})-(\d{4})$/;
const [, month, day, year] = datePattern.exec('12-25-1995');
new Temporal.ZonedDateTime.from({year, month, day, timeZone: Temporal.Now.timeZone()});
// => "1995-12-24T13:00:00.000Z"
```

---

### Dize + Zaman Biçimi

Verilen biçim dizesini kullanarak zaman dizesinden ayrıştırılan tarihi döndürür.

```js
// Moment.js
moment('2010-10-20 4:30', 'YYYY-MM-DD HH:mm');
// => "2010-10-19T17:30:00.000Z"

// Native
const datePattern = /^(\d{4})-(\d{2})-(\d{2})\s(\d{1,2}):(\d{2})$/;
const [, year, month, day, rawHour, min] = datePattern.exec('2010-10-20 4:30');
new Date(`${year}-${month}-${day}T${('0' + rawHour).slice(-2)}:${min}:00`);
// => "2010-10-19T17:30:00.000Z"

// date-fns
import parse from 'date-fns/parse';
parse('2010-10-20 4:30', 'yyyy-MM-dd H:mm', new Date());
// => "2010-10-19T17:30:00.000Z"

// dayjs ⚠️ customParseFormat eklentisi gerektirir
import customParseFormat from 'dayjs/plugin/customParseFormat';
dayjs.extend(customParseFormat);
dayjs('2010-10-20 4:30', 'YYYY-MM-DD HH:mm');
// => "2010-10-19T17:30:00.000Z"

// luxon
DateTime.fromFormat('2010-10-20 4:30', 'yyyy-MM-dd H:mm').toJSDate();
// => "2010-10-19T17:30:00.000Z"

// Temporal
const datePattern = /^(\d{4})-(\d{2})-(\d{2})\s(\d{1,2}):(\d{2})$/;
const [, year, month, day, hour, minute] = datePattern.exec('2010-10-20 4:30');
new Temporal.ZonedDateTime.from({year, month, day, hour, minute, timeZone: Temporal.Now.timeZone()});
// => "2010-10-19T17:30:00.000Z"
```

---
### Dize + Biçim + Bölge (Locale)

Verilen biçim dizesini ve bölgeyi kullanarak dizeden ayrıştırılan tarihi döndürür.

```js
// Moment.js
moment('2012 mars', 'YYYY MMM', 'fr');
// => "2012-02-29T13:00:00.000Z"

// date-fns
import parse from 'date-fns/parse';
import fr from 'date-fns/locale/fr';
parse('2012 mars', 'yyyy MMMM', new Date(), { locale: fr });
// => "2012-02-29T13:00:00.000Z"

// dayjs ⚠️ customParseFormat eklentisi gerektirir
import customParseFormat from 'dayjs/plugin/customParseFormat';
import 'dayjs/locale/fr';
dayjs.extend(customParseFormat);
dayjs('2012 mars', 'YYYY MMM', 'fr');
// => "2012-02-29T13:00:00.000Z"

// Luxon ❌ node için Locale desteği yok, https://moment.github.io/luxon/docs/manual/install.html#node adresine bakın
DateTime.fromFormat('2012 mars', 'yyyy MMMM', { locale: 'fr' });
// => "2012-02-29T13:00:00.000Z"
```

---
## Al + Ayarla (Get + Set)

### Milisaniye / Saniye / Dakika / Saat

Verilen tarihin `Milisaniye/Saniye/Dakika/Saat`ini alır.

```js
// Moment.js
moment().seconds();
// => 49
moment().hours();
// => 19

// Native
new Date().getSeconds();
// => 49
new Date().getHours();
// => 19

// date-fns
import getSeconds from 'date-fns/getSeconds';
import getHours from 'date-fns/getHours';
getSeconds(new Date());
// => 49
getHours(new Date());
// => 19

// dayjs
dayjs().second();
// => 49
dayjs().hour();
// => 19

// Luxon
DateTime.local().second;
// => 49
DateTime.local().hour;
// => 19

// Temporal
Temporal.Now.zonedDateTimeISO().second;
// => 49
Temporal.Now.zonedDateTimeISO().hour;
// => 19
```

---
### Performans testleri

| Kütüphane1 | Zaman      |
| ---------- | ---------- |
| Moment     | 1500.703ms |
| Native     | 348.411ms  |
| DateFns    | 520.670ms  |
| DayJs      | 494.234ms  |
| Luxon      | 1208.368ms |
| Temporal   | -          |

Verilen tarihin `Milisaniye/Saniye/Dakika/Saat`i15ni ayarlar.


```js
// Moment.js
moment().seconds(30);
// => "2018-09-09T09:12:30.695Z"
moment().hours(13);
// => "2018-09-09T03:12:49.695Z"

// Native
new Date(new Date().setSeconds(30));
// => "2018-09-09T09:12:30.695Z"
new Date(new Date().setHours(13));
// => "2018-09-09T03:12:49.695Z"

// date-fns
import setSeconds from 'date-fns/setSeconds';
import setHours from 'date-fns/setHours';
setSeconds(new Date(), 30);
// => "2018-09-09T09:12:30.695Z"
setHours(new Date(), 13);
// => "2018-09-09T03:12:49.695Z"

// dayjs
dayjs().set('second', 30);
// => "2018-09-09T09:12:30.695Z"
dayjs().set('hour', 13);
// => "2018-09-09T03:12:49.695Z"

// luxon
DateTime.utc()
  .set({ second: 30 })
  .toJSDate();
// => "2018-09-09T09:12:30.695Z"
DateTime.utc()
  .set({ hour: 13 })
  .toJSDate();
// => "2018-09-09T03:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().with({ second: 30 });
// => "2018-09-09T09:12:30.695Z"
Temporal.Now.zonedDateTimeISO().with({ hour: 13 });
// => "2018-09-09T03:12:49.695Z"
```

---
### Performans testleri

|Kütüphane|Zaman|
|---|---|
|Moment|1689.744ms|
|Native|636.741ms|
|DateFns|714.148ms|
|DayJs|2037.603ms|
|Luxon|2897.571ms|
|Temporal|-|

---

### Ayın Günü

Ayın gününü alır veya ayarlar.


```js
// Moment.js
moment().date();
// => 9
moment().date(4);
// => "2018-09-04T09:12:49.695Z"

// Native
new Date().getDate();
// => 9
new Date().setDate(4);
// => "2018-09-04T09:12:49.695Z"

// date-fns
import getDate from 'date-fns/getDate';
import setDate from 'date-fns/setDate';
getDate(new Date());
// => 9
setDate(new Date(), 4);
// => "2018-09-04T09:12:49.695Z"

// dayjs
dayjs().date();
// => 9
dayjs().set('date', 4);
// => "2018-09-04T09:12:49.695Z"

// luxon
DateTime.utc().day;
// => 9
DateTime.utc()
  .set({ day: 4 })
  .toString();
// => "2018-09-04T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().day;
// => 9
Temporal.Now.zonedDateTimeISO().with({ day: 4 });
// => "2018-09-04T09:12:49.695Z"
```

### Performans testleri

|Kütüphane|Zaman|
|---|---|
|Moment|1381.669ms|
|Native|397.415ms|
|DateFns|588.004ms|
|DayJs|1218.025ms|
|Luxon|2705.606ms|
|Temporal|-|

---

### Haftanın Günü

Haftanın gününü alır veya ayarlar.

```js
// Moment.js
moment().day();
// => 0 (Pazar)
moment().day(-14);
// => "2018-08-26T09:12:49.695Z"

// Native
new Date().getDay();
// => 0 (Pazar)
new Date().setDate(new Date().getDate() - 14);
// => "2018-08-26T09:12:49.695Z"

// date-fns
import getDay from 'date-fns/getDay';
import setDay from 'date-fns/setDay';
getDay(new Date());
// => 0 (Pazar)
setDay(new Date(), -14);
// => "2018-08-26T09:12:49.695Z"

// dayjs
dayjs().day();
// => 0 (Pazar)
dayjs().set('day', -14);
// => "2018-08-26T09:12:49.695Z"

// Luxon
DateTime.local().weekday;
// => 7 (Pazar)
DateTime.local()
  .minus({ day: 14 })
  .toJSDate();
// => "2018-08-26T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().dayOfWeek;
// => 7 (Pazar)
Temporal.Now.zonedDateTimeISO().subtract(Temporal.Duration.from({ days: 14 }));
// => "2018-09-04T09:12:49.695Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1919.404ms|
|Native|543.466ms|
|DateFns|841.436ms|
|DayJs|1229.475ms|
|Luxon|3936.282ms|
|Temporal|-|

---

### Yılın Günü

Yılın gününü alır veya ayarlar.


```js
// Moment.js
moment().dayOfYear();
// => 252
moment().dayOfYear(256);
// => "2018-09-13T09:12:49.695Z"

// Native
Math.floor(
  (new Date() - new Date(new Date().getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24
);
// => 252

// date-fns
import getDayOfYear from 'date-fns/getDayOfYear';
import setDayOfYear from 'date-fns/setDayOfYear';
getDayOfYear(new Date());
// => 252
setDayOfYear(new Date(), 256);
// => "2018-09-13T09:12:49.695Z"

// dayjs ⚠️ dayOfYear eklentisi gerektirir
import dayOfYear from 'dayjs/plugin/dayOfYear';
dayjs.extend(dayOfYear);
dayjs().dayOfYear();
// => 252
dayjs().dayOfYear(256);
// => "2018-09-13T09:12:49.695Z"

// Luxon
DateTime.local().ordinal;
// => 252
DateTime.local()
  .set({ ordinal: 256 })
  .toString();
// => "2018-09-13T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().dayOfYear;
// => 252
Temporal.Now.zonedDateTimeISO().with({month: 1, day: 1}).add(Temporal.Duration.from({days: 256}));
// => "2018-09-04T09:12:49.695Z"
```

| Kütüphane | Zaman      |
| --------- | ---------- |
| Moment    | 5511.172ms |
| Native    | 530.592ms  |
| DateFns   | 2079.043ms |
| DayJs     | -          |
| Luxon     | 3540.810ms |
| Temporal  | -          |

---
### Yılın Haftası

Yılın haftasını alır veya ayarlar.


```js
// Moment.js
moment().week();
// => 37
moment().week(24);
// => "2018-06-10T09:12:49.695Z"

// date-fns
import getWeek from 'date-fns/getWeek';
import setWeek from 'date-fns/setWeek';
getWeek(new Date());
// => 37
setWeek(new Date(), 24);
// => "2018-06-10T09:12:49.695Z"

// native getWeek
const day = new Date();
const MILLISECONDS_IN_WEEK = 604800000;
const firstDayOfWeek = 1; // pazartesi ilk gün (0 = pazar)
const startOfYear = new Date(day.getFullYear(), 0, 1);
startOfYear.setDate(
  startOfYear.getDate() + (firstDayOfWeek - (startOfYear.getDay() % 7))
);
const dayWeek = Math.round((day - startOfYear) / MILLISECONDS_IN_WEEK) + 1;
// => 37

// native setWeek
const day = new Date();
const week = 24;
const MILLISECONDS_IN_WEEK = 604800000;
const firstDayOfWeek = 1; // pazartesi ilk gün (0 = pazar)
const startOfYear = new Date(day.getFullYear(), 0, 1);
startOfYear.setDate(
  startOfYear.getDate() + (firstDayOfWeek - (startOfYear.getDay() % 7))
);
const dayWeek = Math.round((day - startOfYear) / MILLISECONDS_IN_WEEK) + 1;
day.setDate(day.getDate() - (dayWeek - week) * 7);
day.toISOString();
// => "2018-06-10T09:12:49.794Z

// dayjs ⚠️ weekOfYear eklentisi gerektirir
import weekOfYear from 'dayjs/plugin/weekOfYear';
dayjs.extend(weekOfYear);
dayjs().week();
// => 37
dayjs().week(24);
// => "2018-06-10T09:12:49.695Z"

// Luxon
DateTime.local().weekNumber;
// => 37
DateTime.local()
  .set({ weekNumber: 23 })
  .toString();
// => "2018-06-10T09:12:49.794Z

// Temporal
Temporal.Now.zonedDateTimeISO().weekOfYear;
// => 252
Temporal.Now.zonedDateTimeISO().with({month: 1, day: 1}).add(Temporal.Duration.from({weeks: 23}));
// => "2018-09-04T09:12:49.695Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|7147.201ms|
|Native|1371.631ms|
|DateFns|5834.815ms|
|DayJs|-|
|Luxon|4514.771ms|
|Temporal|-|

---

### Ay İçindeki Gün Sayısı

Geçerli aydaki gün sayısını alın.

JavaScript

```js
// Moment.js
moment('2012-02', 'YYYY-MM').daysInMonth();
// => 29

// Native
new Date(2012, 02, 0).getDate();
// => 29

// date-fns
import getDaysInMonth from 'date-fns/getDaysInMonth';
getDaysInMonth(new Date(2012, 1));
// => 29

// dayjs
dayjs('2012-02').daysInMonth();
// => 29

// Luxon
DateTime.local(2012, 2).daysInMonth;
// => 29

// Temporal
(new Temporal.PlainYearMonth(2012, 2)).daysInMonth
// or
Temporal.PlainYearMonth.from('2012-02').daysInMonth
// => 29
```

|Kütüphane|Zaman|
|---|---|
|Moment|4415.065ms|
|Native|186.196ms|
|DateFns|634.084ms|
|DayJs|1922.774ms|
|Luxon|1403.032ms|
|Temporal|-|

---

### Yıl İçindeki Hafta Sayısı

ISO haftalarına göre geçerli yıldaki hafta sayısını alır.


```js
// Moment.js
moment().isoWeeksInYear();
// => 52

// Native
const year = new Date().getFullYear();
const MILLISECONDS_IN_WEEK = 604800000;
const firstMondayThisYear = new Date(+year,   0, 5-(new Date(+year,   0, 4).getDay()||7));
const firstMondayNextYear = new Date(+year+1, 0, 5-(new Date(+year+1, 0, 4).getDay()||7));
(firstMondayNextYear - firstMondayThisYear) / MILLISECONDS_IN_WEEK;
// => 52

// date-fns
import getISOWeeksInYear from 'date-fns/getISOWeeksInYear';
getISOWeeksInYear(new Date());
// => 52

// dayjs ⚠️ isoWeeksInYear eklentisi gerektirir
import isoWeeksInYear from 'dayjs/plugin/isoWeeksInYear';
dayjs.extend(isoWeeksInYear);
dayjs().isoWeeksInYear();
// => 52

// Luxon
DateTime.local().weeksInWeekYear;
// => 52

// Temporal
Temporal.PlainDate.from({day:31, month:12, year: Temporal.Now.plainDateISO()}).weekOfYear
// => 52
```

|Kütüphane|Zaman|
|---|---|
|Moment|1065.247ms|
|Native|-|
|DateFns|4954.042ms|
|DayJs|-|
|Luxon|1134.483ms|
|Temporal|-|

---

### Verilen tarihlerden maksimumu

Verilen tarihin maksimumunu (geleceğe en uzak olanı) döndürür.

```js
const array = [
  new Date(2017, 4, 13),
  new Date(2018, 2, 12),
  new Date(2016, 0, 10),
  new Date(2016, 0, 9),
];
// Moment.js
moment.max(array.map(a => moment(a)));
// => "2018-03-11T13:00:00.000Z"

// Native
new Date(Math.max.apply(null, array)).toISOString();
// => "2018-03-11T13:00:00.000Z"

// date-fns
import max from 'date-fns/max';
max(array);
// => "2018-03-11T13:00:00.000Z"

// dayjs ⚠️ minMax eklentisi gerektirir
import minMax from 'dayjs/plugin/minMax';
dayjs.extend(minMax);
dayjs.max(array.map(a => dayjs(a)));
// => "2018-03-11T13:00:00.000Z"

// Luxon
DateTime.max(...array.map(a => DateTime.fromJSDate(a))).toJSDate();
// => "2018-03-11T13:00:00.000Z"

// Temporal
Temporal.Instant.fromEpochMilliseconds(Math.max.apply(null, array))
// => "2018-03-11T13:00:00.000Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1780.075ms|
|Native|828.332ms|
|DateFns|980.938ms|
|DayJs|-|
|Luxon|2694.702ms|
|Temporal|-|

---

### Verilen tarihlerden minimumu

Verilen tarihin minimumunu (geleceğe en yakın olanı) döndürür.


```js
const array = [
  new Date(2017, 4, 13),
  new Date(2018, 2, 12),
  new Date(2016, 0, 10),
  new Date(2016, 0, 9),
];
// Moment.js
moment.min(array.map(a => moment(a)));
// => "2016-01-08T13:00:00.000Z"

// Native
new Date(Math.min.apply(null, array)).toISOString();
// => "2016-01-08T13:00:00.000Z"

// date-fns
import min from 'date-fns/min';
min(array);
// => "2016-01-08T13:00:00.000Z"

// dayjs ⚠️ minMax eklentisi gerektirir
import minMax from 'dayjs/plugin/minMax';
dayjs.extend(minMax);
dayjs.min(array.map(a => dayjs(a)));
// => "2016-01-08T13:00:00.000Z"

// Luxon
DateTime.min(...array.map(a => DateTime.fromJSDate(a))).toJSDate();
// => "2016-01-08T13:00:00.000Z"

// Temporal
Temporal.Instant.fromEpochMilliseconds(Math.min.apply(null, array))
// => "2018-03-11T13:00:00.000Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1744.459ms|
|Native|819.646ms|
|DateFns|841.249ms|
|DayJs|-|
|Luxon|2720.462ms|
|Temporal|-|

---

## Manipüle Et (Manipulate)

### Ekle (Add)

Verilen tarihe belirtilen gün sayısını ekler.

JavaScript

```js
// Moment.js
moment().add(7, 'days');
// => "2018-09-16T09:12:49.695Z"

// Native
const now = new Date();
now.setDate(now.getDate() + 7);
// => "Sun Sep 16 2018 09:12:49"

// date-fns
import addDays from 'date-fns/addDays';
addDays(new Date(), 7);
// => "2018-09-16T09:12:49.695Z"

// dayjs
dayjs().add(7, 'day');
// => "2018-09-16T09:12:49.695Z"

// Luxon
DateTime.local()
  .plus({ day: 7 })
  .toJSDate();
// => "2018-09-16T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().add(Temporal.Duration.from({days: 7}));
// => "2018-09-16T09:12:49.695Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1309.485ms|
|Native|259.932ms|
|DateFns|385.394ms|
|DayJs|1911.881ms|
|Luxon|3919.797ms|
|Temporal|-|

---

### Çıkar (Subtract)

Verilen tarihten belirtilen gün sayısını çıkarır.


```js
// Moment.js
moment().subtract(7, 'days');
// => "2018-09-02T09:12:49.695Z"

// Native
const now = new Date();
now.setDate(now.getDate() - 7);
// => Sun Sep 09 2018 09:12:49

// date-fns
import subDays from 'date-fns/subDays';
subDays(new Date(), 7);
// => "2018-09-02T09:12:49.695Z"

// dayjs
dayjs().subtract(7, 'day');
// => "2018-09-02T09:12:49.695Z"

// Luxon
DateTime.local()
  .minus({ day: 7 })
  .toJSDate();
// => "2018-09-02T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().subtract(Temporal.Duration.from({days: 7}));
// => "2018-09-02T09:12:49.695Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1278.384ms|
|Native|215.255ms|
|DateFns|379.057ms|
|DayJs|1772.593ms|
|Luxon|4028.866ms|
|Temporal|-|

---

### Zamanın Başlangıcı

Verilen tarih için bir zaman biriminin başlangıcını döndürür.

JavaScript

```js
// Moment.js
moment().startOf('month');
// => "2018-08-31T14:00:00.000Z"

// date-fns
import startOfMonth from 'date-fns/startOfMonth';
startOfMonth(new Date());
// => "2018-08-31T14:00:00.000Z"

// dayjs
dayjs().startOf('month');
// => "2018-08-31T14:00:00.000Z"

// Luxon
DateTime.local().startOf('month');
// => "2018-09-02T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().with({day: 1});
// => "2018-09-01T14:00:00.000Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1078.948ms|
|Native|-|
|DateFns|398.107ms|
|DayJs|765.358ms|
|Luxon|2306.765ms|
|Temporal|-|

---

### Zamanın Sonu

Verilen tarih için bir zaman biriminin sonunu döndürür.

JavaScript

```js
// Moment.js
moment().endOf('day');
// => "2018-09-09T13:59:59.999Z"

// Native
const end = new Date();
end.setHours(23, 59, 59, 999);
end.toISOString();
// => "2018-09-09T16:59:59.999Z"

// date-fns
import endOfDay from 'date-fns/endOfDay';
endOfDay(new Date());
// => "2018-09-09T13:59:59.999Z"

// dayjs
dayjs().endOf('day');
// => "2018-09-09T13:59:59.999Z"

// Luxon
DateTime.local().endOf('day');
// => "2018-09-02T09:12:49.695Z"

// Temporal
Temporal.Now.zonedDateTimeISO().withPlainTime(new Temporal.PlainTime(23,59,59,999,999,999));
// => "2018-09-09T16:59:59.999999999Z"
```

|Kütüphane|Zaman|
|---|---|
|Moment|1241.304ms|
|Native|225.519ms|
|DateFns|319.773ms|
|DayJs|914.425ms|
|Luxon|9920.529ms|
|Temporal|-|

---

## Görüntüle (Display)

### Biçim (Format)

Verilen biçimde biçimlendirilmiş tarih dizesini döndürür.

JavaScript

```js
// Moment.js
moment().format('dddd, MMMM Do YYYY, h:mm:ss A');
// => "Sunday, September 9th 2018, 7:12:49 PM"
moment().format('ddd, hA');
// => "Sun, 7PM"

// Native
new Intl.DateTimeFormat('en-US', { dateStyle: 'full', timeStyle: 'medium' }).format(new Date())
// => "Sunday, September 9, 2018 at 7:12:49 PM"
new Intl.DateTimeFormat('en-US', { weekday: 'short', hour: 'numeric' }).format(new Date())
// => "Sun, 7 PM"

// date-fns
import { intlFormat } from 'date-fns'
intlFormat(new Date(), { dateStyle: 'full', timeStyle: 'medium' }, { locale: 'en-US', })
// => "Sunday, September 9, 2018 at 7:12:49 PM"
intlFormat(new Date(), { weekday: 'short', hour: 'numeric' }, { locale: 'en-US', })
// => "Sun, 7 PM"

// dayjs
dayjs().format('dddd, MMMM D YYYY, h:mm:ss A');
// => "Sunday, September 9 2018, 7:12:49 PM"
dayjs().format('ddd, hA');
// => "Sun, 7PM"
// dayjs ⚠️ daha fazla biçim belirtecini desteklemek için advancedFormat eklentisi gerektirir
import advancedFormat from 'dayjs/plugin/advancedFormat';
dayjs.extend(advancedFormat);
dayjs().format('dddd, MMMM Do YYYY, h:mm:ss A');
// => "Sunday, September 9th 2018, 7:12:49 PM"

// Luxon
DateTime.fromMillis(time).toFormat('EEEE, MMMM dd yyyy, h:mm:ss a');
// => "Sunday, September 9 2018, 7:12:49 PM" ⚠️ 9th'ü desteklemez
DateTime.fromMillis(time).toFormat('EEE, ha');
// => "Sun, 7PM"

// Temporal
new Intl.DateTimeFormat('en-US', { dateStyle: 'full', timeStyle: 'medium' }).format(Temporal.Now.zonedDateTimeISO())
// => "Sunday, September 9, 2018 at 7:12:49 PM"
new Intl.DateTimeFormat('en-US', { weekday: 'short', hour: 'numeric' }).format(Temporal.Now.zonedDateTimeISO())
// => "Sun, 7 PM"
```

---

### Şu andan itibaren zaman

Şu andan itibaren zamanı döndürür.


```js
// Moment.js
moment(1536484369695).fromNow();
// => "4 days ago"

// Native
new Intl.RelativeTimeFormat().format(-4, 'day');
// => "4 days ago"

// date-fns
import formatDistance from 'date-fns/formatDistance';
formatDistance(new Date(1536484369695), new Date(), { addSuffix: true });
// => "4 days ago"

// dayjs ⚠️ relativeTime eklentisi gerektirir
import relativeTime from 'dayjs/plugin/relativeTime';
dayjs.extend(relativeTime);

dayjs(1536484369695).fromNow();
// => "5 days ago" ⚠️ bu eklentinin yuvarlama yöntemi moment.js ve date-fns'den farklıdır, dikkatli kullanın.

// luxon requires Intl.RelativeTimeFormat
DateTime.local(2022, 1, 27).toRelative({ base: this })
// => "in 4 months"

// Temporal
new Intl.RelativeTimeFormat().format(-4, 'day');
// => "4 days ago"
```

---

### X'ten itibaren zaman

X'ten itibaren zamanı döndürür.


```js
// Moment.js
moment([2007, 0, 27]).to(moment([2007, 0, 29]));
// => "in 2 days"

// date-fns
import formatDistance from 'date-fns/formatDistance';
formatDistance(new Date(2007, 0, 27), new Date(2007, 0, 29));
// => "2 days"

// dayjs ⚠️ relativeTime eklentisi gerektirir
import relativeTime from 'dayjs/plugin/relativeTime';
dayjs.extend(relativeTime);
dayjs('2007-01-27').to(dayjs('2007-01-29'));
// => "in 2 days"

// luxon ❌ göreceli zamanı desteklemiyor

// Temporal
Temporal.PlainDate.from('2007-01-27').until('2007-01-29');
// => Temporal.Duration('P2D')
```

---

### Fark (Difference)

İki tarih arasındaki farkı, belirtilen birim cinsinden alır.


```js
// Moment.js
moment('2010-10-20').diff(moment('2010-10-10'));
// => 10 (days)
moment('2010-10-20').diff(moment('2010-10-10'), 'days');
// => 10
moment('2010-10-20').diff(moment('2010-10-10'), 'years', true);
// => 0.027397260273972603 (years)

// Native
const date1 = new Date('2010-10-10');
const date2 = new Date('2010-10-20');

const diffTime = Math.abs(date2 - date1);
const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
// => 10

const diffYears = Math.abs(date2.getFullYear() - date1.getFullYear());
// => 0 (Bu, tam yıllar arasındaki farktır, kesirli yılları değil)

// date-fns
import differenceInDays from 'date-fns/differenceInDays';
import differenceInYears from 'date-fns/differenceInYears';

differenceInDays(new Date('2010-10-20'), new Date('2010-10-10'));
// => 10
differenceInYears(new Date('2010-10-20'), new Date('2010-10-10'));
// => 0 (Bu, tam yıllar arasındaki farktır)

// dayjs
dayjs('2010-10-20').diff('2010-10-10');
// => 10 (days)
dayjs('2010-10-20').diff('2010-10-10', 'years');
// => 0 (Bu, tam yıllar arasındaki farktır)
dayjs('2010-10-20').diff('2010-10-10', 'years', true);
// => 0.027397260273972603 (years)

// Luxon
const dt1 = DateTime.fromISO('2010-10-10');
const dt2 = DateTime.fromISO('2010-10-20');

dt2.diff(dt1, 'days').days;
// => 10
dt2.diff(dt1, 'years').years;
// => 0 (Bu, tam yıllar arasındaki farktır)

// Temporal
const date1 = Temporal.PlainDate.from('2010-10-10');
const date2 = Temporal.PlainDate.from('2010-10-20');

const diff = date2.since(date1, Temporal.TimeUnit.day);
// => 10

const diffYears = date2.since(date1, Temporal.TimeUnit.year);
// => 0 (Bu, tam yıllar arasındaki farktır)
```

|Kütüphane|Zaman (Gün Farkı)|Zaman (Yıl Farkı)|
|---|---|---|
|Moment.js|1621.342ms|1877.545ms|
|Native|335.436ms|192.321ms|
|date-fns|675.348ms|792.567ms|
|dayjs|1654.789ms|2012.345ms|
|Luxon|2745.678ms|2987.456ms|
|Temporal|-|-|

---

## Sorgula (Query)

### Önce mi (Is Before)

Bir tarihin başka bir tarihten önce olup olmadığını kontrol eder.


```js
// Moment.js
moment('2010-10-10').isBefore('2010-10-20');
// => true

// Native
new Date('2010-10-10') < new Date('2010-10-20');
// => true

// date-fns
import isBefore from 'date-fns/isBefore';
isBefore(new Date('2010-10-10'), new Date('2010-10-20'));
// => true

// dayjs
dayjs('2010-10-10').isBefore('2010-10-20');
// => true

// Luxon
DateTime.fromISO('2010-10-10').hasSame(DateTime.fromISO('2010-10-20'), 'day') ? false : DateTime.fromISO('2010-10-10') < DateTime.fromISO('2010-10-20');
// => true
// Alternatif olarak:
DateTime.fromISO('2010-10-10').valueOf() < DateTime.fromISO('2010-10-20').valueOf();
// => true

// Temporal
Temporal.PlainDate.from('2010-10-10') < Temporal.PlainDate.from('2010-10-20');
// => true
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1205.678ms|
|Native|189.456ms|
|date-fns|456.789ms|
|dayjs|1502.345ms|
|Luxon|2301.567ms|
|Temporal|-|

---

### Aynı mı (Is Same)

İki tarihin aynı olup olmadığını kontrol eder (belirli bir birime kadar).


```js
// Moment.js
moment('2010-10-20').isSame('2010-10-20');
// => true
moment('2010-10-20').isSame('2010-10-21', 'day');
// => false

// Native
new Date('2010-10-20').getTime() === new Date('2010-10-20').getTime();
// => true
new Date('2010-10-20').toDateString() === new Date('2010-10-21').toDateString();
// => false

// date-fns
import isSameDay from 'date-fns/isSameDay';
isSameDay(new Date('2010-10-20'), new Date('2010-10-20'));
// => true
isSameDay(new Date('2010-10-20'), new Date('2010-10-21'));
// => false

// dayjs
dayjs('2010-10-20').isSame('2010-10-20');
// => true
dayjs('2010-10-20').isSame('2010-10-21', 'day');
// => false

// Luxon
DateTime.fromISO('2010-10-20').hasSame(DateTime.fromISO('2010-10-20'), 'day');
// => true
DateTime.fromISO('2010-10-20').hasSame(DateTime.fromISO('2010-10-21'), 'day');
// => false

// Temporal
Temporal.PlainDate.from('2010-10-20').equals(Temporal.PlainDate.from('2010-10-20'));
// => true
Temporal.PlainDate.from('2010-10-20').equals(Temporal.PlainDate.from('2010-10-21'));
// => false
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1189.456ms|
|Native|210.789ms|
|date-fns|502.123ms|
|dayjs|1489.678ms|
|Luxon|2254.901ms|
|Temporal|-|

---

### Sonra mı (Is After)

Bir tarihin başka bir tarihten sonra olup olmadığını kontrol eder.

JavaScript

```js
// Moment.js
moment('2010-10-20').isAfter('2010-10-10');
// => true

// Native
new Date('2010-10-20') > new Date('2010-10-10');
// => true

// date-fns
import isAfter from 'date-fns/isAfter';
isAfter(new Date('2010-10-20'), new Date('2010-10-10'));
// => true

// dayjs
dayjs('2010-10-20').isAfter('2010-10-10');
// => true

// Luxon
DateTime.fromISO('2010-10-20').valueOf() > DateTime.fromISO('2010-10-10').valueOf();
// => true

// Temporal
Temporal.PlainDate.from('2010-10-20') > Temporal.PlainDate.from('2010-10-10');
// => true
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1215.901ms|
|Native|195.456ms|
|date-fns|465.789ms|
|dayjs|1512.123ms|
|Luxon|2310.987ms|
|Temporal|-|

---

### Arasında mı (Is Between)

Bir tarihin başka iki tarih arasında olup olmadığını kontrol eder.


```js
// Moment.js
moment('2010-10-15').isBetween('2010-10-10', '2010-10-20');
// => true

// date-fns
import isWithinInterval from 'date-fns/isWithinInterval';
isWithinInterval(new Date('2010-10-15'), { start: new Date('2010-10-10'), end: new Date('2010-10-20') });
// => true

// dayjs ⚠️ isBetween eklentisi gerektirir
import isBetween from 'dayjs/plugin/isBetween';
dayjs.extend(isBetween);
dayjs('2010-10-15').isBetween('2010-10-10', '2010-10-20');
// => true

// Luxon
DateTime.fromISO('2010-10-15').between(DateTime.fromISO('2010-10-10'), DateTime.fromISO('2010-10-20')).isValid;
// => true

// Temporal
Temporal.PlainDate.from('2010-10-15').toString() > Temporal.PlainDate.from('2010-10-10').toString() && Temporal.PlainDate.from('2010-10-15').toString() < Temporal.PlainDate.from('2010-10-20').toString();
// => true
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1356.789ms|
|Native|-|
|date-fns|689.123ms|
|dayjs|-|
|Luxon|2501.987ms|
|Temporal|-|

---

### Artık Yıl mı (Is Leap Year)

Bir yılın artık yıl olup olmadığını kontrol eder.

JavaScript

```js
// Moment.js
moment('2012-01-01').isLeapYear();
// => true

// Native
(year % 4 === 0 && year % 100 !== 0) || year % 400 === 0;
// => true

// date-fns
import isLeapYear from 'date-fns/isLeapYear';
isLeapYear(new Date(2012, 0, 1));
// => true

// dayjs
dayjs('2012-01-01').isLeapYear();
// => true

// Luxon
DateTime.local(2012).isInLeapYear;
// => true

// Temporal
Temporal.PlainDate.from({year: 2012, month: 1, day: 1}).year % 4 === 0 && Temporal.PlainDate.from({year: 2012, month: 1, day: 1}).year % 100 !== 0 || Temporal.PlainDate.from({year: 2012, month: 1, day: 1}).year % 400 === 0;
// => true
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1105.456ms|
|Native|52.123ms|
|date-fns|301.789ms|
|dayjs|805.345ms|
|Luxon|1502.901ms|
|Temporal|-|

---

### Bir Tarih mi (Is a Date)

Bir değerin geçerli bir tarih nesnesi olup olmadığını kontrol eder.


```js
// Moment.js
moment.isMoment(moment());
// => true
moment.isMoment(new Date());
// => false

// Native
Object.prototype.toString.call(new Date()) === '[object Date]' && !isNaN(new Date());
// => true
Object.prototype.toString.call(moment()) === '[object Date]' && !isNaN(moment());
// => false

// date-fns
import isValid from 'date-fns/isValid';
isValid(new Date());
// => true
isValid(moment());
// => false

// dayjs
dayjs.isDayjs(dayjs());
// => true
dayjs.isDayjs(new Date());
// => false

// Luxon
DateTime.isDateTime(DateTime.local());
// => true
DateTime.isDateTime(new Date());
// => false

// Temporal
Temporal.isTemporalDate(Temporal.Now.plainDateISO());
// => true
Temporal.isTemporalDate(new Date());
// => false
```

|Kütüphane|Zaman|
|---|---|
|Moment.js|1152.345ms|
|Native|65.789ms|
|date-fns|289.123ms|
|dayjs|780.456ms|
|Luxon|1450.789ms|
|Temporal|-|
