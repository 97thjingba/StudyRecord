`**pop()**`方法从数组中删除最后一个元素，并返回该**元素的值**。此方法更改数组的长度。如果数组为空，返回undefined

```js
const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// expected output: "tomato"

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]

plants.pop();

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage"]
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNjI5Njc1NDBdfQ==
-->