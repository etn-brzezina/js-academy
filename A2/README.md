# DOM

HTML DOM je stromová struktura elementů na stánce. JavaScript můžeme přistupovat a měnit tyto elementy

## Co je to DOM?
DOM definuje standard pro přistupování k dokumentům. Je rozdělený do tří částí:
- Core DOM - standard pro všechny typy dokumentů
- XML DOM - standard pro XML dokumenty
- HTML DOM - standard pro HTML dokumenty

## Co s ním dokážeme dělat?
HTML DOM je prostředek který nám umožňuje přistupovat, měnit, přidávat a mazat HTML elementy. JavaScript dokáže:
- Měnit HTML elementy na stránce
- Měnit atributy HTML elementů
- Měnit CSS
- Přidávat nové elemnty a atributy
- Mazat existující elemnty a atributy 
- Reagovat na existující eventy na stránce
- Vytvářet nové eventy

## DOM objekty
- Javascript (a jiné jazyky) můžou k DOMu přistupovat
- HTML objkty jsou v DOMu definované jako objekty, které mají vlastnosti a metody
- Vlastnosti jsou hodnoty, které můžeme číst nebo nastavovat

## Document
- document je root stromové struktury (html tag) - všechny ostatní elementy jsou pod ním
- Pokud chceme přistoupit k nějakému elementu ve stránce, vždy k němu přistupujeme přes document

### Hledání elementů
Metoda | Popis 
--- | --- 
document.getElementById(id) | Najde element podle id atributu
document.getElementsByTagName(name) | Najde kolekci elementů podle tagu
document.getElementsClassName(class) | Najde kolekci elementů podle css třídy
document.querySelectorAll(css selektor) | Najde kolekci elementů podle libovolného css selektoru

```html
<html>
    <body>

    <p id="demo"></p>

        <script>
            document.getElementById("demo") // Metoda, která vrací DOM element jako objekt
            .innerHTML = "Hello World!"; // Vlastnost, která umožňuje číst/nastavit dětský obsah elementu
        </script>

    </body>
</html>
```

### Přidávání a odebíraní eventů
Metoda | Popis 
--- | --- 
document.getElementById(id).addEventListener(event, function) | Vytvoří nový event listener
document.getElementById(id).removeEventListener(event, function) | Odstraní event listener (funkce slouží jako identifikátor - odstraní přesně tu funkci, kterou mu předáme)

```html
<html>
    <body>

        <script>
            document.addEventListener('click', function() {
                alert('you clicked me!');
            })
        </script>

    </body>
</html>
```

### Změny elementů
Metoda/Vlastnost | Popis 
--- | --- 
element.innerHTML = hodnota | Změní vnitřní HTML strukturu elementu
element.attribute = hodnota | Změní hodnotu HTML atributu
element.setAttribute(atribut, hodnota) | Změní hodnotu HTML atributu
element.style.property = nové styly | Nastaví hodnotu vlastnosti css

```html
<html>
    <body>

        <p class="red">Lorem ipsum</p>
        <p>Lorem ipsum</p>
        <p class="red">Lorem ipsum</p>
        <p>Lorem ipsum</p>
        <p class="red">Lorem ipsum</p>
        <p>Lorem ipsum</p>
        <p class="red">Lorem ipsum</p>
        <p>Lorem ipsum</p>

        <button id="highlight">Hightlight paragraphs</button>

        <script>

            document.getElementById('highlight').addEventListener('click', function() {

                var importantParagraphs = document.getElementsByClassName("red"); // Metoda, která vrací kolekci DOM elementů

                for (i = 0; i < importantParagraphs.length; i++) {
                    importantParagraphs[i].style.color = "red"; // Změníme barvu každého elementu pomocí vlastnosti style
                }

            });

        </script>

    </body>
</html>
```

### Přidávání a odebírání elementů
Metoda | Popis 
--- | --- 
document.createElement(element) | Vytvoří nový HTML element (ale nikam ho nevloží)
document.removeChild(element) | Odstraní HTML element
document.getElementById(id).appendChild(element) | Přidá do struktury (elementu s předaným id) nový HTML element
document.replaceChild(element) | Vymění HTML element za jiný

## Práce s eventy

### Přidávání eventů
### Odebírání eventů
### Mouse eventy
### Keyboard eventy

## Práce s uzly (elementy)

### Přidávání elementů
### Odstraňování elementů

```html
<html>
    <body>

        <script>
            // TODO: TodoList Example
        </script>

    </body>
</html>
```

## Navigace
- parentNode
- childNodes[nodenumber]
- firstChild
- lastChild
- nextSibling
- previousSibling

# BOM

## Window
## Screen
## Location
## History
## Navigator
## Popup alert
## Timing
## Cookies, storage

# AJAX

## XMLHttpRequest
## Request
## Response

# jQuery

## Syntaxe
## Selektory
## Eventy
## Efekty
## DOM
## AJAX
