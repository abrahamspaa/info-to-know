
## Augular Forms

Template + component + data base

### Type of forms building

* Template Driven Approach (Using HTML and Data binding)
* Reactive Driven Approach or Model driven (Using form model and validation in component code)

### Different Between TDA(Template Driven Approach) and RDA(Reactive Driven Approach)

TDA
* Easy To use 
* Two way data binding
* Track the form and input element state (Ex: Submit disabled)

RDA
* More Flexible
* More Complex scenarios 
* Immutable data model
* Action on value change 
* Dynamically add input to the form 
* Reactive transformation -> Debounce Time or DistinctUntillChanged (validation trigger after some time if you want)
* Easy to unit test

### State 
This is stated are manged by form build blocks, which is used in RDA or TDA

* value changed
  * Pristine 
  * Dirty 
* Validity 
  * Valid 
  * Error 
* Visited 
  * Touched (User touched the input)
  * Un Touched (User not touched the input) 
  
### Form Building block 

* Form Control - Input element status (E.x: Input field)
* Form Group - Can have group of form control (E.x: Form element)
* Form Model - Form state e.x: dirity, value;
  * TDM
    * Form model generate automatically.
  * RDM 
    * Model Defined 
    * Data Model defined 



Ref: 
https://angular.io/start/start-forms
https://github.com/DeborahK/Angular-ReactiveForms
