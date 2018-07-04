# Základní informace o jazyku

- multi-platformní, objektově orientovaný, slabě typovaný programovací jazyk 
- dokáže běžet v prohlížeči i na serveru
- nekompiluje se - je tzv. runtime based

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

## Podmínky a porovnávání

Inline `if` podmínka:
```javascript
if(true) callSomeFunction();
```

Bloková `if` podmínka:
```javascript
if(true) { //vykoná se vždy
    callSomeFunction();
} else {
    callOtherFunction();
}
```

Switch/Case podmínka:
```javascript
var condition = 'hello';

switch(condition) {
    case 'ahoj':
        callSomeFunction();
        break;
    case 'hello':
        callOtherFunction();
        break;
    default:
        callDefaultFunction();        
}
```

## Logické operace

Negace:
```javascript
if(!false) callSomeFunction();

var a = 3;
if (a != 4) callSomeFunction();
```

### Pravdivé a nepravdivé hodnoty
Všechny hodnoty v JavaScriptu mohou být vyhodnoceny jako pravdivé nebo nepravdivé(truthy/falsy) -  jsou konvertovány na `true`/`false`.

Příklady pravdivě vyhodnocených výrazů:
```javascript
if (true)
if ({})
if ([])
if (42)
if ("foo")
if (new Date())
if (-42)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)
```

Příklady nepravdivě vyhodnocených výrazů:
```javascript
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
```

Pro převedení jakékoliv hodnoty na boolean můžeme tedy využít dvojitou negaci:
```javascript
var a = 'hello!';

console.log(!!a); // => true
```
