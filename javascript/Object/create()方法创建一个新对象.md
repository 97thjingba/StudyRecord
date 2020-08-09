`Object.create()`方法创建一个新对象，使用现有的对象来提供新创建的对象的__proto__

```js
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // inherited properties can be overwritten

me.printIntroduction();
// expected output: "My name is Matthew. Am I human? true"
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMTExMjY0MTNdfQ==
-->