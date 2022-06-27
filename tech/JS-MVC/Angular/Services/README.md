## What is Services?
- Focused on particular task 
- Can be focused in global or root injector, and component and its child component injector

## How to create Service?

```cmd
ng generate service modulesName/serviceName
or 
ng generate service serviceName // To create under app.modules 
```

1. Below file will be created for root injector

```ts 
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class NameService {
  constructor() { }
}
```

2. Below file will be created for component injector

```ts 
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class NameService {
  constructor() { }
}
```

```ts 
import { Component } from '@angular/core';

@Component({
  providers: [NameService]
});

export class NameComponent {}
```

## How to access service?

```ts
import { Component } from '@angular/core';

import { NameService } from './name';

@Component({
  selector: 'app-child',
  template: `
    <h3>{{hero.name}} says:</h3>
    <p>I, {{hero.name}}, am at your service, {{masterName}}.</p>
  `
})
export class ChildComponent implements OnInit {
  constructor(private nameService: NameService) {  }
  
  ngOnInit() {
    this.nameService.getNames();
  }
}
```

## How to access HTTP in service?

```ts
// app.module.ts
import { HttpClientModule } from '@angular/common/http';

@ngModule({
  imports: [HttpClientModule]
});
```

```ts 
import { Observable } from 'rxjs';
import { Injectable } from '@angular/core';
import { catchError, tap } from 'rxjs/operators';
import { HttpClient, HttpErrorResponse } from '@angular/common/http';

@Injectable({
  providedIn: 'root',
})
export class NameService {
  constructor(private http: HttpClient) { }
  
  getNames() : Observable<Names[]> {
    return this.http.get<Names[]>('url').pipe(
      tap( data => data),
      catchError(this.handleError)
    );
  }
  
  private handleError (errors: HttpErrorResponse) {
    if (errors.error instanceof ErrorEvent ) {
      // client error
    } else {
      // server error
      console.log(` Error status: ${errors.status}, ${errors.message} `);
    }
  }
}
```



