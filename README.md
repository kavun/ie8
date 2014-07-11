# [IE8 \> IE7][]

-   [WAI-ARIA Accessiblity Features][]

-   querySelector / querySelectorAll

-   localStorage / sessionStorage

-   JSON.parse / JSON.stringify

-   hashchange event

-   CSS outline

-   CSS table display

-   CSS counters

-   CSS3 box-sizing

-   CSS content for pseudo elements

-   Data URIs

-   Cross document messaging

-   Cross origin resource sharing

## WAI-ARIA Accesiblity Features

> Semantic information about widgets, structures, and behaviors, in
> order to allow assistive technologies to convey appropriate
> information to persons with disabilities.

> http://www.w3.org/TR/wai-aria/

## Examples

`aria-labelledby`, `aria-invalid`, `aria-expanded`, `aria-readonly`

    <label for="name">Name</label>
    <input type="text" id="name" />

    <label id="lblName">Name</label>
    <input type="text" aria-labelledby="lblName" />

## querySelector() / querySelectorAll()

IE7 vanilla

    var inputs = document.getElementsByTagName('input');
    var checkboxes = [];
    for (var i = 0, l = inputs.length; i < l; i++) {
        if (inputs[i].type === 'checkbox') {
            checkboxes.push(inputs[i]);
        }
    }

jQuery

    var checkboxes = $('input[type="checkbox"]');

IE8 vanilla

    var checkboxes = document.querySelectorAll('input[type="checkbox"]');

## Uses of querySelector(All)

### Single Element

    document.querySelector('input'); // will return only one input
    document.querySelectorAll('input'); // will return all inputs

### Select by ID

    // selects a single element with id="lblSoupSize"
    document.querySelector('#lblSoupSize');

### Select by className

    document.querySelectorAll('.soups');

## Uses of querySelector(All)

### Select by attribute

    document.querySelector('[data-soupid="4d7c6b21"]');

### Relative selectors

    document.querySelector('.soup .spoon');

## localStorage / sessionStorage

Persistent storage in the browser

In IE7 ... [cookies][]

In IE8 ...

    interface Storage {
      readonly attribute unsigned long length;
      DOMString? key(unsigned long index);
      getter DOMString? getItem(DOMString key);
      setter creator void setItem(DOMString key, DOMString value);
      deleter void removeItem(DOMString key);
      void clear();
    };

## Session Storage

> Maintains a storage area that's available for the duration of the page
> session. A page session lasts for as long as the browser is open and
> survives over page reloads and restores. Opening a page in a new tab
> or window will cause a new session to be initiated.

> https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage

    sessionStorage.setItem('soupOfTheDay', 'tomato');
    sessionStorage.getItem('soupOfTheDay');

## Local Storage

> The same as` sessionStorage `[...] but it is persistent

> https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage

    localStorage.setItem('soupOfTheWeek', 'bisque');
    localStorage.getItem('soupOfTheWeek');

## JSON.parse / JSON.stringify

In IE7 (ASP.NET Ajax)

-   `Sys.Serialization.JavaScriptSerializer.serialize()`

-   `Sys.Serialization.JavaScriptSerializer.deserialize()`

In IE8

-   `JSON.parse()`

-   `JSON.stringify()`

<!-- -->

    JSON.stringify({ soupOfTheYear: 'black bean' });
    > "{"soupOfTheYear":"black bean"}"

## hashchange event

## CSS outline

## CSS table display

## CSS counters

## CSS3 box-sizing

## CSS content for pseudo elements

## Data URIs

## Cross document messaging

## Cross origin resource sharing

  [IE8 \> IE7]: http://caniuse.com/#compare=ie+7,ie+8
  [WAI-ARIA Accessiblity Features]: http://www.w3.org/TR/wai-aria/
  [cookies]: http://www.quirksmode.org/js/cookies.html#ex
