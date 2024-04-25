## Front-End Bible:
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



