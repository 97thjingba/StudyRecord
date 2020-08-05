**`values()`**  方法返回一个新的  **`Array Iterator`**  对象，该对象包含数组每个索引的值

```js
const array1 = ['a', 'b', 'c'];
const iterator = array1.values();

for (const value of iterator) {
  console.log(value);
}

// expected output: "a"
// expected output: "b"
// expected output: "c"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE1NTMyOTkxXX0=
-->