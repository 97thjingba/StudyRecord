


In iOS devices,  `screenHeight === windowHeight`; in Android devices with bottom navigator bar,  `screen height === windowHeight + statusBarHeight + bottomNavigatorBarHeight`; in Android devices without bottom navigator bar, bottomNavigatorBarHeight is zero.

```
import {Dimensions, StatusBar} from 'react-native'; 

const DEVICE_HEIGHT = Dimensions.get('screen').height;
const STATUS_BAR = StatusBar.statusBarHeight || 24; 
const WINDOW_HEIGHT = Dimensions.get('window').height;


```

[![enter image description here](https://i.stack.imgur.com/LSyW5.png)](https://i.stack.imgur.com/LSyW5.png)


参考：
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwNzQzMjk4M119
-->