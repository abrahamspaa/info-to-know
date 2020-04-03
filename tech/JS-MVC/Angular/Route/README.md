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

## Pre-fetch data 

We can feed data to the route by below 

* Route Parameters (/names/:id)
* Options Parameters 
* Query Parameters 
* Route Data Property ({ path: '/names', component: NamedisplayComponent, data: { pageTitle: 'Names' }})
* Route Resolver 
* Angular Service 

Route Resolver Example, it will be like a service 
```js
import { Observable } from 'rxjs';
import { Injectable } from '@angular/core';
import { Resolver, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';

import { Name } from './name';
import { NameService } from './name.service';

@Injectable({
  providedIn: 'root'
})

export class NameResolver implements Resolver <Name> {
  contructor (private: nameService: NameService) {}

  resolve(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<Name> {
    const id = Number(route.paramMap.get('id'));

    if (!id) {
      return null; // of({ name: null, error: { message: 'no id passed' } })
    }
    
    
    return this.nameService.getNameList(id);
    
  } 
}

// module.ts

{ path : 'name/:id/edit', component: name, resolve: { resolvedData: NameResolver }}

// NameEditCompoenent

import { ActivatedRoute } from '@angular/core';

contructor (private: route: ActivatedRoute) {
  this.nameList = this.route.snapshot.data['resolvedData'];
}
```

need to change when every data updated then follow below instead of above code 

```js 
// NameEditComponent 
contructor (private: route: ActivatedRoute) {}

ngOnInit(): void {
 this.route.data.subscribe( data => {
   const resovledData = data['resolvedData'];
 })
}
```

## Child Route 

```js 
(app or feature).module.ts 

{
  path: 'name/:id',
  component: NameDetail, 
  childern: [
    { path: 'address', component: AddressDetail }
  ]
}
  ]
}
```

```html 

<div>
  <h1>Primay Heading</h1>
  
  <router-outlet></router-outlet>
```
Access child route
```html
[routerLink]=['/names', name.id, 'edit', 'address']
or
[routerLink]=['address'] // in the feature module
```
```js
this.route.navigate(['/names', this.name.id, 'edit', 'address'])
// or 
this.route.navigate(['address', { relativeTo: this.route/*(activatedRoute)*/ }])
```

To resolve data in parent route for child 

```js 
this.route.parent.snapshot.data['name']

// or 

this.route.parent.data.subscribe( data => {
// logic data
})
```
## Component-less route 
```js
{
  path: 'names'
  childern: [
    { path: '', component: NameListCOmponent},
    { path: ':id', component: IDComponent },
    { path: ':id/address', }
  ]
}
```

## Animation

To highlight the active route link 
```html
  [routeLink]="['names']" routerLinkActive="className"
```
how to do animation 

* import BrowserAnimationModule
```js
// app.module.ts

import { BrowserAnimationModule } from '@angular/platform-browser/animations';

imports: [
  BrowserAnimationModule
]
```
* Define the animation
```js
// put it in a common place 
```
* Register the animation in a component 
```js
// app.component.js
import { slideInAnimation } from '<new path>'
@Component({
  animation: [slideInAnimation]
})
```
```html
<div [@slideInAnimation]="o.isActivated ? 0.activatedRoute : ''">
  <router-outlet #o="outlet"></router-outlet>
</div>
```
* trigger it 


## Loading 

```
// app.component

import { Router, Event, NavigationStart, NavigationEnd, NavigationError, NavigationCancel } from '@angular/router';

loading = true;
constructor (private router: Router) {
  router.events.subscribe((routerEvent: Event) => {
    if(routerEvent instanceof NavigationStart) {
      this.loading = true;
    }
    
    if (routerEvent instanceof NavigationEnd || routerEvent instanceof NavigationError || routerEvent instanceof NavigationCancel) {
      this.loading = false;
    }
  })
}

```

```html 
  class="loading" *ngIf="loading"
```

## Lazy loading 

How it works ?

* App loads
* Download imported modules (Waits)
* Template Appears 
* when navigated to lazy loading route 
* Download features (Waits)
* Templated loaded

when we make it?
* If it is feature module 
* Routes grouped under single parent 
* Not Imported in any other module 

How to make it

* Just add your code in below formate only 
* if you already added in app.module remove it

```js
// route.app
Router.forRoot([
  {
    path: 'names',
    loadChildren: () => import('./names/name.module').then(m => m.NameModule)
  }
])

// name.module

Router.forRoot([
  {
    path: '',
    component: NameDetails
  }
])
```

Use canLoad for asyn modules loading. To avoid unwanted showing for html elements


## Preloading 

How it is works 

* App loads
* Download imported modules (Waits)
* Template Appears 
* Preload Modules 
* when navigated to lazy loading route 
* Templated loaded

Type of preload 

* no preload (default)
* Preload all (canLoad will not work)
```js
// app-routing.module.ts

import { RouterModule, PreloadAllModules } from '@angular/router';

RouterModule.forRoot([
  { 
    path: '',
    loadChildren: () => impor('').then(module => module.name)
  }
], { preloadingStrategy: PreloadAllModules})
```
* Custom preload 
```js
// Custom Service 
import { Observable, of } from 'rxjs' ;
import { Injectable } from '@angular/core';
import { PreloadingStrategy } from '@angular/router';

@Injectable({
  providedIn: 'root'
});

export class Custom implements PreloadingStrategy {
  preload(route: Route, load: Function): Observable <any> {
    return route.data && route.data['preload'] ? load() : of(null);
  }
}
// app-routing.module.ts

import { Custom } from // Custom Service path;

RouterModule.forRoot([
  { 
    path: '',
    loadChildren: () => impor('').then(module => module.name),
    data: {
      preload: true 
    }
  }
], { preloadingStrategy: Custom })

```



