###  内置对象

-   Object是JavaScript中所有对象的父对象；
-   数据封装类对象：Object、Array、Boolean、Number、String；
-   其他对象：Function、Arguments、Math、Date、RegExp、Error、JSON、全局对象；

### 定义对象的方式

-   对象字面量: var obj = {};
-   构造函数: var obj = new Object();
-   Object.create(); var obj = Object.create(Object.prototype);

### 通过new的方式和通过字面量的方式创建对象区别

-   通过字面量的方式创建对象，不会调用Object()构造函数，简介并且性能更好；
-   通过new操作符创建对象时，需要调用Object()构造函数，本质上是方法调用，涉及到在__proto__链中遍历该方法，当找到方法后，会产生调用方法必须的堆栈信息，方法结束后，需要释放堆栈，在性能上不如使用字面量的方式创建对象。


**1.所有对象都有__proto__属性。**

**2.只有函数对象才有prototype属性。**

**3.protoype对象默认有两个属性：constructor 和  **proto**。**

**4.实例对象的__proto__指向的是函数的protoype**

**5.函数对象的prototype属性是外部共享的，而__proto__是隐式的。**

**6.函数和Object的__proto__的顶端是null**


![enter image description here](https://image-static.segmentfault.com/226/042/2260424593-5938e36c1fdc4_articlex)


**JavaScript中constructor属性指向创建当前对象的构造函数**。

```
var a = 'zuckjet';
console.log(a.constructor)  // ƒ String() { [native code] }

function b() {}
console.log(b.constructor)  // ƒ Function() { [native code] }

var c = {name: 'zuckjet'};
console.log(c.constructor);  //ƒ Object() { [native code] }

```

## 起源

看了上面的代码示例，也许你会觉得constructor属性在对象里，但其实constructor属性是在原型里。

```
function test() {}
var obj = new test();
console.log(obj.hasOwnProperty('constructor')); //false
console.log(obj.__proto__.hasOwnProperty('constructor')); //true
```

hasOwnProperty方法是来判定对象是否包含指定名称的属性，不会向原型链搜索。要想搜索原型链可以用in关键字（’constructor’ in obj）。

既然是constructor属性时从属于构造函数的prototype,那么为什么实例也有constructor属性呢？

```
function Foo() {}
var foo = new Foo()
foo.constructor === Foo // true，这是为什么
```

原因如下：

-   Foo.prototype本身还是实例foo的原型。
-   由于原型链机制，当在foo中查找属性constructor时，如果没有找到，则往原型上找。而Foo.prototype刚好有属性constructor。
-   foo.constructor的值就是Foo.prototype.constructor的值，也就是Foo。

## constructor属性是不可靠的

```
function Foo() {}
Foo.prototype = {}
var foo = new Foo()
foo.constructor === Object  // true，可以看出不是Foo了
```

-   foo没有constructor属性，还是往原型Foo.prototype上找
-   Foo.prototype本来是有constructor属性的，但是在这里它已经被重新定义变成{}
-   找不到constructor，接着往原型链上查找。（{}是由Object构造函数生成的，它的原型是Object.prototype）找到了Object.prototype，含有属性constructor，值为Object

## 用处

为了将实例的构造器的原型对象暴露出来, 比如你写了一个插件,别人得到的都是你实例化后的对象, 如果别人想扩展下对象,就可以用 instance.constructor.prototype 去修改或扩展原型对象
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1NjM0OTY2Nl19
-->