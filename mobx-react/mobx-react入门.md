
HomeStore 类
```js
import { observable} from "mobx";
class HomeStore {
  @observable homeNum = 0;
}
export default HomeStore;
```

oneStore 类
```js
import { observable} from "mobx";
class OneStore {
  @observable oneNum = 3333;
}
export default OneStore;
```

将两个类合并到Store类里
```js
import HomeStore from "./homeStore";
import OneStore from "./oneStore";
let oneStore = new OneStore();
let homeStore = new HomeStore();
const stores = {
  oneStore,
  homeStore
};
/// 默认导出接口
export default stores;
```

App.js
```js
import React from "react";
import { Provider } from "mobx-react";
import stores from "./store";
ReactDOM.render(
  <Provider {...stores}>
    <Router />
  </Provider>,
  document.getElementById("root")
);
```

```js
import React, { Component } from "react";
+ import { observer, inject } from "mobx-react";
+ @inject("homeStore")
+ @observer
class Home extends Component {
  constructor(props) {
    super(props);
    this.state = {};
  }
  render() {
    return (
    );
  }
}
export default Home;
```
#####  observer 把组件变成响应式组件，数据更新时可以触发渲染.
#####  inject把数据注册到组件。

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1ODU0MzUxMiwtMTM2OTgwNjk4N119
-->