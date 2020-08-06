`split()` 方法使用指定的分隔符字符串将一个[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)对象分割成子字符串**数组**，以一个指定的分割字串来决定每个拆分的位置

```js
const str = 'The quick brown fox jumps over the lazy dog.';

const words = str.split(' ');
console.log(words[3]);
console.log(words);
// expected output: "fox"
// Array ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog."]

const chars = str.split('');
console.log(chars);
console.log(chars[8]);
// expected output: "k"
// ["T", "h", "e", " ", "q", "u", "i", "c", "k", " ", "b", "r", "o", "w", "n", " ", "f", "o", "x", " ", "j", "u", "m", "p", "s", " ", "o", "v", "e", "r", " ", "t", "h", "e", " ", "l", "a", "z", "y", " ", "d", "o", "g", "."] > "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
// ["The quick brown fox jumps over the lazy dog."]

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzA1Mjc1OTgwXX0=
-->