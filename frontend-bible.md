## Front-End Bible:


* ## April 9, 2024
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
* ## April 8, 2024
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


* ## April 5, 2024
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

* ## April 4, 2024
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



