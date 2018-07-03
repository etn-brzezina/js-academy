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

## Hledání elementů

| Metoda                                  | Popis                                                  |
| --------------------------------------- | ------------------------------------------------------ |
| document.getElementById(id)             | Najde element podle id atributu                        |
| document.getElementsByTagName(name)     | Najde kolekci elementů podle tagu                      |
| document.getElementsClassName(class)    | Najde kolekci elementů podle css třídy                 |
| document.querySelectorAll(css selektor) | Najde kolekci elementů podle libovolného css selektoru |

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

## Práce s eventy

V JavaSccriptu můžeme funkce reagující na nějakou událost definovat dvěma způsoby

- Pomocí HTML Event atributů
- Pomocí Event Listenerů

### HTML event atributy

Eventy můžeme definovat pomocí HTML atributů

```html
<html>
    <body>
        <h1 onclick="this.innerHTML = 'Ooops!'">Click on this text!</h1>
    </body>
</html>
```

Pomocí `this` můžeme odkazovat na element na kterém je definovaný

```html
<html>
    <body>
        <h1 onclick="changeText(this)">Click on this text!</h1>

        <script>

        function changeText(element) {
            element.innerHTML = "Ooops!";
        }

        </script>
    </body>
</html>
```

Nebo můžeme zavolat funkci, které `this` předáme jako parametr

### Event Listenery

Event listenery nám umožňují vytvářet/odebírat eventy na konkrétní element přímo z JavaScript kódu

| Metoda                                                                    | Popis                       |
| ------------------------------------------------------------------------- | --------------------------- |
| document.getElementById(id).addEventListener(event, function, useCapture) | Vytvoří nový event listener |
| document.getElementById(id).removeEventListener(event, function)          | Odstraní event listener     |

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

### addEventListener

- `addEventListener()` vytvoří event handler na konkrétní element přímo z JavaScript kódu
- `addEventListener()` přidá nový handler aniž by přepsal existující
- Můžeme přidat různé množství eventů na jeden element
- Můžeme přidat různé množství stejných typů eventů na jeden element (dvě různé funkce regující na klik)
- První parametr je název eventu (`click`, `keydown`, etc..), narozdíl od HTML atributů nepoužíváme `on` prefix
- Druhým parametrem je funkce, která má na event reagovat, jako první parametr se jí předá Event object
- Třetí parametr je boolean určující použití bubbling, nebo capturing a je nepovinný

### Bubbling a capturing
V JavaScriptu jsou dvě možnosti jak se vypořádat s "pořadím" ve kterém se mají eventy zavolat - bubbling a capturing

Pokud máme `<p>` uvnitř `<div>`, oba elementy mají definovaný `click` event a klikneme na na odstavec, který event se má vykonat první?

- Při bubblingu se první vykoná nejvíce zanořený event a až po té jeho "nadřazené" - první se tedy vykoná `click` na `<p>` a až po té na `<div>`
- Při capturingu se první vykoná nejméně zanořený event a až po té jeho "podřazené" - první se tedy vykoná `click` na `<div>` a až po té na `<p>`

### Předávání parametrů


### removeEventListener

- `removeEventListener()` odstraní konkrétní event (funkci) z vybraného elementu (funkce slouží jako identifikátor - odstraní přesně tu funkci, kterou mu předáme)

### Event object

#### `e.preventDefault()`
#### `e.stopPropagation()`
#### `e.target`

### Event reference
Kompletní seznam všechy typů eventů, metod a vlastností můžeme najít na [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event)

## Změny elementů

| Metoda/Vlastnost                       | Popis                                 |
| -------------------------------------- | ------------------------------------- |
| element.innerHTML = hodnota            | Změní vnitřní HTML strukturu elementu |
| element.attribute = hodnota            | Změní hodnotu HTML atributu           |
| element.setAttribute(atribut, hodnota) | Změní hodnotu HTML atributu           |
| element.style.property = nové styly    | Nastaví hodnotu vlastnosti css        |

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

## Přidávání a odebírání elementů

| Metoda                                           | Popis                                                         |
| ------------------------------------------------ | ------------------------------------------------------------- |
| document.createElement(element)                  | Vytvoří nový HTML element (ale nikam ho nevloží)              |
| document.removeChild(element)                    | Odstraní HTML element                                         |
| document.getElementById(id).appendChild(element) | Přidá do struktury (elementu s předaným id) nový HTML element |
| document.replaceChild(element)                   | Vymění HTML element za jiný                                   |

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
