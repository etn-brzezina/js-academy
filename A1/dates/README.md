# Datum (a čas)

- Objekt `Date` slouží k práci s datem a časem
- Datum je určeno jako počet uběhlých milisekund od 1. ledna 1970

```js
var date = new Date();

console.info(date); // => Wed Jul 18 2018 01:00:00 GMT+0100 (Středoevropský letní čas)
```

## Vytvoření date/time objektu

Máme celkem čtyři možnost jak vytvořit datum/čas

```js
new Date()
new Date(year, month, day, hours, minutes, seconds, milliseconds)
new Date(milliseconds)
new Date(date string)
```

```js
var date = new Date(1999999999999); // počet uběhlých milisekund od 1. ledna 1970

console.info(date); // => Wed May 18 2033 05:33:19 GMT+0200 (Středoevropský letní čas)
```

## Převod řetězce na datum

```js
var msec = Date.parse("March 21, 2012");
var d = new Date(msec);

console.info(d); // => Wed Mar 21 2012 00:00:00 GMT+0100 (Středoevropský standardní čas)
```

### Vstupní formáty

JavaScript v základu rozumí třem různém formátům data a času

| Typ                             | Ukázka                         |
| ------------------------------- | ------------------------------ |
| ISO date (mezinárodní standard) | "2015-03-25T12:00:00Z"         |
| Short Date                      | "03/25/2015"                   |
| Long Date                       | "Mar 25 2015" or "25 Mar 2015" |

_ISO formát v JavaScriptu podléhá přísné specifikaci, ostatní formáty se můžou v různých prohlížečích chovat nepředvídatelně_

### Výstupní formát

Nezávisle na vstupním formátu JavaScript při převodu data na string vždy vrátí výsledek v následujícím formátu

`Wed Mar 25 2015 01:00:00 GMT+0100 (Středoevropský standardní čas)`

## Get metody

| Meotda            | Popis                                                    |
| ----------------- | -------------------------------------------------------- |
| getFullYear()     | Vrátí rok v čtyřčíselném formátu (yyyy)                  |
| getMonth()        | Vrátí měsíc jako číslo (0-11)                            |
| getDate()         | Vrátí den jako číslo (1-31)                              |
| getDay()          | Vrátí den v týdnu jako číslo                             |
| getHours()        | Vrátí hodinu (0-23)                                      |
| getMinutes()      | Vrátí minuty (0-59)                                      |
| getSeconds()      | Vrátí sekundy (0-59)                                     |
| getMilliseconds() | Vrátí milisekundy (0-999)                                |
| getTime()         | Vrátí "čas" - počet uběhlých milisekund od 1. ledna 1970 |

## Set metody

| Meotda            | Popis                                                      |
| ----------------- | ---------------------------------------------------------- |
| setDate()         | Vrátí den jako číslo (1-31)                                |
| setFullYear()     | Nastaví rok (volitelně i měsíc a den)                      |
| setHours()        | Nastaví hodiny (0-11)                                      |
| setMilliseconds() | Nastaví milisekundy (0-999)                                |
| setMinutes()      | Nastaví minuty (0-23)                                      |
| setMonth()        | Nastaví měsíc (0-11)                                       |
| setSeconds()      | Nastaví sekundy (0-59)                                     |
| setTime()         | Nastaví "čas" - počet uběhlých milisekund od 1. ledna 1970 |

## Porovnávání dat a času

```js
var today, someday, text;
today = new Date();
someday = new Date();
someday.setFullYear(2100, 0, 14);

if (someday > today) {
  text = "Today is before January 14, 2100.";
} else {
  text = "Today is after January 14, 2100.";
}

console.info(text); // => Today is before January 14, 2100.
```

## Intervaly

Pokud chceme zjsitit kolik času uběhlo mezi dvěma Date objekty, stačí je odečíst

```js
var today, someday;
today = new Date();
someday = new Date();
someday.setFullYear(2100, 0, 14);

console.info(someday - today); // => 4103601685058
```

_Počet milisekund nám je ale v praxi opět k ničemu_

## Převod intervalu na string

Bohužel JavaScript nativně nemá funkci, která dokáže převést počet milisekund na časový interval (např. **2 měsíce, 1 týden, 2 dny, 7 hodin, 20 minut**)

```js
var daysCount = [31,28,31,30,31,30,31,31,30,31,30,31];

function yearDiff(d1, d2) {
  years = d1.getFullYear() - (d2.getFullYear() + 1);
  years = years < 0 ? 0 : years;
  
  return years;
}
function monthDiff(d1, d2) {
  months =
    d1.getFullYear() == d2.getFullYear()
      ? d1.getMonth() - 1 - d2.getMonth()
      : d1.getMonth() + (12 - (d2.getMonth() + 1));
  if (months >= 12) {
    years = years + Math.floor(months / 12);
    months = months % 12;
  }
  
  return months;
}
function isLeapYear(year) {
  return (year % 4 === 0 && year % 100 !== 0) || year % 400 === 0;
}
function getAdjustedDays(d) {
  var adjustedDays = 0;
  for (i = d.getMonth() + 1; i <= 12; i++) {
    if (daysCount[i] == 31) {
      adjustedDays++;
    }
  }
  return adjustedDays;
}
function daysDiff(d1, d2) {
  var month = d2.getMonth();
  if (month == 1 && months === 0 && years === 0) {
    days = d1.getDate() - d2.getDate();
  } else if (month == 1) {
    days =
      (isLeapYear(d2.getFullYear()) ? 29 - d2.getDate() : 28 - d2.getDate()) +
      d1.getDate() +
      (d2.getDate() == d1.getDate() ? 1 : 2);
    days = Math.ceil(days - getAdjustedDays(d2) / 2);
  } else {
    days =
      daysCount[month] -
      d2.getDate() +
      d1.getDate() +
      (d2.getMonth() == d1.getMonth() ? 2 : 1);
    days = Math.ceil(days - getAdjustedDays(d2) / 2);
  }
  if (days >= 30) {
    months = months + Math.floor(days / 30); //averge are 30 days
    days = days % 30;
  }
  
  return days;
}
function hourDiff(d1, d2) {
  hours = d1.getHours() - (d2.getHours() + 1);
  hours = hours < 0 ? 0 : hours;
  
  return hours;
}
function minuteDiff(d1, d2) {
  minutes = d1.getMinutes() - (d2.getMinutes() + 1);
  minutes = minutes < 0 ? 0 : minutes;
  
  return minutes;
}
function secondDiff(d1, d2) {
  second = d1.getSeconds() - (d2.getSeconds() + 1);
  second = second < 0 ? 0 : second;
  
  return second;
}

function getInterval(d1, d2) {
  var date, dateToCompare;
  
  if(d1 > d2) {
    date = d1;
    dateToCompare = d2;
  }
  
  else {
    date = d2;
    dateToCompare = d1;
  }
  
  return {
    years: yearDiff(date, dateToCompare),
    months: monthDiff(date, dateToCompare),
    days: daysDiff(date, dateToCompare),
    hours: hourDiff(date, dateToCompare),
    minutes: minuteDiff(date, dateToCompare),
    seconds: secondDiff(date, dateToCompare)
  };
}

console.info(getInterval(new Date(), new Date(1987, 2, 4, 0, 0, 0)));
console.info(getInterval(new Date(), new Date(2005, 8, 25, 0, 0, 0)));
console.info(getInterval(new Date(), new Date(2005, 8, 25, 0, 0, 0)));
```

## Vlastní výstupní formát

```js
function toDateString(date) {
  if (date === null || date === undefined) return null;

  return date.getDate() + ". " + date.getMonth() + ". " + date.getFullYear();
}
```

## A nejde to snadněji?

Jde. Existuje spousta knihoven, které práci s datem usnadňují, nejznámejší je asi moment.js

```js
moment().format('MMMM Do YYYY, h:mm:ss a'); // červenec 18. 2018, 1:00:31 pm
moment().format('dddd');                    // středa
moment().format("MMM Do YY");               // čvc 18. 18
moment().format('YYYY [escaped] YYYY');     // 2018 escaped 2018
moment().format();                          // 2018-07-18T13:00:31+02:00
```

```js
moment("20111031", "YYYYMMDD").fromNow(); // před 7 lety
moment("20120620", "YYYYMMDD").fromNow(); // před 6 lety
moment().startOf('day').fromNow();        // před 13 hodinami
moment().endOf('day').fromNow();          // za 11 hodin
moment().startOf('hour').fromNow();       // před 2 minutami
```
