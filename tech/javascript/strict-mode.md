# Use of Strict mode
  * Eliminates some JavaScript silent errors
  * JavaScript engines to perform optimizations
  
# How to use it?
* Strict mode for scripts - Add *'use strict'* at the top of the script file 
* Strict mode for functions - Add *'use strict'* inside the function 
* Strict mode for modules - Add *strict* at the export 

# Error 
* Non declared variable
  * Function 
   ```js

   var print = "print me";

   function print (out) {
    'use strict';
    printThis = out; // Use var or declare global
    console.log(printThis);
   }

   print('hello world');
   console.log(printThis)

   ```
  * Script 

   ```js
   'use strict';
   print = "print me"; // Use var or declare global

   function print (out) {
    let printThis = outl
    console.log(printThis);
   }

   print('hello world');
   console.log(printThis)

   ```
* Read only properties 
```js 
'use strict';
var obj = {};

Object.defineProperty(obj, 'readonly', {
 enumerable: false,
 configurable: false,
 writable: false,
 value: 'Hello world'
});

obj.message = 'Hello world'; // Throws error 

```
* Deleting properties 
```js
'use strict';

var obj = { a: 1, b: 2 },
  myVar = 10;
  
delete obj.a;
delete myVar;  // this will not delete
delete obj; // this will not delete

console.log(myVar);
console.log(obj);
```
* Duplicates
```js
'use strict';

function x(a, b, a) { // Second a will throw an error
 console.log(a);
}
x(1, 2, 3);
```
* Octal and Hexidecimals 
```js
'use strict';

var x = 100,
 y = 012, // throws error
 z = 002; // throws error
 
console.log(x + y + z) // 112
```
* With 
* This scope 
* Eval


