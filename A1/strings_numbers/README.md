# Řetězce a čísla

Řetězec je nula, nebo více znaků v uvozovkách - text

## String vlastnosti

V JavaScriptu je všechno objekt. Stejně tak řetězec - to znamená že na něm existují i vlastnosti

### Length

Stejně jako u pole nám vlastnost `.length` vrací "velikost" řetězce - jeho délku

```js
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

console.info(txt.length); // => 26
```

## Speciální znaky

Pokud zapíšeme řetězec do dvojitých závorek a použijeme tyto závorky JavaScript to "nepochopí"

```js
var x = "We are the so-called "Vikings" from the north."; // => Uncaught SyntaxError: Unexpected identifier
```

_Stejný princip platí pokud použijme jednoduché závorky a ty pak vepíšeme do řetězce_

### Escape characters

- Pokud potřebujeme do řetězce vložit podobný znak, umožní nám to escape sekvence
- Escape sekvence jsou znaky zapsané za obráceným lomítkem

| Kód | Výsledek             |
| --- | -------------------- |
| \b  | Backspace            |
| \f  | Form Feed            |
| \n  | New Line             |
| \r  | Carriage Return      |
| \t  | Horizontal Tabulator |
| \r  | Carriage Return      |
| \v  | Vertical Tabulator   |

### Zalomení na více řádků
Pokud je náš řetězec příliš dlouhý a chceme ho zalomit na více řádků, můžeme použít obrácené lomítko, nebo řetězce spojit pomocí `+`

```js
// TODO: Example
```

## String metody

### Vyhledávání v řetězcích
Pro vyhledávání v řetězcích máme tři metody: `.indexOf()`, `lastIndexOf()` a `search()`

#### indexOf()
- Metoda `.indexOf()` vrací pozici prvního výskytu vyhledávaného řetězce
- Pomocí druhého parametru můžeme určit začáteční pozici pro vyhledávání

```js
// TODO: Example
```

#### lastIndexOf()
- Metoda `.lastIndexOf()` vrací pozici posledního výskytu vyhledávaného řetězce
- Pomocí druhého parametru můžeme určit začáteční pozici pro vyhledávání

```js
// TODO: Example
```

#### search()
- Metoda `.search()` vrací pozici prvního výskytu vyhledávaného řetězce
- Narozdíl od `.indexOf()` můžeme použít regulární výraz
- Metoda search nemá druhý argument pro začáteční pozici pro vyhledávání

```js
// TODO: Example
```


### Získání části řetězce
Pro získání části řetězce máme tři metody `slice(start, end)`, `substring(start, end)`, `substr(start, length)`

#### substring()
Metoda substring vyjme část řetězce od určitého indexu do určitého indexu a vrátí ho jako nový řetězec (bez změny původního řetězce)

##### Syntaxe

`str.substring(beginIndex[, endIndex])`

##### Ukázka

```js
var str = 'The morning is upon us.'

console.info(str.substring(1, 8)); // => "he morn"
```

#### slice()
Metoda slice vyjme část řetězce od určitého indexu do určitého indexu a vrátí ho jako nový řetězec (bez změny původního řetězce)

##### Syntaxe

`str.slice(beginIndex[, endIndex])`

##### Ukázka

```js
var str = 'The morning is upon us.'

console.info(str.slice(1, 8)); // => "he morn"
console.info(str.slice(4, -1)); // => "morning is upon us"
str.slice(-3); // => "us."
```

#### substr()
Metoda substr vyjme část řetězce od určitého indexu do nějaké délky znaků a vrátí ho jako nový řetězec (bez změny původního řetězce)

##### Syntaxe

`str.substr(beginIndex[, endIndex])`

##### Ukázka

```js
var aString = 'Mozilla';

console.log(aString.substr(0, 1));   // 'M'
console.log(aString.substr(-3));     // 'lla'
console.log(aString.substr(1));      // 'ozilla'
console.log(aString.substr(-20, 2)); // 'Mo'
```

### Řetězec jako pole

#### split()

Metoda `split()` nám umožňuje rozdělit řetězec do pole pomocí nějakého oddělovače

#### join()

Metoda `join()` nám umožňuje spojit pole řetězců do jednoho pomocí nějakého oddělovače

### RegExp
- Regulární výraz je řetězec speciálních znaků,které vytváří vyhledávací vzor
- Při vyhledávání, nebo nahrazování textu často nechceme hledat výskyt konkrétního řetězce (slova, věty), ale zajímá nás všechny výskyty, odpovídající nějakému vzoru

```js
var str = "Visit Microsoft!";
var res = str.replace(/microsoft/i, "Etnetera! We've got cookies!!! ");
```

### test()

Metoda `test()` otestuje řetězec pomocí regulárního výrazu a vrátí `true`, nebo `false` podle toho jestli řetězec výrazu odpovídá

### exec()

Metoda `exec()` otestuje řetězec pomocí regulárního výrazu a vrátí nalezený text, nebo v případě žádného výskytu `null`

```js
var str = "Visit Microsoft!";
console.info(str.exec(/microsoft/i)); // => Microsoft
```

### match()

Metoda `match` otestuje řetězec pomocí regulárního výrazu a vrátí pole řetězců, které odpovídají zadanému vzoru

### Nahrazování částí řetězce

#### replace()

Metoda `replace`

```js
var str = "Visit Microsoft!";
var res = str.replace(/microsoft/i, "Etnetera! We've got cookies!!! ");
```

## Matematické operace

### Math metody
V JavaScriptu máme k dispozici globální objekt `Math` na kterém jsou definované funkce pro matematické operace jako umocňování, odmocňování, zaokrouhlování atd...

### Math.round()
Math.round(x) returns the value of x rounded to its nearest integer

### Math.ceil()
Math.ceil(x) returns the value of x rounded up to its nearest integer:

### Math.floor()
Math.floor(x) returns the value of x rounded down to its nearest integer

### Math.pow()
Math.pow(x, y) returns the value of x to the power of y

### Math.sqrt()
Math.sqrt(x) returns the square root of x

### Math.abs()
Math.abs(x) returns the absolute (positive) value of x

### Math.sin()

### Math.cos()

## Math properties (konstanty)

```js
Math.E        // returns Euler's number
Math.PI       // returns PI
Math.SQRT2    // returns the square root of 2
Math.SQRT1_2  // returns the square root of 1/2
Math.LN2      // returns the natural logarithm of 2
Math.LN10     // returns the natural logarithm of 10
Math.LOG2E    // returns base 2 logarithm of E
Math.LOG10E   // returns base 10 logarithm of E
```
