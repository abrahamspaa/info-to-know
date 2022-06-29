# Angular Routing

## How is works 
<img width="991" alt="Screenshot 2022-06-28 at 9 36 25 PM" src="https://user-images.githubusercontent.com/3948750/176227590-c6f35308-7ee8-40dc-b25c-69a134c5c5aa.png">


## RouterModule 
We need import RouterModule below to access routes

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

## Feature module or small module

Pros 

* Seperate code 
* Lazying loading 

How to do? 

* Import Route (app.module)
* Config route (feature.module)
* activate the routes (this.route.navigateByUrl('/name'))

## Data access
Ways of accessing data inside the component or modules 

### Route Parameter 
1. Update path in module 
```js
{ path: '/names/:id', component: NameDetailComponent }
```
2. Add navigation 
```html
<a [routerLink]=['/names', this.id]>
```
or
```js
this.router.navigate(['/names', this.id])
```
3. Access data or value in component
```js 
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { }

// Using snapshot 

this.route.snapshot.paramMap.get('id');

// Using Observable

this.route.paramMap.subscribe(
  params => {
    const id = params.get('id');
    
    ///
  }
)
```
4. URL will be `/names/1`

### Optional Params 
1. Update path in module 
```js
{ path: '/names', component: NameDetailComponent }
```
2. Add navigation 
```html
<a [routerLink] = ['/names', { name: name}]> Back </a>
```
or
```js
this.router.navigate(['/names', { name: names}])
```
3. Access data or value in component
```js
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { 
  this.route.snapshot.paramMap.get('name') // Paul
}
```
4. URL will be `/names;name=Paul`

### Query params 

1. Update path in module 
```js
{ path: '/names', component: NameDetailComponent }
```
2. Add navigation 
```html
<a [routerLink] = ['/names'] [queryParams] = "{ name: 'Paul'}"> Back </a>
```
or 
```ts
this.router.navigation(['names'], {
  name: 'Paul'
})
```
3. Access data or value in component
```js
import { ActivatedRoute } from '@angular/router';

constructor(private route:ActivatedRoute) { 
  this.route.snapshot.queryParamMap.get('name') // Paul
}
```
4. URL will be `/names?name=Paul`
5. To retain the Query params 
```html
<a [routerLink] = ['/names'] [queryParams] = "{ name: 'Paul'}" queryParamsHandling='preserve'> Back </a>
```
or 
```ts
this.route.navigate(['names'], { queryParamsHandling: 'preserve' });
```

### Route Data Property 
```ts
// module.ts
({ path: '/names', component: NamedisplayComponent, data: { pageTitle: 'Names' }})
```
### Route Resolver
Route resolver is a service, which will await till the data resolved then only View will render.
1. Create resolver 
```cmd
ng generate resolver <folder-name>/<resolve-name>
```

2. Build service 
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
```

3. Add resolve to the config 
```js
// module.ts

{ path : 'name/:id/edit', component: name, resolve: { resolvedData: NameResolver }}
```

4. Access the data in component
```js
// NameEditCompoenent

import { ActivatedRoute } from '@angular/core';

contructor (private: route: ActivatedRoute) {
  this.nameList = this.route.snapshot.data['resolvedData'];
}
```
 or 
```js 
// NameEditComponent 
contructor (private: route: ActivatedRoute) {}

ngOnInit(): void {
 this.route.data.subscribe( data => {
   const resovledData = data['resolvedData'];
 })
}
```
### Angular Service 

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

1. import BrowserAnimationModule
```js
// app.module.ts

import { BrowserAnimationModule } from '@angular/platform-browser/animations';

imports: [
  BrowserAnimationModule
]
```
2. Create needed animation
```js
// put the needed animation in a new common file 
```
3. Register the animation in a component 
```js
// app.component.js
import { slideInAnimation } from '<new path to create>'
@Component({
  animation: [slideInAnimation]
})
```
```html
<div [@slideInAnimation]="o.isActivated ? 0.activatedRoute : ''">
  <router-outlet #o="outlet"></router-outlet>
</div>
```
4. trigger the animation in the route-outlet 


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

## Secondary routes

1. Added outlet in app.html
```html
app.html

<router-outlet name="chat-bot"></router-outlet>
```
2. Mention route in router

```ts
// module.ts

RouterModule.forChild[{
  path: 'chat',
  component: NameList,
  outlet: 'chat-bot'
}]
```
3. Mention the code for navigation 
```ts
<a [routerLink]="[{ outlets: { popup: ['message']}}]">
```

4. to close the router
```ts
<a [routerLink]="[{ outlets: { popup: null }}]">
```

## Guards

This will validate or guards the route before/after. Route guards is build as a services. 

Type of Guards
- canActivate (Navigate into the route)
- canActivateChild (Navigate into the child route)
- canDeactivate (Navigate way from the route)
- canLoad (Prevent async loading)
- resolve (prefetch the data)

How Guards work?
<img width="951" alt="Screenshot 2022-06-29 at 7 51 53 PM" src="https://user-images.githubusercontent.com/3948750/176460325-f9dd36c9-087d-49ad-9584-8e6d0b761f1e.png">

if any guards return false, all pending guards will be cancelled.

How to create a Guards?

1. Create a Guards service `ng generate guard <folder-name>/<file-name>`
2. 

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

Ref: https://github.com/DeborahK/Angular-Routing

