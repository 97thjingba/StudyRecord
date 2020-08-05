`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素

```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```


```js
var newArray = arr.filter(callback(element[, index[, array]])[, thisArg])
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4ODQ1NDU5OV19
-->