**copyWithin()** 方法浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度

```js
const array1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(array1.copyWithin(0, 3, 4));
// Array ["d", "b", "c", "d", "e", "f", "g"]

const array2 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(array2.copyWithin(1, 3, 5));
// Array ["a", "d", "e", "d", "e", "f", "g"]

const array3 = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];
console.log(array3.copyWithin(1, 3));
// Array ["a", "d", "e", "f", "g", "f", "g"]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyNTU2NTA5MiwtNDA0Nzk3NTY0LC03Mz
k1MjYwMCwtMjA4ODc0NjYxMl19
-->