**`slice()`**  方法提取某个字符串的一部分，并返回一个新的字符串，且不会改动原字符串 

same as array.slice();

**左开右闭**

```js
const str = 'The quick brown fox jumps over the lazy dog.';

console.log(str.slice(31));
// expected output: "the lazy dog."

console.log(str.slice(4, 19));
// expected output: "quick brown fox"

console.log(str.slice(-4));
// expected output: "dog."

console.log(str.slice(-9, -5));
// expected output: "lazy"

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM1NjM4NDkwNiwtODc0ODY4NzhdfQ==
-->