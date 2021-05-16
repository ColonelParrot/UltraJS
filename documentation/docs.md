# UltraJS Documentation

## Selecting

UltraJS uses the `f()` selector to select objects. It is based on CSS Selectors, and has the ability to select elements by id, class, tag name, attribute, etc,.

For example, to select the element with the id `test`, use:

```javascript
f('#test')
```

The `f()` selector also accepts a second argument, the scope. For example, `f('#test')` is equivalent to `f('#test', document)`. (removed in version 0.2, re-added in version 0.3)

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
