

```js
const iterator1 = array1.entries();
console.log(iterator1);
> Object { }

console.log(iterator1.next().value);
// expected output: Array [0, "a"]
// Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]
//> Array [1, "b"]

console.log(iterator1.next().value);
// > Array [2, "c"]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwMTUwNzAwXX0=
-->