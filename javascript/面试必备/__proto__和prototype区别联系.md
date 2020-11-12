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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2MzIyMjI5MF19
-->