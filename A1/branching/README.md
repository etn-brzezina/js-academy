# Větvení

## Podmínky a porovnávání

### Inline `if` podmínka:
```javascript
if(true) callSomeFunction();
```

### Bloková `if` podmínka:
```javascript
if(true) { //vykoná se vždy
    callSomeFunction();
} else {
    callOtherFunction();
}
```

### Switch/Case podmínka:
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

#### Break statement
Break statement "vyskočí" ze switch podmínky - už se nezajímá, jestli proměnná splňuje nějakou další podmínku

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

## Cykly
- Cyklus nám umožňuje vykonat stejnou operaci (blok kódu) několikrát
- V Javascriptu máme několik typů cyklů:
    - for - pevně daný počet iterací
    - for/in - iterace vlastností objektu
    - while - iterace dokud platí podmínka (nemusí se spustit vůbec)
    - do/while - iterace dokud platí podmínka (spustí se vždy alespoň jednou)

### For loop
Cyklus `for` nám umožňuje vykonat stejný kus kódu předem daným počtem časů (iterací)

_Sestavení řetězce ze seznamu v poli_
```js
    var cars = ["Škoda", "Opel", "Audi", "BMW"];
    var text = ""; // Seznam aut

    // "Ručně" sestavený string
    text += cars[0] + ", "; 
    text += cars[1] + ", "; 
    text += cars[2] + ", "; 
    text += cars[3];

    // Sestavení stringu pomocí for cyklu
    for (var i = 0; i < cars.length; i++) { 
        text += cars[i];
        if(i + 1 < cars.length) text += ", ";
    }

    console.info(text);
```

### For/in loop
Cyklus for/in nám umožňuje procházet vlastnosti objektu

```js
var person = {fname:"John", lname:"Doe", age:25}; 

var text = "";
for (var x in person) {
    text += x + ": " + person[x];
}

console.info(text);
```

### While loop
Cyklus while probíhá tak dlouho, dokud jeho podmínka platí. Pokud je podmínka neplatná od začátku, cyklus se nespustí

```js
var cars = ["Škoda", "Opel", "Audi", "BMW"];
var i = 0;
var text = "";

while (cars[i]) {
    text += cars[i];
    i++;
    if(i < cars.length) text += ", ";
}
```

### Do/while loop
Cyklus while probíhá tak dlouho, dokud jeho podmínka platí. Spustí se minimálně jednou, i přes to, že podmínka od začátku neplatí

```js
var i = 11;
do {
    text += "The number is " + i;
    i++;
}
while (i < 10);
```

### Break/continue
- `break` statement přeruší vykonávání cyklu a pokračuje vyhodnocováním dalšího kódu
- `continue` statement přeruší aktuální iteraci cyklu a přejde na další
