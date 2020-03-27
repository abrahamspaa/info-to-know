# RxJs 

Reactive Extension for JS (RxJs) for more declarative and reactive approach. Was developed my microsoft as Rx.Net.

RxJs is a library for composing asyn and event-based programs by using observable sequences.

Collect, Pipe (Transform, filter, Process), Combine, Cache.

## Why RxJS ?

Instead of RxJS we can use below and there corns.

* Callback - But it will be good for nested operations 
* Promises - Cancel promise is not possible 
* Async/Await - Can handle single emission

## Observer 

Which is collect of callbacks which repsoned to it. 

Observer will do below items 

* next()
* error()
* complete()

```js 
const observable = {
  next: a => a,
  error: a => a,
  complete: a => a
}
```

### Observer streams 

Any stream of data produced over time like Numbers, Strings, Events, Object Literals and HTTP Request

```js 
const streams = new Observable (a => {
  a.next('data 1');
  a.next('data 2');
  a.complete()
})
```

## Subscription

Call the Observers. Collection of Observers

```js 
const observable = {
  next: a => a,
  error: a => a,
  complete: a => a
}

const streams = new Observable (a => {
  a.next();
  a.next();
  a.complete()
});

const subsription = streams.subscribe(observable);

```
## un subscription

```js

const subsription = streams.subscribe(observable);
subsription.unsubscribe
```

## of/from Observable 

Create observable function, follow below

```js 
import { of, from } from 'rxjs';

const streams = of ('data1', 'data2');  // Output will be [data1, data2]

const streams = from(['data1', 'data2']); // Output will be data1, data2
```


## RxJS Operators

An operators is a function which transform and manipulate items in a Observable. We use Pipe method.

```js
of(2, 4, 6)
  .pipe(
    map(i => i * 2 ),
    tap(i => console.log(i)),
    take(2)
  )
  .subcribe(console.log)
```

### Async Pipe

```js
names: Names[] = [];

constructor(private nameService: AuthService) {}

ngOnInit() {
  this.nameSubcribe = this.nameService.getNames().subscribe(names => this.names = names)
}

ngOnDestroy(): void {
  this.nameSubcribe.unsubscribe();
}
```

```html
<div *ngIf="names">
  <ul *ngFor="let name of names">
     <li>{{ name.id }}</li>
  </ul>
</div>

```
With Async Pipe
```


names$: Observable<Names[]>;

constructor(private nameService: AuthService) {}

ngOnInit() {
  this.names$ = this.nameService.getNames();
}
```

```html
<div *ngIf="names$ | async as names">
  <ul *ngFor="let name of names">
     <li>{{ name.id }}</li>
  </ul>
</div>

```
### catchError

```js
import { EMPTY } from 'rxjs';

this.http.get<Name[]>(url).pipe(catchError(this.handleError));

handleError(){
  return EMPTY;
}

```

## Combaining Streams 

* combaineLatest 
* forkJoin
* withLastestFrom


## Data Streams and Action Streams 

Data Streams 

```js
names$ = this.http.get<Names[]>(url)
```

Action Streams 

* Use built-in streams 
* fromEvent
* Subject/Behaviour Subject (Common way)
  - Observable is unicast and Subject Multicast
  - Behaviour Subject will have default value. 

Step in actions 

* Create Subject or BehaviourSubject
* Combined action and data Streams 
* Emit the value to actions `this.<actionName>.next(+<value>)`


## Caching value

*sharedReply(1)* will cache the value

## High-order Observable/ map

A observable emits an observable is called High-order Observable

Check below 
* concatMap 
* mergeMap
* switchMap

## Side loading 
* need to do manually 

```js 
selectedNames$ = this.selectedNames$
  .pipe(
    filter(selectedName => Boolean(selectedName)),
    mergeMap(selectedName => 
      from(selectedName.companyId)
        .pipe(
          mergeMap(companyId => this.http.get<Company>(`${url}/${companyId}`)),
          toArray()
        )
      )
    )

```



Ref:

* https://rxjs.dev/
* https://rxmarbles.com/
* https://github.com/DeborahK/Angular-RxJS/tree/master/APM-Final
