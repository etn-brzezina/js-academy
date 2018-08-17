# jQuery

__jQuery je knihovna pro snadnou manipulaci s DOMem.__

jQuery se na určitou dobu stalo de-facto standardem pro manipulaci s DOMem, protože ho díky velmi jendoduchému a přímočarému API mohl používat začátečník i zkušený programátor.
Zároveň sloužilo jako polyfill pro mnoho funkcí, které různé prohlížeče (ne)podporovaly, jako například XMLHttpRequest(XHR) - čili AJAX.

Dnes už prohlížeče dohnaly potřebné nedostatky v podpoře různých API a standardů včetně DOM metod. jQuery se tak dostalo do ústraní a ustoupilo specializovaným technologiím jako je třeba React.

Tato kapitola se zaměří především na to, jak nahradit jQuery obyčejným čistým (vanilla) JavaScriptem.

## Selektory

jQuery vždy vrací pole elementů, zatímco čistý JavaScript může vracet buď jeden element nebo NodeList (speciální kolekci elementů).

```javascript
// jQuery
var $root = $("#root"); // => Array<Node>

// Vanilla JS
var root1 = document.getElementById("root"); // => Node
var root2 = document.querySelector("#root"); // => Node
var root3 = document.querySelectorAll("#root"); // => NodeList<Node>
```

Proto je při práci v čistém JavaScriptu vždy přemýšlet nad tím, zda pracuji s jedním nebo více prvky.

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

Zacházení s množinou elementů, na které chceme přidat eventlistenery je už trochu komplikovanější.

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

```html
<div id="gallery">
  <div><a class="item" href="#">Click me!</a></div>
  <div><a class="item" href="#">Click me!</a></div>
  <div><a class="item" href="#">Click me!</a></div>
  <div><a class="item" href="#">Click me!</a></div>
</div>
```

```javascript
// jQuery
$("#gallery").on("click", ".item", function() {
    console.log("clicked gallery item!");
});

// Vanilla JS
var gallery = document.getElementById("gallery");

gallery.addEventListener("click", function(event) {
    var clickedElement = event.target;
    if (clickedElement.classList.contains("item")) {
        console.log("clicked gallery item!");
    }
});
```

## DOM

### `.addClass()`

```javascript
// jQuery
$("a").addClass("item");

// Vanilla JS
document.querySelector("a").classList.add("item");
```

### `.removeClass()`

```javascript
// jQuery
$("a").removeClass("item");

// Vanilla JS
document.querySelector("a").classList.remove("item");
```

### `.toggleClass()`
```javascript
// jQuery
$("a").toggleClass("item");

// Vanilla JS
document.querySelector("a").classList.toggle("item");
```

### `.attr()`

```html
<a href="https://google.com">Google</a>
```
Get:

```javascript
// jQuery
$("a").attr("href"); // => "https://google.com"

// Vanilla JS
document.querySelector("a").getAttribute("href"); // => "https://google.com"
```

Set:
```javascript
// jQuery
$("a").attr("href", "https://seznam.cz"); // => "https://seznam.cz"

// Vanilla JS
document.querySelector("a").setAttribute("href", "https://seznam.cz"); // => "https://seznam.cz"
```

### `.parent()`
```javascript
// jQuery
$("a").parent();

// Vanilla JS
document.querySelector("a").parentNode;
```

### `.remove()`
```javascript
// jQuery
$("a").remove();

// Vanilla JS
var element = document.querySelector("a");
element.parentNode.removeChild(element);
```

## Efekty

### `.show()`

```javascript
// jQuery
$("#item").show();

// Vanilla JS
document.querySelector("#item").style.display = "";
```

### `.hide()`

```javascript
// jQuery
$("#item").hide();

// Vanilla JS
document.querySelector("#item").style.display = "none";
```

### `.fadeIn()`

```javascript
// jQuery
$("#item").fadeIn();

// Vanilla JS
var element = document.querySelector("#item");

element.classList.add('show');
element.classList.remove('hide');
```
```css
.show {
  transition: opacity 400ms;
}
.hide {
  opacity: 0;
}
```

## Utility

### `Date.now()`

```javascript
// jQuery
$.now();

// Vanilla JS
Date.now();
```

### `JSON.parse()`
```javascript
// jQuery
$.parseJSON(string);

// Vanilla JS
JSON.parse(string);
```

### `.extend()`
```javascript
// jQuery
$.extend({}, objA, objB);

// Vanilla JS (ES2015+)
Object.assign({}, objA, objB);
```

## AJAX

### `GET` Request

```javascript
// jQuery
$.ajax({
  type: 'GET',
  url: '/my/url',
  success: function(resp) {

  },
  error: function() {

  }
});
```

```javascript
// Vanilla JS
var request = new XMLHttpRequest();

request.open('GET', '/my/url', true);

request.onload = function() {
  if (this.status >= 200 && this.status < 400) {
    // Success!
    var resp = this.response;
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

```javascript
// Fetch API (ES2015+)
fetch('/my/url')
    .then(function(reponse) {
        if (reponse.status >= 200 && response.status < 400) {
            // Success!
            var resp = response;
          } else {
            // We reached our target server, but it returned an error
            throw new Error("Server error:" + response.status);
          }
    })
    .catch(function(error) {
        // There was a connection error of some sort
    });
```

### `POST` Request

```javascript
// jQuery
$.ajax({
  type: 'POST',
  url: '/my/url',
  data: data
});
```

```javascript
// Vanlla JS
var request = new XMLHttpRequest();

request.open('POST', '/my/url', true);
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
request.send(data);
```

```javascript
// Fetch API (ES2015+)
fetch('/my/url', {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
        },
        body: data
    })
```

### Get JSON

```javascript
// jQuery
$.getJSON('/my/url', function(data) {
    // Handle data
});
```

```javascript
// Vanilla JS
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (this.status >= 200 && this.status < 400) {
    // Success!
    var data = JSON.parse(this.response);
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

```javascript
// Fetch API (ES2015+)
fetch('/my/url')
    .then(function(response) {
        return response.json();
    })
    .then(function(data) {
        // Handle data
    })
    .catch(function(error) {
        // Handle error
    })
```
