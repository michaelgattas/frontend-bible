# Front-End Bible:

## July 3, 2024

### JS: 
* In ES6, you can define a default value for each function parameter directly in the parameter list of your function
```javascript
function getPropertyNames(o, a = []) {
    for (let property in o) a.push(property);
    return a;
}
```
* You can also the value of a previous parameter to define the default value of the parameters that follow it:
```javascript
const rectangle = (width, height = width * 2) => ({width, height});
rectangle(1) // => {width: 1, height: 2}
```

### HTML: 
#### The `<noscript>` element
* This element defines a section of HTML to be inserted if a script type on the page is unsupported or if scripting is currently turned off in the browser
```HTML
<noscript>
    <!--    anchor linking to external file -->
    <a href="https://www.mozilla.org"/>External Link</a>
</noscript>
<p>Rocks!</p>
```

#### The `<object>` element
* This element represents an external resource, which can be treated as an image, nested browsing context, or a resource to be handled by a plugin
```HTML
<object type="application/pdf" data="/media/examples/In-CCO.pdf" width="250" height="200"></object>
```
* Relevant attributes:
  * `data`: the URL of the resource to be embedded
  * `form`: the form element that the object element is associated with (must be an ID of a `<form>` element in the same document)
  * `height`: the height of the object
  * `type`: a content type specified by data

### CSS:
#### Scoping Proximity
* Another advanced topic that you might not use right away but may need to understand in the future is `@scope`
* This is an at-rule that enables you to create a block of rules that only apply to a specific subsection of the HTML on your page
* For example, you can specify styles that will only apply to `<img>` elements when they're nested inside elements that have a `feature` class
```CSS
@scope (.feature) {
    img {
        border: 1px solid black;
        display: block;
    }
}
```
* Scoping proximity is the mechanism that resolves conflicts between scoped elements
* It states that when two scopes have conflicting styles, the style with the smallest number of hops up the DOM tree to the scope root wins

* Skills assessment: check the index.html and styles.css files for the rundown

#### Cascade Layers
* Cascade Layers are explicit specificity containers providing simpler and greater control over CSS declarations that ultimately get applied

## July 2, 2024

### JS:

* Javascript's binding of `this` is particularly finicky
    * Arrow functions automatically inherit the `this` value from the environment in which they are defined
    * Nested functions, however, do not

```javascript
let o = {
    m: function () {
        let self = this; // Save the this value in a variable
        this === o // => true: this is the object o
        f(); // Call f() as a regular function

        function f() {
            this === o // => false: this is the global object (in non-strict mode) or undefined (in strict mode)
            self === o // => true: self is the outer this value
        }
    }
}
```

* In the method `m`, we can assign the `this` value to a variable `self`, and within the nested function `f`, we can
  use `self` instead of this to refer to the containing object
* Inside the nested function `f()`, the `this` keyword is not equal to the object `o`, but rather the global object
  or `undefined` in strict mode
* This is widely considered to be a flaw in the Javascript language, and it is important to be aware of
* Another workaround is to use the `bind()` method to bind the `this` value to a function

```javascript
const f = (function () {
    this === 0 // true, since we bound this function to the outer this  
}).bind(this);
```

* Constructor functions do not normally use the `return` keyword
    * They instead initialize the new object and then return implicitly when they reach the end of their body

* Indirect Invocation:
    * All JS functions have two methods called `call()` and `apply()`
    * These both invoke a function indirectly
    * Both methods allow you to explicitly specify the `this` value for the invocation, which you can invoke any
      function as a method of any object, even if it is not actually a method of that object
    * Both allow you to specify the arguments to be passed to the function
    * `call()` uses its own argument list as arguments to the function
    * `apply()` expects an array of values to be passed as arguments to the function

### HTML:

* The `<meter>` represents a scalar value within a known range or a fractional value
    * `value` attribute: the value of the scalar measurement
    * `min` attribute: the lower bound of the range
    * `max` attribute: the upper bound of the range
    * `low` attribute: the upper bound of the low range
    * `high` attribute: the lower bound of the high range
    * `optimum` attribute: the optimal value of the gauge

### CSS:
* When you declare CSS in cascade layers, the order of precedence is determined by the order in which the layers are declared
* CSS styles declared outside any layer are combined, in the order in which those layers are declared, into an unnamed layer, as if it were the last layer declared
* With competing normal (not important) styles, late layers take precedence over earlier defined layers
* For styles flagged with `!important`, however, the order is reversed, with important styles in earlier layers taking precedence over important styles in later layers
* Inline styles take precedence over all author styles, no matter the layer

* When you have multiple style blocks in different layers providing competing values for a property on a single element, the order in which the layers are declared determines the precedence
* Specificity between layers doesn't matter, but specificity within a single layer does

## July 1, 2024

### JS:

* Arrow functions inherit the value of `this` from the environment in which they are defined, rather than defining their
  own invocation context
* Arrow functions also differ from other functions in that they do not have a `prototype` property, which means they
  cannot be used as constructor functions for new classes

* Functions can be invoked in 5 ways:
    * As functions
    * As methods
    * As constructors
    * Indirectly through their `call()` and `apply()` methods
    * Implicitly, via JS language features that do not appear like normal function invocations

* Conditional invocation is possible, where you write

```javascript
f?.(x)
    // this is equivalent to
    (f !== null && f !== undefined) ? f(x) : undefined
```

* Method function invocation binds `this` keyword to the invocation context of the object on which the method is called

### HTML:

* The `<meta>` element represents metadata that can't be represented by other HTML meta-related elements (
  like `<base>`, `<link>`, `<script>`, `<style>`, or `title`)
* The type of metadata provided by the `<meta>` element can be one of the following:
    * If the `name` attribute is set, the `<meta` element provides document-level metadata, applying to the whole page
    * If the `http-equiv` attribute is set, the `<meta>` element is a pragma directive, providing information equivalent
      to what can be given by a similarly-named HTTP header
    * If the `charset` attribute is set, the `<meta>` element is a charset declaration, giving the character encoding in
      which the document is encoded
    * If the `itemprop` attribute is set, the `<meta>` element provides user-defined metadata

### CSS:

* It's possible for users to set custom stylesheets to override the developer's styles
    * E.g., a visually impaired user might want to set the font size on all web pages they visit to be double the normal
      size to allow for easier reading
* Order of overriding declarations:
    * Conflicting declarations will be applied in the following order, with later ones overriding earlier ones:
        * Declarations in user agent style sheets (e.g., the browser's default styles)
        * Normal declarations in user style sheets (custom styles set by a user)
        * Normal declarations in author style sheets (styles set by the developer)
        * Important declarations in author style sheets
        * Important declarations in user style sheets
        * Important declarations in user agent style sheets

## June 27, 2024

### JS:

#### Functions

* In addition to function declarations, you can use a function expression
* Function expressions appear within the context of a larger expression or statement, and the name is optional

```javascript
// This function expression defines a function that squares its argument
// Not that we assign it to a variable
const square = function (x) {
    return x * x;
};

// Function expressions can include names, which is useful for recursion.
const f = function fact(x) {
    if (x <= 1) return 1; else return x * fact(x - 1);
};
```

### HTML:

#### The `<mark>` element

* The `<mark>` element represents text which is highlighted for reference or notation purposes due to the marked
  passage's relevance in the enclosing context
* Do not use it purely for formatting purposes
* Also, most screen reading technologies do not announce the presence of the `<mark>` element by default, so you can add
  a `::before` or `::after` pseudo-element to make it known
* Sometimes, screen readers will deliberately disabled announcing content that creates extra verbosity, so do not abuse
  this technique

#### The `<menu>` element

* The `<menu>` element is described in the HTML as a semantic alternative to `<ul>`, but treated by browsers (and
  exposed through the accessibility tree) as no different from a `<ul>`
* It represents an unordered list of items (which are represented by `<li>` elements)
* Primarily, `<ul>` is used for display, while `<menu>` is used for interactive items

### CSS:

#### Inline styles

* Inline styles take precedence over all normal styles, no matter the specificity

#### !important

* There is a special piece of CSS that you can use to overrule all of the above calculations, even inline styles

## June 26, 2024

### JS:

#### Array to String Conversions

* The `join()` method converts all elements of an array to strings at concatenates them, returning the resulting string
    * You can specify an optional string that separates the elements in the returned string
    * If no separator string is specified, a comma is used
    * This is effectively the inverse of `String.split()`
    * Arrays' inbuilt `toString()` method is effectively `join()` with no arguments
* In addition to the static methods `Array.of()` and `Array.from()`, there is an inbuilt `Array.isArray()` which returns
  true/false depending on the value of the passed in argument

#### Strings as Arrays

* Strings behave like read-only arrays of UTF-16 Unicode characters
* Instead of accessing individual characters with the `charAt()` method, you can use square brackets

```javascript
let s = "test";
s.charAt(0) // => "t"
s[1] // => "e"
```

* Strings behaving like arrays also means that we can apply generic array methods to them

```javascript
Array.prototype.join.call("Javascript", " ") // => "J a v a s c r i p t"
```

* Because strings are immutable values, so they are treated like read-only arrays
* Array methods like `push()`, `sort()`, `reverse()`, and `splice()` do not work on strings

#### Functions

* Functions defined using the `function` keyword are **hoisted** in a program, meaning they can be invoked before their
  definition in a block of code

### HTML:

#### The `<main>` element

* This is used to represent the dominant content of the `<body>` of a document
* It consists of content that is directly related to or expands upon the central topic of a document, or the central
  functionality of an application
* A document must not have more than one `<main>` element that doesn't have the `hidden` attribute specified

#### The `<map>` element

* This element is used with the `<area>` element to define an image map (a clickable link area)
* It must contain the `name` attribute with no space characters

### CSS:

#### Specificity

* To further understand specificity as it pertains to CSS rule application, consider the following about selector
  specificity:
    * **Identifiers**: Score one in this column for each ID selector contained inside the overall selector.
    * **Classes**: Score one in this column for each class selector, attribute selector, or pseudo-class contained
      inside the overall selector.
    * **Elements**: Score one in this column for each element selector or pseudo-element contained inside the overall
      selector.

## June 25, 2024

### JS:

#### `indexOf()` and `lastIndexOf()` Methods

* Each of these search an array for an element with a specified value and return the index of the first such element
  found, or -1 if none is found
* `indexOf()` searches the array from the beginning, and `lastIndexOf()` searches from the end
* Each uses the `===` operator, so objects are compared by equivalent reference, not value
* If you want to actually look at object contents, use `find()` with a custom predicate function
* Each of these methods take an optional second argument, which is the index at which to begin the search

#### `includes()`

* This method takes a single argument and returns `true` if the array contains that value or `false` otherwise
* This method uses a slightly different version of equality that does consider `NaN` to be equal to itself
* This means that `includes()` is a good way to check for the presence of `NaN` in an array, but `indexOf()` is not

#### `sort()`

* This method sorts the elements of an array in place and returns the sorted array
* When called with no arguments, it sorts the array elements in alphabetical order (temporarily converting them to
  strings to perform the comparison, if necessary)
* Undefined elements are sorted to the end of the array
* If you want to sort an array of numbers, you must pass a comparison function as an argument
    * If the first argument should appear after the second in the sorted array, the function should return a positive
      number
    * If the first argument should appear before the second, the function should return a negative number
    * If the two arguments are equal, the function should return 0
* An interesting example would be to sort an array of strings, with case ignored in the alphabetical comparison

```javascript
let a = ["Banana", "apple", "Cherry", "decks"]
a.sort() // => ["Banana", "Cherry", "apple", "decks"]
a.sort((a, b) => {
    let s = a.toLowerCase(), t = b.toLowerCase();
    if (a > b) return 1
    if (a < b) return -1
    return 0
}) // => ["apple", "Banana", "Cherry", "decks"]
```

#### `reverse()`

* This method reverse the order of the elements of an array and returns the reversed array
* It does this in place, or without creating a new array

### HTML:

#### The `<link>` element

* This specifies relationships between the current document and an external resourrce
    * It's most commonly used to link to stylesheets, but also used to establish site icons
* It's placed inside the `<head>` element, like this

```HTML

<link href="main.css" rel="stylesheet"/>
<link href="favicon.ico" rel="icon"/>
```

* Often times you can use the `rel` attribute to indicate special icon types for use on various mobile platforms
* `sizes` attribute can be used to specify the size of the icon
* `type` attribute can be used to specify the MIME type of the linked resource
* You can also provide a media type or query inside a `media` attribute
    * This resource will then only be loaded if the media condition is true

### CSS:

* In ascending, the factors that apply the final styling to an element are:
    * Source Order
    * Specificity
    * Important
* Source Order:
    * If you have more than one rule, all of which have exactly the same weight, then the one that comes last in the CSS
      will win
    * Source order only matters when the specificity weight of the rule is the same

## June 21, 2024

### JS:

* The `fill()` method sets the elements of an array, or a slice of an array, to a specified value
* It mutates the array it's called on, and also returns the modified array

```javascript
let a = new Array(5); // start the array with no elements and length 5
a.fill(0); // => [0, 0, 0, 0, 0]
a.fill(9, 1); // => [0, 9, 9, 9, 9]; fill with 9 starting at index 1
a.fill(8, 2, -1) // => [0, 9, 8, 8, 9]; fill with 8 starting at index 2 and ending at the second-to-last index
```

* First argument is the value to fill
* Second argument is the start index
    * If omitted, the entire array will be filled
* Third argument is the end index
    * If omitted, the array will be filled to the end index

* The `copyWithin()` method copies a slice of an array to a new position within the array
* It modifies the array in place and returns the modified array, but will not change the length of the array
* First argument specifies the destination index to which the first element will be copied
* The second argument is the index of the first element to be copied
    * If this is omitted, 0 is used
* The third argument specifies the end of the slice of elements to be copied
    * If omitted, the length of the array is used
* Elements from the start index up to, but not including, the end index will be copied

```javascript
let a = [1, 2, 3, 4, 5];
a.copyWithin(1) // => [1, 1, 2, 3, 4]: copy the entire array to index 1
a.copyWithin(2, 3, 5) // => [1, 1, 3, 4, 4]: copy last 2 elements to index 2
a.copyWithin(0, -2) // => [4, 4, 3, 4, 4]: negative offsets work, too
```

### HTML:

#### The `<legend>` element

* This represents a caption for the content of its parent `<fieldset>`

```HTML

<fieldset>
    <legend>Choose your favorite monster</legend>
    <input type="radio" id="kraken" name="monster" value="K"/>
    <label for="kraken">Kraken</label><br/>

    <input type="radio" id="sasquatch" name="monster" value="S"/>
    <label for="sasquatch">Sasquatch</label><br/>

    <input type="radio" id="mothman" name="monster" value="M"/>
    <label for="mothman">Mothman</label>
</fieldset>
```

* Check this example out in `index.html`

#### The `<li>` element

* Used to represent an item in a list
* Must be contained in a parent element: an unordered list or ordered list, or a menu
* Notable Attributes:
    * `value`: this integer attribute indicates the current ordinal value of the list item as defined by the `<ol>`
      element
        * The only allowed value for this attribute is a number, even if the list is displayed with Roman numerals or
          letters

### CSS:

#### Universal values and Inheritance

* The CSS shorthand property `all` can be used to apply one of these inheritance values to (almost) all properties at
  once
* Its value can be any one of the inheritance values (`inherit`, `initial`, `revert`, `revert-layer`, or `unset`)
    * It's a convenient way to undo changes made to styles so that you can get back to a known starting point before
      beginning new changes
    * Example to follow on Monday

## June 20, 2024

### JS:

#### Subarrays

* `slice()`: the `slice()` method returns a slice, or subarray of the specified array.
    * Its two arguments specify the start and end of the slice to be returned
    * In includes the first argument index up to, **but not including** the second argument index
    * If only one argument is specified, the returned array contains all elements from the argument index to the end of
      the array
    * If either argument is negative, it specifies an array element relative to the length of the array
    * An argument of -1, for example, specifies the last element of the array, and the element -2 specifies the element
      before that one
    * `slice()` does not modify the array on which it is invoked
  ```javascript
  let a = [1, 2, 3, 4, 5];
  a.slice(0, 3); // returns [1, 2, 3]
  a.slice(3); // returns [4, 5]
  a.slice(1, -1); // returns [2, 3, 4]
    a.slice(-3, -2); // returns [3]
  ```
* `splice()` is a general-purpose method for inserting or removing elements from an array
    * Unlike `slice()` and `concat()`, `splice()` modifies the array on which it is invoked
    * The first argument to `splice()` specifies the array position at which the insertion and/or deletion is to begin
    * The second argument specifies the number of elements that should be deleted from (spliced out of) the array
        * This is another key difference
            * The second argument to `slice()` is an end index
            * The second argument to `splice()` is a length
  ```javascript
  let a = [1, 2, 3, 4, 5, 6, 7, 8];
  a.splice(4) // => [5, 6, 7, 8]; a is now [1, 2, 3, 4]
  a.splice(1, 2) // => [2, 3]; a is now [1, 4]
  a.splice(1, 1) // [4]; a is now [1]
  ```
    * The first two arguments to `splice()` specify the position and number of elements to delete
    * The arguments can be followed by any number of arguments that specify elements to be inserted at the point of the
      first argument in the array
  ```javascript
  let a = [1, 2, 3, 4, 5];
  a.splice(2, 0, "a", "b") // []; a is now [1, 2, "a", "b", 3, 4, 5]
  a.splice(2, 2, [1, 2], 3) // ["a", "b"] a is now [1, 2, [1, 2], 3, 3, 4, 5]
  ```

### HTML:

#### The `<label>` element represents a caption for an item in a user interface

* Associating a `<label>` with a form control, such as `<input>` or `<textarea>` offers some major advantages
    * The label is not just visually, but programmatically associated with its control, allowing screen readers to
      dictate the content more accurately
    * Tapping/touching the label propagates the focus to the associated input, allowing for a larger hit area on a
      control or textarea
* To associate a label with a text input, you first add an `id` to the associated input
* Next, you add the `for` attribute to the label with the matching `id`
* Don't add interactive anchor tags or buttons inside a label, instead use the `for` attribute to associate the label
  with the input
* Don't add headers or similar elements for the sake of styling, instead use CSS to achieve such effects

### CSS:

#### Inheritance

* Properties like `width`, `margin`, `padding`, and `border` are not inherited properties
* You can often guess whether a property will be inherited if you know what aspect the property value will style
* CSS provides five universal property values for controlling inheritance. Every CSS property accepts these values
    * `inherit`: sets the property value applied for a selected element to the same as that of its parent element.
      This "turns on" inheritance
    * `initial`: sets the property value to its default value
    * `revert`: resets the property value to the browser's default styling rather than the defaults applied to that
      property. This value acts like `unset` in many cases
    * `revert-layer`: resets the property value applied to a selected element to the value established in a previous
      cascade layer
    * `unset`: resets the property value to its inherited value if it inherits, or to its default value if it does not

## June 14, 2024

### JS:

#### Array Iterator Methods

* These work by iterating over arrays and calling a function you provide for each element
* If an array is sparse, the function you pass is not invoked for nonexistent elements
* The `forEach()` Method
    * The argument is the function to be invoked for each element
    * The function can have three parameters
        * The value of the element
        * The index of the element
        * The array object being traversed
    * If you want to ignore parameters, you can simply use the first parameter
      ```javascript
      let data = [1, 2, 3, 4, 5], sum = 0;
      
      data.forEach(value => { sum += value}) // sum == 15
      
      data.forEach((v, i, a) => { a[i] = v + 1;}) // data == [2, 3, 4, 5, 6]
      ```
    * Note that `forEach()` does not provide a way to terminate iteration before all elements have been passed to the
      function, like a `break` statement in a `for` loop

* The `map()` Method
    * This passes each element of the array on which is invoked to the function you specify and returns an array
      containing the values returned by your function
    * The function you pass should return a value
    * The function returns a new array: it does not modify the array it is invoked on
    * If the array is sparse, the function won't be called on missing elements, but the returned array will be sparse in
      the same way as the original array (with the same length and missing elements)

* The `filter()` Method
    * This method returns an array containing a subset of the elements of the original array
    * The function you pass should be a "predicate", returning `true` or `false`
    * The return value is always a `dense` array, and missing elements from sparse arrays will be skipped
    * To close a sparse array, you could do this
      ```javascript
      let dense = sparse.filter(() => true);
      a = a.filter(x => x !== undefined && x !== null) // this is a way to remove undefined and null, and close gaps
      ```
* `find()` and `findIndex()`
    * These work like `filter()` in that they iterate through your array looking for elements for which your predicate
      function returns a truthy value
    * Unlike `filter`, they stop iterating the first time the predicate finds an element
    * `find()` returns the first found element, and `findIndex()` returns the index of the matching element
        * If no matching element is found `find()` returns undefined and `findIndex()` returns -1

* `every()` and `some()`
    * These are array predicates: they apply a predicate function you specify to the elements of the array, then
      return `true` and `false`
    * The `every()` method is like a mathematical "for all" quantifier, returning true only if your predicate returns
      true to all elements in the array
    * The `some()` method is like a mathematical "there exists" quantifier, returning true if there exists at least one
      element in the array for which the predicate returns true, and false otherwise
    * Note that both `every()` and `some()` stop iterating elements as soon as they know what to return
        * Some returns `true` as soon as one element returns `true`, and `every()` returns `false` as soon as one
          element returns `false`
    * Note also that `every()` returns true and `some()` returns false for empty arrays, by mathematical convention

* `reduce()` and `reduceRight()`
    * These combine the elements of an array, using the function you specify, to produce a single value
    * This is a common operation in functional programming and also goes by the names "inject" and "fold"
    * The `reduce()` function takes two arguments
        * The first is the function that performs the reduction operation
            * The task of this function is to somehow combine or reduce two values into a single value and to return
              that reduced value
        * The second (optional) argument is an initial value to pass to the function
        * Functions used with `reduce()` are different than the functions used with `forEach()` and `map()`
            * The familiar value, index, and array values are passed as the second, third, and fourth arguments
            * The first argument is the accumulated result of the reduction so far
                * On the first call to the function, the first argument is the initial value you passed as the second
                  argument to `reduce()`
                * On subsequent calls, it is the value returned by the previous call to the function
        * Calling `reduce()` on an empty array with no initial value argument causes a `TypeError`
        * If you call it on an array with only one value (either one element in an array and no initial value, or an
          element array and an intial value), it simply returns that one value without ever calling the reduction
          function
    * The `reduceRight()` method works just like `reduce()`, except that it processes the array from highest index to
      lowest (right-to-left)

* `flat()` and `flatMap()`
    * `flat()` creates and returns a new array that contains the same elements as the array it is called on, except that
      any elements that are themselves arrays are "flattened" into the return array
      ```javascript
      [1, [2, 3]].flat() // => [1, 2, 3]
      [1, [2, [3]]].flat() // => [1, 2, [3]]
      ```
        * When calls with no arguments, `flat()` flattens one level of nesting
        * If you want to flatten more levels, pass a number to `flat()`
    * `flatMap()` works just like `map()` but the returned array is automatically flattened as if passed to `flat()`
        * In other words, `a.flatMap(f)` is a shorthand for `a.map(f).flat()`

* The `concat()` method creates and returns a new array that contains the elements of the original array on
  which `concat()` was invoked, followed by each of the arguments passed into `concat()`
    * If any of these arguments is itself an array, then the elements of that array are concatenated rather than the
      array itself
    * Note that it will only flatten the outermost arguments passed in, and not any nested arrays
    * Note that `concat()` creates a new copy of the array it is called on
        * Because this can be an expensive operation, consider using `push()` or `splice()` instead of creating a new
          one

#### Stacks and Queues with `push()`, `pop()`, `shift()`, and `unshift()`

* The `push()` and `pop()` methods allow you to work with arrays as if they were stacks
    * `push()` adds one or more elements to the end of an array, and returns the new length of the array
        * Unlike `concat()`, `push()` does not flatten array arguments
    * `pop()` removes the last element of an array, decrements the length of the array, and returns the removed value
    * Both methods modify the array in place
    * The `push()` method does not flatten an array you pass to it, but if you want to push all of the elements from one
      array onto another array, you can use the spread operator to flatten it explicitly
  ```javascript
    a.push(...values);
  ```

* The `unshift()` and `shift()` methods behave much like `push()` and `pop()`, except that they insert and remove
  elements from the beginning of an array rather than from the end
    * `unshift()` adds an element or elements to the beginning of the array, shifts the existing array elements up t
      higher indexes to make room, and returns the new length of the array
    * `shift()` removes and returns the first element of the array, shifting all subsequent elements down one place to
      occupy the newly vacant space at the start of the array
    * You could use `unshift()` and `shift()` to implement a stack, but it would be less efficient that using `push()`
      and `pop()` due to the moving of elements
    * Instead, you can implement a queue data structure by using `push()` to add elements at the end of an array
      and `shift()` to remove them from the start of the array
    * Keep in mind that if you use `unshift()` with multiple elements, all of them will be inserted at once, which will
      cause a different ordering of the elements than unshifting them one at a time
  ```javascript
  let a = [] // a == []
  a.unshift(1) // a == [1]
  a.unshift(2) // a == [2, 1]
  a = []
  a.unshift(1, 2) // a == [1, 2]
  ```

### HTML:

* The `<ins>` element represents a range of text that has been added to a document
    * You can use the `<del>` element to similarly represent a range of text that has been deleted from the document
    * The presence of the `<ins>` element is not announced by most screen reading technology in its default
      configuration
    * It can be made to be announced by using the CSS `content` property, along with the `::before` and `::after`
      pseudo-elements
      ```CSS
      ins::before,
      ins::after {
        clip-path: inset(100%);
        clip: rect(1px, 1px, 1px, 1px);
        height: 1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
        }
      ins::before {
        content: " [insertion start] ";
      }
      ins::after {
        content: " [insertion end] ";
      }
      ``` 
* The `<kbd>` or Keyboard Input Element
    * This represents a span of inline text denoting textual user input from a keyboard, voice input, or any other text
      entry device
    * Nesting a `<kbd>` element within another `<kbd>` element represents an actual key or other unit of input as a
      portion of larger input
    * Nesting a `<kbd>` element inside a `<samp>` element represents input that has been echoed back to the user by the
      system
    * Nesting a `<samp>` element inside a `<kbd>` element represents input which is based on text presented by the
      system, such as the names of menus and menu items, or the names of buttons displayed on the screen

### CSS

#### Cascade, specificity, and inheritance

* This topic controls how CSS is applied to HTML and how conflicts between style declarations are resolved
* Stylesheets **cascade**, which means the origin, the cascade layer, and the order of CSS rules matter
    * When two rules from the same cascade layer apply and both have equal specificity, the one that is defined last in
      the stylesheet is the one that will be used
      ```CSS
      h1 {
        color: red;
      }
      h1 {
        color: blue;
      }
      ```
    * In this case the rules are from the same source, have an identical element selector, and therefore carry the same
      specificity, but the last one in the source order wins
* **Specificity** is the algorithm that the browser uses to decide which property value is applied to an element
    * If multiple style blocks have different selectors that configure the same property with different values and
      target the same element, specificity decides the property value that gets applied to the element
    * An element selector is less specific. It will select all elements of that type that appear on a page, so it has
      less weight
        * Pseudo-element selectors have the same specificity as regular element selectors
    * A class selector is more specific, so it has more weight
        * Attribute selectors and pseudo-classes have the same weight as a class
  ```CSS
  .main-heading {
    color: red;
  }
  h1 {
    color: blue;
  }
  ```
    * In this case, the class selector is more specific than the element selector, so the color of the `.main-heading`
      class will be red
* **Inheritance** - some property values set on parent elements are inherited by their child elements, and some aren't
    * E.g., if you set a `color` and `font-family` on an element, every element inside it will also be styled with that
      color and font, unless you've applied different values directly to them
    * Some properties do not inherit, so if you set a `width` of 50% on an element, all of its descendants do not get a
      width of 50% of their parent's width
        * If this was the case, CSS would be super frustrating and require much more styling

## June 13, 2024

### JS:

#### Arrays

* Arrays are a specialized kind of object
* The square brackets used to access array elements work just like the square brackets used to access object properties
* JS converts the numeric array index you specify to a string–the index 1 becomes the string "1", then uses that string
  as a property name

```javascript
let o = {};
o[1] = "one";
o["1"] // => "one"; numeric and string property names are the same
```

* All indexes are property names, but only property names that are integers between 0 and 2^32 - 2 are indexes
* All arrays are objects, and you can create properties of any name on them
* If you use properties that are array indexes, however, arrays have the special behavior of updating their length
  property as needed
* Note that you can index an array using numbers that are negative or that are not integers
    * In this case, they are simply stores as properties of the array object, and do not affect the `length` property
* If you index an array with a string that happens to be a non-negative integer, it behaves as an array index, not an
  object property

```javascript
a[-1.23] = true; // this creates a property names "-1.23"
a["1000"] = 0; // this sets the 1000th element of the array
a[1.000] // Array index 1. same as a[1] = 1
```

#### Sparse Arrays

* Sparse arrays have a length value greater than the number of elements

#### Array Length

* If you assign a value to an array whose index i is greater than or equal to the array's current `length`, the value of
  the `length` property is set to `i + 1`
* In order to maintain the length invariant is that, if you set the length property to a non-negative integer `n`
  smaller than its current value, any array elements whose index is greater than or equal to `n` are deleted from the
  array:

```javascript
a = [1, 2, 3, 4, 5];
a.length = 3;
a.length = 0; // deletes all elements
a.length = 5; // length is 5, but no elements, like new Array(5)
```

* Pushing a value onto an array is the same as assigning the value to `a[a.length]`
* You can use the `unshift()` method to insert a value at the beginning of an array
* The `pop()` method is the opposite of `push()`, removing the last element of the array and returning it
* Similarly the `shift()` method removes and returns the first element of the array, reducing the length by 1 and
  shifting all elements down to an index one lower than their current index
* You can delete array elements with the `delete` operator, just as you can delete object properties

```javascript
let a = [1, 2, 3]
delete a[2] // a now has no element at index 2
2 in a // => false: no array index 2 is defined
a.length // => 3: delete does not affect array length
```

* If you delete an element from an array, it becomes sparse
* `splice()` is the general purpose method for inserting, deleting, or replacing array elements
    * It alters the length property and shifts array elements to higher or lower indexes as needed

#### Iterating Arrays

* The`for/of` loop returns the elements of an array in ascending order
    * It has no special behavior for sparse arrays and simply returns `undefined` for any array elements that do not
      exist
    * If you want to use a `for/of` loop for an array and need to know the index os each array element, use
      the `entries()` method of the array, along with destructuring assignment, like this:

```javascript
let everyother = "";
for (let [index, letter] of letters.entries()) {
    if (index % 2 === 0) everyother += letter;
}
```

* Another good way to iterate arrays is with `forEach()`
    * This is not a new form of the `for` loop, but an array method that offers a functional approach to array iteration
    * It iterates the array in order, and actually passes the array index to your function as a second argument
    * Unlike the `for/of` loop, the `forEach()` function is aware of sparse arrays and does not invoke your function for
      elements that are not there
* Sometimes, good ole-fashioned iteration is useful, using a standard `for` loop

#### Multidimensional Arrays

* JS does not have true multidimensional arrays, but you can simulate them with arrays of arrays

### HTML:

#### The `<input>` element

* The `<input>` element is used to create interactive controls for web-based forms in order to accept data from the user
    * More Types include:
        * `number`: a control for entering a number. Displays a spinner and adds default validation, displays a numeric
          keypad in some devices with dynamic keypads
        * `password`: a single-line text field whose value is obscured. Will alert user if site is not secure
        * `radio`: a radio button, allowing a single value to be selected out of multiple choices with the same `name`
          value
        * `range`: a control for entering a number whose exact value is not important. Displays as a range widget
          default to the middle value. Used in conjunction with `min` and `max` to define the range of acceptable values
        * `reset`: a button that resets the contents of the form to default values
        * `search`: a single line text field for entering search strings. Line-breaks are automatically removed from the
          input value. May include a delete icon in supporting browsers that can be used to clear the field. Displays a
          search icon instead of enter key on some devices with dynamic keypads
        * `submit`: a button that submits the form
        * `tel`: a control for entering a telephone number. Displays a telephone keypad in some devices with dynamic
          keypads
        * `text`: a single-line text field. Line-breaks are automatically removed from the input value
        * `time`: a control for entering a time value with no time zone. Displays a time picker or numeric wheels for
          hours and minutes when active in supporting browsers
        * `url`: a field for editing a URL. It looks like a `text` input, but has validation parameters and a keyboard
          optimized for URL entry
        * `week`: a control for entering a date consisting of a week-year number and a week number within that year.
          Displays a week picker or numeric wheels for week and year when active in supporting browsers

### CSS:

* For CSS today, I am completing the Selectors Assessment tasks

## June 12, 2024

### JS:

#### Arrays

* `Array.of()` enables you to input arguments and allow them to be the elements of the newly created array (even if
  there is just one
    * Using the `Array` constructor with a single numeric argument will create an array with that length, not with that
      element
* `Array.from()` is another ES6 factory function
    * It takes an Array-like or iterable object and returns an array that contains the same elements
    * It is also a simple way to create a shallow copy of an array
    * This function is important because it allows for the copying of Array-like objects
    * This function also allows for a second argument, which is a function to be applied to each element being passed
      into the array
        * In other words, you can perform mapping as you're building your new array
* _Array-like Objects_ are objects who have a numeric length property defined, along with properties whose names happen
  to integers
    * These are somewhat common as return-types for built-in browser methods

### HTML:

#### The `<input>` element

* The `<input>` element is used to create interactive controls for web-based forms in order to accept data from the user
* Within it, a multitude of data and control widgets are available, depending on the client's device and user agent
    * Types include:
        * `button`: A push button with no default behavior, displaying the value of the `value` attribute, and nothing
          by default
        * `checkbox`: A check box allowing single values to be selected/deselected
        * `color`: A control for specifying a color, which opens a color picker in supporting browsers
        * `date`: a control for entering a date (year, month, and day, with no time). opens a date picker or numeric
          wheels for years, months and day when active in supporting browsers
        * `datetime-local`: A control for entering a date and time, with no time zone. Opens a date picker or numeric
          wheels for date- and time-components when active in supporting browsers
        * `email`: A field for editing an e-mail address. It looks like a `text` input, but has validation parameters
          and a keyboard optimized for email addresses
        * `file`: A control that lets the user select a file. Use the `accept` attribute to define the types of files
          that the control can select
        * `hidden`: A control that is not displayed but whose value is submitted to the server. Useful for form
          honey-pots!
        * `image`: A graphical submit button. You must use the `src` attribute to define the source of the image and
          the `alt` attribute to define alternative text
        * `month`: A control for entering a month and year, with no time zone. Opens a date picker or numeric wheels for
          month and year when active in supporting browsers

### CSS:

* Before completing the combinator/selector assessment tomorrow, here's a bite-sized tidbit:
    * The `::selection` pseudo-element applies styles to the portion of a document that has been highlighted by the user

## June 11, 2024

### JS:

#### Accessor Properties: Getters and Setters

```javascript
let p = {
// x and y are regular read-write data properties. x: 1.0,
    y: 1.0,
    // r is a read-write accessor property with getter and setter.
    // Don't forget to put a comma after accessor methods.
    get r() {
        return Math.hypot(this.x, this.y);
    }, set r(newvalue) {
        let oldvalue = Math.hypot(this.x, this.y);
        let ratio = newvalue / oldvalue;
        this.x *= ratio;
        this.y *= ratio;
    },
    // theta is a read-only accessor property with getter only.
    get theta() {
        return Math.atan2(this.y, this.x);
    }
};
p.r // => Math.SQRT2 p.theta // => Math.PI / 4
```

* This object has data properties to represent the x and y coordinates of the point, and it has accessor properties that
  give the equivalent polar coordinates of the point
* The code uses accessor properties to define an API that provides two representations (Cartesian coordinates and polar
  coordinates) of a single set of data
* Other reasons to use accessor properties include sanity checking of property writes and returning different values on
  each property read:

```javascript
// This object generates strictly increasing serial numbers
const serialnum = {
    // This data property holds the next serial number. // The _ in the property name hints that it is for internal use only.
    _n: 0,
    // Return the current value and increment it
    get next() {
        return this._n++;
    },
    // Set a new value of n, but only if it is larger than current
    set next(n) {
        if (n > this._n) this._n = n;
        else throw new Error("serial number can only be set to a larger value");
    }
};

serialnum.next = 10;
serialnum.next
serialnum.next

// Set the starting serial number
// => 10
// => 11: different value each time we get next
```

#### Arrays

* Arrays use 32-bit indexs, so the first element is index 0, and the maximum available index is 2^32 - 2, for a maximum
  array size of 4,294,967,295 elements
* JS arrays are dynamic, they grow or shrink as needed, and there is no need to declare a fixed size for the array when
  you create it or reallocate it when the size changes
* JS arrays may be sparse (the elements need not have contiguous indexes, and there may be gaps
* Every array has a `length` property
* For sparse arrays, `length` is larger than the highest index of any element (it will be the length of the array if all
  elements were contiguous)
* JS arrays are specialized forms of JS objects, and array indexes are object property names
    * Implementations of arrays are typically optimized so that accessing numerically indexed array elements is
      generally significantly faster than access to regular object properties
* Arrays inherit properties from `Array.prototype`, which defines a rich set of array manipulation methods
* JS strings behave like arrays of characters
* ES6 introduces a set of new array classes known as `typed arrays`
    * Unlike regular JS arrays, typed arrays have a fixed length and a fixed numeric element type
    * They offer high performance and byte-level access to binary data
* There are several ways to create arrays:
    * Array literals
        * Very simple, just a comma-separated list of elements within square brackets
    * The `...` spread operator on an iterable object
      ```javascript
      let a = [1, 2, 3];
      let b = [0, ...a, 4];
      ```
        * The dots "spread" the elements of the array `a` so that a is replaced by its elements
        * The operator is a convenient way to create a shallow copy of an array
      ```javascript
      let original = [1,2,3]; 
      let copy = [...original];
      copy[0] = 0; // Modifying the copy does not change the original
      original[0] // => 1
      ```
    * The `Array()` constructor
        * This is almost always superceded by the ease/functionality of the Array Literal Syntax
        * But, you can create an array like
          this: `let a = new Array(10); // this would create an array with 10 undefined elements`
            * Note that no values are stored in the array, and the array index properties "0" and "1" and so on are not
              even defined for the array
        * Explicitly specify two or more array elements or a single non-numeric element for the array:
            * `let a = new Array(5, 4, 3, 2, 1, 'testing', 'testing'); // => [5, 4, 3, 2, 1, 'testing', 'testing']`
    * The `Array.of()` and `Array.from()` factory methods
        * Since the `Array()` constructor will interpret a single numeric element as a length, and multiple elements are
          array elements, this means you cannot simply create an Array with one numeric element using the constructor

### HTML:

* The `<img>` element embeds an image into the document
    * The `src` attribute is required, and contains the path to the image you want to embed
    * The `alt` attribute is also required, and **incredibly useful for accessibility**
    * Supported image formats:
        * APNG, BMP, GIF, JPEG, PNG, SVG, WebP

### CSS:

#### Combinators

* The descendant combinator, typically represented by a single space character, combines two selectors such that
  elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, etc.) element
  matching the first selector

```CSS
body article p {
    color: red;
}
```

* The child combinator, represented by the `>` character, matches only elements that are direct children of a parent
  element

```CSS
article > p {
    color: red;
}
```

* The next sibling combinator, represented by the `+` character, selects only the element that is immediately preceded
  by the former element
* For example, to select all `<img>` elements that are immediately preceded by a `<p>` element

```CSS
p + img {
    margin-top: 20px;
}
```

* The subsequent-sibling combinator, which selects all elements that follow (at any distance) the former sibling element

```CSS
p ~ img {
    margin-top: 20px;
}
```

## June 10, 2024

### JS:

#### Shorthand Methods

* When a function is defined as a property of an object, we call it a method
* In ES6, the object literal syntax (and also class definition syntax we'll see in Chapter 9) has been extended to allow
  a shortcut where the function keyword and the colon are omitted

```javascript
let square = {
    area() {
        return this.side * this.side;
    },
    side: 10
};
square.area() // => 100
```

#### Property Getters and Setters

* All of the object properties discussed up til now are __data properties__
* JS also supports __accessor properties__ (getters and setters), which do not have a single value but instead have one
  or two accessor methods: a _getter_ and/or a _setter_
* If a property has both a getter and a setter method, it is a read/write property
* If it has only a setter method, it is a write-only property (something that is not possible with data properties)
    * Attempts to read it always evaluate to undefined

### HTML:

#### The `<iframe>` element

* This represents a nested browsing context, embedding another HTML page into the current one
* Each embedded browsing context has its own document and allows URL navigations
* The navigations of each embedded browsing context are linearized into the session history of the topmost browsing
  context
* The topmost browsing context, the one with no parent, is usually the browser window, represented by the `Window`
  object
* Relevant attributes:
    * `allow`: specifies a permissions policy for the `<iframe>`
    * `allowfullscreen`
    * `browsingtopics`: specifies that the selected topics for the current user should be sent with the request for
      the `<iframe>`'s sources. See more under the `Topics API`
    * `credentialless`: set to `true` means that content will be loaded in a new, ephemeral context. It doesn't have
      access to the network, cookies, and storage data associated with its origin
    * `csp`: a Content security policy enforced for the embedded resource
    * `referrerpolicy`: indicates which referrer to send when fetching the frame's resource
    * `sandbox`: controls the restriction applied to the content embedded in the `<iframe>`

### CSS:

#### Pseudo-Classes:

* A pseudo-class is a selector that selects elements that are in a specific state, e.g., they are the first element of
  their type, or they are being hovered over by the mouse pointer
* E.g. `:hover` is a pseudo-class
* Other pseudo-classes
  are `:hover`, `:focus`, `:first-child`, `:last-child`, `:nth-child()`, `:nth-last-child()`, `:nth-of-type()`, `:nth-last-of-type()`, `:first-of-type`, `:last-of-type`, `:only-child`, `:only-of-type`, `:empty`, `:not()`, `:target`, `:enabled`, `:disabled`, `:checked`, `:default`, `:valid`, `:invalid`, `:in-range`, `:out-of-range`, `:required`, `:optional`, `:read-only`, `:read-write`, `:placeholder-shown`, `:root`, `:scope`, `:user-invalid`, `:blank`, `:nth-match()`, `:nth-last-match()`, `:current`, `:past`, `:future`, `:active`,

#### Pseudo-Elements

* Pseudo-elements behave in a similar way, but as if you added a whole new HTML element into the markup, rather than
  applying a class to existing elements
* Pseudo-elements start with a double colon `::`
* An example is `::first-line`, which will automatically select and style the first line of a text element and style it
  as though it had a special span with a class name assigned to it
* There are a couple of special pseudo-elements, which are used along with the `content` property to insert content into
  your document using CSS
* The use of `::before` and `::after` pseudo-elements along with the `content` property is referred to as "Generated
  Content" in CSS

## June 6, 2024

### JS:

#### Shorthand Properties

* In JS, you can assign variable properties to an object the following way:

```javascript
let x = 1, y = 2;
let o = {
    x: x,
    y: y
};
```

* In ES6, you can use shorthand property names to simplify this process

```javascript
let x = 1, y = 2;
let o = {x, y};
````

#### Computed Property Names

* Sometimes you need to create an object with a specific property, but the name of that property is not a compile-time
  constant that you can type literally in your source code
* Instead, the property name you need is stored in a variable or is the return value of a function that you invoke
* You can't use a basic object literal for this kind of property
* Instead, you have to create an object and then add the desired properties as an extra step:

```javascript
const PROPERTY_NAME = "p1";

function computePropertyName() {
    return "p" + 2
}

let o = {};
o[PROPERTY_NAME] = 1;
o[computePropertyName()] = 2;
```

* In ES6, you can use computed property names to simplify this process

```javascript
const PROPERTY_NAME = "p1";

function computePropertyName() {
    return "p" + 2
}

let p = {
    [PROPERTY_NAME]: 1,
    [computePropertyName()]: 2
};
```

#### Symbols as Property Names

* The Computed Property syntax also enables you to use Symbol values as property names

```javascript
const extension = Symbol("my extension symbol");
let o = {
    [extension]: { /* extension data here */}
};
```

* Symbols are opaque values. You can't do anything with them other than use them as property names
* Every symbol is different from every other symbol, which means that they are good for creating unique property names
* Symbols are primitives, not objects, so `Symbol()` is not a constructor function that you invoke with `new`
* Creating a `Symbol`s with identical strings will still yield different symbols
* The string returned by `Symbol.toString()` is not the same as the string you passed to `Symbol()`
* The point of symbols is not security, but to define a safe extension mechanism for JS objects
    * If you received a 3rd-party object and wanted to add a property to it, you could use a symbol as the property name
      to avoid any chance of a name collision

#### Spread Operator:

* The spread operator will copy properties of an existing object into a new object using the "spread" operator `...`
  inside an object literal

```javascript
let position = {x: 1, y: 3};
let dimensions = {width: 100, height: 75};
let rect = {...position, ...dimensions};
rect.x + rect.y + rect.width + rect.height // => 179
dimensions.height = 50;
rect.height // => 75: the rect object has its own copy of the height property
```

* If the object that is spread and the object it is being spread into both have a property with the same name, then the
  value of that property will be the one that comes last:

```javascript
let o = {x: 1};
let p = {x: 0, ...o};
p.x // => 1: the value from object o overrides the initial value
let q = {...o, x: 2};
q.x // => 2: the value 2 overrides the previous value from o.
```

## June 5, 2024

### JS:

* In addition to the basic `toString()` method, objects all have a `toLocaleString()`
    * The default `toLocaleString()` method defined by Object doesn't do any localization itself
    * It simply calls `toString()` and returns that value
    * The Date and Number classes define customized versions of `toLocaleString()` that attempts to format numbers,
      dates, and times according to local conventions
* The `valueOf()` method is much like the `toString() method, but it is called when JS needs to convert an object to
  some primitive type other than a string (typically, a number)
    * You can define your own `valueOf()` method for your own classes, like defining a custom `valueOf()` method below
  ```javascript
  let point = {
      x: 1,
      y: 1,
      valueOf: function() { return Math.hypot(this.x, this.y); }
  };
  ```
    * Date class does something similar, where it converts all times into their millisecond distance from Jan 1 1970 for
      direct date comparison using the `<` or `>` operators
* The `toJSON()` method:
    * `Object.prototype` does not actually define a `toJSON()` method, but `JSON.stringify()` looks for a `toJSON()`
      method on any object it is asked to serialize
    * If the method exists, it is invoked, and the return value is serialized, instead of the original object

### HTML:

* The `<hgroup>` HTML element represents a heading and related content.
    * It groups a single `<h1>-<h6>` element with one of more `<p>` elements
    * The `<hgroup>` presently has no strong accessibility semantics
    * The content of the element (a heading and optional paragraphs) is what is exposed by browser accessibility APIs)
* The `<hr>` element is the Thematic Break (Horizontal Rule) element
    * It represents a thematic break between paragraph-level elements
    * For example, a change of scene in a story, or a shift of topic within a section
    * Historically, this has been presented as a horizontal rule or line
    * While it may still be displayed as a horizontal rule in visual browsers, this element is now defined in semantic
      terms, rather than presentation terms
    * If you solely wish to draw a horizontal line, you should do so using appropriate CSS
* The `<html>` or HTML Document/Root element represents the top-level element in an HTML document.
    * While HTML does not require authors to specify `<html>` element start and ending tags, doing so allows you to
      specify the `lang` attribute for the webpage
* The `<i>` element (or Idiomatic Text Element) represents a range of text that is set off from the normal text for some
  reason
    * Examples are idiomatic text, technical terms, taxonomical designations, among others
    * In earlier versions of the HTML specification, the `<i>` element was merely a presentation element used to display
      text in italics, much like the `<b>` element was used for bold letters
    * These tags now define semantics rather than appearance.
    * A gentle reminder for the appropriate markup for alternative text:
        * Use `<em>` to indicate stress emphasis.
        * Use `<strong>` to indicate importance, seriousness, or urgency.
        * Use `<mark>` to indicate relevance.
        * Use `<cite>` to mark up the name of a work, such as a book, play, or song.
        * Use `<dfn>` to mark up the defining instance of a term.

### CSS:

* Substring Match Selectors:
    * For more advanced matching of attribute values, you can use these substring match selectors
        * `[attr^=value]` - Selects elements that have the `attr` attribute with a value that begins exactly
          with `value`
        * `[attr$=value]` - Selects elements that have the `attr` attribute with a value that ends exactly with `value`
        * `[attr*=value]` - Selects elements that have the `attr` attribute with a value containing the
          substring `value`
    * It may help to note that `^` and `$` are the symbols for the beginning and end of a string, in RegExp respectively
    * If you want to match attribute values case-insensitively you can use the value `i` before the closing bracket
        * For example, `[attr^="value" i]` would match `value`, `Value`, `VALUE`, etc.

## June 4, 2024

### JS:

* _Object serialization_ is the process of converting an object's state to a string from which it can later be restored
    * `JSON.stringify()` and `JSON.parse()` serialize and restore JavaScript objects
* JSON is a subset of JS syntax, and it can't represent all JS values
    * Objects, arrays, strings, finite numbers, `true`, `false`, and null are supported and can be serialized and
      restored
    * `NaN`, `Infinity`, `-Infinity` are not supported and will be serialized to `null`
    * Date objects are serialized to ISO-formatted date strings (see the `Date.toJSON()` function), but `JSON.parse()`
      leaves these in string form and does not restore the original Date object
    * Function, RegExp, and Error objects and the `undefined` value cannot be serialized or restored
    * `JSON.stringify()` serializes only the enumerable own properties of an object
* All JS objects (except those explicitly created without a prototype) inherit properties from Object.prototype
    * These inherited properties are primarily methods, and because they are universally available they are of
      particular interest to JS programmers
* The `toString()` method takes no arguments; it returns a string that represents the value of the object on which it is
  invoked
    * JS invokes this method of an object whenever it needs to convert the object to a string
    * This occurs, for example, when you use the + operator to concatenate a string with an object or when you pass an
      object to a method that expects a string

### HTML:

* The `<head>` element contains machine-readable information (metadata) about the document, like its title, scripts, and
  style sheets
* The `<header>` element represents introductory content, typically a group of introductory or navigational aids
    * It may also have a logo, a search form, an author name, and other elements
    * The header has identical meaning to the site-wide banner, unless nested within sectioning content
    * In this case the `<header>` element is not a landmark
    * The `banner` ARIA role is intended to be used in the context of a site-wide header, such as a masthead
        * Unless a `<header>` is a descendant of an `<aside>`, `<footer>`, `<article>`, or `<nav>`, it is considered a
          site-wide header

### CSS:

* Attribute Selectors
    * These selectors enable the selection of an element based on the presence of an attribute alone, or on various
      matches against the value of the attribute
        * `[attr]`, example `a[title]` matches elements with an `attr` attribute
        * `[attr=value]`, example `a[href="https://www.example.com"]` matches elements with an `attr` that is
          exactly `value`
        * `[attr~=value]`, example `a[rel~="external"]` matches elements with exactly the `attr`, or contains the
          attribute in its space separated list of values
        * `[attr|=value]`, example `a[lang|="en"]` matches elements with exactly the `attr`, or with the attribute
          followed by a hyphen and more characters

## June 3, 2024

### JS:

* A common operation in JS is to copy properties of one object to another object
    * It is easy to do that with code like this
  ```javascript
  let target = {x: 1}, source = {y: 2, z: 3};
  for (let key of Object.keys(source)) {
      target[key] = source[key];
  }
  target // => {x: 1, y: 2, z: 3}
  ```
* Because this is a common operation, various JS frameworks have defined utility functions, often named `extend()` to
  perform this copying operation
* In ES6, this ability comes as `Object.assign()`
    * For each source object, it copies enumerable own properties of that object (including Symbol-named ones) and
      assigns them to the target object
    * It also copies properties with ordinary property get and set operations, so if a source has a getter or a target
      has a setter, they will be invoked during the copy, but will not be copied themselves
    * If you wanted to copy default properties to an object only if the target did not have that existing property, you
      would NOT want to do this
  ```javascript
  Object.assign(o, defaults); // overwrites everything in o with defaults
  ```
    * Instead, you would want to do this
  ```javascript
  o = Object.assign({}, defaults, o); // applies defaults to an empty object, then assigns existing properties from o last, overriding defaults
  ```
    * You can also express this object-copy-and-override operation using spread operators
  ```javascript
  o = {...defaults, ...o}; // same as above
  ```
* Object serialization is the process of converting an object's state to a string from which is can later be restored
* The functions `JSON.stringify()` and `JSON.parse()` serialize and restore JavaScript objects

### HTML:

* The `<form>` element is used to submit information to some aspect of an application (normally a remote server)
    * Pertinent attributes:
        * `accept-charset`: specifies the character encodings that are to be used for the form submission
        * `autocapitalize`: specifies whether the form should have autocapitalization
        * `autocomplete`: specifies whether the form should have autocomplete
        * `name`: the name of the form, must not be an empty string, and must be unique among all `<form>` elements
        * `rel`: controls the annotations and what kind of links the form creates
            * Annotations include `external`, `nofollow`, `opener`, `noopener`, and `noreferrer`
            * Link types include `help`, `prev`, `next`, `search`, and `license`
    * Attributes for form submission:
        * `action`: the URL that processes the form submission. This can be overriden by a `formaction` attribute on
          a `button`, `<input type="submit"` or `<input type="image">` element. This attribute is ignored
          when `method="dialog` is set
        * `enctype`: the encoding type that the form should use when submitting data. This can be overriden by
          a `formenctype` attribute on a `button`, `<input type="submit"` or `<input type="image">` element. This
          attribute is ignored when `method="dialog` is set
            * If the value of the `method` is `post`, the `enctype` attribute is the MIME type of the form submission.
              Possible values:
                * `application/x-www-form-urlencoded`: the default value if the attribute is not specified
                * `multipart/form-data`: the value used for an `<input type="file">` element
                * `text/plain`: a single line of text
        * `method`: the HTTP method to submit the form with
            * `post`: form data is sent as the request body
            * `get`: form data is appended to the `action` URL with a `?` separator. Use this method when the form has
              no side effects
            * `dialog`: when the form is inside a `<dialog>`, closes the dialog and causes a submit event to be fired on
              submission, without submitting data or clearing the form
        * `novalidate`: Boolean attribute that indicates that the form should not be validated when submitted
            * It can be overriden by a `formnovalidate` attribute on a `button`, `<input type="submit"`
              or `<input type="image">` element
        * `target`: indicates where to display the response after submitting the form. It is a name keyword for a
          browsing context (e.g., tab, window, or iframe)
            * `_self`: the response will be displayed in the same frame
            * `_blank`: the response will be displayed in a new window or tab
            * `_parent`: the response will be displayed in the parent frame
            * `_top`: the response will be displayed in the full body of the window
            * `_unfencedTop`: load the form response inside an embedded fenced frame into the top-level frame
* The `<h1>`-`<h6>` elements represent six levels of section headings
    * `<h1>` is the highest section level and `<h6>` is the lowest
        * Each are block-level elements, starting on a new line and taking up the full width available in their
          containing block
        * Heading information can be used by user agents to construct a table of contents for a document automatically
        * Do not use heading elements to resize test. That's what CSS font-size is for
        * Do not skip heading levels
        * Avoid using multiple `<h1>` elements on a single page
    * A common technique for users of screen reading software is to generate a list of sectioning content and use it to
      determine the page's layout
    * Sectioning content can be labeled using a combination of the `aria-labelledby` and `id` attributes, with a label
      concisely describing the purpose of the section. This is userful if there is more than one sectioning element on
      the same page

### CSS:

* A `Type Selector` (aka `Tag Name` or `Element` selector selects a given element type
    * For example, `p` selects all `<p>` elements
* The `Universal Selector` selects everything in your document, or in a parent element if it is being chained , using as
  asterisk
    * You can use the universal selector to make your CSS easier to read. For example
  ```CSS 
  article :first-child {
      margin-top: 0;
  }
  ```
    * This could be confused with `article:first-child`, so it could also be written as:
  ```CSS
  article *:first-child {
      margin-top: 0;
  }
  ```
* The `Class Selector` selects elements with a specific class attribute
    * For example, `.example` selects all elements with `class="example"
* The `ID Selector` selects elements with an id, denoted by `#`
    * For example, `#example` selects the element with `id="example"`

## May 31, 2024

### JS:

* You can check whether an object has a property with a given name using
    * `in` operator - returns true if it has an own or inherited property with that name
    * `hasOwnProperty()` method - returns true if an object has an own property with that name
    * `propertyIsEnumerable()` method - returns true if a property is an own property and is enumerable
  ```javascript
  let o = { x: 1 };
  o.propertyIsEnumerable("x") // => true: o has an own enumerable property x
  o.propertyIsEnumerable("toString") // => false: toString is an inherited method
  Object.prototype.propertyIsEnumerable("toString") // => false: property is not enumerable
  ```
    * or simply by querying the property
    * The `for/in` loop iterates over all enumerable (either own or inherited) properties of a specified object
    * An alternative to using the `for/in` loop is getting an array of property names and then looping over them with
      a `for/of` loop
    * The four functions you can use to get an array of property names are:
        * `Object.keys()` - returns an array of the names of the enumerable own properties of an object
            * Does not include non-enumerable properties, inherited properties, or properties whose name is a Symbol
        * `Object.getOwnPropertyNames()` works like `Object.keys()` but returns an array of the names of non-enumerable
          own properties as well, as long as their names are strings
        * `Object.getOwnPropertySymbols()` returns an array of the names of the own properties of an object whose names
          are Symbols, whether or not they are enumerable
        * `Reflect.ownKeys()` returns all own property names, both enumerable and non-enumerable, both string and Symbol

### HTML:

* The `footer` element represents a footer for its nearest ancestor sectioning content or sectioning root element
* It typically contains information about the author of the section, copyright data, or links to related documents

### CSS:

* A `pseudo-class` selects an element which is in a specific state
    * For example, a `:hover` pseudo-class selects an element when the user hovers over it
* A `pseudo-element` selects a certain part of an element rather than the entire element
    * For example, a `p::first-line` pseudo-element selects the first line of a paragraph element
* Combinators:
    * You can combine selectors in order to target elements that have a specific relationship to other elements
    * E.g. `article > p { }` would select all `<p>` elements that are direct children of an `<article>` element

## May 30, 2024

### JS:

* The `delete` operator only deletes own properties, not inherited ones
* To delete an inherited property, you must delete it from the prototype object in which it is defined. Doing this
  affects every object that inherits the property
* The delete expression evaluates to `true` if the delete succeeded or if the delete had no effect (such as deleting a
  nonexistent property)
* `delete` also evaluates to `true` when used with an expression that is not a property access expression
* `delete` does not remove properties that have a configurable attribute of `false`
* In strict mode, attempting to delete a non-configurable property causes a `TypeError`
* In non-strict mode, `delete` simply returns `false` when used on a non-configurable property

### HTML:

* `<figcaption>` represents a caption or legend describing the rest of the contents of its parent `<figure>` element,
  providing the element an accessible description
* The `<figure>` HTML element represents self-contained content, potentially with an optional caption, which is
  specified using the `<figcaption>` element
    * Usually a `<figure>` is an image, illustration, diagram, code snippet, etc. that is referenced in the main flow,
      but that can be moved to another part of the document or to an appendix without affeecting the main flow

### CSS:

* With CSS selectors, you have type, class, and ID selectors
* You also have attribute selectors
    * These give you different ways to select elements based on the presence of a certain attribute on an element
  ```CSS
  a[title] {
      font-size: 15px;
  }
  ```
    * This would equate to selecting all elements with a title
    * You can also make selections using selectors for every element with a specific attribute value:
  ```CSS
  a[href="https://www.example.com"] {
      color: red;
  }
  ```

## May 29, 2024

### JS:

* Property Access expressions do not throw an error if a property does not exist
* It does throw an error, however, ifyou try to access a project of an object that does not exist

```javascript
    let o = {x: 1};

o.y // => undefined
o.y.length // => TypeError: Cannot read property 'length' of undefined

```

* Fortunately, conditional property access (options chaining) can be used to avoid this error

```javascript
    let len = o.y?.length; // len is undefined if o.y does not exist
```

* An attempt to set a property on `null` or `undefined` will cause a TypeError
* Attempts to set properties on other values do not always success either
    * Some properties are read-only and cannot be set
    * Some objects do not allow the addition of new properties
* In strict mode, a TypeError is thrown whenever an attempt to set a property fails
    * Outside of strict mode, these failures are usually silent
* Concisely describing when property assignment will fail is difficult, but intuitive
* An attempt to set a property `p` of an object `o` fails in these circumstances:
    * `o` has own property `p` that is read-only
    * `o` has inherited property `p` that is read-only: it is not possible to hide an inherited read-only property with
      an own property of the same name
    * `o` does not have an own property p; `o` does not inherit a property `p` with a setter method and `o`'
      s `extensible` attribute is `false`

### HTML:

* The `<fieldset>` element is used to group several controls as well as labels `<label>` within a web form

```HTML

<form>
    <fieldset>
        <legend>Choose your favorite monster</legend>

        <input type="radio" id="kraken" name="monster" value="K"/>
        <label for="kraken">Kraken</label><br/>

        <input type="radio" id="sasquatch" name="monster" value="S"/>
        <label for="sasquatch">Sasquatch</label><br/>

        <input type="radio" id="mothman" name="monster" value="M"/>
        <label for="mothman">Mothman</label>
    </fieldset>

</form>
```

* You can use a `<legend>` element to provide a caption for the `<fieldset>` element
* You can also provide a `disabled` attribute to the `<fieldset>` element to disable all of the controls within it

### CSS:

* Web Fonts
    * As discussed previously, you can describe a font family in CSS using the `font-family` property
  ```CSS
  p { 
      font-family: "Times New Roman", Times, serif;
  }
  ```
    * In addition to this method, you can also load fonts from the web using the `@font-face` rule
  ```CSS
  @font-face {
      font-family: "MyWebFont";
      src: url("myfont.woff2");
  }
  ```
    * All major browsers support `WOFF/WOFF2` (Web Open Font Format versions 1 and 2)
    * The order of files provided will affect what gets loaded first
    * So if you provide multiple files to be loaded to populate a web font, use `WOFF2`, then `WOFF` as a fallback
    * If you have to support older browsers, you should provide `EOT` (Embedded Open Type), `TTF` (TrueType Font), and
      SVG web fonts for download

## May 28, 2024

### JS:

* If you are to assign property `x` to the object `o`, and `o` already has a property `x`, the property will be
  overwritten
    * If `o` inherits a property `x` from its prototype chain, that inherited property is now hidden by the newly
      created own property with the same name
* Property assignment examines the prototype chain only to determine whether the assignment is allowed
    * If `o` inherits a read-only property named `x` for example, the assignment is not allowed
* The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript
  because it allows us to selectively override inherited properties
* There is one exception to the rule that a property assignment either fails or creates or sets a property in the
  original object
    * If o inherits the property x, and that property is an accessor property with a setter method, then that setter
      method is called rather than creating a new property x in o
    * Note, however, that the setter method is called on the object o, not on the prototype object that defines the
      property, so if the setter method defines any properties, it will do so on o, and it will again leave the
      prototype chain unmodified
    *

### HTML:

* The `<embed>` element is used to embed external content at the specific point in the document.
    * This content is provided by an external application or other source of interactive content such as a browser
      plug-in
    * Most modern browsers have deprecated and removed support for browser plug-ins, so relying upon `<embed>` is not
      wise for the average user's browser
    * It has the following notable attributes:
        * `height`: the displayed height of the resource, in CSS pixels
        * `width`: the displayed width of the resource, in CSS pixels
        * `src`: the URL of the resource being embedded
        * `type`: the MIME type of the resource
    * A MIME type is a two-part identifier for file formats and format contents transmitted on the Internet
        * Stands for **Multipurpose Internal Mail Extensions**
        * The first part is the type, and the second part is the subtype
        * For example, the MIME type for HTML is `text/html`
        * The MIME type for a JPEG image is `image/jpeg`
        * The MIME type for a PDF document is `application/pdf`
* The `<fencedframe>` element represents a nested browsing context, embedding another HTML page into the current one
    * They are very similar to `<iframes>`, except that:
        * Communication between frame content and embedded site is restricted
        * It can access cross-site data, but only in a very specific set of controlled circumstances that preserve user
          privacy
        * It can't be manipulated or have its data accessed via regular scripting (e.g. reading or setting the source
          URL)
        * It content can only be embedded via specific APIs
        * The frame can't access the embedding context's DOM, not can the embedding context access the frame's DOM
    * Notable attributes include:
        * `allow`: specifies a Permissions Policy for the `<fencedframe>
        * `width`, `height`
    * The only features that can be enabled by a policy inside fenced frames are the specific features designed to be
      used inside fenced frames:
        * Protected Audience API
            * attribution-reporting
            * private-aggregation
            * shared-storage
            * shared-storage-select-url
        * Shared Storage API
            * attribution-reporting
            * private-aggregation
            * shared-storage
            * shared-storage-select-url
    * Focusing across frame boundaries is limited. User initiated actions such as a click or a tab can do so, as there
      is no fingerprinting risk there
        * `HTMLElement.focus()` is prohibited, however, because a malicious script could use a series of such calls to
          leak inferred information across the boundary

### CSS:

* Styling Links:
    * Link States: by taking advantage of the different states that links can be in, you can style them effectively
        * `:link` pseudo class will select any link that has a destination (not just a named anchor)
        * `:visited` pseudo class will select any link that has been visited
        * `:hover` pseudo class will select any link that is being hovered over
        * `:active` pseudo class will select any link that is being activated
        * `:focus` pseudo class will select any link that is currently focused
    * The default link styles can be turned off/changed using the following CSS properties:
        * `color`
        * `cursor`
        * `outline`

## May 23, 2024

### JS:

* `Object.create()` creates a new object, using the first argument as the prototype of that object:

```javascript
        let o1 = Object.create({x: 1, y: 2}); // o1 inherits properties x and y

o1.x + o1.y // => 3

```

* You can pass `null` to create a new object that does not have a prototype, but if you do this, the newly created
  object will not inherit anything, not even basic methods like `toString()` (which means it won't work with the +
  operator either)

```javascript 
  let o2 = Object.create(null); // o2 inherits no props or methods.
```  

* If you want to create an ordinary empty object (like the object returned by `{}` or `new Object()`),
  pass `Object.prototype` to `Object.create()`

```javascript
  let o3 = Object.create(Object.prototype); // o3 is like {} or new Object().
````

* One use case for creating a prototype chain is that a library method might unintentionally augment the values in the
  original object. Instead, you can pass in your object as a prototype of the new object, which will guard against
  accidental modifications

```javascript
  let x = {x: "don't change this value"};

library.function(Object.create(o));
```

* Javascript objects are associative arrays (like a hash map or dictionary)
    * In C, C++, Java, and similarly strongly type languages, an object can only have a fixed number of properties, and
      the names of these properties must be defined in advance
    * Since JS is a loosely typed language, this rule does not apply
    * When you use the `.` operator to access a property of an object, the name of the property is expressed as an
      identifier
        * Identifiers must be typed literally into your JavaScript program; they are not a datatype, so they cannot be
          manipulated by the program
    * On the other hand, when you access a property of an object with teh `[]` array notation, the name of the property
      is expressed as a string
        * Strings are JS datatypes, so they can be manipulated by the program
        * Basically, these values can be handled at runtime, while the dot operator is more strict and requires
          identifiers, not strings

### HTML:

* The `<div>` element is the generic container for flow content
    * The `<div>` should only be used when no other semantic elements (like `<article>` or `<nav>` are appropriate)
* The `<dl>` or **Description List** element encloses a list of groups of terms
    * The `<dt>` or description term element is used to define the term being defined
    * The `<dd>` or description details element is used to define the description, definition, or value for the
      preceding term
    * Tip:
        * It can be handy to define a key-value separator in the CSS, such as:
      ```CSS
      dt::after {
        content: ": ";
      }
      ```
* The `<dt>` or **Description Term** element specifies a term in a description or definition list
    * Must be used inside of a `<dl>` element
* The `<em>` or **Emphasis** element marks text that has stress emphasis
    * This is semantically different from the `<i>` or `<cite>` elements, which are used for other types of emphasis

### CSS:

* Controlling List Counting
    * Sometimes you might want to:
        * Start from a number other than 1
        * Count Backwards
        * Count in steps of more than 1
    * HTML and CSS have some tools to help
        * Check `index.html` for example
        * Add `start` attribute to the list element to start from a number besides 1
        * Add `reversed` attribute to the list element to start from the final number and count backwards
        * Add `value` attributes with different numbers to list item elements in order to count in steps of more than 1

## May 22, 2024

### JS:

* All objects in JS have a second object (called a prototype) tied to them
* Any object created with the `new` keyword inherits the prototype of the constructor function
    * e.g. `let o = new Object();` will inherit the prototype of the `Object` constructor, or `Object.prototype`
* All objects created from Object literals will inherit `Object.prototype`
* Almost all objects have a prototype, but only a relatively small number of objects have a prototype property
    * It is these objects with prototype properties that define the prototypes for all other objects
* `Object.prototype` is one of the rare objects in JS that has no prototype
    * Other prototype objects are normal objects that do have a prototype
    * Most built-in constructors (and most user-defined constructors) have a prototype that inherits
      from `Object.prototype`
        * e.g., `Date.prototype` inherits from `Object.prototype`
            * So, an object created by `new Date()` will inherit from `Date.prototype` and `Object.prototype`
            * This linked series of prototype objects is called a **_Prototype Chain_**
* Chapter 9 will describe how to set Class constructors up to assign object prototypes for instances created by the
  constructor

### HTML:

* Wrap-up of the HTML dialog element today

### CSS:

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

### JS:

* Any value in Javascript that is not a string, a number, a Symbol, or `true`, `false`, `null`, or `undefined` is an
  object
* A property name on an Object can be any string, including the empty string (or any Symbol)
* The value may be any Javascript value, or it may be a getter or setter function (or both)
* An `own property` refers to a non-inherited property
* In addition to its name and value, each property has three property attributes:
    * The _writable_ attribute specifies whether the value of the property can be set
    * The _enumerable_ attribute specifies whether the property name is returned by a `for/in` loop
    * The _configurable_ attribute specifies whether the property can be deleted and whether its attributes can be
      altered
* Many of JS's built-in objects have properties that are read-only, non-enumerable, or non-configurable
* By default, however, all properties of the objects you create are writable, enumerable, and configurable

### HTML:

* Today, I am practicing the usage of dialogs in the `index.html` file attached

### CSS:

* The `outline` and `border` properties in CSS have different properties
    * The border is added to the inside of the element, while outline is added to the outside of the element
* The CSS selector `x + y` will select the first instance of a `y` following an `x` element.
    * This is the adjacent sibling selector

## May 14, 2024

### JS:

* Unlike statements, **declarations** in JS code don't necessarily "make things happen"
* Rather, they provide structure for the code and are run before code is actually executed
* These declarations include `let`, `var`, `const`, `class`, `function`, `import`, and `export`
* You've already learned much about the `let`, `var`, `const`, and `function` declarations
* `class` is on the way
* `import` and `export` are both used to link to **modules** in JS
    * A _module_ is a file of Javascript code with its own global namespace, completely independent of all other modules
    * Values within modules are private and cannot be accessed by external modules unless they've been explicitly
      exported
    * The export keyword is sometimes used in addition to other declarations
    * When a module exports only a single value, this is typically done with the special form `export default`
  ```javascript
  export const TAU = 2 * Math.PI;
  export function magnitude(x,y) { return Math.sqrt(x*x + y*y); }
  export default class Circle { /* class definition omitted here */ }
  ```

## May 13, 2024

### JS:

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
    * Assignments to non-writable properties and attempts to create new properties on non-extensible objects throw
      a `TypeError`
        * In non-strict mode, these assignments fail silently
    * Code passed into `eval` is executed in its own scope, rather than the caller's scope
    * The Arguments object in a function holds a static copy of the values of the arguments passed to the function
        * In non-strict mode, the Arguments object has a magical behavior in which elements of the array and named
          function parameters both refer to the same value
    * The `delete` operator throws a `SyntaxError` when used on a non-configurable property
        * In non-strict mode, the `delete` operator returns `false` when used on a non-configurable property
    * It is a Syntax Error for an object literal to define two properties of the same name
    * Octal Integers (beginning with a 0 and not followed by an x) are not allowed
    * Identifiers `eval` and `arguments` are treated as reserved words, and you cannot change their value
        * You cannot assign a value to their identifiers, declare them as variables, use them as function names, use
          them as function parameter names, or use them as the identifier of a `catch` block
    * The ability to examine the call stack is restricted
        * `arguments.caller` and `arguments.callee` are not allowed, and both throw a `TypeError` within a strict mode
          function

### HTML:

* The `<dialog>` represents a modal or non-modal dialog box or other interactive component, such as a dismissible alert,
  inspector, or subwindow
    * Modal dialog boxes interrupt interaction with the rest of the page, while non-modal dialog boxes allow interaction
      with the rest of the page
    * Javascript should be used to display the `<dialog>` element
        * Use the `.showModal()` method to display a modal dialog box
        * Use the `.show()` method to display a non-modal dialog box
        * A dialog box can be closed using the `.close()` method
        * Modal dialogs can also be closed by pressing the `esc` key
    * The `tabindex` attribute must not be used on the `<dialog>` element
    * The `open` attribute is a boolean attribute that controls whether the dialog box is displayed
        * It's recommended to use the `.show()` or `.showModal()` methods to display the dialog box
        * If a dialog is opened using the `open` attribute, it will be displayed as a non-modal dialog box
    * HTML `<form>` elements can be used to close a dialog if they have the `method="dialog"` attribute set, or if the
      button used to submit the form has the `formmethod="dialog"` attribute set

### CSS:

* The `line-height` property sets the height of each line of text
* Similarly, you can set the `letter-spacing` and `word-spacing` properties to adjust the space between characters and
  words, respectively

## May 10, 2024

### JS:

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
// The break statements jump here. If we arrive here with success == false then there was somthing wrong with the matrix
we
were
given.
// Otherwise, sum contains the sum of all cells of the matrix

```

* The `continue` statement is used to skip the rest of the body of a loop and jump back to the top of the loop to begin
  a new iteration
    * In the case of a `for` loop, the increment expression is evaluated before the loop condition is tested
    * In the case of a `while` loop, the loop condition is tested before the loop body is executed
    * Here's an example:

```javascript
  for (let i = 0; i < data.length; i++) {
    if (!data[i]) continue; // Skip null and undefined values
    total += data[i];
}
```

* The `return` statement is used to make the interpreter jump from a function invocation back to the code that invoked
  it
* The `yield` statement is much like the return statement but is used only in ES6 generator functions to produce the
  next value in the generated sequence of values without actually returning.
    * In order to understand the `yield`, you must understand iterators and generators
* The `throw` statement is used to throw an exception, which is a signal that an error or other unusual condition has
  occurred
    * The `throw` statement requires a single argument, which is the value of the exception that is thrown
    * The `throw` statement is typically used in conjunction with the `try/catch/finally` statement
* The `finally` statement is used to specify a block of code that will be executed after a `try` or `catch` block,
  regardless of whether an exception is thrown
    * If any part of the `try` block is executed, the `finally` block will also be executed
    * This statement is often used to clean up resources, such as closing files or network connections

### HTML:

* The `<dfn>` element is used to indicate a term being defined.
    * It should be used to indicate the term being defined, not the definition itself
    * The ancestor of the `<dfn>` element should be a `<p>`, `<section>`, `<article>`, or `<aside>` element that
      contains the full definition of the elemtn
    * Or it can be used with `<dd>/<dt>` elements in a `<dl>` element

### CSS:

* The `text-align` property is used to position horizontal alignment of text within its parent container
    * The `text-align` property can have one of the following
      values: `left`, `right`, `center`, `justify`, `start`, `end`, `match-parent`, `initial`, `inherit`
    * The `text-align` property is inherited by child elements
    * The `text-align` property only affects inline-level and inline-block elements
    * The `text-align` property does not affect block-level elements
    * The `text-align` property does not affect table elements
    * The `text-align` property does not affect flex items

## May 9, 2024

### JS:

* Another form of statement in JS is a `jump` statement
    * The `break` statement makes the interpreter jump to the end of a loop or other statement
    * The `continue` statement makes the interpreter skip the rest of the body of a loop and jump back to the top of a
      loop to begin a new iteration
    * The `return` statement makes the interpreter jump from a function invocation back to the code that invoked it and
      also supplies the value for the invocation
    * The `throw` statement is a kind of interim return from a generator function
        * It is designed to work with `try/catch/finally` statements
* Furthermore, any statement may be labeled by preceiding it with an identifier and a colon:
  ```javascript
  identifier: statement
  ```
    * This is useful for nested loops, where you can break out of the inner loop by referencing the outer loop

### HTML:

* The `<dd>` element provides the description, definition, or value for the preceding term `<dt>` in a description
  list `<dl>`
    * This is called the description details element
* The `<del>` element is used to indicate that text has been deleted from a document
    * This is typically displayed with a strikethrough
    * The `cite` attribute can be used to provide a URL to the source of the deletion
    * The `datetime` attribute can be used to provide a machine-readable date and time for the deletion
    * This could be used to show changes, similar to the `<ins>` element

### CSS:

* In terms of font-size, a `<p>` tag will be set with a default value of `16px` by default
* Using `em` can be tricky when you're setting the font-size of a parent element, as it will be relative to the parent
  element
* Using `rem` is a better choice, as it will be relative to the root element, which is the `<html>` element
* `font-style` is the property used to turn italic text on or off
* `font-weight` is the property used to set the weight of the font
* `text-transform` allows you to set your font to be transformed
    * `none`: prevents any transformation
    * `lowercase`, `uppercase`, `capitalize`
    * `full-width`: converts the text to full-width characters that are written inside a fixed width square
* `text-decoration` is the property used to set the decoration of the text
    * `none`, `underline`, `overline`, `line-through`, `blink`
* `text-shadow` allows you to apply drop shadows to your text, setting the horizontal and vertical offsets, blur radius,
  and color

## May 8, 2024

### JS:

* The `for/in` loop iterates over the properties of an object
    * It will iterate over all enumerable properties of an object, including inherited properties
    * The `for/in` loop is not recommended for use with arrays, as it will iterate over the indices of the array, as
      well as any other enumerable properties
    * The `for/of` loop is recommended for use with arrays, as it will only iterate over the values of the array
    * In addition to built-in methods, many of the built-in properties of objects are non-enumerable
    * All properties and methods defined by your code are enumerable by default
    * The `for/in` loop will iterate over all enumerable string-named properties, whether they are inherited up the
      prototype chain or not
* You will learn more about enumerable properties later

### HTML:

* The `<data>` element is used to provide a machine-readable version of the content within it

  ```HTML
    <p>New Products:</p>

<ul>
    <li>
        <data value="398">Mini Ketchup</data>
    </li>
    <li>
        <data value="399">Jumbo Ketchup</data>
    </li>
    <li>
        <data value="400">Mega Jumbo Ketchup</data>
    </li>
</ul>
  ```

* The `<datalist>` element is used to provide a list of predefined `<option>` elements within another control
    * The `<datalist>` element is used in conjunction with the `<input>` element to provide a list of predefined options
      for the user to choose from
    * The `<datalist>` is given a unique id, which is then referenced by the `list` attribute of the `<input>` element
    * This can be used for autocomplete functionality, or to provide a list of options for the user to choose from

### CSS:

* Today, I start the CSS grids assessment. See `index.html` and `styles.scss` for details

## May 7, 2024

### JS:

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

### HTML:

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
    * The `<colgroup>` element should always appear within a table, after any `<caption>` elements but before
      any `<thead>`, `<tbody>`, `<tfoot>`, or `<tr>` elements

### CSS:

* The ability to add subgrids enables even more flexibility within this layout model
* Check the accompanying `index.html` and `styles.scss` files for a full example

## May 6, 2024

### JS:

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

### HTML:

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

### CSS:

* In addition to setting the `grid-column` and `grid-row` properties, you can also use `grid-template-areas` to define
  the layout of different sections
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

### JS:

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

### HTML:

* The `<canvas>` element uses either the canvas scripting API or the WebGL API to draw graphics and animations
* It uses the global attributes, and some noticeable ones are:
    * `height` : The height of the canvas
    * `width` : The width of the canvas
* Unlike the `<img>` element, the `<canvas>` element requires the closing tag
* iOS devices notably limit maximum canvas size to 4,096 x 4,096 pixels, whereas most other browsers allow 10,000 x
  10,000 pixels
* Using the `OffscreenCanvas` API, you can create a canvas that is not visible in the DOM, but can be used to render
  images offscreen
* It is good practice to include alternative text within the canvas to describe what is happening on the canvas
* For more detailed description of using the `Offscreen Canvas` API and the `Canvas` API

### CSS:

* You can specify an item's placement within the grid using
  the `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end` properties
* These are often shortened to `grid-column` and `grid-row` properties
* For example:
* ```CSS
    .item {
        grid-column: 1 / 3;
        grid-row: 1 / 3;
    }
    ```
    * This will place the item in the first column, spanning two columns, ending after the 3rd, and in the first row,
      spanning two rows, ending after the 3rd

## May 2, 2024

### JS:

* `else if` is not actually a statement in proper JS, and is instead an idiom used by programmers to make these nested
  conditionals more legible
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
  The purpose of these `case` statements is to provide a starting point for the code block to execute, and the `break`
  statement is used to exit the `switch` statement

### HTML:

* The `<button>` attribute is used to define a button
    * It inherits the global attributes
    * Notable attributes include `autofocus`, `disabled`, and `type`
    * When the button is part of a form, the `type` attribute can be `submit`, `reset`, or `button`
        * The `submit` type will submit the form data to the server, and is the default type if the `type` attribute is
          not specified
        * If your buttons are not for submitting form data to a server, be sure to set their `type` attribute
          to `button`
            * Otherwise, the default behavior of the button will be to submit the form data to the server, possibly
              destroying the current state of teh document
    * If a button is attached to a form, the following attributes help direct this call:
        * `formaction` : The URL that processes the form data when the form is submitted
        * `formenctype` : The encoding type for the form data
        * `formmethod` : The HTTP method used to submit the form data
        * `formnovalidate` : A Boolean attribute that specifies that the form data should not be validated when
          submitted
        * `formtarget` : The target window or frame where the form data is submitted
        * `name` : The name of the button, which is submitted with the form data
        * `value` : The value of the button, which is submitted with the form data
        * `form` : The form element id that the button is associated with
    * For accessibility, it's best practice to include text along with any icon within a button, to ensure cultural or
      technological gaps in understanding can be overcome by the user
* Firefox will add a small dotted border around a button when it is focused, but this can be removed with the following
  CSS:
  ```CSS
  button::-moz-focus-inner {
    outline: none;
  }
  ```

### CSS:

* If you set a `grid-auto-rows` value to `100px' but want to make sure than any overflown text in a row would still
  display
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
* You can also configure a value that allows as many columns as will fit, using a combination of `auto-fit`
  and `minmax()`
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

### JS:

* The comma operator (`,`) is used to evaluate any left-hand operands, then return the value of the right-hand-most
  operand
* An example would be

```javascript 
  i = 0, j = 0, k = 2;

// you could also write something like
i = 0, j = 0, k = someVal === 2 // in this case, the comma operator discards the left operand values and returns '
someVal
' assigned to k for comparison to the number 2

```

* The most common example of the comma operator is in a `for` loop, where multiple variables are used, and operands with
  side effects exist on both sides of the comma

```javascript
  for (let i = 0, j = 1; i < 10, j < 5; i++, j++) {
    console.log(i, j)
}
```

* **Expressions** are evaluated to produce a value, but **Statements** are executed to make something happen

### HTML:

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
    * There are accessibility concerns associated with the `<br>` element, as it can be misused to create a new
      paragraph, when a `<p>` element should be used instead
    * For the purpose of screen readers and accessibility, it is recommended not to use a `<br>` element to create a new
      paragraph

### CSS:

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
* Implicit grids extends the defined explicit grid when content is placed outside of that grid, such as into the rows by
  drawing additional grid lines
* By default, tracks created in the grid are auto-sized, which means they're large enough to contain their content
* You can also give them a size using `grid-auto-rows` and `grid-auto-columns`
* Using `grid-auto-columns` with `grid-template-columns` will not overwrite the explicit grid

## April 29, 2024

### JS:

* The `eval` function is used to evaluate a string as JavaScript
    * Generally, the `eval` function will use the variable environment of the code that calls it
    * This means that the `eval` function can access variables in the calling code, reassign them, etc.
    * It can also create new variables in that scope using the `var` variable declaration keyword
    * `let` and `const` variables are block-scoped, so they will not be accessible outside the `eval` function
    * If the `eval` is aliased and called by any other name, its scope will be treated as global scope, and any local
      variables or functions from the calling scope will not be accessible within the `eval` code

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

* The notable difference is the context in which the eval function is called, and the scope in which it is executed
      in each case

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

### HTML:

* The `<bdo>` or Bi-directional Text Override element is used to override the Unicode bidirectional algorithm
    * This is useful when you want to display text in a different direction than the surrounding text
    * The `dir` attribute is used to specify the direction of the text
    * The `dir` attribute can have one of three values: `ltr`, `rtl`, or `auto`
    * The `ltr` value specifies that the text should be displayed from left to right
    * The `rtl` value specifies that the text should be displayed from right to left
    * The `auto` value specifies that the text should be displayed in the direction of the surrounding text
    * The main difference between the `bdi` and `bdo` elements is that the `bdi` element isolates the text from its
      surrounding text, while the `bdo` element overrides the Unicode bidirectional algorithm
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

### CSS:

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

### JS:

* The assignment operator `=` has right-to-left associativity which means that the rightmost expression is evaluated
  first
    * This is why you can chain assignments like `let a = b = c = 5`
    * The rightmost expression is evaluated first, and then assigned to the next variable to the left
    * This is also why you can chain assignments with different types of variables
    * For example, `let a = b = 'hello'` will assign the string `'hello'` to `b`, and then assign `b` to `a`
* Also, the assignment operator might be nested inside more complex logic, like `(a = b) === 0`
    * In this case, the assignment operator is evaluated first, and then the comparison operator is evaluated

### HTML:

* The `<bdi>` element is used to tell a browser about bi-directional text
    * This is useful when you have text in multiple languages, or text that is mixed with numbers
    * The `<bdi>` element isolates the text from its surrounding text, so that the browser can display it correctly
    * For example:
    * ```html
      <p>Here is some text in English: <bdi>שלום</bdi></p>
      ```

### CSS:

* The `display` property in CSS is used to determine how an element is displayed
    * The `display` property is used to determine the layout of an element, and how it interacts with other elements on
      the page
    * The `display` property is one of the most important properties in CSS, and is used to control the layout of a web
      page
        * The `block` value makes an element a block-level element, which means it will take up the full width of its
          container, and will start on a new line
        * The `inline` value makes an element an inline-level element, which means it will only take up as much width as
          it needs, and will not start on a new line
        * The `inline-block` value makes an element an inline-block element, which means it will take up as much width
          as it needs, but will start on a new line
        * The `flex` value makes an element a flex container, which means it will lay out its children in a flex layout
        * The `grid` value makes an element a grid container, which means it will lay out its children in a grid layout
        * The `none` value makes an element invisible, and it will not take up any space on the page
        * The `table` value makes an element a table element, which means it will lay out its children in a table layout
        * The `flow-root` value makes an element a block-level element, and establishes a new block formatting context

## April 25, 2024

### JS:

* The `instanceof` operator checks if an object is an instance of a class
    * It returns `true` if the object is an instance of the class, and `false` otherwise
    * It can also be used to check if an object is an instance of a subclass
    * It can also be used to check if an object is an instance of an interface
    * Interesting, it's not quite the same thing as `typeof`, which checks the type of a variable
* For example, if you were to declare `x = 2` and `y = new Number(2)`, then `x instanceof Number` would return `false`,
  while `y instanceof Number` would return `true`
* This is because `x` is a primitive number, while `y` is an instance of the `Number` class
* The difference between a primitive number and an instance of the `Number` class is that the `Number` class has methods
  and properties that can be accessed
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

### HTML:

* The `<base>` element specifies the base URL to use for all relative URLs in a document
    * The `<base>` element must have an `href` attribute, which specifies the base URL, or a `target` attribute, which
      specifies the default target for all hyperlinks and forms in the document
    * The `<base>` element must be placed inside the `<head>` element
    * The `<base>` element is supported by all major browsers
    * A document's used base URL can be accessed by scripts with `Node.baseURI`. If the document has no <base> elements,
      then baseURI defaults to `location.href`

### CSS:

* In a `display: grid` context, you can use `fr`, or fractional units to take up a given proportion of the available
  space
* For example:
```CSS
.container {
display: grid;
grid-template-columns: 1fr 2fr 1fr;
}
```

## April 24, 2024

### JS:

* The `in` operator expects a lefthand argument that is a string, symbol, or can evaluate to a string, and a righthand
  side argument that is an Object
* The `in` operator will return `true` if the lefthand argument is a property of the righthand object, and `false`
  otherwise
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

### HTML:

* The `<b>` element is a stylistic element that provides bold formatting to text
    * It is no longer recommended, with either `<strong>` or `<span>` with CSS `font-weight` styling being preferred
    * Here's where the docs get nitpicky:
        * The `<strong>` element indicates text of certain **importance**
        * The `<em>` element indicates text of certain _emphasis_
        * The `<mark>` element indicates text with certain relevance (highlighting)
    * If there is no semantic importance, emphasis, or relevance, then the `<span>` element with CSS styling is
      recommended

### CSS:

* **Font stacks** enable you to create fall-backs if a web-font fails to load
* The `font-family` property can take a comma-separated list of font names, with the browser trying each font in order

```CSS
p {
font-family: "Trebuchet MS", Verdana, sans-serif;

}

```

* In this case, the browser will first try to load "Trebuchet MS", then "Verdana", and finally any sans-serif font

## April 23, 2024

### JS:

* The shift left operator `<<` shift the bits of a number to the left, filling empty bits with 0's
    * This is effectively the same as multiplying by 2
* The shift right operator `>>` shifts the bits of a number to the right, filling the empty bits with the sign bit (0
  for positive numbers, 1 for negative numbers)
    * This is effectively the same as dividing by 2, but always rounding down
* In a strict equality check, `NaN` is no equal to itself.
    * A good shorthand way is to use the global `isNaN()` function or to check is `x !== x`
* Also, in a strict equality check, `0` is equal to `-0`

### HTML:

* The `<article>` element is a semantic element that defines a self-contained piece of content that could be distributed
  and reused independently
    * It could be a blog post, a forum post, a news article, or a comment
    * The `<article>` element is a block-level element, and will typically be displayed in a normal font
    * The `<article>` element is a semantic element, and should be used to provide meaning to the content
    * The `<article>` element is supported by all major browsers
* The `<aside>` element is a semantic element that defines content that is tangentially related to the content around it
    * It could be a sidebar, a pull quote, a glossary, or a related article
    * The `<aside>` element is a block-level element, and will typically be displayed in a normal font
    * The `<aside>` element is a semantic element, and should be used to provide meaning to the content
    * The `<aside>` element is supported by all major browsers

### CSS:

* The `justify-items` property is ignored in a flex container, as it only applies to grid containers
* Instead, justifying items in a flex container is done with the `justify-content` property
    * `start`, `end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch`, `safe`, `unsafe`

## April 22, 2024

### JS:

* The increment and decrement operators have a pre- and post- versions, which return the value before or after
  increment/decrement
* For example:
```javascript
  let x = 5 
  let y = x++ // y == 5, x == 6
  let z = ++x // z == 7, x == 7
```

* Basically the pre- or post- defines if the change to the original will happen pre- or post- the assignment to
  the `lval` in question
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

* A block-level element always starts on a new line, taking up the entire space availab to it along the main-axis (
  x-axis for English text)
* An inline-level element only takes up as much space as it needs, and does not start on a new line. A span is an
  exampel of an inline element.
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

* The `<address>` HTML element indicates that the enclosed HTML provides contact information for a person or people, or
  for an organization
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
    * We call this **operator precedence** (which operator is evaluated first) and **operator associativity** (which
      operator is evaluated first in the case of operators with the same precedence)
    * Generally, access operators and invocation operators take top precedence
    * Mult/Division operators take precedence over Add/Subtract operators
    * Use parentheses to ensure the order of operations you want
* The `??`, or **Nullish Coalescing Operator** in JS returns its right-hand side operand when its left-hand side operand
  is null or undefined
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
* We either use a _dot_ followed by a valid identifier (cannot be a number, reserved keyword, or start with a number or
  special character)
* Or we use an expression to access a property, which is evaluated to a string literal or symbol
* In either case, accessing a property that doesn't exist will return `undefined`
* Optional Chaining allows the ability to access deeply nested properties without throwing an error if a property
  doesn't exist
    * It's denoted by a `?.` after the object or array, and will return `undefined` if the property doesn't exist
    * It's especially useful when working with APIs, where the data structure may not be consistent
    * It's also useful when working with user input, where the data may not be complete

### HTML:

* The `<a>` or "anchor" tag is used to create hyperlinks to other web pages, files, locations within the same page,
  email addresses, or any other URL\
* The `href` indicates the destination of the link
    * Acceptable alternative link formats include:
        * Telephone numbers with `tel:` URLs
        * Email addresses with `mailto:` URLs
        * SMS text messages with `sms:` URLs
* `hreflang` specifies the language of the linked resource - allowed values are the same as the global `lang` attribute
* `ping` is a space-separated list of URLs to which, when the link is followed, post requests with the body `ping` will
  be sent
    * These are typically used for trackers, analytics, and other monitoring purposes
* `referrerpolicy` specifies how much of the referrer information should be sent when following the link
    * `no-referrer` : The `Referer` header will not be sent
    * `no-referrer-when-downgrade` : The `Referer` header will not be sent to a less secure destination
    * `origin` : Only the origin of the document will be sent (its scheme/protocol, host and port)
    * `origin-when-cross-origin` : The full URL will be sent if the destination is the same origin, otherwise only the
      origin will be sent
    * `same-origin` : The full URL will be sent if the destination is the same origin, otherwise no `Referer` header
      will be sent
    * `strict-origin` : The full URL will be sent if the destination is the same origin, otherwise only the origin will
      be sent
    * `strict-origin-when-cross-origin` : The full URL will be sent if the destination is the same origin, otherwise
      only the origin will be sent
    * `unsafe-url` : The full URL will be sent, regardless of the destination
* `rel` specifies the relationship between the current document and the linked document
* `target` specifies where to open the linked document
    * `_blank` : Opens the linked document in a new window or tab
    * `_self` : Opens the linked document in the same frame as it was clicked
    * `_parent` : Opens the linked document in the parent frame
    * `_top` : Opens the linked document in the full body of the window
    * `framename` : Opens the linked document in a named frame
* You can also link to sections below with an `href` of `#section-name`, where the id is set to another section
* Using an `<a>` tag with a `target="_blank"` attribute will open the link in a new tab, with some security
  considerations
    * The new tab or window will often have access to the original page, through the `window.opener` property
    * In a "Tabnabbing" attack, the new tab will change its location to a phishing site, while the original page is
      still open
    * In a "Reverse Tabnabbing" attack, the original (legitimate) page have its location changed to a phishing site, as
      the new tab accesses the `window.opener` property
    * Many browsers have implemented security measures to prevent these attacks, but it's still a good idea to be aware
      of the risks, and use `noopener` and `noreferrer` attributes to prevent these attacks

### CSS:

* If you had a flex container and wanted to ensure that overflowing elements in your flex direction will wrap onto a
  following row/column, you can set `flex-wrap: wrap`
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
* Finally, you have to handle `ondragover` and `ondrop` events for the target element(s), since their default behavior
  is normally not to accept drag events
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
        * Flex items will always remain in a single row or column, overflowing their container if their combined
          width/height exceeds the containing element width/height.

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
    * The `<audio>` element has no intrinsic visual output of its own unless the controls attribute is specified, in
      which case the browser's default controls are shown
    * If you attribute multiple `<source>` elements to an `<audio>` element, the browser will choose the first one it
      can play
    * Audio elements do not inherently support subtitles or captions (WebVTT)
        * You either need to use a `<video>` element or a JavaScript library to add subtitles
    * There are a number of events emitted by the `<audio>` element, including:
        * `onplay`, `onpause`, `onvolumechange`, `onseeking`, `onseeked`, `onended`, `oncanplay`, `oncanplaythrough`, `onloadedmetadata`, `onloadeddata`, `onwaiting`, `onplaying`, `onstalled`, `onsuspend`, `onabort`, `onerror`

### CSS:

* The `css justify-content` property defines how the browsers sets the spaces between and around content items along the
  main (x) axis of a flex container
    * `start', `end`, `center`, `space-between`, `space-around`, `space-evenly`, `stretch`, `safe`, `unsafe`
* The `justify-items` property sets the default alignment for items inside a grid container along the inline (x) axis
* The `justify-self` property sets the alignment of an item within its containing grid or flexbox, overriding
  the `justify-items` property if it's present
    * `auto`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `safe`, `unsafe`

## April 9, 2024

### JS:

* You can include multiple variables, multiple loop conditions, and even multiple increment/decrement operators inside
  of a `for` loop
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

* The `align-content` property sets the distribution of space between and around content items along a flexbox's cross
  axis, or a grid or block-level element's block axis
    * `start`, `end`, `center`
    * `space-between`, `space-around`, `space-evenly`, `stretch`
    * `safe`, `unsafe` - safety resets alignment to the `start` value to prevent data loss in the case of overflow,
      but `unsafe` honors the alignment value
* The `align-items` property sets the `align-self` for all direct children as a group
* The `align-self` property sets the alignment of an item within its containing flexbox or grid
    * `auto`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `safe`, `unsafe`
* SO Link to more specifically describe how these properties work
  together: https://stackoverflow.com/questions/31250174/css-flexbox-difference-between-align-items-and-align-content

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
 outline:

5
px solid red

;
  ```

## April 5, 2024

* ### JS:
* The global functions `parseInt()` and `parseFloat()` can be used to converted strings with leading numbers into
  either integers or floating point numbers

```javascript
parseInt('34 tribes') // returns 34
parseFloat('3.14 pies') // returns 3.14
parseInt('3.14 pies') // returns 3
parseFloat('.14') // return 0.14, because the first character is NaN
parseInt('.14') // returns NaN, because integers can't start with '.'
parseFloat('$14') // returns NaN, because numbers can't start with '$'
```
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
```

  ### CSS:
  * The difference between `em` and `rem` units are that `em` refers to an element's parent's font size, while a `rem`
    refers to the root element's (the HTML document's) font size

## April 4, 2024

* ### JS:
    * The unary + operator `(+x)` will convert a value to a number (equivalent of `Number(x)`)
    * JS Symbols
* Numbers have a toString method that accepts a radix (or base) as an argument and returns a number in Base Radix

```javascript
    let n = 17;
let binary = "0b" + n.toString(2); // binary == "0b10001"  
let octal = "0o" + n.toString(8); // octal == "0o21"  
let hex = "0x" + n.toString(16); // hex == "0 
```

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
```



