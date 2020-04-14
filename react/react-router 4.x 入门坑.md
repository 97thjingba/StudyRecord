在 React Router 4.x 发布之前，我们在项目中使用的是 React Router 3.x。随着第四版 React Router 的正式亮相，其精简的 API 、语义化的路由匹配方案以及动态路由等变化，都彰显着此次升级的颠覆性。所以，我们决定在新的 React 项目中使用 4.x（React Router 4.x）开发，亲身实践之后发现： 4.x 不仅是 API 的简单改变，还有整个设计理念的变化；初次使用确实有一些别扭，更可怕的是按照 API 文档写出的代码，有时运行时会出现一些莫名其妙的红色错误（此刻的心情 down 到谷底~）。为了避免大家在使用时遇到同样的问题多绕弯子，我们把开发过程中遇到的问题以及相应的解决方法做了汇总。

### 4.x 使用问题汇总

#### 1. 包引用方式

在之前的 3.x 中，在入口文件中定义路由时，我们会这么写：

```
import React from 'react';
import ReactDOM from 'react-dom';
import {Router, Route, browserHistory} from 'react-router';
import * as routePaths from './js/constants/routePaths';
import Index from './js/pages/Index';
 
ReactDOM.render((
    <Router history={history}>
        <div className="container">
            <Route path={routePaths.INDEX} component={Index} />
        </div>
    </Router>
    ),
    document.getElementById('app')
);
```

但是保存后运行发现页面报错了，如下图所示：

![](https://user-gold-cdn.xitu.io/2018/7/19/164b1bea58ae2b7a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)  ![](https://user-gold-cdn.xitu.io/2018/7/19/164b1bea5881b6be?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

解决方法：

```
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter, Route } from 'react-router-dom';
import * as routePaths from './js/constants/routePaths';
import Index from './js/pages/Index';
 
ReactDOM.render((
    <BrowserRouter>
        <div className="container">
            <Route path={routePaths.INDEX} component={Index} />
        </div>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

页面显示正常，问题解决。接下来我们对该解决方法进行详细的解释：

4.x 中采用了单代码仓库模型架构，所以里面包含了若干个相互独立的包，如下所示：

-   `react-router` React Router 核心
-   `react-router-dom` 用于 DOM 绑定的 React Router
-   `react-router-native` 用于 React Native 的 React Router
-   `react-router-redux` React Router 和 Redux 的集成
-   `react-router-config` 用于配置静态路由

因此，在实际的 web 项目开发中，`react-router` 和 `react-router-dom` 不必同时引用。在  `react-router-dom` 中包含类似 `<BrowserRouter>` 的 DOM 类组件，所以只需要引入  `react-router-dom` 包就可以了。

使用方法：

```
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';
```

关于 `<BrowserRouter>`  是什么？下面的问题中会有详细介绍，莫急~

#### 2. 页面中多个模块同时渲染问题

我们同时定义了多个模块，当路由切换时发现这些模块会同时渲染出来。比如像下面这样定义：

```js
ReactDOM.render((
    <BrowserRouter>
        <div className="container">
            <Route path="/" component={Index} />
            <Route path="/card" component={Card} />
        </div>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

当访问 `path="/card"`  的页面时，`path="/"`  的页面也会被渲染出来。不同于 3.x 中路由匹配时的独一无二特性，4.x 中有了一层包含关系：如匹配 `path="/card"` 的路由会匹配 `path="/"`  的路由。那么这个问题怎么解决呢？有以下两种方法：

##### （1）使用 <Router> 的 `exact`  关键字

```js
ReactDOM.render((
    <BrowserRouter>
        <div className="container">
            <Route path="/" exact component={Index} />
            <Route path="/card" component={Card} />
        </div>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

##### （2）使用独立路由：  `<Switch>`

```js
import { BrowserRouter, Route, Switch, Redirect } from 'react-router-dom';
 
ReactDOM.render((
    <BrowserRouter>
        <Switch>
            <div className="container">
                <Route path="/" exact component={Index} />
                <Route path="/card" component={Card} />
            </div>
        </Switch>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

完美！模块可以实现独立渲染了。我们来看下这样解决问题的原因：

首先需要了解下  `<Router>` 。它是所有路由组件共用的底层接口，在 4.x 中，你可以将各种组件及标签放进 `<Router>`  组件中。比如：

```js
<Router>
    <div>
        <ul>
            <li><Link to="/">Home</Link></li>
        </ul>
        <hr/>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
    </div>
</Router>
```

需要注意的是：  `<Router>` 下只允许存在一个子元素，如存在多个则会报错。所以在上面的代码中，需要使用 `<div></div>`  将其他元素包裹起来。

在实际的项目中，我们一般不会直接使用  `<Router>` ，而是使用如下所示的更高级的路由。在这里将会介绍到第一个问题中用到的 `<BrowserRouter>` 以及其他常用的高级路由。咳咳，集中精力了哈，重头戏来了！

###### <BrowserRouter>

使用 HTML5 提供的 history API ( `pushState` , `replaceState` 和 `popstate` 事件) 来保持 UI 和 url 的同步。下面介绍一下该路由组件中的 5 个属性：

-   basename: string

当前位置的基准  `url`  。如果你的页面部署在服务器的二级（子）目录，你需要将 `basename`  设置到此子目录。 正确的  `url`  格式是前面有一个前导斜杠，但不能有尾部斜杠。

```
<BrowserRouter basename="/calendar"/>
<Link to="/today"/> // 渲染为 <a href="/calendar/today">
```

-   getUserConfirmation: func

当导航需要确认时执行的函数。默认使用 `window.confirm` 。

```js
// 使用默认的确认函数
const getConfirmation = (message, callback) => {
  const allowTransition = window.confirm(message)
  callback(allowTransition)
}
<BrowserRouter getUserConfirmation={getConfirmation}/>
```

-   forceRefresh: bool

当设置为  `true`  时，在导航的过程中整个页面将会刷新。 只有当浏览器不支持 HTML5 的 history API 时，才设置为  `true`  。

```
const supportsHistory = 'pushState' in window.history
<BrowserRouter forceRefresh={!supportsHistory}/>
```

-   keyLength: number

`location.key`  的长度，默认是 6。点击同一个链接时，每次该路由下的  `location.key`  都会改变，可以通过 `key`  的变化来刷新页面。

```
<BrowserRouter keyLength={12}/>
```

-   children: node

渲染单一子组件（元素）。

###### <HashRouter>

HashRouter 是一种特定的  `<Router>`  ， HashRouter 使用 url 的  `hash`  (例如： window.location.hash ) 来保持 UI 和 url 的同步。由于使用 hash 的方式记录导航历史不支持  `location.key` 和 `location.state`  ，该技术仅用于支持传统的浏览器，此 API 不再赘述。

这两个是经常使用的，剩下的还有 `<MemoryRouter>`  、`<NativeRouter>`  、  `<StaticRouter>`，有兴趣的同学可以自己了解一下。

介绍完 `<Router>`，当然也要说下 `<Route>`  ，我们使用最频繁的组件，主要职责是当页面的访问地址与 `Route` 上的 `path` 匹配时渲染出对应的 UI 界面。

<Route> 属性值主要有：

-   path: string

可以被  `path-to-regexp`  解析的有效 url 路径。如果没有  `path`，路由将总是被匹配。

```
<Route path="/users/:id" component={User}/>
```

-   exact: bool

为  `true`  时，则要求路径与 `location.pathname` 必须完全匹配。通过下表解释一下：

![](https://user-gold-cdn.xitu.io/2018/7/19/164b1bea58aac3e5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

-   strict: bool

为 `true`  时，有结尾斜线的路径只能匹配有斜线的 `location.pathname` 。见下表：

![](https://user-gold-cdn.xitu.io/2018/7/19/164b1bea5890ddfb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

第二个属性值 `exact` 就是我们用来解决多个模块同时渲染问题的，默认值为  `true`  。

在这里简要提下 `<Route>` 渲染的三种方法：

-   `<Route component>`  当访问地址和路由匹配时，一个  `React component`  将会被渲染
-   `<Route render>` 此方法适用于内联渲染，而且不会产生重复装载问题
-   `<Route children>`

当需要判断访问地址与路由是否匹配时，可以使用此方法。当不匹配时，  `match`  为 null。

我们上面代码示例中使用的是第一种方法 `<Route component>`，这三种渲染方法都会用到 `match` 、`location` 、  `history`  这些属性值。这里不再详细介绍，使用时可以查阅官方文档。

需要注意的是 ：每一种渲染方法都有其适用背景， <Route component> 的优先级比 <Route render> 高，而他们又都优先于 <Route children> ，所以在同一个 <Route> 应该只使用一种方法，我们大多数使用的是 component 方法。

说完第一种解决方法的原理，来剖析下第二种方法：  `<Switch>`  。

该组件只渲染第一个与当前访问地址匹配的 `<Route>` 或 `<Redirect>` 。它和多个堆叠的 <Route> 组件之间的区别是：  `<Switch>` 只渲染一个路由。

在解决方法 （2）中，当我们访问 `/card` ，  `<Switch>` 将会开始寻找与之匹配的路由，查找到 `<Route path="/card"/>` 匹配后，`<Switch>` 将会停止寻找然后开始渲染 `/card`  。`<Switch>`

-   children: node

`<Switch>`  下的子节点只能是  `<Route>`  或  `<Redirect>`  元素且只有与当前访问地址匹配的第一个子节点才会被渲染。

#### 3. 如何定义默认访问页面

当用户手动修改 url 时，有时我们需要定义一个默认页面，重新引导用户的操作，这个该如何实现呢？

使用  `<Redirect>`  。比如当用户手动输入  `/test`  之后，我们需要跳转至首页，则代码如下所示：

```js
ReactDOM.render((
    <BrowserRouter>
        <div className="container">
            <Switch>
                <Route path={routePaths.INDEX} exact component={Index} />
                <Route path={routePaths.CARD} component={Card} />
                <Redirect to="/" />
            </Switch>
        </div>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

方法解析：`<Redirect>`  渲染时将会导向一个新的地址，这个新的地址将会覆盖掉  `history`  堆栈中的当前地址。

其常用的属性是：

-   to: string

重定向的 url 地址。

```js
<Redirect to="/somewhere/else"/>
```

-   to: object

重定向的  `location`  对象。

```js
<Redirect to={{
  pathname: '/login',
  search: '?utm=your+face',
  state: { referrer: currentLocation }
}}/>
```

-   push: bool

取值为  `true`  时，重定向操作将会把新地址加入到访问的历史记录里面，并不会替换掉当前的地址。

```
<Redirect push to="/somewhere/else"/>
```

-   from: string

需要匹配的将要被重定向的路径。

```
<Switch>
  <Redirect from='/old-path' to='/new-path'/>
  <Route path='/new-path' component={Place}/>
</Switch>
```

需要注意的是：`<Route>`  元素使用  `path`  属性进行匹配，`<Redirect>`  元素使用  `from`  属性进行匹配。如果元素中没有对应的  `path`  或  `from`，那么它们将匹配任何当前的访问地址。

#### 4. 路由激活状态的控制

相信大家对于  `<link>`  组件都不陌生，在 3.x 中，当需要将当前点击的理由置为激活状态时，我们可以这样设置：

```
//通过Style进行配置
<li><Link to="/home" activeStyle={{ color: 'red' }}>Home</Link></li>
 
//通过类名进行设置
<li><Link to="/home" activeClassName="active">Home</Link></li>
```

但是，一般情况下只有主导航的链接才需要知道自己是否被激活。因此需要对主导航的  `<Link>`  进行一层包装，这样就不必记得哪些地方有  `activeClassName`  或  `activeStyle`  。所谓的对  `<Link>`  包装就是自定义  `<Link>`  组件，通过自定义实现特别的  `Style`  。在 3.x 中，具体实现方法如下：

```js
// modules/NavLink.js
import React from 'react';
import { Link } from 'react-router';
 
export default class NavLink extends React.Component({
    constructor(props) {
        super(props);
    }
 
    render() {
        return <Link {...this.props} activeClassName="active"/>
    }
})
//使用方法：
import NavLink from './NavLink'
// ...
<li><NavLink to="/home">Home</NavLink></li>
```

但是，在 4.x 中我们不需要做这些包装工作，因为它直接提供了  `<NavLink>`  组件供我们使用。使用方法：

```js
<NavLink
  to="/faq"
  activeClassName="selected"
>FAQs</NavLink>
```

下面对  `<NavLink>`  做下简单介绍：

该组件是  `<Link>`  的特殊版本，当遇到匹配的 URL 渲染元素时会添加样式属性，适用于页面导航部分。

-   activeClassName: string

导航选中时的样式名，默认样式名为  `active`。

```js
<NavLink
  to="/faq"
  activeClassName="selected"
>FAQs</NavLink>
```

-   activeStyle: object

导航选中时的样式。

```js
<NavLink
  to="/faq"
  activeStyle={{
    fontWeight: 'bold',
    color: 'red'
   }}
>FAQs</NavLink>
```

-   exact: bool

若值为  `true`，当访问地址严格匹配时激活样式才会生效。

```js
<NavLink
  exact
  to="/profile"
>Profile</NavLink>
```

-   strict: bool

若值为  `true`，只有当访问地址后缀斜杠严格匹配（有或无）时激活样式才会生效。

```js
<NavLink
  strict
  to="/events/"
>Events</NavLink>
```

-   isActive: func

用于添加页面激活时的操作逻辑。

```js
const oddEvent = (match, location) => {
  if (!match) {
    return false
  }
  const eventID = parseInt(match.params.eventID)
  return !isNaN(eventID) && eventID % 2 === 1
}
 
<NavLink
  to="/events/123"
  isActive={oddEvent}
>Event 123</NavLink>
```

以上是  `<NavLink>`  组件的属性介绍，供大家学习。

#### 5. 页面跳转

在 3.x 中，跳转页面可以使用以下方式：

```js
import { browserHistory } from 'react-router';
//第一种方法
browserHistory.push('/some/path');
//第二种方法
this.context.router.push('/some/path');
//第三种方法
<Link to="'/some/path'"></Link>
```

在 4.x 中使用  `push`  方法跳转页面时，如果按照上面的写法，页面会报错：

![](data:image/svg+xml;utf8,<?xml version="1.0"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="690" height="118"></svg>)

针对该问题有以下两种解决方法：

##### （1）使用 history 控制路由的跳转

```js
this.props.history.push('/some/path');
```

简单介绍下  `history`：

`history`  指的是  `history`  包，是 4.x 中的重要依赖之一。常见的  `history`  路由方案有三种形式，分别是：

-   browser history 在 DOM 上的实现，用于支持 HTML5 history API 的浏览器；
-   hash history 在 DOM 上的实现，用于旧版浏览器；
-   memory history 在内存上的实现，用于测试或非 DOM 环境（如  `React Native`）。

`history`  对象包含的属性和方法如下所示：

-   `length`: number history 堆栈中的地址数目
-   `action`: string 当前的动作 (PUSH , REPLACE , 或者是 POP )
-   `location`: object 当前访问地址信息组成的对象
-   `push(path, [state])`: func 在 history 堆栈信息里加入一个新路径
-   `replace(path, [state])`  : func 替换 history 堆栈信息里的当前路径
-   `go(n)`  : func 将 history 堆栈中的指针向前移动 n
-   `goBack()`: func 等同于 go(-1)
-   `goForward()`: func 等同于 go(1)
-   `block(prompt)`  : func 阻止跳转

需要注意的是：`history`  对象是可变的，所以不要从  `history.location`  直接获取，而是需要通过  `<Route>`  的`prop`  来获取  `location`。

##### （2）使用  `Context`，获得  `router`  对象

```js
import React from "react";
import PropTypes from "prop-types";
 
class MyComponent extends React.Component {
  static contextTypes = {
    router: PropTypes.object
  }
  constructor(props, context) {
     super(props, context);
  }
  ...
  myFunction() {
    this.context.router.history.push("/some/Path");
  }
  ...
}
```

以上两种方法中推荐使用第一种，因为  `React`  不推荐使用  `context`  , 在未来版本中有可能被抛弃哦。

#### 6. 切换路由后，页面仍然停留在上一个页面的位置

由 A 页面跳转到 B 页面，B 页面停留在 A 页面的位置，没有返回到顶部。

问题分析：在  `React Router`  早期版本中大家可以使用滚动恢复的开箱即用功能，但是在 4.x 中路由切换时并不会恢复滚动位置，用户需要对 window 和独立组件的滚动位置进行管理。可以使用  `withRouter`  组件：  `withRouter`  可以访问历史对象的属性和最近的  `<Route>`  匹配项，当路由的属性值 {  `match`,  `location`,  `history`  } 改变时，`withRouter`  都会重新渲染。该组件可以携带组件的路由信息，避免组件之间一层层传递。使用方法如下：

```js
withRouter(MyComponent)
```

这样就可以获取到 MyComponent 组件的路由信息了。

解决方法：使用  `withRouter`  封装  `ScrollToTop`  组件。这里就用到了  `withRouter`  携带路由信息的特性，通过对比`props`  中  `location`  的变化，实现页面的滚动。

##### （1）定义  `ScrollToTop`  组件，代码如下：

```js
import React, { Component } from 'react';
import { Route, withRouter } from 'react-router-dom';
class ScrollToTop extends Component {
    componentDidUpdate(prevProps) {
        if (this.props.location !== prevProps.location) {
          window.scrollTo(0, 0)
        }
    }
    render() {
        return this.props.children
    }
}
 
export default withRouter(ScrollToTop);
```

##### （2）在定义路由处引用该组件，例如：

```js
ReactDOM.render((
    <BrowserRouter>
        <ScrollToTop>
            <div className="container">
                <Route path={routePaths.INDEX} exact component={Index} />
                <Route path={routePaths.CARD} component={Card} />
            </div>
        </ScrollToTop>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

这样处理之后，当跳转页面时都会自动回到该页面的顶部位置。

#### 7. 页面之间如何传值？

问题背景：当路由发生跳转时我们可能需要携带一些参数。

解决方法：使用  `props`  属性，介绍以下三种传值方法：

##### （1）`props.params`

指定一个 path ，然后指定通配符可以携带参数到指定的  `path`  ：

```
<Route path='/user/:name' component={UserPage}></Route>
```

跳转 UserPage 页面时，可以这样写：

```js
//link方法
<Link to="/user/sam">用户</Link>
//push方法
this.props.history.push("/user/sam");
```

在 UserPage 页面中通过  `this.props.params.name`  获取值。

上面的方法可以传递一个或多个值，但是每个值的类型都是字符串，没法传递一个对象。如果要传的话可以将 json 对象转换为字符串，传递过去之后再将 json 字符串转换为对象。

```js
let data = {id:3,name:sam,age:36};
data = JSON.stringify(data);
let path = '/user/${data}';
 
//在页面中获取值时
let data = JSON.parse(this.props.params.data);
```

##### （2）`query`

`query`  方式可以传递任意类型的值，但是页面的  `url`  也是由  `query`  的值拼接的，`url`  很长且是明文传输。

```js
//定义路由
<Route path='/user' component={UserPage}></Route>
 
//数据定义
let data = {id:3,name:sam,age:36};
let path = {
    pathname: '/user',
    query: data,
}
 
//页面跳转
<Link to={path}>用户</Link>
this.props.history.push(path);
 
//页面取值
let data = this.props.location.query;
let {id,name,age} = data;
```

##### （3）`state`

`state`  方式类似于  `post`，依然可以传递任意类型的数据，而且可以不以明文方式传输。

```js
//定义路由
<Route path='/user' component={UserPage}></Route>
 
//数据定义
let data = {id:3,name:sam,age:36};
let path = {
    pathname: '/user',
    state: data,
}
 
//页面跳转
<Link to={path}>用户</Link>
this.props.history.push(path);
 
//页面取值
let data = this.props.location.state;
let {id,name,age} = data;
```

在实际的项目开发中，大家可以根据项目需要选择合适的传值方法。

#### 8. 使用  `<BrowserRouter>`  配置路由，上传页面至服务器后页面出现 404

问题背景：项目中控制路由跳转使用的是  `<BrowserRouter>`，代码如下：

```js
ReactDOM.render((
    <BrowserRouter>
        <div className="container">
            <Route path={routePaths.INDEX} exact component={Index} />
            <Route path={routePaths.CARD} component={Card} />
        </div>
    </BrowserRouter>
    ),
    document.getElementById('app')
);
```

在开发过程中使用是没有问题的，但是将页面上传至服务器之后，问题就来了：用户访问的资源不存在，页面是空白的。

问题分析：`<BrowserRouter>`  是使用 React-Router 应用推荐的  `history`  方案。它使用浏览器中的 History API 用于处理 url，创建一个像  `example.com/list/123`  这样真实的 url。当通过真实 url 访问网站的时候，由于路径是指向服务器的真实路径，但该路径下并没有相关资源，所以用户访问的资源不存在。

解决方法：

##### （1）使用  `<HashRouter>`。

它使用 url 中的 hash（#）部分去创建路由，举例来说，用户访问  `http://www.example.com/`  ，实际会看到的是  `http://www.example.com/#/`  。  
为什么本地开发时没有问题呢？那是因为我们的  `React`  脚手架中使用  `webpack-dev-server`  做了配置。

```js
webpackConfig.devServer = {
    disableHostCheck: true,
    contentBase: path.resolve(__dirname, 'build'),
    compress: true, //gzip压缩
    historyApiFallback: true
};
```

##### （2）如果要使用  `<BrowserRouter>`  的话，服务器需要进行相关路由配置，方法见扩展阅读 [1]。

#### 9. React Router 4.x 如何配置按需加载？

问题背景：当访问首页时会一次性请求所有的 js 资源，这会大大影响页面的加载速度和用户体验。所以添加按需加载功能是必要的。

问题分析：4.x 官网中推荐使用  `bundle loader`  实现代码拆分，所以我们选择使用  `bundle loader`  。

解决方法：配置按需加载的步骤如下：

##### （1）安装  `bundle-loader`。

```
npm install --save-dev bundle-loader
```

##### （2）定义  `Bundle.js`。

`<Bundle>`  组件会接受一个名为  `load`  的  `props`，  `load`  是一个组件异步加载的方法，该方法需要传入一个回调函数作为参数，然后回调函数会在方法内异步接收加载完的组件，详细代码如下：

```js
import React, { Component } from 'react';
export default class Bundle extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            // short for "module" but that's a keyword in js, so "mod"
            mod: null
        }
    }
 
    componentWillMount() {
        this.load(this.props)
    }
 
    componentWillReceiveProps(nextProps) {
        if (nextProps.load !== this.props.load) {
            this.load(nextProps)
        }
    }
 
    load(props) {
        this.setState({
            mod: null
        })
        props.load((mod) => {
            this.setState({
                // handle both es imports and cjs
                mod: mod.default ? mod.default : mod
            })
        })
    }
 
    render() {
        if (!this.state.mod)
            return false
        return this.props.children(this.state.mod)
    }
}
```

##### （3）入口文件  `app.jsx`  配置。

使用  `bundle-loader`  为每个页面组件配置按需加载，默认打开的首页可以直接引入，不需要使用  `<Bundle>`  组件进行处理，代码如下所示：

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { HashRouter, Route } from 'react-router-dom';
import * as routePaths from './js/constants/routePaths';
import Bundle from './js/constants/Bundle.js';
//默认打开页面直接引入
import Index from './js/pages/Index';
//其他页面异步引入
import CardContainer from 'bundle-loader?lazy&name=app-[name]!./js/pages/Card';
import './assets/css/index.scss';
 
const Card = () => (
    <Bundle load={CardContainer}>
        {(Card) => <Card />}
    </Bundle>
)
 
ReactDOM.render((
    <HashRouter>
        <div className="container">
            <Route path={routePaths.INDEX} exact component={Index} />
            <Route path='/card' component={Card} />
        </div>
    </HashRouter>
    ),
    document.getElementById('app')
);
```

##### （4）`webpack.config.js`  修改，配置子文件名称。

```
webpackConfig.output = {
    path: path.resolve(__dirname, 'build/' + config.ftpTarget),
    publicPath: config.publicPath + '/',
    filename: 'js/[name].js',
    chunkFilename: 'js/[id].js'
}
```

这样配置之后，打包出来的 js 文件已经进行了拆分，每个页面对应一个自己的 js ，当访问该页面时才加载相应的资源。

#### 10.  `this.props.history.push()`  进行路由跳转时报错

问题背景：配置按需加载后，首页可以正常跳转子页面，而在子页面中进行页面跳转时出现报错：`this.props.history.push中'push'is undefined`  。

问题分析：项目中使用  `this.props.history.push()`  方法实现路由跳转，未进行文件拆分时可以正常使用，但是当进行文件拆分之后，子文件中无法获取  `this.props.history`  对象。

解决方法：使用  `withRouter`  封装页面组件。示例代码如下：

```js
import React from 'react';
import { withRouter } from 'react-router-dom';
 
class Card extends React.Component {
  constructor(props) {
      super(props);
 
    }
    render() {
      return (
        <div className="wrapper">
          <p>这是第二页：测试</p>
      </div>
      );
    }
}
export default withRouter(Card);
```

这样封装之后，就无需一级级传递  `React Router`  的属性，子文件内也可以拿到需要的路由信息。

以上列出的内容就是我们在使用 4.x 开发时遇到的一些问题，针对每个问题不仅给出了解决方法，还介绍了解决方法中涉及到的知识点。对于一些未介绍到的内容，大家可以移步官网进行深度学习（见扩展阅读 [2]）。

### 小结

对于新项目来说，使用 React Router 4.x 进行开发是一个不错的选择。因为其组件化的思想和 React 很像，学习起来比较容易、上手快。除了官网 [2] ，扩展阅读中我们还给出了 React Router 4.x 的其他学习文档 [3][4]，供大家参考。值得注意的是，上述问题解决方法中的示例代码使用的是 React v16 版本，在实际使用时需要结合自己的环境进行适当修改。

React Router 4.x 此次带来的改变是颠覆性的，对于我们使用者来说是一种挑战，同时也是一种知识的有趣探索。组件化路由设计理念和动态路由的配置给我们的项目开发带来了更大的灵活性。文中在介绍问题解决方法时对一些 4.x 的 API 做了简要的介绍，对于一些更细节化的东西，需要我们移步官网进行深入的学习，然后再慢慢的探索。React Router 的作者说过版本号要永远和 React 保持一致，所以相信我们的 React Router 探索之旅将会一直进行着……同志们，Hold On！

参考：[https://juejin.im/entry/5b50518bf265da0f6436c34a](https://juejin.im/entry/5b50518bf265da0f6436c34a)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk3MjcxODUyMCwyMjk4MTg4MTJdfQ==
-->