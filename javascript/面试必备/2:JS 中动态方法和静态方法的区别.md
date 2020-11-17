1.  静态方法：在构造函数本身上定义的方法，只能通过构造函数本身调用，new出来的对象不能够调用。  
    实例代码：

```js
      //创建构造函数f1
       function f1(){}

       //静态方法
       f1.static = function(){
           console.log("我是一个静态方法");
       }
       f1.static();        //  我是一个静态方法

```

2.  动态方法：也叫做实例方法，它是通过prototype原型对象添加的，所有的实例对象都能够继承调用。通过先定义一个引用变量，指向构造函数定义的新对象，数对象中的属性 prototype可以想成一个指针，指向一个方法。  
    实例代码：

```js
       //创建构造函数f2
        function f2(){}

        //动态方法
        f2.prototype.instance = function(){
            console.log("我是一个动态方法");
        }
        //创建构造函数f2的实例对象
        var a = new f2();
        a.instance();       //  我是一个动态方法
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3MzcwMTMyMF19
-->