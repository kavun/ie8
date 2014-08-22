# What's new in IE8?
## More than you think, now that IE7 is gone

[☛ View Slides](http://kavun.github.io/ie8)

## New features in IE8

[Comparison of features in IE7 & IE8](http://caniuse.com/#compare=ie+7,ie+8)

- WAI-ARIA Accessiblity Features
- querySelector / querySelectorAll
- JSON.parse / JSON.stringify
- localStorage / sessionStorage
- hashchange event
- CSS outline
- CSS table display
- CSS counters
- CSS3 box-sizing
- CSS content for pseudo elements
- Data URIs
- Cross document messaging
- Cross origin resource sharing

## WAI-ARIA Accesiblity Features

> Semantic information about widgets, structures, and behaviors, in
> order to allow assistive technologies to convey appropriate
> information to persons with disabilities.

> http://www.w3.org/TR/wai-aria/

`aria-labelledby`, `aria-invalid`, `aria-expanded`, `aria-readonly`

```html
<label for="name">Name</label>
<input type="text" id="name" />

<label id="lblName">Name</label>
*<input type="text" aria-labelledby="lblName" />
```

## querySelector / querySelectorAll

✗ IE7 vanilla
```js
var inputs = document.getElementsByTagName('input');
var checkboxes = [];
for (var i = 0, l = inputs.length; i < l; i++) {
    if (inputs[i].type === 'checkbox') {
        checkboxes.push(inputs[i]);
    }
}
```

✓ jQuery
```js
var checkboxes = $('input[type="checkbox"]');
```

★ IE8 vanilla
```js
var checkboxes = document.querySelectorAll('input[type="checkbox"]');
```

Single element
```js
document.querySelector('input'); // will return only one input
document.querySelectorAll('input'); // will return all inputs
```

Select by `id`
```js
// selects a single element with id="lblSoupSize"
document.querySelector('#lblSoupSize');
```

Select by `className`
```js
document.querySelectorAll('.soups');
```

Select by attribute
```js
document.querySelector('[data-soupid="4d7c6b21"]');
```

Relative selectors
```js
document.querySelector('.soup .spoon');
```

[More selectors](http://www.w3.org/TR/CSS2/selector.html)

## JSON.parse / JSON.stringify

In IE7 you could use `JavaScriptSerializer` from ASP.NET Ajax, or you could shim `JSON` with [bestiejs/json3](http://bestiejs.github.io/json3/)
```js
var obj = Sys.Serialization.JavaScriptSerializer.serialize(json);
var json = Sys.Serialization.JavaScriptSerializer.deserialize(obj);
```

In IE8
```js
var obj = JSON.parse(json);
var json = JSON.stringify(obj);
```
```js
JSON.stringify({ soupOfTheYear: 'black bean' });
// > "{"soupOfTheYear":"black bean"}"
```

## localStorage / sessionStorage

Persistent storage *in the browser*

In IE7 we had [cookies](http://www.quirksmode.org/js/cookies.html#ex)

In IE8 we have *the Storage interface*
```
interface Storage {
    readonly attribute unsigned long length;
    DOMString? key(unsigned long index);
    getter DOMString? getItem(DOMString key);
    setter creator void setItem(DOMString key, DOMString value);
    deleter void removeItem(DOMString key);
    void clear();
};
```

#### Session Storage

In browser storage that persists for a single _page_ session.

What's a session?
- Browser is open
- Persists between page reloads
- New tab or a redirect will create a new _page_ session

Useful for saving state of a page (form fields) in case of accidental refresh by a user.

```js
sessionStorage.setItem('soupOfTheDay', 'tomato');
sessionStorage.getItem('soupOfTheDay');
```

#### Local Storage

Same as `sessionStorage` but it ...
- persists between redirects
- persists when opening and closing the browser
- exists across a whole domain

Useful for
- caching assets (like [addyosmani/basket.js](http://addyosmani.github.io/basket.js/))
- saving user preferences like color scheme or font size preferences
- saving reusable form fields, like "User Name"

```js
localStorage.setItem('soupOfTheWeek', 'bisque');
localStorage.getItem('soupOfTheWeek');
```

```js
var obj = { soup: 'Kale' };

// set with JSON.stringify
localStorage.setItem('soup', JSON.stringify(obj));

// get with JSON.parse
obj = JSON.parse(localStorage.getItem('soup'));
```

## hashchange event

```js
window.onhashchange = function () {
    alert(location.hash);
};

function hashTo(hash) {
    location.hash = hash;
}

hashTo('hashySoup');
// > #hashySoup
```

## [CSS outline](http://codepen.io/kavun/pen/axhiv)

## [CSS table display](http://codepen.io/kavun/pen/Jovdn)

## [CSS counters](http://codepen.io/kavun/pen/pGcnk)

## [CSS3 box-sizing](http://codepen.io/kavun/pen/LjFiq?editors=110)

## [CSS content for pseudo elements](http://codepen.io/kavun/pen/slEod)

## [Data URIs](http://codepen.io/kavun/pen/iByxo?editors=100)

## Cross document messaging

- Enables cross-origin communication via `window.postMessage`
- Same-origin would be locations with the same protocol (`http` port `80`), so cross-origin would be across different protocols
- `window` can be
    - `contentWindow` of an `iframe` element
    - the object returned by `window.open`
    - an object in `window.frames`
- When listening for messages sent with `window.postMessage`, **always** check the message's `origin` (URL) and `sender` (`window`) properties to prevent cross-site scripting attacks

## Cross origin resource sharing (CORS)
How can we make an AJAX call from one domain to another?

- Before CORS there was JSONP for cross domain resource loading
```js
function myCallback(data) {}
var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'http://www.someserver.com/api?callback=myCallback';
document.body.appendChild(script);
```
- IE8 added partial support for CORS with its `XDomainRequest` object
```js
var xhr = new XDomainRequest();
xhr.open('GET', 'https://someserver.com/someresource');
```
- All other modern browsers use XMLHttpRequest2 which builds CORS into `XMLHttpRequest`
```js
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://someserver.com/someresource', true);
```

#### More information

- More information from IEInternals about ["Restrictions, Limitations and Workarounds" of `XDomainRequest`](http://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx)
- Cross-browser tutorials on CORS
    - [HTML5Rocks - "Using CORS"](http://www.html5rocks.com/en/tutorials/cors/)
    - [Telerik - "Using CORS with All (Modern) Browsers"](http://blogs.telerik.com/kendoui/posts/11-10-03/using_cors_with_all_modern_browsers)

# Enjoy IE8!
Until you find out [how much better IE9 became](http://caniuse.com/#compare=ie+8,ie+9)