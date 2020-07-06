安卓和ios的全局screen的区别
In iOS devices,  `screenHeight === windowHeight`; in Android devices with bottom navigator bar,  `screen height === windowHeight + statusBarHeight + bottomNavigatorBarHeight`; in Android devices without bottom navigator bar, bottomNavigatorBarHeight is zero.
```js
import {Dimensions, StatusBar} from 'react-native'; 
const DEVICE_HEIGHT = Dimensions.get('screen').height;
const STATUS_BAR = StatusBar.statusBarHeight || 24; 
const WINDOW_HEIGHT = Dimensions.get('window').height;
```
[![enter image description here](https://i.stack.imgur.com/LSyW5.png)](https://i.stack.imgur.com/LSyW5.png)

参考：[https://stackoverflow.com/questions/46126521/android-navigation-bar-height-react-native](https://stackoverflow.com/questions/46126521/android-navigation-bar-height-react-native)

导航栏和状态栏和tabBar
----------

![状态栏与导航栏](https://user-gold-cdn.xitu.io/2019/4/4/169e65bb7831f958?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 
一般情况下.
| iphone型号 | 状态栏 | 导航栏|tabBar
|--|--|--|--|
|非iphoneX|20|44|49|
|iphoneX|44|44|83(49+34)|
对于原生的TabBar，IPhoneX在底部增加了34的所谓的安全区域.不影响HomeBar

TabBar
tabBar是在App荧幕底部出现的栏，提供了在不同的版面之间进行快速切换的途径，tabbar的背景颜色是半透明，可以有调色，tabBar在所有荧幕尺寸都保持一样的高度，并且在键盘出现时会隐藏起来。

### ios手机的一些其他机型尺寸大小等等
[https://www.jianshu.com/p/f9f2425d1960](https://www.jianshu.com/p/f9f2425d1960)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5MzA4ODkxOCwtOTk4MDgwMjIwLDE4Mz
A2ODk4NDYsMTcwODE2NzI1OCwtMTAyMTUzMjQxOF19
-->