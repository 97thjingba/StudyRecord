es6: 

```js
class Math {
    // 构造函数
    constructor(x,y) {
        this.x = x;
        this.y = y;
    }
    add() {
        return this.x + this.y;
    }
}
let math = new Math(1,2);
console.log(math.add());
```

es5: 

```js
// 一个数学计算的方法
function Math(x, y) {
    this.x = x;
    this.y = y;
}

// 在原型中添加 add方法， 其作用是返回两个数的和
Math.prototype.add = function() {
    return this.x + this.y;
}

var math = new Math(1,2);
console.log(math.add())
```

本质： es6的class真正的本质只是一个语法糖
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MzU1NDQ5NDNdfQ==
-->