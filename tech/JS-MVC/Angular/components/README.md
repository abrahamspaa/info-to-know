# Component 

Angular derived by component based architecture. It is import from `import Component from '@angular/core'`. `@Component` is the most important one. Once the component created we need to add this component in app module  or feature modle under declarations.


## How it works 

<img width="731" alt="Screenshot 2022-06-01 at 7 26 31 AM" src="https://user-images.githubusercontent.com/3948750/171312573-621867c7-cf48-405f-b529-3a5bd94ac01f.png">


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

- In built pipes eg {{firstName | lowercase}}
- Custom pipes 



### Class

File will be created in format of '.ts'. In this we will writing the business logic and template support code. Component **Decorator** imported from angular/core 


### Metadata

Meta data is added via `@Component` function 

```js
@Component({
  selector: 'hi-world'
})
```
