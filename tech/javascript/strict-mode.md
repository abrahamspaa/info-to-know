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
