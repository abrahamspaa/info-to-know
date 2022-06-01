# Component 

Angular derived by component based architecture. It is import from `import Component from '@angular/core'`. `@Component` is the most important one. Once the component created we need to add this component in app module  or feature modle under declarations.


## How it works 

<img width="731" alt="Screenshot 2022-06-01 at 7 26 31 AM" src="https://user-images.githubusercontent.com/3948750/171312573-621867c7-cf48-405f-b529-3a5bd94ac01f.png">


### Template

File will be created in format of '.html'. In this we will writing the HTML code, binding, interpolation, etc. 

#### one way Binding

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


### Class

File will be created in format of '.ts'. In this we will writing the business logic and template support code. Component **Decorator** imported from angular/core 


### Metadata

Meta data is added via `@Component` function 

```js
@Component({
  selector: 'hi-world'
})
```
