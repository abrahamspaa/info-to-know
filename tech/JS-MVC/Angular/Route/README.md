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
