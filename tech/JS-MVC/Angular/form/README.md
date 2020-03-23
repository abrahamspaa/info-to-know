
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
* Add ReactiveFormModule to import array in app.modules
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

#### TDM (FormsModule)

Import Below for using TDM
* ngForm 
* ngModel 
* ngModelGroup 


Note: ngModel will be create automatically 

```html
<form (ngSubmit)="save()"> // FormGroup 
 <input [(ngModel)] = "cutomer.firstname" name="firstName" #firstNameVar="ngModel" /> // FormControl, we have user '#' Template reference variable.  
</form>
```

* HTML to TDM 

HTML code
```html
<form>
 <div>
  <label for="name">Name</label>
  <input id="name" required minlenght="3" />
 </div>
 <button type="submit">save</button>
</form>
```
Angular TDM code 
```html
<form novalidate (ngSubmit)="save(checkForm)" #checkForm="ngForm">
 <div>
  <label for="name">Name</label>
  <input id="name" required minlenght="3" 
         [(ngModel)]="customer.name"
         name="name"
         #nameVar="ngModel"
         [ngClass]='{'is-valid': nameVar.touched && !nameVar.valid}'/>

  <span *ngIf="nameVar.errors">
   Please enter your name.
  </span>
 </div>
  <button type="submit">save</button>
</form>
```

```js
...
import { NgForm } from '@angular/forms'; 
...

export class form implments OnInit {
 ngOnInit() {}
 
 save(formData: NgForm) {
  console.log(formData)
  console.log(formData.value)
 }
}
```

#### RDM (ReactiveFormsModule)

- We need to create FormControl, FormGroup and FromModel

*Form Model*
* Root FormGroup (Ex: Form html element)
* FormControl (Ex: input)
* Nested FormGroups 

Import Below for RDM 

* formGroup 
* formControl
* formControlName
* formGroupName
* formArrayName

Note: ngModel willn't be create automatically

* HTML to RDM 

HTML code
```html
<form>
 <div>
  <label for="name">Name</label>
  <input id="name" required minlenght="3" />
 </div>
 <button type="submit">save</button>
</form>
```
Angular RDM code 
```html
<form novalidate (ngSubmit)="save()" [formGroup]="userForm">
 <div>
  <label for="name">Name</label>
  <input id="name"
         formControlName="name"
         [ngClass]='{'is-valid': formError.name}'/>

  <span *ngIf="formError.name">
   {{formError.name}}
  </span>
 </div>
 
 <div>
  <label for="password">Password</label>
  <input id="password"
         formControlName="password"
         [ngClass]='{'is-valid': formError.password}'/>

  <span *ngIf="formError.password">
   {{formError.password}}
  </span>
 </div>
  <button type="submit">save</button>
</form>
```
```js
import { FormGroup, FormControl } from '@angular/forms';


export class login implements OnInit {
 userForm: FormGroup;
 
 ngOnInit(): void {
  this.userForm: new FormGroup({ // Root form Group
   name: new FormControl(),
   password: new FormControl()
  }); // this is called Form Model
 }
 
 save() {
  console.log(this.userForm)
  console.log(this.userForm.value)
 }
}
```

##### Acceessing Form model

```js

// Option 1
userForm.controls.name.valid
// Option 2
userForm.get('name').valie

// Options 3

name = new FormControl();

ngOnInit: void() {
  this.userForm = new FormGroup({
   name: this.name,
.....
  })
}
name.valid
```


Ref: 
* https://angular.io/start/start-forms
* https://github.com/DeborahK/Angular-ReactiveForms
