## 创建对象的不同方法解析

下面讲解三种常见的创建对象方法。

## 对象字面量

比如：

```
var Person = {
    name: 'jessica',
    age: 27
}
```

这种形式就是对象字面量，通过对象字面量构造出的对象，其__proto__指向Object.prototype。  
所以，其实Object是一个函数也不难理解了。Object、Function都是是js自带的函数对象。  
可以跑下面的代码看看：

```
console.log(typeof Object); 
console.log(typeof Function);
```

## 构造函数

就如我前面讲的，形如：

```
function Person(){}
var person1 = new Person();
```

这种形式创建对象的方式就是通过构造函数创建对象，这里的构造函数是Person函数。上面也讲过了，通过构造函数创建的对象，其__proto指向的是构造函数的prototype属性指向的对象。

## Object.create

```
var person1 = {
    name: 'jessica',
    age: 27
}
var person2 = Object.create(person1);
```

这种情况下，person2的__proto__指向person1。在没有Object.create函数的时候，人们大多是这样做的：

```
Object.create = function(p) {
    function f(){};
    f.prototype = p;
    return new f();
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NTQwODE3MDZdfQ==
-->