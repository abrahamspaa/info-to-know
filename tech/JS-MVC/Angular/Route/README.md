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


