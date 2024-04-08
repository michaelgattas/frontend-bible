## Front-End Bible:

* ### April 4th, 2024
  * #### JS:
    * The unary + operator `(+x)` will convert a value to a number (equivalent of `Number(x)`)
    * JS Symbols
    * Numbers have a toString method that accepts a radix (or base) as an argument and returns a number in Base Radix  
      ```javascript
        let n = 17;    
        let binary = "0b" + n.toString(2); // binary == "0b10001"  
        let octal = "0o" + n.toString(8); // octal == "0o21"  
        let hex = "0x" + n.toString(16); // hex == "0 ```
    #### HTML:
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


* ### April 5th, 2024
  * #### JS:
    * The global functions `parseInt()` and `parseFloat()` can be used to converted strings with leading numbers into either integers or floating point numbers
      ```javascript
      parseInt('34 tribes') // returns 34
      parseFloat('3.14 pies') // returns 3.14
      parseInt('3.14 pies') // returns 3
      parseFloat('.14') // return 0.14, because the first character is NaN
      parseInt('.14') // returns NaN, because integers can't start with '.'
      parseFloat('$14') // returns NaN, because numbers can't start with '$'
      
    #### HTML:
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
