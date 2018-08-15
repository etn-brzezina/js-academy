# jQuery

__jQuery je knihovna pro snadnou manipulaci s DOMem.__

jQuery se na určitou dobu stalo de-facto standardem pro manipulaci s DOMem, protože ho díky velmi jendoduchému a přímočarému API mohl používat začátečník i zkušený programátor.
Zároveň sloužilo jako polyfill pro mnoho funkcí, které různé prohlížeče (ne)podporovaly, jako například XMLHttpRequest(XHR) - čili AJAX.

Dnes už prohlížeče dohnaly potřebné nedostatky v podpoře různých API a standardů včetně DOM metod. jQuery se tak dostalo do ústraní a ustoupilo specializovaným technologiím jako je třeba React.

Tato kapitola se zaměří především na to, jak nahradit jQuery obyčejným čistým (vanilla) JavaScriptem.

## Syntaxe

```javascript
// jQuery
```

## Selektory

```javascript
// jQuery
var $root = $("#root"); // => Array<Node>

// Vanilla JS
var root1 = document.getElementById("root"); // => Node
var root2 = document.querySelector("#root"); // => Node
var root3 = document.querySelectorAll("#root"); // => NodeList<Node>
```

## Eventy

Pro přidání event listeneru na jeden element je náhrada jQuery velmi jednoduchá.

```javascript
// jQuery
$("#button").on("click", function() {
    console.log("clicked!");
});

// Vanilla JS
document.querySelector("#button").addEventListener("click", function() {
    console.log("clicked!");
});
```

Zacházení s množinou elementů, na které chceme přidat even tlistenery je už trochu komplikovanější.

```javascript
// jQuery
$("a").on("click", function() {
    console.log("clicked!");
});

// Vanilla JS
var elements = document.querySelectorAll("a");
var elementsArray = Array.from(elements); // `elements` není Array, ale NodeList, je třeba ho tedy převést na pole pomocí `Array.from()`, abychom nad ním mohli iterovat pomocí metody `forEach`

elementsArray.forEach(function(element) {
   element.addEventListener("click", function() {
       console.log("clicked!");
   });
});
```

Jak ale na delegování eventů? I toto se dá ve Vanilla JS snadno vyřešit.

## Efekty

## DOM

## AJAX
