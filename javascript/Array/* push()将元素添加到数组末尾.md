`push()` 方法将一个或多个元素添加到数组的末尾，并返回该数组的新长度

```js
const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');
console.log(count);
// expected output: 4
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens', 'cats', 'dogs');
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows", "chickens", "cats", "dogs"]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1ODA0Nzc2NjddfQ==
-->