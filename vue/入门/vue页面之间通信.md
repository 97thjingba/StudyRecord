前言：在vue中页面通讯有vuex,localStorage，bus等方法，个人认为如果项目不是很大，状态管理也没有很复杂的话，使用 Vuex 有种杀鸡用牛刀的感觉；localStorage这个方法的取来取去感觉又很烦；所以可以使用bus；

1.而bus则是使用  `$emit`，`$on`，`$off`分别来分发、监听、取消监听事件

![](https://pic4.zhimg.com/80/v2-6de655ccd9725fe4278c647399c737b3_720w.jpg)

![](https://pic3.zhimg.com/80/v2-a34d7d7607bc115a9df9cfeb47ff53a6_720w.jpg)

![](https://pic3.zhimg.com/80/v2-c644ad6e0d9b3eaa907858876e5372b6_720w.jpg)

2.配置以及使用

2.1 在项目中创建bus文件

![](https://pic3.zhimg.com/80/v2-2d019c86dd3d302cbeb036e62d327bee_720w.jpg)

2.2 在需要的文件中引入

挂载 销毁

![](https://pic3.zhimg.com/80/v2-229e3cd61ba8bf4dc4828ba1cedb3e66_720w.jpg)

监听

![](https://pic1.zhimg.com/80/v2-134f1d7bbe36bb6de7da76e7ee99136c_720w.jpg)

参考： https://zhuanlan.zhihu.com/p/264635209


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0NjA3MjI5MiwxODc5NzgwMzYwXX0=
-->