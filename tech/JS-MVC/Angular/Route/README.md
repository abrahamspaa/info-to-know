# Angular Routing

## Routing process 
* URL is changed
* Match the path -> if not match re-direct 
* Check the Guards 
* Resolve Data 
* Activiate the component
* Display the template is correct router-outlet

## RouterModule 
When u import RouterModule below will be accessable 

```js
// app.module
import { RouterModule } from '@angular/router';

imports: [
  RouterModule.forRoot([])
]
```

`forRoot` method used only once in the app, `forChild` method for all module

* Serivce (will be used in  RouterModule.forRoot())
* Configuration (will be used in RouterModule.forRoot(), RouterModule.forChild())
* Directives (will be used in RouterModule.forRoot(), RouterModule.forChild())
  * RouterLink 
  * RouterLinkActive
  * RouterOutlet
  
## Hash based url 

```js
// app.module
import { RouterModule } from '@angular/router';

imports: [
  RouterModule.forRoot([
    { path: 'welcome', component: WelcomeComponent }
  ], { useHash: true })
]
```

## Feature module 

Pros 

* Seperate code 
* Lazying loading 

How to do? 

* Import Route (app.module)
* Config route (feature.module)
* activate the routes (this.route.navigateByUrl('/name'))

## Route Parameter 

```js
{ path: '/names/:id', component: NameDetailComponent }
{ path: '/names/:id/edit', component: NameDetailEditComponent }
```

```html
<a [routerLink]=['/names', this.id]>
```
```js
this.router.navigate(['/names', this.id])
```

we can use activated Routes 

```js 
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { }

// using snapshot 

this.route.snapshot.paramMap.get('id');

// Observable

this.route.paramMap.subscribe(
  params => {
    const id = params.get('id');
    
    ///
  }
)
```
### Optional Params 

```html
[routerLink] = ['/names', { name: 'Paul'}]

// /names;name=Paul
```
to get values

```js
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { 
  this.route.snapshot.paramMap.get('name') // Paul
}
```
### Query params 

which can we used both optional Params and Query params


```html
[routerLink] = ['/names'] [queryParams] = "{ name: 'Paul'}"

// /names;name=Paul
```

```js
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { 
  this.route.snapshot.queryParamMap.get('name') // Paul
}
```
