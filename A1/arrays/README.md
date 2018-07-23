# Práce s poli

Pole v programování obecně je nějaký výčet hodnot klíč => hodnota

- V JavaScriptu je pole speciální druh objektu, jehož klíče jsou indexováné (inkrementované číselné hodnoty)
- Nad polem se dá iterovat, filtrovat, přidávat i odebírat hodnoty.
- V JavaScriptu neexistuje nic jako asociativní pole - tuto funkci zastávají objekty

Pole se v JavaScriptu nejčastěji definuje takzvaným Array literálem:

```javascript
var arr = []; // prázdné pole
var arr2 = ['string 1', 'string 2', 'string 3'];
```

K hodnotám pole můžeme přistupovat pomocí indexu dané hodnoty v poli. Index je tzv. zero-based, první položka má tedy index `0`.
```javascript
var arr = ['string 1', 'string 2', 'string 3'];

console.log(arr[0]); // => 'string 1'
console.log(arr[1]); // => 'string 2'
console.log(arr[8]); // => undefined
``` 

Hodnoty můžeme do pole přřazovat podobně jako do proměnných za použití indexu

```js
var arr = [];

arr[0] = 'string 1';
arr[1] = 'string 2';
arr[2] = 'string 3';
```

## Array vlastnosti
Stějně jako obyčejný objekt může mít pole vlastnosti.

### Length
Vlastnost `length` obsahuje velikost (počet prvků) pole

```js
var arr = ['string 1', 'string 2', 'string 3'];
console.log(arr.length); // => 3
```

## Array metody
Stějně jako obyčejný objekt může mít pole metody (funkce), tyto slouží k různým pčelům jako například řazení, filtrování, nebo procházení jednotlivých hodnot

## Přidávání a odebírání hodnot

### Přidání hodnoty do pole

K přidání jedné, nebo více hodnot na konec pole slouží metoda `push()`:
```javascript
var arr = [];
arr.push('random string');
arr.push(78);

console.log(arr); // => ['random string', 78]
``` 

K přidání jedné, nebo více hodnot na začátek pole slouží metoda `unshift()`:
```javascript
var arr = [];
arr.unshift('random string');
arr.unshift(78);

console.log(arr); // => [78, 'random string']
``` 

### Přidání/odebrání hodnot na konkrétní pozici

### splice()

Metoda `.splice()` nám umožňuje odebirat a/nebo přidávat nové položky do pole

#### Syntaxe
`array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`

```js
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
var removed = myFish.splice(2, 0, 'drum');

// myFish is ["angel", "clown", "drum", "mandarin", "sturgeon"] 
// removed is [], no elements removed
```
_Remove 0 elements from index 2, and insert "drum"_

```js
var myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'];
var removed = myFish.splice(3, 1);

// removed is ["mandarin"]
// myFish is ["angel", "clown", "drum", "sturgeon"]
```
_Remove 1 element from index 3_

```js
var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
var removed = myFish.splice(2, 1, 'trumpet');

// myFish is ["angel", "clown", "trumpet", "sturgeon"]
// removed is ["drum"]
```
_Remove 1 element from index 2, and insert "trumpet"_

### Odebrání hodnoty z pole
K odebrání jedné, nebo více hodnot od konce pole slouží metoda `pop()`:
```javascript
var arr = ['random string', 78];
arr.pop();

console.log(arr); // => ['random string']
``` 

### Iterace nad hodnoty v poli
K iteraci nad hodnotami pole můžeme použít výrazy `for` nebo `while`:
```javascript
var arr = ['alfa', 'beta', 'gamma', 'delta'];

// deklarujeme iterátor | deklarujeme podmínku do kdy se má nad polem iterovat | uděláme operaci s iterátorem (nejčastěji přičteme 1)
for(var i = 0; i < arr.length; i++) {
    // Vypíšeme do konzole každou hodnotu pole 
    console.log(arr[i]);
}

var j = 0;
while (j < arr.length) {
    // Vypíšeme do konzole každou hodnotu pole 
    console.log(arr[j]);
    j++;
}
```

Dnes už naštěstí existují metody pro mnohem přímočařejší přístup pro iteraci nad polem

#### .forEach()
Metoda `forEach` pro každou hodnotu v poli zavolá funkci (kteoru jsme jí dali), které jako argument danou hodnotu předá jako parametr

```javascript
var arr = ['alfa', 'beta', 'gamma', 'delta'];

arr.forEach(function(item) {
    console.log(item);
})
```

#### .map()
Metoda `map` nám umžňuje vytvořit nové pole za použití hodnot jiného pole

##### Syntaxe
```js
arr.map(function callback(currentValue[, index[, array]]) {
    // Return element for new_array
}[, thisArg])
```

Pro každou položku pole na které metodu voláme, se zavolá callback funkce, která nám umožňuje vrátit hodnotu
Vrácená hodnota se vloží nakonec nového pole, které je výsledkem funkce


Callback funkce, která je jediným parametrem dosatne dva parametry:
- element - aktuální položka pole
- index - index aktuální položky pole
- array - pole na které jsme metodu zavolali
- thisArg - reference na this

```js
var numbers = [65, 44, 12, 4];

function multiplyArrayElement(num) {
    return num * 2;

console.info(numbers.map(multiplyArrayElement)); // => [130, 88, 24, 8]
}
```

#### .reduce()
Metoda `reduce()` nám umožňuje projít pole a "redukovat ho" na jednu hodnotu (např. sečíst všechna čísla v poli)

##### Syntaxe
````arr.reduce(callback(accumulator, currentValue[, currentIndex, array]))````

Callback funkce, která je jediným parametrem dosatne čtyři parametry:
- accumulator - hodnota vrácená předchozí iterací
- currentValue - aktuální položka pole
- currentIndex - index aktuální položky pole
- array - pole na které jsme metodu zavolali


##### Ukázka

```js
var arr = [0, 1, 2, 3, 4];

var result = arr.reduce(function(accumulator, currentValue, currentIndex, array) {
  return accumulator + currentValue;
});

console.info(result); // => 10
```

#### .filter()

Pro filtrování hodnot v poli slouží metoda `filter()`, která vrátí nové pole s položkami, které splní danou podmínku.

##### Syntaxe
`arr.filter(callback(element[, index[, array]])[, thisArg])`

Callback funkce, která je jediným parametrem dosatne čtyři parametry:
- element - aktuální položka pole
- index - index aktuální položky pole
- array - pole na které jsme metodu zavolali
- thisArg - reference na this

##### Ukázka

```javascript
var arr = [1, 2, 3, 4, 5, 6];

var filteredArr = arr.filter(function(item) {
    return item > 3;
})

console.log(filteredArr); // => [4, 5, 6]
```

#### .every()

Metoda `every()` vrací `true`, nebo `false` podle toho zda všechny prvky pole splňůjí stejnou podmínku

##### Syntaxe
`arr.every(callback(element[, index[, array]])[, thisArg])`

Callback funkce, která je jediným parametrem dosatne tři parametry:
- element - aktuální položka pole
- index - index aktuální položky pole
- array - pole na které jsme metodu zavolali
- thisArg - reference na this

##### Ukázka

```javascript
var arr = [1, 2, 3, 4, 5, 6];

var filteredArr = arr.every(function(item) {
    return item > 3;
})

console.log(filteredArr); // => false
```

#### .some() 

Metoda `some()` vrací `true`, nebo `false` podle toho zda alespoň jeden prvek pole splňuje nějakou podmínku

##### Syntaxe
`arr.some(callback(element[, index[, array]])[, thisArg])`

Callback funkce, která je jediným parametrem dosatne tři parametry:
- element - aktuální položka pole
- index - index aktuální položky pole
- array - pole na které jsme metodu zavolali
- thisArg - reference na this

##### Ukázka

```javascript
var arr = [1, 2, 3, 4, 5, 6];

var filteredArr = arr.some(function(item) {
    return item > 3;
})

console.log(filteredArr); // => true
```

## Hledání hodnot


### indexOf()
- Metoda `.indexOf()` vrací pozici prvního výskytu vyhledávané položky
- Pomocí druhého parametru můžeme určit začáteční pozici pro vyhledávání

```js
// TODO: Example
```

### lastIndexOf()
- Metoda `.lastIndexOf()` vrací pozici posledního výskytu vyhledávané položky
- Pomocí druhého parametru můžeme určit začáteční pozici pro vyhledávání

```js
// TODO: Example
```

### find() a findIndex()
- Metoda `.find()` vrací první položku, která projde předanou test funkcí
- Metoda `.findIndex()` vrací index první položkuy, která projde předanou test funkcí

##### Syntaxe
`arr.find(callback(element[, index[, array]])[, thisArg])`

Callback funkce, která je jediným parametrem dosatne čtyři parametry:
- element - aktuální položka pole
- index - index aktuální položky pole
- array - pole na které jsme metodu zavolali
- thisArg - reference na this

```js
function isPrime(element, index, array) {
  var start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}

console.log([4, 6, 8, 12].find(isPrime)); // undefined, not found
console.log([4, 5, 8, 12].find(isPrime)); // 5
```

## Řazení hodnot

### .reverse()
Metoda `reverse()` vrací pole, které má obrácené pořadí prvků, než pole na kterém metodu voláme

```js
var arr = [1, 2, 3, 4, 5, 6];
var reversedArray = arr.reverse();

console.info(reversedArray); // => [6, 5, 4, 3, 2, 1]
```

### .sort()
- Metoda `sort()` vrací pole, seřazené podle libovolné, námi řízené, logiky
- Způsoby řazení můžou být podle abecedy nebo čísel, sestupně nebo vzestupně
- Ve výchozím stavu metoda `sort()` řadí hodnoty jako stringy v ASC pořadí

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];

console.info(fruits.sort()); // => ["Apple", "Banana", "Mango", "Orange"]
```

_Při použití metody na číselné pole bez porovnávací funkce řazení neodpovídá, protože se čísla berou jako stringy_
```js
var fruits = [2, 3, 8, 25];

console.info(fruits.sort()); // => [2, 25, 3, 8]
```

#### compareFunction
- Pokud chceme použít jiný způsob řazení, musíme předat metodě `sort()` předat funkci, která provede porovnání prvků
- Funkce má dva parametry - dva aktuálně porovnávané prvky
- Porovnávací funkce může vracet tři různé hodnoty
    - Pokud chceme prvek posunout __před__ porovnávaný prvek - musíme vrátit hodnotu __-1__
    - Pokud chceme prvek posunout __za__ porovnávaný prvek - musíme vrátit hodnotu __1__
    - Pokud na pořadí porovnávaných prvků nezáleží vracíme hodnotu __0__

```js
// TODO: example
```
