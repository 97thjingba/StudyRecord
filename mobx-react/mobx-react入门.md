
HomeStore 类
```
import { observable} from "mobx";
class HomeStore {
  @observable homeNum = 0;
}
export default HomeStore;
```

oneStore 类
```
import { observable} from "mobx";
class OneStore {
  @observable oneNum = 3333;
}
export default OneStore;
```

将两个类合并到Store类里
```
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

```d
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjEyOTEyMTE3XX0=
-->