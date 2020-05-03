# Array 

## Modified array Object 

```js
Array.from([1,2,3], number => ({id: number})) // [{ id: 1, id: 2, id: 3}]
```

## Common value between two arrays 

```js
[1,2,3].filter(x => [3,4].includes(x)) // [3]
```
## Merge Array 
```js 
var arrA = [12,3,4], arrB = [4,5,6];
[...arrA, ...arrB] // [12, 3, 4, 4, 5, 6]
```

## Common Merge Array 
```js 
var arrA = [12,3,4], arrB = [4,5,6];
[...new Set([...arrA, ...arrB])] // [12, 3, 4, 5, 6]
```
