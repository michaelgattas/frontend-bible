## Front-End Bible:

## May 22, 2024
  ## JS:
  * All objects in JS have a second object (called a prototype) tied to them
  * Any object created with the `new` keyword inherits the prototype of the constructor function
    * e.g. `let o = new Object();` will inherit the prototype of the `Object` constructor, or `Object.prototype`
  * All objects created from Object literals will inherit `Object.prototype`
  * Almost all objects have a prototype, but only a relatively small number of objects have a prototype property
    * It is these objects with prototype properties that define the prototypes for all other objects
  * `Object.prototype` is one of the rare objects in JS that has no prototype
    * Other prototype objects are normal objects that do have a prototype
    * Most built-in constructors (and most user-defined constructors) have a prototype that inherits from `Object.prototype`
      * e.g., `Date.prototype` inherits from `Object.prototype`
        * So, an object created by `new Date()` will inherit from `Date.prototype` and `Object.prototype`
        * This linked series of prototype objects is called a **_Prototype Chain_**
  * Chapter 9 will describe how to set Class constructors up to assign object prototypes for instances created by the constructor
  ## HTML: 
  * Wrap-up of the HTML dialog element today
  ## CSS:
  * Styling lists in CSS is much like styling any other text, with some unique properties
  * The three types of lists in CSS are:
    * Unordered lists (`<ul>`)
    * Ordered lists (`<ol>`)
    * Definition lists (`<dl>`)
  * List-Specific Styles
    * These properties can be set on `<ul>` and `<ol>` elements
      * `list-style-type` : The type of bullet or numbering used
      * `list-style-position` : The position of the bullet or numbering, whether inside or outside the list item
      * `list-style-image` : An image to use as the bullet or numbering

## May 21, 2024
  ## JS:
  * Any value in Javascript that is not a string, a number, a Symbol, or `true`, `false`, `null`, or `undefined` is an object
  * A property name on an Object can be any string, including the empty string (or any Symbol)
  * The value may be any Javascript value, or it may be a getter or setter function (or both)
  * An `own property` refers to a non-inherited property
  * In addition to its name and value, each property has three property attributes:
    * The _writable_ attribute specifies whether the value of the property can be set
    * The _enumerable_ attribute specifies whether the property name is returned by a `for/in` loop
    * The _configurable_ attribute specifies whether the property can be deleted and whether its attributes can be altered
  * Many of JS's built-in objects have properties that are read-only, non-enumerable, or non-configurable
  * By default, however, all properties of the objects you create are writable, enumerable, and configurable
  ## HTML:
  * Today, I am practicing the usage of dialogs in the `index.html` file attached
  ## CSS:
  * The `outline` and `border` properties in CSS have different properties
    * The border is added to the inside of the element, while outline is added to the outside of the element
  * The CSS selector `x + y` will select the first instance of a `y` following an `x` element. 
    * This is the adjacent sibling selector

## May 14, 2024
  ## JS:
  * Unlike statements, **declarations** in JS code don't necessarily "make things happen"
  * Rather, they provide structure for the code and are run before code is actually executed
  * These declarations include `let`, `var`, `const`, `class`, `function`, `import`, and `export`
  * You've already learned much about the `let`, `var`, `const`, and `function` declarations
  * `class` is on the way
  * `import` and `export` are both used to link to **modules** in JS
    * A _module_ is a file of Javascript code with its own global namespace, completely independent of all other modules 
    * Values within modules are private and cannot be accessed by external modules unless they've been explicitly exported
    * The export keyword is sometimes used in addition to other declarations
    * When a module exports only a single value, this is typically done with the special form `export default`
    ```javascript
    export const TAU = 2 * Math.PI;
    export function magnitude(x,y) { return Math.sqrt(x*x + y*y); }
    export default class Circle { /* class definition omitted here */ }
    ```
## May 13, 2024
  ## JS:
  * The `debugger` directive is used to tell the interpreter to pause execution and enter the debugger
    * This is useful for debugging code, as it allows you to inspect the state of the program at that point
    * This acts very similarly to a `breakpoint` set with your developer tools
    * It is only available when the developer tools are open
    * Often used in conjunction with breakpoints, which are set in the developer tools
    * Not a statement in the strict sense, but rather a directive to the interpreter
    * Not supported in all browsers, and should not be used in production code
  * The `use strict` directive is used to enable strict mode in JavaScript
    * Strict mode is a way to opt in to a restricted variant of JavaScript
    * It catches common coding errors and makes it easier to write "secure" JavaScript
    * It is a string literal, and must be the first statement in a script or function
    * It is not a statement, but a directive to the interpreter
    * It is supported in all modern browsers
  * `strict mode` has the following key differences with `non-strict mode`:
    * The `with` statement is not allowed
    * All variables must be declared before they are used
    * All functions invoked as functions (rather than as methods) have a `this` value of `undefined`
      * In non-strict mode, the `this` value would be the global object
    * Assignments to non-writable properties and attempts to create new properties on non-extensible objects throw a `TypeError`
      * In non-strict mode, these assignments fail silently
    * Code passed into `eval` is executed in its own scope, rather than the caller's scope
    * The Arguments object in a function holds a static copy of the values of the arguments passed to the function
      * In non-strict mode, the Arguments object has a magical behavior in which elements of the array and named function parameters both refer to the same value
    * The `delete` operator throws a `SyntaxError` when used on a non-configurable property
      * In non-strict mode, the `delete` operator returns `false` when used on a non-configurable property
    * It is a Syntax Error for an object literal to define two properties of the same name 
    * Octal Integers (beginning with a 0 and not followed by an x) are not allowed
    * Identifiers `eval` and `arguments` are treated as reserved words, and you cannot change their value
      * You cannot assign a value to their identifiers, declare them as variables, use them as function names, use them as function parameter names, or use them as the identifier of a `catch` block
    * The ability to examine the call stack is restricted
      * `arguments.caller` and `arguments.callee` are not allowed, and both throw a `TypeError` within a strict mode function
  ## HTML: 
  * The `<dialog>` represents a modal or non-modal dialog box or other interactive component, such as a dismissible alert, inspector, or subwindow
    * Modal dialog boxes interrupt interaction with the rest of the page, while non-modal dialog boxes allow interaction with the rest of the page
    * Javascript should be used to display the `<dialog>` element
      * Use the `.showModal()` method to display a modal dialog box
      * Use the `.show()` method to display a non-modal dialog box
      * A dialog box can be closed using the `.close()` method
      * Modal dialogs can also be closed by pressing the `esc` key
    * The `tabindex` attribute must not be used on the `<dialog>` element
    * The `open` attribute is a boolean attribute that controls whether the dialog box is displayed
      * It's recommended to use the `.show()` or `.showModal()` methods to display the dialog box
      * If a dialog is opened using the `open` attribute, it will be displayed as a non-modal dialog box
    * HTML `<form>` elements can be used to close a dialog if they have the `method="dialog"` attribute set, or if the button used to submit the form has the `formmethod="dialog"` attribute set
  ## CSS:
  * The `line-height` property sets the height of each line of text
  * Similarly, you can set the `letter-spacing` and `word-spacing` properties to adjust the space between characters and words, respectively

## May 10, 2024
  ## JS:
  * Labeled break statements can allow you to break out of a deeply nested loop. Here's an example
  ```javascript
  let matrix = getData(); // get a 2D array of data from somewhere
  // Now sum all the numbers in the matrix
  let sum = 0, success = false;
  // Start with a labeled statement that we can break out of if errors occur
  computeSum: if (matrix) {
      for (let x = 0; x < matrix.length; x++) {
          let row = matrix[x];
          if (!row) break computeSum;
          for (let y = 0; y < row.length; y++) {
              let cell = row[y];
              if (isNaN(cell)) break computeSum;
              sum += cell;
          }
      }
      success = true;
  }
  // The break statements jump here. If we arrive here with success == false then there was somthing wrong with the matrix we were given.
  // Otherwise, sum contains the sum of all cells of the matrix
  ```
  * The `continue` statement is used to skip the rest of the body of a loop and jump back to the top of the loop to begin a new iteration
    * In the case of a `for` loop, the increment expression is evaluated before the loop condition is tested
    * In the case of a `while` loop, the loop condition is tested before the loop body is executed
    * Here's an example:
    ```javascript
    for (let i = 0; i < data.length; i++) {
        if (!data[i]) continue; // Skip null and undefined values
        total += data[i];
    }
    ```
  * The `return` statement is used to make the interpreter jump from a function invocation back to the code that invoked it
  * The `yield` statement is much like the return statement but is used only in ES6 generator functions to produce the next value in the generated sequence of values without actually returning.
    * In order to understand the `yield`, you must understand iterators and generators
  * The `throw` statement is used to throw an exception, which is a signal that an error or other unusual condition has occurred
    * The `throw` statement requires a single argument, which is the value of the exception that is thrown
    * The `throw` statement is typically used in conjunction with the `try/catch/finally` statement
  * The `finally` statement is used to specify a block of code that will be executed after a `try` or `catch` block, regardless of whether an exception is thrown
    * If any part of the `try` block is executed, the `finally` block will also be executed
    * This statement is often used to clean up resources, such as closing files or network connections
  ## HTML:
  * The `<dfn>` element is used to indicate a term being defined. 
    * It should be used to indicate the term being defined, not the definition itself
    * The ancestor of the `<dfn>` element should be a `<p>`, `<section>`, `<article>`, or `<aside>` element that contains the full definition of the elemtn
    * Or it can be used with `<dd>/<dt>` elements in a `<dl>` element
  ## CSS:
  * The `text-align` property is used to position horizontal alignment of text within its parent container
    * The `text-align` property can have one of the following values: `left`, `right`, `center`, `justify`, `start`, `end`, `match-parent`, `initial`, `inherit`
    * The `text-align` property is inherited by child elements
    * The `text-align` property only affects inline-level and inline-block elements
    * The `text-align` property does not affect block-level elements
    * The `text-align` property does not affect table elements
    * The `text-align` property does not affect flex items

## May 9, 2024
  ## JS:
  * Another form of statement in JS is a `jump` statement
    * The `break` statement makes the interpreter jump to the end of a loop or other statement
    * The `continue` statement makes the interpreter skip the rest of the body of a loop and jump back to the top of a loop to begin a new iteration
    * The `return` statement makes the interpreter jump from a function invocation back to the code that invoked it and also supplies the value for the invocation
    * The `throw` statement is a kind of interim return from a generator function
      * It is designed to work with `try/catch/finally` statements
  * Furthermore, any statement may be labeled by preceiding it with an identifier and a colon:
    ```javascript
    identifier: statement
    ```
    * This is useful for nested loops, where you can break out of the inner loop by referencing the outer loop
  ## HTML: 
  * The `<dd>` element provides the description, definition, or value for the preceding term `<dt>` in a description list `<dl>`
    * This is called the description details element
  * The `<del>` element is used to indicate that text has been deleted from a document
    * This is typically displayed with a strikethrough
    * The `cite` attribute can be used to provide a URL to the source of the deletion
    * The `datetime` attribute can be used to provide a machine-readable date and time for the deletion
    * This could be used to show changes, similar to the `<ins>` element
  ## CSS:
  * In terms of font-size, a `<p>` tag will be set with a default value of `16px` by default
  * Using `em` can be tricky when you're setting the font-size of a parent element, as it will be relative to the parent element
  * Using `rem` is a better choice, as it will be relative to the root element, which is the `<html>` element
  * `font-style` is the property used to turn italic text on or off
  * `font-weight` is the property used to set the weight of the font
  * `text-transform` allows you to set your font to be transformed
    * `none`: prevents any transformation
    * `lowercase`, `uppercase`, `capitalize`
    * `full-width`: converts the text to full-width characters that are written inside a fixed width square
  * `text-decoration` is the property used to set the decoration of the text
    * `none`, `underline`, `overline`, `line-through`, `blink`
  * `text-shadow` allows you to apply drop shadows to your text, setting the horizontal and vertical offsets, blur radius, and color
    

## May 8, 2024
  ## JS:
  * The `for/in` loop iterates over the properties of an object
    * It will iterate over all enumerable properties of an object, including inherited properties
    * The `for/in` loop is not recommended for use with arrays, as it will iterate over the indices of the array, as well as any other enumerable properties
    * The `for/of` loop is recommended for use with arrays, as it will only iterate over the values of the array
    * In addition to built-in methods, many of the built-in properties of objects are non-enumerable
    * All properties and methods defined by your code are enumerable by default
    * The `for/in` loop will iterate over all enumerable string-named properties, whether they are inherited up the prototype chain or not
  * You will learn more about enumerable properties later
  ## HTML:
  * The `<data>` element is used to provide a machine-readable version of the content within it
  ```HTML
    <p>New Products:</p>
    <ul>
      <li><data value="398">Mini Ketchup</data></li>
      <li><data value="399">Jumbo Ketchup</data></li>
      <li><data value="400">Mega Jumbo Ketchup</data></li>
    </ul>
  ```
  * The `<datalist>` element is used to provide a list of predefined `<option>` elements within another control
    * The `<datalist>` element is used in conjunction with the `<input>` element to provide a list of predefined options for the user to choose from
    * The `<datalist>` is given a unique id, which is then referenced by the `list` attribute of the `<input>` element
    * This can be used for autocomplete functionality, or to provide a list of options for the user to choose from
  ## CSS:
  * Today, I start the CSS grids assessment. See `index.html` and `styles.scss` for details

## May 7, 2024
  ## JS:
  * Because strings are iterated by Unicode codepoint, not by UTF-16 character, 
  * The string "I❤JS" has a length of 5, but would be iterated as 4 characters
  * Sets are also iterable in a very predictable, simple way
  * Maps are slightly different because they are iterated not by key or value, but by key/value pairs
    * Here's an example of Map iteration:
    ```javascript 
      let m = new Map([[1, "one"]]); 
      for(let [key, value] of m) {
          key // => 1
          value // => "one" 
      }
    ```
  * The `for/await` loop was introduced in ES2018 and will be covered later, but here's an example
    ```javascript
    async function printStream(stream) {
        for await (let chunk of stream) { 
            console.log(chunk);
        }
    }
    ```
  ## HTML:
  * The `<col>` element defines one or more columns in a column group represented by its parent `<colgroup>` element
    * It's only valid as a child of a `<colgroup>` element that has no span attribute defined
    * An example: 
    ```HTML
    <table>
        <caption>
          Superheros and sidekicks
        </caption>
        <colgroup>
          <col />
          <col span="2" class="batman" />
          <col span="2" class="flash" />
        </colgroup>
        <tr>
          <td></td>
          <th scope="col">Batman</th>
          <th scope="col">Robin</th>
          <th scope="col">The Flash</th>
          <th scope="col">Kid Flash</th>
        </tr>
        <tr>
          <th scope="row">Skill</th>
          <td>Smarts, strong</td>
          <td>Dex, acrobat</td>
          <td>Super speed</td>
          <td>Super speed</td>
        </tr>
    </table>
    ```
    * Here, a `<col>` element is used to group them and assign custom classes, for styling
  * The `<colgroup>` element is used to define a group of columns within a table
    * The `span` attribute specifies the number of columns the `<colgroup>` element should span. 
    * It defaults to 1 and must not be present if there are any `<col>` elements as children
    * The `<colgroup>` element should always appear within a table, after any `<caption>` elements but before any `<thead>`, `<tbody>`, `<tfoot>`, or `<tr>` elements
  ## CSS:
  * The ability to add subgrids enables even more flexibility within this layout model
  * Check the accompanying `index.html` and `styles.scss` files for a full example

## May 6, 2024
  ## JS:
  * A `for/of` loop works on any iterable object in JS
    * This includes Arrays, Strings, Sets, and Maps
  * In order to iterate over an object, you must use
    * A `for/in` loop
    * The `Object.keys()`, `Object.values()`, or `Object.entries()` methods
  * You can destructure an object in a `for/of` loop like so
    ```javascript
    const obj = {a: 1, b: 2, c: 3}
    for (const [key, value] of Object.entries(obj)) {
        console.log(key, value)
    }
    ```
  ## HTML:
  * The `<caption>` element is used to define a table caption
    * This provides an accessible description. 
    * It should be the first child of a `<table>` element
  * The `<cite>` element is used to define the title of a work
    * This is typically used for a book, movie, song, or other creative work
    * It should be used to provide a citation to the work
    * This is normally used inside of a `<blockquote>` or `<q>` element
    * Most browsers will style the `<cite>` element with italics, but you can override this with CSS
  * The `<code>` element is used to define a piece of computer code
    * This is normally formatted using the user agent's monospace font
  ## CSS:
  * In addition to setting the `grid-column` and `grid-row` properties, you can also use `grid-template-areas` to define the layout of different sections
  * Check the `index.html`/`styles.scss` files for a full example, but here's an example:
  ```CSS 
    .container {
      display: grid;
      grid-template-areas:
        "header header"
        "sidebar content"
        "footer footer";
      grid-template-columns: 1fr 3fr;
      gap: 20px;
    }
    
    header {
      grid-area: header;
    }
    
    article {
      grid-area: content;
    }
    
    aside {
      grid-area: sidebar;
    }
    
    footer {
      grid-area: footer;
    }
  ```
## May 3, 2024
  ## JS:
  * Explicitly, the `for` loop syntax is 
  ```javascript 
    for (initialize; test; increment) { 
        statement 
    }
  ```
  * An interesting way to compare it to a `while` loop:
  ```javascript
    initialize;
    while (test) {
        statement;
        increment;
    }
  ```
  * Most `for` loops are numeric, but they can be used to iterate over many different types of data structures:
  ```javascript
  function tail(o) {
    for (; o.next; o = o.next) /* empty */ ;
    return o;
  }
  ```
  ## HTML: 
  *  The `<canvas>` element uses either the canvas scripting API or the WebGL API to draw graphics and animations
  * It uses the global attributes, and some noticeable ones are:
    * `height` : The height of the canvas
    * `width` : The width of the canvas
  * Unlike the `<img>` element, the `<canvas>` element requires the closing tag
  * iOS devices notably limit maximum canvas size to 4,096 x 4,096 pixels, whereas most other browsers allow 10,000 x 10,000 pixels
  * Using the `OffscreenCanvas` API, you can create a canvas that is not visible in the DOM, but can be used to render images offscreen
  * It is good practice to include alternative text within the canvas to describe what is happening on the canvas
  * For more detailed description of using the `Offscreen Canvas` API and the `Canvas` API
  ## CSS: 
  *  You can specify an item's placement within the grid using the `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end` properties
  * These are often shortened to `grid-column` and `grid-row` properties
  * For example: 
  * ```CSS
    .item {
        grid-column: 1 / 3;
        grid-row: 1 / 3;
    }
    ```
    * This will place the item in the first column, spanning two columns, ending after the 3rd, and in the first row, spanning two rows, ending after the 3rd

## May 2, 2024
  ## JS:
  * `else if` is not actually a statement in proper JS, and is instead an idiom used by programmers to make these nested conditionals more legible
  * A `switch` statement in JS looks like this:
  ```javascript
    switch (expression) {
        case value1: // starting point 1
        // code block
        break;
        case value2: // starting point 2
        // code block
        break;
        default: // final starting point
        // code block
    }
  ```
  * It's also worth noting that the `===` operator is used to check equality in this context
  The purpose of these `case` statements is to provide a starting point for the code block to execute, and the `break` statement is used to exit the `switch` statement
  ## HTML: 
  * The `<button>` attribute is used to define a button 
    * It inherits the global attributes
    * Notable attributes include `autofocus`, `disabled`, and `type`
    * When the button is part of a form, the `type` attribute can be `submit`, `reset`, or `button`
      * The `submit` type will submit the form data to the server, and is the default type if the `type` attribute is not specified
      * If your buttons are not for submitting form data to a server, be sure to set their `type` attribute to `button`
        * Otherwise, the default behavior of the button will be to submit the form data to the server, possibly destroying the current state of teh document
    * If a button is attached to a form, the following attributes help direct this call:
      * `formaction` : The URL that processes the form data when the form is submitted
      * `formenctype` : The encoding type for the form data
      * `formmethod` : The HTTP method used to submit the form data
      * `formnovalidate` : A Boolean attribute that specifies that the form data should not be validated when submitted
      * `formtarget` : The target window or frame where the form data is submitted
      * `name` : The name of the button, which is submitted with the form data
      * `value` : The value of the button, which is submitted with the form data
      * `form` : The form element id that the button is associated with
    * For accessibility, it's best practice to include text along with any icon within a button, to ensure cultural or technological gaps in understanding can be overcome by the user
  * Firefox will add a small dotted border around a button when it is focused, but this can be removed with the following CSS:
    ```CSS
    button::-moz-focus-inner {
      outline: none;
    }
    ```
  ## CSS:
  * If you set a `grid-auto-rows` value to `100px' but want to make sure than any overflown text in a row would still display
  * In this case, simply use the `minmax()` function to set a minimum and maximum height for the row
  * For example:
  ```CSS
    .container {
        display: grid;
        grid-template-columns: 100px 100px 100px;
        grid-auto-rows: minmax(100px, auto);
    }
  ```
  * In this case, the row will be at least 100px tall, but will expand to fit the content if it is larger than 100px
  * You can also configure a value that allows as many columns as will fit, using a combination of `auto-fit` and `minmax()`
  * For example:
  ```CSS
    .container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        grid-auto-rows: minmax(100px, auto);
        gap: 20px;
    }
  ```

## April 30, 2024
  ## JS:
  * The comma operator (`,`) is used to evaluate any left-hand operands, then return the value of the right-hand-most operand
  * An example would be 
  ```javascript 
  i = 0, j = 0, k = 2;
  // you could also write something like 
  i = 0, j = 0, k = someVal === 2 // in this case, the comma operator discards the left operand values and returns 'someVal' assigned to k for comparison to the number 2
  ```
  * The most common example of the comma operator is in a `for` loop, where multiple variables are used, and operands with side effects exist on both sides of the comma
  ```javascript
  for (let i = 0, j = 1; i < 10, j < 5; i++, j++) {
    console.log(i, j)
  }
  ```
  * **Expressions** are evaluated to produce a value, but **Statements** are executed to make something happen
  ## HTML:
  * The `<body>` element represents the content of an HTML document.
    * There can only be one body element
    * In addition to the global attributes, the body element has the following:
      * `onafterprint`: function to call after the user has printed the doc
      * `onbeforeprint`: function to call before the user prints the doc
      * `onbeforeunload`: function to call before the doc is unloaded
      * `onblur`: function to call when the element loses focus
      * `onerror`: function to call when an error occurs
      * `onfocus`: function to call when the element gets focus
      * `onhashchange`: function to call when there has been a change in the anchor part of the URL
      * `onlanguagechange`: function to call when the user changes the language of the page
      * `onload`: function to call when the element is finished loading
      * `onmessage`: function to call when the element receives a message
      * `onoffline`: function to call when the browser starts to work offline
      * `ononline`: function to call when the browser starts to work online
      * `onpopstate`: function to call when the window's history changes
      * `onredo`: function to call when the document performs a redo
      * `onresize`: function to call when the document view is resized
      * `onstorage`: function to call when the storage area has changed
      * `onundo`: function to call when the document performs an undo
      * `onunload`: function to call when the document is being unloaded
  * The `<br>` element is used to insert a line break in text
    * The `<br>` element is an empty element, which means it does not have a closing tag
    * This element is meant to break up a paragraph, like a poem or a speech, where specific line breaks are necessary
    * Never adjust the margins on a `<br>` element, and instead adjust the `line-height` property of the parent element
    * There are accessibility concerns associated with the `<br>` element, as it can be misused to create a new paragraph, when a `<p>` element should be used instead
    * For the purpose of screen readers and accessibility, it is recommended not to use a `<br>` element to create a new paragraph
  ## CSS:
  * You can repeat all or part of a track listing using the CSS `repeat()` function
  * E.g.
  ```CSS
  .container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 20px;
  }
  ```
  * Explicit grids are created using `grid-template-columns` and `grid-template-rows
  * Implicit grids extends the defined explicit grid when content is placed outside of that grid, such as into the rows by drawing additional grid lines
  * By default, tracks created in the grid are auto-sized, which means they're large enough to contain their content
  * You can also give them a size using `grid-auto-rows` and `grid-auto-columns`
  * Using `grid-auto-columns` with `grid-template-columns` will not overwrite the explicit grid

## April 29, 2024
  ## JS:
  * The `eval` function is used to evaluate a string as JavaScript
    * Generally, the `eval` function will use the variable environment of the code that calls it
    * This means that the `eval` function can access variables in the calling code, reassign them, etc.
    * It can also create new variables in that scope using the `var` variable declaration keyword
    * `let` and `const` variables are block-scoped, so they will not be accessible outside the `eval` function
    * If the `eval` is aliased and called by any other name, its scope will be treated as global scope, and any local variables or functions from the calling scope will not be accessible within the `eval` code
    ```javascript 
    const geval = eval
    let x = "global", y = "global"
    function f() {
        let x = "local"
        eval("x += 'changed';")
        return x;
    }
    function g() {
        let y = "local"
        geval("y += 'changed';")
        return y;
    }
    
    console.log(f(), x); // Local variable changed: prints "localchanged global"
    console.log(g(), y); // Global variable changed: prints "local globalchanged"
    ```
    * The notable difference is the context in which the eval function is called, and the scope in which it is executed in each case
  * The `delete` operator is used to remove a property from an index or object
    * The `delete` operator returns `true` if the property is successfully deleted, and `false` otherwise
    * If the property is non-existent, `delete` will return `true`
    * If the property is non-configurable, `delete` will return `false`
    ```javascript 
     let obj = {a: 1, b: 2, c: 3}
     delete obj.a // true
     delete obj.d // true
     delete obj // false
     
     let arr = [1, 2, 3]
     delete arr[0] // true
     delete arr[3] // true
     delete arr // false
     console.log(arr) // [empty, 2, 3]
     console.log(arr.length) // 3, because the array still has 3 elements, this is called a "sparse array"
    ```
  ## HTML:
  * The `<bdo>` or Bi-directional Text Override element is used to override the Unicode bidirectional algorithm
    * This is useful when you want to display text in a different direction than the surrounding text
    * The `dir` attribute is used to specify the direction of the text
    * The `dir` attribute can have one of three values: `ltr`, `rtl`, or `auto`
    * The `ltr` value specifies that the text should be displayed from left to right
    * The `rtl` value specifies that the text should be displayed from right to left
    * The `auto` value specifies that the text should be displayed in the direction of the surrounding text
    * The main difference between the `bdi` and `bdo` elements is that the `bdi` element isolates the text from its surrounding text, while the `bdo` element overrides the Unicode bidirectional algorithm
    ```html 
    <h1>Famous seaside songs</h1>
    <p>The English song "Oh I do like to be beside the seaside"</p>
    <p>Looks like this in Hebrew: <span dir="rtl">אה, אני אוהב להיות ליד חוף הים</span></p>
    <p>In the computer's memory, this is stored as <bdo dir="ltr">אה, אני אוהב להיות ליד חוף הים</bdo></p>
    ```
  * The `<blockquote>` element is used to define a block of text that is quoted from another source
    * You can use the `cite` attribute to specify the source of the quotation
    * You can also use a `<cite>` element to specify the title of the source
    * See the `index.html` file to see how you can use a footer to cite the source of the quote
    * Also keep in mind that you can use a `<q>` element to define a short inline quotation
  ## CSS:
  * Grids, grids, grids
    * The `grid-template-columns` property is used to define the number and size of columns in a grid container
    * Here, you can define the size of each column using a length, a percentage, or a fraction of the available space
    * To add space across both access of the grid, you can specify the gap property:
    ```CSS
    .container {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr;
      gap: 25px;
    }
    ```
    * Alternatively, `column-gap` and `row-gap` properties also specify gap space

## April 26, 2024
  ## JS:
  * The assignment operator `=` has right-to-left associativity which means that the rightmost expression is evaluated first
    * This is why you can chain assignments like `let a = b = c = 5`
    * The rightmost expression is evaluated first, and then assigned to the next variable to the left
    * This is also why you can chain assignments with different types of variables
    * For example, `let a = b = 'hello'` will assign the string `'hello'` to `b`, and then assign `b` to `a`
  * Also, the assignment operator might be nested inside more complex logic, like `(a = b) === 0`
    * In this case, the assignment operator is evaluated first, and then the comparison operator is evaluated
  ## HTML:
  * The `<bdi>` element is used to tell a browser about bi-directional text
    * This is useful when you have text in multiple languages, or text that is mixed with numbers
    * The `<bdi>` element isolates the text from its surrounding text, so that the browser can display it correctly
    * For example: 
    * ```html
      <p>Here is some text in English: <bdi>שלום</bdi></p>
      ```
  ## CSS:
  * The `display` property in CSS is used to determine how an element is displayed
    * The `display` property is used to determine the layout of an element, and how it interacts with other elements on the page
    * The `display` property is one of the most important properties in CSS, and is used to control the layout of a web page
      * The `block` value makes an element a block-level element, which means it will take up the full width of its container, and will start on a new line
      * The `inline` value makes an element an inline-level element, which means it will only take up as much width as it needs, and will not start on a new line
      * The `inline-block` value makes an element an inline-block element, which means it will take up as much width as it needs, but will start on a new line
      * The `flex` value makes an element a flex container, which means it will lay out its children in a flex layout
      * The `grid` value makes an element a grid container, which means it will lay out its children in a grid layout
      * The `none` value makes an element invisible, and it will not take up any space on the page
      * The `table` value makes an element a table element, which means it will lay out its children in a table layout
      * The `flow-root` value makes an element a block-level element, and establishes a new block formatting context

## April 25, 2024
  ## JS:
  * The `instanceof` operator checks if an object is an instance of a class
    * It returns `true` if the object is an instance of the class, and `false` otherwise
    * It can also be used to check if an object is an instance of a subclass
    * It can also be used to check if an object is an instance of an interface
    * Interesting, it's not quite the same thing as `typeof`, which checks the type of a variable
  * For example, if you were to declare `x = 2` and `y = new Number(2)`, then `x instanceof Number` would return `false`, while `y instanceof Number` would return `true`
  * This is because `x` is a primitive number, while `y` is an instance of the `Number` class
  * The difference between a primitive number and an instance of the `Number` class is that the `Number` class has methods and properties that can be accessed
  * Here's a code block from JS The Definitive Guide (p. 173) to further explain how the `instanceof` operator works:
  ```javascript
    let d = new Date(); // Create a new object with the Date() constructor
    d instanceof Date // => true: d was created with Date()
    d instanceof Object // => true: all objects are instances of Object
    d instanceof Number // => false: d is not a Number object 
    let a = [1, 2, 3]; // Create an array with array literal syntax
    a instanceof Array // => true: a is an array
    a instanceof Object // => true: all arrays are objects
    a instanceof RegExp // => false: arrays are not regular expressions
  ```
  ## HTML:
  * The `<base>` element specifies the base URL to use for all relative URLs in a document
    * The `<base>` element must have an `href` attribute, which specifies the base URL, or a `target` attribute, which specifies the default target for all hyperlinks and forms in the document
    * The `<base>` element must be placed inside the `<head>` element
    * The `<base>` element is supported by all major browsers
    * A document's used base URL can be accessed by scripts with `Node.baseURI`. If the document has no <base> elements, then baseURI defaults to `location.href`
  ## CSS:
  * In a `display: grid` context, you can use `fr`, or fractional units to take up a given proportion of the available space
  * For example:
    ```CSS
    .container {
      display: grid;
      grid-template-columns: 1fr 2fr 1fr;
    }
    ```

## April 24, 2024
  ## JS:
  * The `in` operator expects a lefthand argument that is a string, symbol, or can evaluate to a string, and a righthand side argument that is an Object
  * The `in` operator will return `true` if the lefthand argument is a property of the righthand object, and `false` otherwise
  * For objects, this is rather intuitive:
    ```javascript
    let obj = {a: 1, b: 2, c: 3}
    console.log('a' in obj) // true
    console.log('d' in obj) // false
    ```
  * For arrays, the `in` will return true if the passed in string/symbol is a valid index of the array.
    * So the "index" is treated like a property in this case
    * It does not evaluate array values
    ```javascript
    let arr = [1, 2, 3]
    console.log('0' in arr) // true
    console.log('1' in arr) // true
    console.log(`3` in arr) // false, because the array only has indices 0, 1, and 2
    ```
  ## HTML: 
  * The `<b>` element is a stylistic element that provides bold formatting to text
    * It is no longer recommended, with either `<strong>` or `<span>` with CSS `font-weight` styling being preferred
    * Here's where the docs get nitpicky:
      * The `<strong>` element indicates text of certain **importance**
      * The `<em>` element indicates text of certain _emphasis_
      * The `<mark>` element indicates text with certain relevance (highlighting)
    * If there is no semantic importance, emphasis, or relevance, then the `<span>` element with CSS styling is recommended
  ## CSS:
  * **Font stacks** enable you to create fall-backs if a web-font fails to load
  * The `font-family` property can take a comma-separated list of font names, with the browser trying each font in order
  ```CSS
    p {
      font-family: "Trebuchet MS", Verdana, sans-serif;
    }
  ```
  * In this case, the browser will first try to load "Trebuchet MS", then "Verdana", and finally any sans-serif font

## April 23, 2024
  ## JS:
  * The shift left operator `<<` shift the bits of a number to the left, filling empty bits with 0's
    * This is effectively the same as multiplying by 2
  * The shift right operator `>>` shifts the bits of a number to the right, filling the empty bits with the sign bit (0 for positive numbers, 1 for negative numbers)
    * This is effectively the same as dividing by 2, but always rounding down
  * In a strict equality check, `NaN` is no equal to itself. 
    * A good shorthand way is to use the global `isNaN()` function or to check is `x !== x`
  * Also, in a strict equality check, `0` is equal to `-0`
  ## HTML:
  * The `<article>` element is a semantic element that defines a self-contained piece of content that could be distributed and reused independently
    * It could be a blog post, a forum post, a news article, or a comment
    * The `<article>` element is a block-level element, and will typically be displayed in a normal font
    * The `<article>` element is a semantic element, and should be used to provide meaning to the content
    * The `<article>` element is supported by all major browsers
  * The `<aside>` element is a semantic element that defines content that is tangentially related to the content around it
    * It could be a sidebar, a pull quote, a glossary, or a related article
    * The `<aside>` element is a block-level element, and will typically be displayed in a normal font
    * The `<aside>` element is a semantic element, and should be used to provide meaning to the content
    * The `<aside>` element is supported by all major browsers
  ## CSS:
  * The `justify-items` property is ignored in a flex container, as it only applies to grid containers
  * Instead, justifying items in a flex container is done with the `justify-content` property
    * `start`, `end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch`, `safe`, `unsafe`
  

## April 22, 2024
  ### JS: 
  * The increment and decrement operators have a pre- and post- versions, which return the value before or after increment/decrement
  * For example: 
    ```javascript
    let x = 5 
    let y = x++ // y == 5, x == 6
    let z = ++x // z == 7, x == 7
    ```
  * Basically the pre- or post- defines if the change to the original will happen pre- or post- the assignment to the `lval` in question
  * Remember, all increment/decrement operators must use `lval`, so must be a 
    * Variable
    * Array item
    * Object property
  ### HTML:
  * The `<area>` element is only used within an image map (`<map>`) element in order to allow for clickable areas
  * It will normally use a `shape` and `coords` attribute to define the clickable area
  * Here's an example from the docs site: 
    ```html
    <map name="infographic">
        <area
            shape="poly"
            coords="129,0,260,95,129,138"
            href="https://developer.mozilla.org/docs/Web/HTTP"
            target="_blank"
            alt="HTTP" 
        />
        <area
            shape="poly"
            coords="260,96,209,249,130,138"
            href="https://developer.mozilla.org/docs/Web/HTML"
            target="_blank"
            alt="HTML" 
        />
        <area
            shape="poly"
            coords="209,249,49,249,130,139"
            href="https://developer.mozilla.org/docs/Web/JavaScript"
            target="_blank"
            alt="JavaScript" 
        />
        <area
            shape="poly"
            coords="48,249,0,96,129,138"
            href="https://developer.mozilla.org/docs/Web/API"
            target="_blank"
            alt="Web APIs" 
        />
        <area
            shape="poly"
            coords="0,95,128,0,128,137"
            href="https://developer.mozilla.org/docs/Web/CSS"
            target="_blank"
            alt="CSS" 
        />
    </map>
    <img usemap="#infographic" src="/media/examples/mdn-info.png" alt="MDN infographic" />
    ```
  ### CSS: 
  * A block-level element always starts on a new line, taking up the entire space availab to it along the main-axis (x-axis for English text)
  * An inline-level element only takes up as much space as it needs, and does not start on a new line. A span is an exampel of an inline element.
  * Here is code from the CSS Docs demonstrating the differences
  * ```html
    <h1>Basic document flow</h1>

    <p>
      I am a basic block level element. My adjacent block level elements sit on new
      lines below me.
    </p>
    
    <p>
      By default we span 100% of the width of our parent element, and we are as tall
      as our child content. Our total width and height is our content + padding +
      border width/height.
    </p>
    
    <p>
      We are separated by our margins. Because of margin collapsing, we are
      separated by the width of one of our margins, not both.
    </p>
    
    <p>
      Inline elements <span>like this one</span> and <span>this one</span> sit on
      the same line along with adjacent text nodes, if there is space on the same
      line. Overflowing inline elements will
      <span>wrap onto a new line if possible (like this one containing text)</span>,
      or just go on to a new line if not, much like this image will do:
      <img src="long.jpg" alt="snippet of cloth" />
    </p>
    ```

## April 17, 2024
  ### JS:
  * In JS, an `lval` is a value that can legally be on the left-side of an assignment expression
    * This includes variables, properties of objects, and elements of arrays
  ### HTML:
  * The `<address>` HTML element indicates that the enclosed HTML provides contact information for a person or people, or for an organization
    * The `address` element is a block-level element, and will typically be displayed in an italic font
    * The `address` element is a semantic element, and should be used to provide meaning to the content
    * The `address` element is supported by all major browsers
  * Although it formats equivalently as using an `<i>` or `<em>` tag, the `<address>` tag is more semantically correct
  * No attributes for this elements beyond the global attributes
  ### CSS:
  * By default, all flex-items have a `order` property of 0
  * Increased order property means an item comes later in the order of items
    * ```CSS
      article {
          order: 1;
      }
      article:nth-of-type(3) {
          order: 2;
      }
      ```
    * This will give the third article a later order than the other articles

## April 16, 2024
  ### JS:
  * Operators in JS do have an order of operation (like PEMDAS)
    * We call this **operator precedence** (which operator is evaluated first) and **operator associativity** (which operator is evaluated first in the case of operators with the same precedence)
    * Generally, access operators and invocation operators take top precedence
    * Mult/Division operators take precedence over Add/Subtract operators
    * Use parentheses to ensure the order of operations you want
  * The `??`, or **Nullish Coalescing Operator** in JS returns its right-hand side operand when its left-hand side operand is null or undefined
    * Unlike the `||` operator, the `??` operator doesn't coerce its left-hand side operand to a boolean
    * Therefore: 
    ```javascript
    let x = null 
    let y = x ?? 'default' // y == 'default'
    x = 0
    y = x ?? 'default' // y == 0, since 0 is not null or undefined
    x = false
    y = x ?? 'default' // y == false, since false is not null or undefined
    ```
  ### HTML:
  * The `<abbr>` or abbreviation element is used to mark up an abbreviation or acronym
    * The `title` attribute is used to provide the full expansion of the abbreviation
    * The `title` attribute is also used to provide a tooltip when the user hovers over the abbreviation
    * The first time using an abbreviation on a page, it's a good idea to use the `<abbr>` element to fully expand it
    * Only extends the global attributes, and has no specific attributes of its own
    * The `<abbr>` element is a semantic element, and should be used to provide meaning to the content
    * Supported by all major browsers
  ### CSS:
  * Within a flex container, you can assign flex values to each flex-item
    * ```CSS
      article {
          flex: 1;
      }
      article:nth-of-type(3) {
          flex: 2;
      }
      ```
    * This will give the third article twice the space of the other articles
## April 15, 2024
  ### JS:
  * In a regular _Property Access Expression_ (like `expression.property` or `expression[expression]`):
  * We either use a _dot_ followed by a valid identifier (cannot be a number, reserved keyword, or start with a number or special character)
  * Or we use an expression to access a property, which is evaluated to a string literal or symbol
  * In either case, accessing a property that doesn't exist will return `undefined`
  * Optional Chaining allows the ability to access deeply nested properties without throwing an error if a property doesn't exist
    * It's denoted by a `?.` after the object or array, and will return `undefined` if the property doesn't exist
    * It's especially useful when working with APIs, where the data structure may not be consistent
    * It's also useful when working with user input, where the data may not be complete
  ### HTML:
  * The `<a>` or "anchor" tag is used to create hyperlinks to other web pages, files, locations within the same page, email addresses, or any other URL\
  * The `href` indicates the destination of the link
    * Acceptable alternative link formats include: 
      * Telephone numbers with `tel:` URLs 
      * Email addresses with `mailto:` URLs 
      * SMS text messages with `sms:` URLs
  * `hreflang` specifies the language of the linked resource - allowed values are the same as the global `lang` attribute
  * `ping` is a space-separated list of URLs to which, when the link is followed, post requests with the body `ping` will be sent
    * These are typically used for trackers, analytics, and other monitoring purposes
  * `referrerpolicy` specifies how much of the referrer information should be sent when following the link
    * `no-referrer` : The `Referer` header will not be sent
    * `no-referrer-when-downgrade` : The `Referer` header will not be sent to a less secure destination
    * `origin` : Only the origin of the document will be sent (its scheme/protocol, host and port)
    * `origin-when-cross-origin` : The full URL will be sent if the destination is the same origin, otherwise only the origin will be sent
    * `same-origin` : The full URL will be sent if the destination is the same origin, otherwise no `Referer` header will be sent
    * `strict-origin` : The full URL will be sent if the destination is the same origin, otherwise only the origin will be sent
    * `strict-origin-when-cross-origin` : The full URL will be sent if the destination is the same origin, otherwise only the origin will be sent
    * `unsafe-url` : The full URL will be sent, regardless of the destination
  * `rel` specifies the relationship between the current document and the linked document
  * `target` specifies where to open the linked document
    * `_blank` : Opens the linked document in a new window or tab
    * `_self` : Opens the linked document in the same frame as it was clicked
    * `_parent` : Opens the linked document in the parent frame
    * `_top` : Opens the linked document in the full body of the window
    * `framename` : Opens the linked document in a named frame
  * You can also link to sections below with an `href` of `#section-name`, where the id is set to another section
  * Using an `<a>` tag with a `target="_blank"` attribute will open the link in a new tab, with some security considerations
    * The new tab or window will often have access to the original page, through the `window.opener` property
    * In a "Tabnabbing" attack, the new tab will change its location to a phishing site, while the original page is still open
    * In a "Reverse Tabnabbing" attack, the original (legitimate) page have its location changed to a phishing site, as the new tab accesses the `window.opener` property
    * Many browsers have implemented security measures to prevent these attacks, but it's still a good idea to be aware of the risks, and use `noopener` and `noreferrer` attributes to prevent these attacks
  ### CSS:
  * If you had a flex container and wanted to ensure that overflowing elements in your flex direction will wrap onto a following row/column, you can set `flex-wrap: wrap`
  * So, if you wanted to distribute child div's along a row with following rows for any extra children, you could write:
    ```CSS
    flex-direction: row;
    flex-wrap: wrap;
    ```
  * Conversely, you can also simply set:
    ```CSS
    flex-flow: row wrap;
    ```

## April 11, 2024
  ### JS:
  * While `null` is a reserved keyword representing the null value, 
  * `undefined` is a property of the global object representing the absence of a value 

 ### HTML:
  * The `draggable` element is useful for creating drag-and-drop functionality in web applications
  * In addition to setting draggable to true or false, you have to set the `ondragstart` handler for the source element
  * Finally, you have to handle `ondragover` and `ondrop` events for the target element(s), since their default behavior is normally not to accept drag events
  * Pertinent YT vid here: https://www.youtube.com/watch?v=hCsuyZHlUtY
  * More about the Drag and Drop API: https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API

  ### CSS:
  * The flexbox model is one-dimensional, meaning it deals with one dimension at a time
    * You're either formatting rows or columns, not both at the same time
  * There is the `main-axis` and the `cross-axis`
    * The `main-axis` is the axis along which the flex items are laid out
    * The `cross-axis` is the axis perpendicular to the main axis
  * You can define the direction of the main axis with the `flex-direction` property
    * `row`, `row-reverse`, `column`, `column-reverse`
  * The area of a document that is laid out using flexbox is called a `flex container`
    * To create a flex container, set the area's `display` property to `flex` or `inline-flex

  * The contents of a flex container will (by default) behave in the following ways:
    * `flex-direction` is set to `row`
    * Items start from the start edge of the main axis
    * Items do not stretch on the main dimension, but can shrink
    * Items stretch on the cross dimension to fill the container
    * The flex-wrap property is set to `nowrap` 
      * Flex items will always remain in a single row or column, overflowing their container if their combined width/height exceeds the containing element width/height.

## April 10, 2024
  ### JS: 
  * Object/Array Destructuring
    * Destructuring is a great way to streamline variable assignment off of one source object or array
      * Array Destructuring
        ```javascript
        // very easy if you want to assign variables with the same names as their indices
        const arr = [1, 2, 3]
        const [a, b, c] = arr
        console.log(a, b, c) // 1, 2, 3
        
        let [x,y] = [1]; // x == 1; y == undefined [x,y] = [1,2,3]; // x == 1; y == 2
        [,x,,y] = [1,2,3,4]; // x == 2; y == 4
        let [x, ...y] = [1,2,3,4]; // y == [2,3,4]
        ```
      * Object Destructuring
        ```javascript
        // very easy if you want to assign variables with the same names as their properties
        const obj = {a: 1, b: 2, c: 3}
        const {a, b, c} = obj
        console.log(a, b, c) // 1, 2, 3
      
        // you can also assign variables with different names than their properties
        const obj2 = {d: 4, e: 5, f: 6}
        const {d: x, e: y, f: z} = obj2
        console.log(x, y, z) // 4, 5, 6
        
        // or destructure functions off of objects for tighter code
        const {sin, cos, tan} = Math
        const {floor, ceil, round} = Math
        
        // you can even destructure any iterable object, including strings!
        let [first, ...rest] = "Hello"; // first == "H"; rest == ["e","l","l","o"]
        ```
  ### HTML:
  * Audio Elements `<audio>`
    * The `<audio>` element has no intrinsic visual output of its own unless the controls attribute is specified, in which case the browser's default controls are shown
    * If you attribute multiple `<source>` elements to an `<audio>` element, the browser will choose the first one it can play
    * Audio elements do not inherently support subtitles or captions (WebVTT)
      * You either need to use a `<video>` element or a JavaScript library to add subtitles
    * There are a number of events emitted by the `<audio>` element, including:
      * `onplay`, `onpause`, `onvolumechange`, `onseeking`, `onseeked`, `onended`, `oncanplay`, `oncanplaythrough`, `onloadedmetadata`, `onloadeddata`, `onwaiting`, `onplaying`, `onstalled`, `onsuspend`, `onabort`, `onerror`
  ### CSS:
  * The `css justify-content` property defines how the browsers sets the spaces between and around content items along the main (x) axis of a flex container
    * `start', `end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch`, `safe`, `unsafe`
  * The `justify-items` property sets the default alignment for items inside a grid container along the inline (x) axis
  * The `justify-self` property sets the alignment of an item within its containing grid or flexbox, overriding the `justify-items` property if it's present
    * `auto`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `safe`, `unsafe`

## April 9, 2024
  ### JS:
   * You can include multiple variables, multiple loop conditions, and even multiple increment/decrement operators inside of a `for` loop
        ```javascript
        functional = () => {
          for (let i =1, x = 7; i < 100 && (i % x !== 0); i++, j--) {
              console.log(i)
          }
        }
        ```
   * Here, we can declare two variables and set two conditions for the loop to run, we could also include multiple 
  ### HTML:
   * The `<nav>` element is used to define a set of navigation links
   * Common examples of navigation sections are menus, tables of contents, and indexes
   * The `<nav>` element is intended only for major block of navigation links
   * Links do not need to be present exclusively inside of a `<nav>` element
   * A footer may contains links outside of a nav element
   * A nav could be used for providing a navbar, or a table of contents within the body of a document
  ### CSS:
   * The `align-content` property sets the distribution of space between and around content items along a flexbox's cross axis, or a grid or block-level element's block axis
     * `start`, `end`, `center`
     * `space-between`, `space-around`, `space-evenly`, `stretch`
     * `safe`, `unsafe` - safety resets alignment to the `start` value to prevent data loss in the case of overflow, but `unsafe` honors the alignment value
   * The `align-items` property sets the `align-self` for all direct children as a group
   * The `align-self` property sets the alignment of an item within its containing flexbox or grid
     * `auto`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `safe`, `unsafe`
   * SO Link to more specifically describe how these properties work together: https://stackoverflow.com/questions/31250174/css-flexbox-difference-between-align-items-and-align-content

## April 8, 2024
  ### JS:
 * Converting Objects to primitive values in JS is very complicated and dependent on the source object
 * For instance, a `Date` object has both a numeric and a string representation. Which is its true primitive value?   
 * All Objects converted to a Boolean are true, except for the special cases of `null` and `undefined`
   * The <i><b>Prefer-String</b></i> Algorithm
     * First tries the `toString` method, returning this primitive value (even if it is not a string)
     * If `toString` returns a non-primitive value, it tries `valueOf` method
     * If `valueOf` returns a non-primitive value, it returns a `TypeError`
   * The <i><b>Prefer-Number</b></i> Algorithm
     * First tries the `valueOf` method, returning this primitive value
     * Next, tries `toString` method
     * Else, returns a `TypeError`
   * The <i><b>No-Preference</b></i> Algorithm
     * This algorithm depends on the class of the object being converted
     * If the object is a Date, it uses the `Prefer-String` algorithm
     * For any other object, it uses the `Prefer-Number` algorithm
   
   * This behavior explains why `Number([])` returns 0
     * First, it tries the `valueOf` method, which returns an empty array, not a primitive value
     * Next, it tries the `toString` method, which returns an empty string
     * `''` is a primitive value that evaluates to zero as it's converted to a number
   * This behavior explains why `Number(['99'])` returns 99
     * First, it tries the `valueOf` method, which returns an array with a single element
     * Next, it tries the `toString` method, which returns a string with a single element
     * `'99'` is a primitive value that evaluates to 99 as it's converted to a number
 ### HTML:
 * The `<input type="password"/>` input type "password" can be used to obfuscate user input in a form
 * Its attributes include:
 * **value**
 * **maxlength**
 * **minlength**
 * **pattern** - a Regex pattern specifying the input format required for form validation
 * **placeholder** 
 * **readonly**
 * **size** - the character width of the input field
 * **autocomplete** - whether the browser will allow autocomplete in the field
 * **on** - allow browser/password manager to input passwords
 * **off** - don't allow
 * **current-password** - allow password manager to enter existing passwords only
 * **new-password** - allow password manager to enter new passwords only  
 ### CSS:
 * The outline property is a shorthand for the 3 outline properties:
 * outline-color - defaults to either invert or currentColor, depending on browser compatibility
 * outline-width - defaults to medium if unspecified
 * outline-style - defaults to none if unspecified
 * 8 other styles to be used for aesthetic sugar
 * Instead of manually setting each property, the outline property can be used to set all three at once
 ```css
 outline: 5px solid red;
  ```

## April 5, 2024
  * ### JS:
    * The global functions `parseInt()` and `parseFloat()` can be used to converted strings with leading numbers into either integers or floating point numbers
      ```javascript
      parseInt('34 tribes') // returns 34
      parseFloat('3.14 pies') // returns 3.14
      parseInt('3.14 pies') // returns 3
      parseFloat('.14') // return 0.14, because the first character is NaN
      parseInt('.14') // returns NaN, because integers can't start with '.'
      parseFloat('$14') // returns NaN, because numbers can't start with '$'

    ### HTML:
    * `tabIndex` is a global attribute attributable to almost all HTML elements (besides `<dialog>`)
    * It defines whether an element is focusable by sequential tab navigation
      * May still be focusable using clicks or the `focus()` method
    * The nearest positive value to zero is focused first, followed by sequentially higher positive values, then zero
    * Any negative tabindex value will never be focused
      ```html
      <input tabIndex="0">Last</input>
      <input tabIndex="-1">Not tabbable </input>
      <input tabIndex="2">Second</input>
      <input tabIndex="1">First</input>
      <input tabIndex="-3">Not tabbable</input>

    ### CSS:
    * The difference between `em` and `rem` units are that `em` refers to an element's parent's font size, while a `rem` refers to the root element's (the HTML document's) font size

## April 4, 2024
  * ### JS:
    * The unary + operator `(+x)` will convert a value to a number (equivalent of `Number(x)`)
    * JS Symbols
    * Numbers have a toString method that accepts a radix (or base) as an argument and returns a number in Base Radix  
      ```javascript
        let n = 17;    
        let binary = "0b" + n.toString(2); // binary == "0b10001"  
        let octal = "0o" + n.toString(8); // octal == "0o21"  
        let hex = "0x" + n.toString(16); // hex == "0 ```
    ### HTML:
    ```html
        <!DOCTYPE html>
            <html>
                <head>
                    <title>Page Title</title>
                </head>
                <body>
                    <h1>This is a Heading</h1>
                    <p>This is a paragraph.</p>
                    <p>This is another paragraph.</p>
                </body>
            </html>



