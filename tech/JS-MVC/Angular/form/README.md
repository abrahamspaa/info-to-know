
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

### Form builder 

* provide as service 
* shorten boilerpalte
* Create form model

Step to create form builder 

Step 1
```js 
import { FormBuilder } from '@angular/forms';
```

Step 2 
```js
constructor(private fb:FormBuilder) { }
```
Step 3
```js
ngOnInit(): void {
 this.userForm = this.fb.group({
  name: null,
  password: null
 })
}
```

### Validation 

```js

this.userForm = this.fb.group({
 name:['default Value', ['validator rules'], 'Async validator']
});
```
Validate over run time
```js 
// Single Validator 

userForm.get('name').setValidator(Validators.required);

// Multi
userForm.get('name').setValidator([Validators.required, Validators.maxLength(4)]);

// Clear
userForm.get('name').clearValidators();

// Update
userForm.get('name').updateValueAndValidity();
```

#### Custom Validation

```js
// single params 
import { AbstractControl } from '@angular/forms';

function <name>(c: AbstractControl): {[key: string]: boolean} | null {
 if(c.value) {
  return {
   <name>: true
  }
  
  return null;
 }

}

// Multi params 

import { AbstractControl, validatorFn } from '@angular/forms';

function <name>(value: string, value1: string) : validatorFn {
 return (c: AbstractControl): {[key: string]: boolean} | null => {
  if(c.value) {
   return {
    <name>: true
   }

   return null;
  }

 }
}
```
#### Cross field Validation

```html
<div formGroupName="parent">
 <input formControlName="child1" />
 <input formControlName="child2" />
</div>
```

```js

import { AbstractControl } from '@angular/forms';

function <name>(c: AbstractControl): {[key: string]: boolean} | null {
 if(c.get('child1').value === c.get('child2').value) {
  return {
   <name>: true
  }
  
  return null;
 }

}

this.userForm = this.fb.group({
 parent: this.fb.group({
  child1: ['', Validators.required],
  child1: ['', Validators.required]
 })
}, { validator: compare})
```

#### Watch and React

```js
this.userForm.get('name').valueChanges.subscribe(
 value => value
)
```

#### Reactive Transformation 

Before
```html
<input formControlName="name"
       [ngClass] = "{ 'is-valid': userForm.get('name').errors ||
                     (userForm.get('name').touched || 
                     userForm.get('name').dirty) && 
                     !userForm.get('name').maxLength) }">

<span *ngIf="userForm.get('name').errors?.required">
 Name must be filled
</span>

<span *ngIf="userForm.get('name').errors?.maxLength">
 Name must max length
</span>
```
After

```js
import { debounceTime } from 'rxjs/operators';
import { AbstractControl } from '@angular/forms';
....
nameMessage: string;

private validationMessage = {
 required: 'Name must be filled',
 maxLength: 'Name must max length'
};

ngOnInit() {
 this.userForm = this.fb.group({
  name: ['', [Validators.required, Validators.maxLength(20)]]
 });
 
 const nameControl =  this.userForm.get('name');
  nameControl.valueChanges
  .pipe(
   debounceTime(1000)
  )
  .subscribe(
   value => this.showError(nameControl)
  )
}

showError(c:AbstractControl): void {
 this.nameMessage = '';
 
 if((c.touched || c.dirty) && c.errors) {
  this.nameMessage = Object.keys(c.errors).map(
   key => this.validationMessage([key]).join(' ');
  )
 }
}

```

```html
<input formControlName="name"
       [ngClass] = "{ 'is-valid': nameMessage}">

{{ nameMessage }}
```

### CRUD 

* use Data Access Layer 
 * Sepration of Concerns
 * Reusablity
 * Data Sharing
 
* Steps to make HTTP calls 

 * Import Http client Module
   ```js
   // app.module.ts

   import { HttpClientModule } from '@angular/common/http';
   ...
   imports: [
    HttpClientModule
   ]
   ```
   
 * Mock Server 
  * use angular-in-memory-web-api
    * yarn -D angular-in-memory-web-api
    * import to app.module or place you want 
      ```js
       // app.module.ts
       import { InMemoryWebApiModule } from 'angular-in-memory-web-api';
       import namd from './name.data.ts'
       ...
       imports: [
        InMemoryWebApiModule.forRoot(name)
       ]
       
       // name.data.ts
       
       import { InMemoryDbService } from 'angular-in-memory-web-api';
       
       export class NameData implements InMemoryDbService {
        createDb() {
         const names = [{
          id: 0,
          ...
         }, {
          id: 1,
          ...
         }]
        }
       }
      ```
 
 * Create Service layer
   ```js
   // NameService
   import { HttpClient, HttpHeaders } from '@angular/common/http';
   import { Observable, of, throwError } from 'rxjs';
   import { catchError, tap, map } from 'rxjs/operators';
   ...
   constructor(private http: HttpClient) {}
   
   getNames(id: number): Observable<> {
    const url = `www.myservice.com/api/name/${id}`
    
    return this.http.get<Name>(url)
     .pipe(
      tap(data => console.log(data)),
      catchError(error => console.error(error))
     );
   } 
   ```
 * Use in names 
  ```js
   contructor(private nameService: NameService)
   getNames(id:number): void {
    this.productService.getNames(id)
     .subcribe({
      next: (name) => this.displayName(name),
      error: err => this.errorMessage = err
     })
   }
  ```
  






Ref: 
* https://angular.io/start/start-forms
* https://github.com/DeborahK/Angular-ReactiveForms
