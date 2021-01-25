`splice()` 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会**改变原数组**


```js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]

months.splice(1,3)
console.log(months);
// Array ["Jan", "May"]

months.splice(0,1) //相当于删除原有数组的第一项
console.log(months);
//  Array ["May"]


```

### 参数

`start​`

指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数，这意味着-n是倒数第n个元素并且等价于`array.length-n`）；如果负数的绝对值大于数组的长度，则表示开始位置为第0位。

`deleteCount`  可选

整数，表示要移除的数组元素的个数。

如果  `deleteCount`  大于  `start`  之后的元素的总数，则从  `start`  后面的元素都将被删除（含第  `start`  位）。

如果  `deleteCount`  被省略了，或者它的值大于等于`array.length - start`(也就是说，如果它大于或者等于`start`之后的所有元素的数量)，那么`start`之后数组的所有元素都会被删除。

如果  `deleteCount`  是 0 或者负数，则不移除元素。这种情况下，至少应添加一个新元素。

`item1, item2, _..._` 可选

要添加进数组的元素,从`start`  位置开始。如果不指定，则  `splice()`  将只删除数组元素。

### 返回值

由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyNjMwODMwNiwxNTg2NTI1MzMwLC0xMj
A2NjU5MjIyLC0xNzAyODMwNDY4XX0=
-->