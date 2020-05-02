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

导航栏和状态栏
----------

![状态栏与导航栏](https://user-gold-cdn.xitu.io/2019/4/4/169e65bb7831f958?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1MTMxOTI1LC0xMDIxNTMyNDE4XX0=
-->