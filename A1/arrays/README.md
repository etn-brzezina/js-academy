# Práce s poli

Pole není nic víc, než výčet hodnot. Pole může obsahovat i další pole, funkce nebo objekty.

Nad polem se dá iterovat, filtrovat, přidávat i odebírat hodnoty.

Pole se v JavaScriptu nejčastěji definuje takzvaným Array literálem (pozn. překladatele: polný literál?):
```javascript
var arr = []; // prázdné pole
var arr2 = ['string 1', 'string 2', 'string 3'];

console.log(arr.length); // => 0
console.log(arr2.length); // => 3
```

K hodnotám pole můžeme přistupovat pomocí indexu dané hodnoty v poli. Index je tzv. zero-based, první položka má tedy index `0`.
```javascript
var arr = ['string 1', 'string 2', 'string 3'];

console.log(arr[0]); // => 'string 1'
console.log(arr[1]); // => 'string 2'
console.log(arr[8]); // => undefined
``` 

## Přidání hodnoty do pole

K přidání hodnoty na konec pole slouží metoda `push()`:
```javascript
var arr = [];
arr.push('random string');
arr.push(78);

console.log(arr); // => ['random string', 78]
```
## Iterace nad hodnoty v poli

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

Dnes už naštěstí existuje mnohem přímočařejší přístup pro iteraci nad polem a to pomocí metody `forEach`:

```javascript
var arr = ['alfa', 'beta', 'gamma', 'delta'];

arr.forEach(function(item) {
    console.log(item);
})
```

Metoda `forEach` pro každou hodnotu v poli zavolá funkci (kteoru jsme jí dali), které jako argument předá položku z pole.  

## Filtrování hodnot v poli

Pro filtrování hodnot v poli slouží metoda `filter`, která vrátí nové pole s položkami, které splní danou podmínku.

```javascript
var arr = [1, 2, 3, 4, 5, 6];

var filteredArr = arr.filter(function(item) {
    return item > 3;
})

console.log(filteredArr); // => [4, 5, 6]
```

