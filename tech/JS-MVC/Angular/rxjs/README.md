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





Ref:

https://rxjs-dev.firebaseapp.com/guide/overview
