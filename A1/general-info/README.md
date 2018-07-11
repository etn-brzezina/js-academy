# Základní informace o jazyku

- multi-platformní, objektově orientovaný, slabě typovaný programovací jazyk 
- dokáže běžet v prohlížeči i na serveru
- nekompiluje se - je tzv. runtime based

## Script

V HTML můžeme zapsat script přimo do `<script>` a `</script>` tagů, v tagovém případě se kód vyhodnotí přímo na místě kde script zapíšeme

```html
<html>
    <body>
    <p>Hello world!!! 
        <script>
            document.write("This is my First JavaScript!");
        </script>
    </p>
    </body>
</html>
```

_document.write dnes nemá a nejspíš nikdy neměl žádné reálné využití, zmiňuji ho pouze jako ukázku_

## Soubory .js

HTML `<script>` tag nám ale zároveň umožňuje zadat cestu k `.js` souboru, ve kterém máme pouze náš JS kód

_index.html_

```html
<script src="./js/main.js"></script>
```

_main.js_

```js
alert("My First JavaScript!");
```

_alert je další způsob uživatelského outputu_

## Kam s ním?
- Do HTML dokumentu můžeme vložit libovolné množství scriptů
- HTML dokument se načítá postupně od začátku po konec
- Pokud narazí na `<script>` nepokračuje ve vykreslování dalšího obsahu, dokud celý script nenačte
- Pokud potřebujeme inicializovat nějakou logiku "co nejdříve po načtení stránky" (Google Analytics), umisťujeme scripty do `<head>` dokumentu
- V případě kdy náš script neovlvňuje vypsání obsahu a je možné ho načíst až po HTML dokumentu, vložíme ho nakonec `<body>` (rychleji se nám načte content stránky a styly, script se spustí až nakonec)

## Console
- Console slouží jako u většiny programovacích jazyků jako development output
- Máme k dizpozici několik úrovní "severity", nebo chceme-li "typu" zprávy:
    - `console.info()` je čistě informativní zpráva
    - `console.log()` je pro výpis nějakých obecných informací o průběhu scriptu
    - `console.warning()` pro nějaké varování
    - `console.error()` pro výpis chyby

## Syntax
- Středníky a složené závorky!!!
- JavaScript je case-sensitive
- Lower Camel Case?

## Komentáře
- Máme možnost používat inline, nebo blokové komentáře
- Kód uvnitř komentářů se nevyhodnotí

```js
// console.log('This is never going to be logged');

/*
* alert('Neither will this');
*/
```

### jsDoc
- jsDoc je API umožňující generovat dokumentaci z popisu v JS komentářích
- Více si o něm povíme později

## Statements
- Program je seznam "instrukcí", které má počítač vykonat
- V programovacím jazyce těmto instrukcím říkáme _statements_ (?příkazy)
- Jednotlivé příkazy oddělujeme středníky

```js
var x, y, z;    // Statement 1
x = 5;          // Statement 2
y = 6;          // Statement 3
z = x + y;      // Statement 4
```

## Operátory

### Aritmetické operátory
| Operátor        | Popis                       |
| ------------- | --------------------------- |
| `+` | Součet |
| `-` | Odečet |
| `*` | Násobení |
| `/` | Dělení |
| `%` | Modulus (zbytek po celočíselném dělení) |
| `++` | Inkrementace |
| `--` | Dekrementace |

### Přiřazování hodnot
| Operátor      |   Stejné jako |
| ------------- |  ------------- |
| `=`  | 	přiřazení hodnoty |
| `+=` | 	`x = x + y` |
| `-=` | `x = x - y` |
| `*=` | 	`x = x * y` |
| `/=` | `x = x / y` |
| `%=` | `x = x % y` |

### Porovávání

| Operátor      |   Popis |
| ------------- |  ------------- |
| `==` | Rovná se |
| `===`  | Rovná se a má stejný typ |
| `!=`  | Nerovná se |
| `!==`  | Nerovná se, nebo nemá stejný typ |
| `>`  | Více než |
| `<`  | Méně než |
| `>=`  | Více, nebo rovno než |
| `<=`  | Méně, nebo rovno než |
| `?`  | Ternární operátor |

### Logické operátory

| Operátor      |   Popis |
| ------------- |  ------------- |
| `&&`	  | A zároveň |
| `||`	  | Nebo |

## Datové typy

JS obsahuje šest primitivních datových typů:
- Boolean - `true` nebo `false`
- `null` - speciální klíčové slovo pro označení prázdné hodnoty
- `undefined` -  označení pro nedefinovanou hodnotu
- Number - Integer nebo Float - `18` nebo `1.2436`
- String - řetězec znaků, které reprezentují textovou hodnotu - `"Ahoj!"`
- Symbol (nový v ECMAScript 2015) - datový typ, jehož instance jsou unikátní a neměnitelné(immutable)

A pak jsou `Object`y...

## Přířazení do proměnných

```javascript
/* Prázdná proměnná */
var a;
console.log(a); // => undefined
console.log(typeof a); // => 'undefined'

/* Číselná hodnota v proměnné */
var b = '1';
console.log(b); // => '1'
console.log(typeof b); // => 'string'

/* Textotvá hodnota v proměnné */
var c = 10;
console.log(c); // => 10
console.log(typeof c); // => 'number'

/* Přiřazení booleanu do proměnné */
var d = true;
console.log(d); // => true
console.log(typeof d); // => 'boolean'
```

```javascript
/* Přiřazení pole do proměnné */
var pole = [];
console.log(pole); // => []
console.log(typeof pole); // => 'object'

var pole2 = ['omg', 'wtf'];
console.log(pole2); // => ['omg', 'wtf']

/* Přiřazení objektu do proměnné */
var obj = {};
console.log(obj); // => {} nebo [object Object]
console.log(typeof obj); // => 'object'

/* Přiřazení funkce do proměnné */
var func = function() {};
console.log(func); // => function() {} 
console.log(typeof func); // => 'function'
```

```javascript
/* POZOR na null a jiné objekty */
var a = null;
console.log(typeof a); // => 'object'

var b = new Date();
console.log(typeof b); // => 'object'
```

## Konverze mezi typy

JavaScript je dynamicky typovaný jazyk. To znamená, že není potřeba určit datový typ proměnné při její deklaraci a datově typy mohou mezi sebou být konvertovány dle porřeby. Následuje příklad: 
```javascript
var answer = 42;
```
Později v kódu se dá do stejné proměnné přiřadit jiná hodnota:
```javascript
answer = 'Thanks for all the fish...';
```
Protože JavaScript je dynamicky typovaný, tato operace je platná a nezpůsobí chybu.

Ve výrazech zahrnujících číslo a string s operátorem `+`, JavaScript automaticky konvertuje numerickou hodnotu na string:
```javascript
x = 'The answer is ' + 42; // => "The answer is 42"
y = 42 + ' is the answer'; // => "42 is the answer"
```

Ve výrazech zahrnujících jiné operátory, JavaScript automaticky nekonvertuje číslo na string:
```javascript
'37' - 7 // => 30
'37' + 7 // => "377"
```

Pro konverzi stringu na číslo lze použít zabudované globální funkce:
```javascript
var a = "12.6";
var b = parseInt(a);
var c = parseFloat(a);

console.log(b); // => 12
console.log(c); // => 12.6
```

Případně lze z čísla získat zpět jeho textovou reprezentaci:
```javascript
var a = 12;
var b = a.toString();
console.log(b); // => '12'
```

## Funkce
Funkce nám umožňují používat stejný kód vícekrát a s různým výsledkem v závislosti na předaných parametrech
- Funkce jsou blok kódu, který vykonává určitou činnost (sada příkazů)  
- Funkce se vykoná, když ji něco invokuje (zavolá)
- Funkci definujeme pomocí kličového slova `function`, je identifikována jménem a kulatými závorkami pro předání __parametrů__
- parametry jsou proměnné, do kterých můžeme funkci předat nějaké hodnoty
- parametry se chovají jako lokální proměnné
- Funkce můžou vracet hodnoty

```js
function name(parameter1, parameter2, parameter3) {
    code to be executed
}
```
_Zápis funkce_

```js
var x = myFunction(4, 3);    // Function is called, return value will end up in x

function myFunction(a, b) {
    return a * b;            // Function returns the product of a and b
}
```
_Funkce která vynásobí dvě předaná čísla_

## Objekty
- Objekty můžeme abstraktně vnímat jako cokoliv co má nějaké vlastnosti a funkce (metody)
- Velice zjednodušeně se dá říct, že jde o nějaký "kontejner" pro různé vlastnosti a metody, které můžou nabývat různých hodnot
- Hodnoty jsou v objektu "uloženy" jako páry __název:hodnota__

### Definice

```js
var person = {
    firstName:"John",
    lastName:"Doe",
    age:50,
    eyeColor:"blue",
    fullName : function() {
        return this.firstName + " " + this.lastName;
    }
};
```

### Přistupování k hodnotám
K hodnotám můžeme přistupovat pomocí __.__ nebo hranatých závorek a jejich názvu

```js
objectName.propertyName
objectName["propertyName"]

objectName.methodName()
objectName["methodName"]() // No fuj.
```

### `This` keyword
- V definici funkce odkazuje na "vlastníka" funkce
- V předchozím příkladu metoda `fullName` patří do objektu `person`
- `this` tedy odkazuje na objekt `person`, kterému funkce `fullName` patří
