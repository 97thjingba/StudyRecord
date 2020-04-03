
## **初始化项目**

首先我们先给项目创建一个文件夹 webpack-react-tutorial：

```js
mkdir webpack-react-tutorial && cd webpack-react-tutorial

```

接着在这个文件夹下创建一个src的子文件夹：

```text
mkdir -p src
```

初始化项目：

```js
npm init -y 

```

## **如何安装配置webpack**

**webpack**

webpack是一款非常有用的前端打包工具，了解[如何使用它](https://link.zhihu.com/?target=https%3A//www.valentinog.com/blog/from-gulp-to-webpack-quickstart/)是React开发者的基础，因为webpack可以将React组件转化成几乎所有浏览器都可以运行的JS code。

让我们先来安装它：

```text
npm i webpack --save-dev
```

你可能会需要webpack-cli，所以也先装上

```text
npm i webpack-cli --save-dev
```

接着在package.json里添加webpack的指令

```text
"scripts": {
  "build": "webpack --mode production"
}
```

到目前为止还不需要写webpack的配置文件。

老版的webpack会自动去找配置文件，但是从webpack 4之后，你就需要自己去匹配需要的配置文件了。

下面我们来安装和配置Babel来编译我们的代码。

**初始化Babel**

为什么要使用Babel?

React Component大多是用JS ES6语法来写的，而浏览器没办法运行ES6的语法，所以就需要工具来将ES6的代码转化成浏览器可以运行的代码（通常是es5的语法）。

webpack本身是不会做这件事情的，需要靠转换器：loader。

一个webpack loader作用就是把输入进去的文件转化成指定的文件格式输出。其中**babel-loader负责将传入的es6文件转化成浏览器可以运行的文件**。

babel-loader需要利用Babel，所以需要预先将Babel配置好。

1.  **babel preset env：**将ES6的代码转成ES5(注意：babel-preset-es2015已经被废弃了)

2**.babel preset react:** 将JSX语法编译成JS

接着安装这两个依赖：

```js
npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev

```

不要忘了配置Babel! 首先要在webpack-react-tutorial文件夹里新建一个文件.babelrc，内容为

```js
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}

```

到这个时候，就可以写一小部分webpack的配置文件了。

创建一个新的文件webpack.config.js，内容为

```js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
 
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};

```

这个webpack的配置很简单。意思就是所有以.js结尾的文件都会用babel-loader把ES6编译转化成ES5的文件。

同时它定义了输入文件的路径为 src/index.js，输出为dist/bundle.js。webpack 4里这两行代码你不写也行，webpack会默认帮你加，但是为了代码可读性，我们还是把它加上。

配置完成之后，我们就可以开始写React 组件了。

## **写React组件**

这里会写两种React组件：[容器](https://link.zhihu.com/?target=https%3A//medium.com/%40learnreact/container-components-c0e67432e005)、[展示](https://link.zhihu.com/?target=https%3A//medium.com/%40dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)组件。如果不了解这两种组件概念的同学可以先了解一下。

简单来说: 容器跟展示组件是React组件的两种模式。

容器组件: 一般比较重数据处理的逻辑会写在这，比如监听外界传入（例如redux） state的变化，或者处理组件内部的state，等等。

展示组件：顾名思义，就是仅仅用来展示的。它一般都是一个纯箭头函数，接受容器组件通过props传来的数据，然后展示我们希望展示的html结构。

在下面的例子中，你会看到它们长啥样。

在本节中，我们来创建只有text input 的超级简单的React表单。

首先先把React库引进来：

```js
npm i react react-dom --save

```

然后创建两个子文件夹来分别放React 容器/展示组件

```js
mkdir -p src/js/components/{container,presentational}

```

接着我们来写一个容器组件，它有下面的特点

1.  有自己的state

2. 渲染一个html表单

将这个容器组件放在container里

```js
touch src/js/components/container/FormContainer.js

```

容器组件的代码如下：

```js
import React, { Component } from "react";
import ReactDOM from "react-dom";

class FormContainer extends Component {
  constructor() {
 super();

 this.state = {
      title: ""
 };
 }

  render() {
 return (
 <form id="article-form">
 </form>
 );
 }
}

export default FormContainer;

```

到目前为止，这个组件还没啥用，它只是一个包裹着子展示组件的外壳。

所以我们来定义一下子组件Input吧。

我们知道[html input](https://link.zhihu.com/?target=https%3A//developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text)有下列的属性：

-   type
-   class
-   id
-   value
-   required

所有的这些属性都由容器组件通过props传给它，这种组件叫做[controlled component](https://link.zhihu.com/?target=https%3A//reactjs.org/docs/forms.html%23controlled-components)。

写一个react组件，最好给它加上[Prop Types](https://link.zhihu.com/?target=https%3A//reactjs.org/docs/typechecking-with-proptypes.html)，**这样一来可以做输入的数据类型检测，二来别人用你的组件，可以很快知道这个组件需要什么input**。

安装prop-types

```js
npm i prop-types --save-dev

```

接着写这个展示组件

```js
import React from "react";
import PropTypes from "prop-types";
const Input = ({ label, text, type, id, value, handleChange }) => (
  <div className="form-group">
    <label htmlFor={label}>{text}</label>
    <input
      type={type}
      className="form-control"
      id={id}
      value={value}
      onChange={handleChange}
      required
    />
  </div>
);
Input.propTypes = {
  label: PropTypes.string.isRequired,
  text: PropTypes.string.isRequired,
  type: PropTypes.string.isRequired,
  id: PropTypes.string.isRequired,
  value: PropTypes.string.isRequired,
  handleChange: PropTypes.func.isRequired
};
export default Input;

```

到这一步我们就可以在容器组件里渲染Input这个子组件了

```js
import React, { Component } from "react";
import ReactDOM from "react-dom";
import Input from "../presentational/Input";
class FormContainer extends Component {
  constructor() {
    super();
    this.state = {
      seo_title: ""
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ [event.target.id]: event.target.value });
  }
  render() {
    const { seo_title } = this.state;
    return (
      <form id="article-form">
        <Input
          text="SEO title"
          label="seo_title"
          type="text"
          id="seo_title"
          value={seo_title}
          handleChange={this.handleChange}
        />
      </form>
    );
  }
}
export default FormContainer;

```

写好组件之后，就可以用webpack来打包这些代码啦。

由于前面我们已经定义了webpack入口文件是 ./src/index.js

所以我们先创建一个index.js文件，在里面引入React组件

```js
import FormContainer from "./js/components/container/FormContainer";

```

写好之后，激动人心的时刻到了!

我们终于可以通过运行

```js
npm run build

```

来生成打包文件，由于我们在配置里定义了输出文件为：dist/bundle.js，所以一切顺利的话， 你现在应该可以看到一个新生成的dist文件，里面有一个bundle.js文件。

## **在HTML文件引入bundle**

为了展示我们的React组件，我们需要让webpack生成一个html文件。上面我们生成的bundle.js就会放在这个html文件的<script>标签里。

webpack需要两个工具来生成这个html文件：[html-webpack-plugin](https://link.zhihu.com/?target=https%3A//webpack.js.org/plugins/html-webpack-plugin/)跟[html-loader](https://link.zhihu.com/?target=https%3A//webpack.js.org/loaders/html-loader/)

首先添加这两个依赖：

```text
npm i html-webpack-plugin html-loader --save-dev
```

然后更新webpack的配置文件

```js
const HtmlWebPackPlugin = require("html-webpack-plugin");
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader"
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      title: 'Set Up Project',
      filename: "./index.html"
    })
  ]
};

```

index.html是我们的模板文件，里面定义了React Component需要插入进入的容器<div>create-article-form</div>，不要忘了在FormContainer里用React.render绑定这个。

```js
<!doctype html>
<html>
  <head>
    <title>Getting Started</title>
  </head>
  <body>
    <div id='create-article-form'>

    </div>
  </body>
</html>

```

在./src/js/components/container/FormContainer.js 加上下面的代码：

```js
const wrapper = document.getElementById("create-article-form");
wrapper ? ReactDOM.render(<FormContainer />, wrapper) : false;

```

最后，在跑一次构建：

```js
npm run build

```

这时候在dist文件夹里就会看到生成的html文件，由于html-webpack-plugin，bundle文件会被自动注入html里。

在浏览器里打开./dist/index.html，你会看到这个React表单。

## webpack dev Server

目前为止，我们来遗留一个问题：每次修改文件的时候，都需要重新跑一次编译

```js
npm run build

```

这样是很麻烦的，我们想达到的效果是**自动重新编译**。

达到这个目标很简单，只需要3行配置就可以启动运行一个开发服务器。

启动服务器之后webpack就会在浏览器里启动你的应用，而且当你修改保存代码之后，webpack dev server还会**自动刷新浏览器的窗口**。

在启动webpack dev server前，需要先安装

```js
npm i webpack-dev-server --save-dev

```

打开package.json 加入start script

```js
"scripts": {
  "start": "webpack-dev-server --open --mode development",
  "build": "webpack"
}

```

保存这个文件，最后在跑这个命令

```js
npm start
```
参考：[https://zhuanlan.zhihu.com/p/47704649](https://zhuanlan.zhihu.com/p/47704649)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjY2OTg2MjQsMTI5MDA1OTU0XX0=
-->