# Component 

Angular derived by component based architecture. It is import from `import Component from '@angular/core'`. `@Component` is the most important one. Once the component created we need to add this component in app module  or feature modle under declarations.


## How it works 

<img width="731" alt="Screenshot 2022-06-01 at 7 26 31 AM" src="https://user-images.githubusercontent.com/3948750/171312573-621867c7-cf48-405f-b529-3a5bd94ac01f.png">

### Class

File will be created in format of '.ts'. In this we will writing the business logic and template support code. Component **Decorator** imported from angular/core

#### Interface 

Is a specification to indentifying data

```js
// As type
export interface Product {
  name: string;
}

export class nameComponent {
 products : Product[] = []; 
}

// Feature set 

export interface Product {
  name: string;
}

export class nameComponent implements Product {
  name: 'Product A'
}
```
#### Life cycle hooks 
<img width="616" alt="Screenshot 2022-06-27 at 7 35 09 PM" src="https://user-images.githubusercontent.com/3948750/175960572-4e3fcfd6-d3cb-4177-80fd-310cc3687308.png">

```js
import { Component, OnInit } from '@angular/core';

export class ProductComponent implements OnInit {
  ngOnInit(): void { }
}
```
Tips
- Dont implement `ngOnChanges` and `ngDoCheck` on same component


#### Getter and Setter

```js
import { Component } from '@angular/core';

export class ProductComponent {
  get listOfProduct(): string {
    return <value>;
  }
  set listOfProduct(value: string) {
    return <value>;
  }
}
```

#### @Input

Parent component 
```js
import { Component } from '@angular/core';
@Component({
  selector: 'parent-one',
  template: `<child-one [name]='parentName'> </child-one>`
});
export class ParentComponent { 
  parentName: string = 'Hello World'
}
```

Child component 
```js
import { Component, Input, OnChanges } from '@angular/core';
@Component({
  selector: 'child-one',
  template: `<h1>hello {{childName}}</h1>`
});
export class ChildComponent implements OnChanges { 
  @Input() name: string = 'No text';
  
  ngOnChanges(): void {
    this.childName = this.name;
  }
}
```

#### @Output

Parent component 
```js
import { Component } from '@angular/core';
@Component({
  selector: 'parent-one',
  template: `<child-one [name]='parentName' (buttonClick)='childValue($event)'></child-one>`
});
export class ParentComponent { 
  parentName: string = 'Hello World'
  childValue(message:string) : void {
    console.log(message) // Button clicked
  }
}
```

Child component 
```js
import { Component, Input, Output, OnChanges } from '@angular/core';
@Component({
  selector: 'child-one',
  template: `<h1>hello {{childName}}</h1><button (click)='onClick()'>Count</button>`
});
export class ChildComponent implements OnChanges { 
  @Input() name: string = 'No text';
  @Output() buttonClick: EventEmitter<string> = new EventEmitter<string>();
  
  ngOnChanges(): void {
    this.childName = this.name;
  }
  
  onClick(): void {
    this.buttonClick.emit('Button clicked')
  }
}
```

### Template

File will be created in format of '.html'. In this we will writing the HTML code, binding, interpolation, etc. 

#### One way Binding

##### Interpolation

Here title is the one way binding
```js
@Component({
  selector: 'hi-world',
  template: `<h1>Hello {{title}}</h1>`
})

export class HelloComponent {
 title: string = 'world'
}
```
or 

```html
<!-- hi-world.html-->
<h1>Hello {{title}}</h1>
```
```js
@Component({
  selector: 'hi-world',
  templateUrl: './hi-world.html'
})

export class HelloComponent {
 title: string = 'world'
}
```

##### Property Binding 

```js
@Component({
  selector: 'hi-world',
  templateUrl: './hi-world.html'
})

export class HelloComponent {
 carsWidth: string = '10px';
 carsHeight: string = '10px';
}

```
```html
<div [style.width]='carsWidth' [style.height]='carsHeight'> Hello</div>
```

```
ng generate directive <directive-name>
```

#### Two way Binding

This ngModel directive, which is coming from FormModules -> @angular/forms, this need to imports in modules 
```js
@Component({
  selector: 'hi-world',
  templateUrl: './hi-world.html'
})

export class HelloComponent {
 firstName: string = 'Paul';
}

```
```html
<input [ngModel]='firstName' />
```

#### Event Binding
```js
@Component({
  selector: 'hi-world',
  templateUrl: './hi-world.html'
})

export class HelloComponent {
  changeValue(): void {
    console.log('hello');
  }
}

```
```html
<div (click)='changeValue()' > Hello</div>
```

#### Directives

Custom HTML element or attribute which used to power up the application.

Type of Directives 
- Built-in directives 
  - (*ngIf, *ngFor) which is coming from BrowserModule -> @angular/platform-browser, this need to imports in modules 
- Custom directives 

#### Pipes 
Change or transforms data and display in HTML 

- In built pipes eg {{price | currency :'USD' | lowercase | }}
- Custom pipes 

##### Custom pipe 

- `ng generate pipe <name>`
- File will be created 
- This file path will be / need to be added into declaration in the module

```js
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'name'
})
 
export class NamePipe implements PipeTransform {
 transform(value: string, args: string): string { // args will have '-'
  return value;
 }
}
```
```hbs 
{{firstName | name: '-'}}
```

### Metadata

Meta data is added via `@Component` function 

```js
@Component({
  selector: 'hi-world'
})
```

