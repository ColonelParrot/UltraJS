# UltraJS Documentation

## Selecting

UltraJS uses the `f()` selector to select objects or arrays of elements. It is based on CSS Selectors, and has the ability to select elements by id, class, tag name, attribute, etc,.

For example, to select the element with the id `test`, use:

```javascript
f('#test')
```

The `f()` selector also accepts a second argument, the scope. For example, `f('#test')` is equivalent to `f('#test', document)`. (removed in version 0.2, re-added in version 0.3)

**All UltraJS code should be wrapped in the `f.defer` utility method to ensure the contents of the page have been loaded**. For example:

```javascript
f.defer(function(){
  //your UltraJS code here
})
```

For more documentation on `.defer()`, check the **UltraJS Utilities** section below.

## Functions

### `.through(callback)`

The `.through()` function loops through all elements selected and accepts a callback parameter. 2 parameters are passed to the callback, the element currently being looped through and the index.
For example, to log all the selected paragraph elements (`<p>`), use:

```javascript
f('p').through(function(element){
  console.log(element);
})
```

### `.listen(event, callback)`

The `.listen()` function attaches an event listener to the selected elements, and accepts 2 parameters - the event name and the callback. The callback also accepts an event.
For example, the following example alerts "You clicked a button" when a user clicks a button:

```javascript
f('button').listen('click', function(){
  alert("You clicked a button");
});
```

### `.elem()`

The `.elem()` function returns the raw element. For example, to get the first HTMLParagraphElement object by DOM order, use:

```javascript
f('p').elem()
```

### `.get(i)`

The `.get()` function returns the index of the selected elements (it's 0 indexed). Note that this returns an `UltraJSElement` and not an HTMLObject.
For example, to get the 5th selected paragraph element, use:

```javascript
f('p').get(4)
```

### `.raw(i)`

The `.raw()` function returns the index of the selected elements (it's 0 indexed). **This returns a raw HTML Element Object**.
For example, to get the 5th selecte paragraph element, use:

```javascript
f('p').raw(4)
```

### `.attr(name, value)`

The `.attr()` function returns the attribute value of the name, or sets the attribute value. If the second parameter is not included, it will return the value of the attribute name specified in the first parameter.

For example:

```javascript
f('img').get(0).attr('src') // returns the source of the image
f('img').get(0).attr('src', 'path/to/img') // changes the source of the image to 'path/to/img'
```
### `.prop(prop)`

The `.prop()` function gets the value of the property specified in the parameter.

### `style(name)`

The `.style()` function gets the value of a style.

### `.styles(json)`

The `.styles()` function sets the style of the selected elements. It accepts a JSON.
For example, to change all paragraph element's font size to `5em`, use:

```javascript
f('p').styles({'font-size':'5em'})
```

### `.append(element)`

The `.append()` function appends an element to all selected elements. The parameter can be an HTML Element Object, or it can be an HTML element in String form.

For example, the following two code samples produce the same result:

```javascript
var p = document.createElement("p");
p.innerText = "Hello World!";
f('div').append(p);
```
and
```javascript
f('div').append('<p>Hello World!</p>');
```

### `.dimensions()`

The `.dimensions()` function returns an array of JSON strings for the dimensions of each selected element.

### `.remove()`

The `.remove()` function deletes the selected elements from the DOM.

### `.coordinates()`

The `.coordinates()` function returns an array of JSON strings for the x, y coordinates are rendered for the client for each selected element.

### `.value(v)`

The `.value()` function sets the value of the selected elements to the defined parameter.

For example, to set all input field values to "Hello World!", use:

```javascript
f('input').value('Hello World!');
```

### `.hide(renderSpace)`

The `.hide()` function hides the selected elements. If the parameter is set to `true`, it will preserve the space allocated for the element.

### `.show()`

The `.show()` function shows the selected elements.

### `.focus()`

The `.focus()` function applies user focus to the last selected element.

For example, to focus on the last `<input>` element on the page, use:

```javascript
f('input').focus();
```

### `.previous()`

The `.previous() function returns an array of the previous element for each of the selected elements, `null` if non-existent.

### `.next()`

The `.next()` function returns an array of the next element for each of the selected elements, `null` if non-existent.

### `.siblings()`

The `.siblings()` function returns an array of arrays containing the siblings of each selected element (excluding the element iself).

For example, consider the following HTML:

```html
<p class="select-me">Paragraph</p>
<b class="select-me">Emphasis</b>
<i class="select-me">Important</i>
```

Using `.siblings()`:

```javascript
f('.select-me').siblings()
```
returns:

```javascript
(3) [Array(2), Array(2), Array(2)]
  0: Array(2)
    0: b.select-me
    1: i.select-me
    length: 2
    __proto__: Array(0)
  1: Array(2)
    0: p.select-me
    1: i.select-me
    length: 2
    __proto__: Array(0)
  2: Array(2)
    0: p.select-me
    1: b.select-me
    length: 2
    __proto__: Array(0)
length: 3
__proto__: Array(0)
```
### `.text(value)`

The `.text()` function returns an array of the textContent of the selected elements. If a value parameter is specified, the textContent of the selected elements will be set to the value.

### `.html(value)`

The `.html()` function returns an array of the innerHTML of the selected elements. If a value parameter is specified, the innerHTML of the selected elements will be set to the value.

### `.matches(selector, singleValue)`

The `.matches()` function checks the selected elements and returns whether the selected elements match a CSS selector. If `singleValue` is `false`, it will return an array of whether each selected element matches a selector.

### `.scrollUp(px), .scrollDown(px), .scrollTop(), .scrollBottom()`

The `.scrollUp(), .scrollDown(), .scrollTop(), .scrollBottom()` functions are scrolling utilities. `.scrollUp(px)` scrolls up the specified number of pixels, `.scrollDown(px)` vice versa. `.scrollTop()` returns an array of the `scrollTop` attribute of each element, `.scrollBottom()` returns an array of the `scrollBottom` attribute of each element.

## UltraJS Utilities [new]

UltraJS utilities are accessed via the `f` object. They are useful additions to your web application.

For example, to call a method below, use `f.methodName()`.

The methods are:

### `.defer(callback, waitForImages)`

The `.defer()` function runs the callback only if the page (and images if specified) has been completely loaded. For example, the following example alerts the user that the images have been loaded once they are loaded:

```javascript
f.defer(function(){
  alert("images have been loaded");
}, true)
```

### `.injectScript(src, integrity, crossorigin)`

The `.injectScript()` function injects scripts dynamically **even after the page has completed loading**, although it works either way. The `integrity` and `crossorigin` parameters are optional.

For example, to inject a script, use:

```javascript
UltraJS.injectScript("path/to/your/script.js")
```

### `.setState(name, callback)`

Sets a name of a state to the given callback. Used along with the `.is()` function. For example, if you want to check whether an element is the active element, you can define a state called 'active' like so:

```javascript
f.setState('active', function(e){
  return e === document.activeElement;
})
```

And then, to check whether the selected elements are the active element, use:
```javascript
f('input').is('active');
```

### `.removeState(name)`

The `.removeState()` function removes a defined state.

