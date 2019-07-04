## 概念

**react 是用于构建用户界面的 javascript 库**

react 三件套：react 、react-dom 、react-scripts、    react-rn（原生DOM）



**特性**：

1. props:组件属性，专门用来连接父子组件间通信，父组件传输父类成员，子组件可以利用但不能编辑父类成员；

2. state：专门负责保存和改变组件内部的状态；

   

### JSX语法

react是使用的 `JSX` 语法，而Vue使用的是 ` 插值表达式` ;

```
{}:表示解析js语句
注释：{/*    */}
传属性值： 
	父 => 子： 属性={属性值}　this.props
	子 ＝＞　父：　标签 this.props.children
```

```js
import React, { Component } from 'react'
export default class index extends Component {
  render() {
    return (
      <div>
        <h2 title={hello}></h2>
		<p>hello React</p>
      </div>
    )
  }
}

import React, { Component } from 'react'
export default class index extends Component {
  render() {
    return (
      <div>
        <h2>{this.props.title}</h2>
        <p>{{this.props.children}}</p>
      </div>
    )
  }
}

import React, { Component } from 'react'
export default class index extends Component {
    constructor() {
        //this.state相当于vue里面的data
        super()
        this.state = {
            
        }
    }
}
```



##### state

this.state 相当于 Vue里面的data；

```js
constructor () {
    this.state = {
        inputValue: ''
    }
 }

等价于

state = {
    inputValue: 'abc'
 }
```



##### ref

ref应用：

- 管理焦点，文本选择或媒体播放。
- 触发强制动画。
- 集成第三方 DOM 库。

```js
// 引用
import React, { Component, createRef } from 'react'

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();   // myRef = createRef()
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```





##### **super与construtor **

* super（）--继承

​		在class方法中，继承是使用 `extends`  关键字来实现的。子类必须在`constructor( )` 调用 `super( ) ` 方法，否则新建实例时会报错。

​		报错原因：子类是没有自己的 this 对象的，它只能继承自父类的 this对象，然后对其进行加工，而super( )就是将父类中的this对象继承给子类的。没有super，子类就得不到this对象。



**怎样判断何时写super（）？**

    1. 如果你用到了constructor就必须写super(),是用来初始化this的，可以绑定事件到this上; 
    2. 如果你在constructor中要使用this.props,就必须给super加参数：super(props)；
    	无论有没有constructor，在render中this.props都是可以使用的，这是React自动附带的； 如果没用到constructor,是可以不写的；React会默认添加一个空的constructor。



**ES5中的new继承做了啥？**

```
当一个构造函数前加上new的时候，做了四件事：
1. 生成一个空的对象并将其作为 this；
2. 将空对象的 __proto__ 指向构造函数的 prototype；
3. 运行该构造函数；
4. 如果构造函数没有 return 或者 return 一个返回 this 值是基本类型，则返回this；如果 return 一个引用类型，则返回这个引用类型。
```

ES5继承： 先创建子类的实例对象this， 再将父类的方法添加到this上（parent.apply (this)）;

ES6继承：先创建父类的实力对象this ( 所以调用super（）方法 ) ， 再用子类的构造函数修改this；



* constructor( ) --构造方法

​       这是ES6对类的默认方法，通过 new 命令生成对象实例时自动调用该方法。并且，该方法是类中必须有的，如果没有显示定义，则会默认添加空的 `constructor( )` 方法。



##### 导入

组件compnents导入：

```js
export { default as TodoHeader } from './TodoHeader'

等价于

import TodoHeader from './TodoHeader'
export {
	TodoHeader
	。。。
}
```



### prop-types包

prop-types ：**检测传输的数据类型是否存在错误**

```bash
# 安装
$ npm install --save prop-types
# 使用
```

```js
import React, { Component } from 'react'
// 引入prop-types
import PropTypes from 'prop-types'

export default class TodoHeader extends Component {
    render() {
        return (
            <div>
            
            </div>
        )
    }
}
TodoHeader.propTypes = {
    title: PropTypes.string.isRequired,
    subtitle: PropTypes.number,
    children: PropTypes.any
}

或者

export default class TodoHeader extends Component {
    // 相当于是给函数添加 propTypes 属性，即：TodoHeader.propTypes
    static propTypes = {
        // isRequired： 必传
        title: PropTypes.string.isRequired,
        subtitle: PropTypes.string,
        // any：任意字符
        children: PropTypes.any
    }
	render（）{
        ....
    }
}
```



### 组件

**创建组件**

在react中创建组件的形式有三种

- 纯函数式定义的无状态组件
- React.createClass 定义的组件
- Extends React.Component 定义的组件



1. **函数式定义的无状态组件**

* 组件不能访问this对象

* 函数式组件的代码量比类组件要少，所以函数式组件相比类组件更简洁

* 是基于**`无状态思想（Stateless Components）`**，无法使用state，也无法使用组件的生命周期方法，这就决定了函数组件都是 ` 展示性组件（Presentational Components）`，接收Props，渲染DOM，而不关注其他逻辑。

  即：`无状态组件只能访问输入的props`,无副作用

* 组件不会被实例化,整体渲染性能得到提升



2. **类组件**

3. 受控型组件

   1. 受控组件：组件的状态变化受到state的控制；

   2. 非受控组件：该组件内部的状态是受state控制；组件的变化不易管理

      模式：

      ```
       组件的值----state控制；
       组件值得变换---通过触发onChange事件，然后由this.setState负责改变；
      ```

4. 无状态组件： 

   1. 若一个组件不含有状态和对状态的处理，则可以将render方法单独抽取出来，成为一个独立的组件
   2. 无状态组件转化为有状态组件，则通过高阶组件转化；方式就是高阶组件通过props传入state。

   特点： 

   ```
   1. 不包含任何状态，但可以包含属性；
   2. 无状态组件生成时不用实例化；
   3. 无状态组件没有this，ref和生命周期；
   ```

   作用：

   ```
   1. 单纯的UI表现，不用涉及太多的交互；
   2. 不用对DOM做过多的操作；
   ```

   

5. 高阶组件

   一个包含了另一个React组件的React组件；本质上就是一个函数.

   包装方式：`属性代理和反向代理`；
   特点：不会改变被包装组件的内容，结构，不会复制它的行为，是利用它创建一个新的行为；

   - 属性代理

     定义：高阶组件接受外界实行，然后通过包装环境传递给被包装组件；

     Name : 可以指定返回组件的名称；
     
   - 反向代理
   
     定义：指定的组件作为另一个组件的父类，而继承了的组件就是一个高阶组件
     特点：
   
     	1. 该组件是被动被继承；
     	2）高阶组件可以通过this来获取父类的state，props，生命周期函数和渲染函数；
     3）一般来说，若调用父类的生命周期和渲染函数，用super来调用，以便保护父类的生命周期和渲染函数；
     
      	2. 优势：
          渲染劫持：高阶组件通过props属性来决定父类的渲染树是否被渲染（props不能创建或者改变props的名称，但可以更改和操作props的值）；

​     

### Context

Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。

API:

* React.createContext
* Context.Provider
* Context.Consumer

相当于

* 保存全局的共享资源，使用 Provider

* 获取全局的共享资源，使用 Consumer



Context使用

```js
# 引入Context
import React, { Component, createContext } from 'react'

# 创建Context，解构出 Provider 和 Comsumer；
const {
    Provider,
    Consumer: CounterConsumer  // 解构Consumer并重新赋值到 CounterConsumer 里面去
} = createContext()

# 自定义 Provider 组件
class CounterProvider extends Component {
    render（）{
        return（
        <Provider
        	value={}   		// 将需要全局共享的资源作为 <Provider> 元素的 value 属性值
        ></Provider>
        ）
    }
}
render(
    <CounterProvider>
        <Counter />
    </CounterProvider>,
    document.querySelector('#root')
)

# 自定义 Consumer 组件
class Counter extends Component {
    render () {
        return (
            // Cosumer是一个函数
            <CounterConsumer>
                {
                    // 函数参数就是在 Provider 的 value 中共享的资源 {}
                    (arg) => {
                        const {count} = arg
                        console.log(arg)
                        return (
                            <>
                            	....
                            </>
                        )
                    }
                }
            </CounterConsumer>
        )
    }
}
```



### 将函数组件转换成 class 组件

通过以下五步将 `Clock` 的函数组件转成 class 组件：

1. 创建一个同名的 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)，并且继承于 `React.Component`。
2. 添加一个空的 `render()` 方法。
3. 将函数体移动到 `render()` 方法之中。
4. 在 `render()` 方法中使用 `this.props` 替换 `props`。
5. 删除剩余的空函数声明。



### 生命周期

生命周期：**挂载--- 更新--- 卸载**

**挂载**

当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：

* constructor()
* static getDerivedStateFromProps()
* render()
* componentDidMount()
  * `componentDidMount()` 会在组件挂载后（插入 DOM 树中）立即调用。依赖于 DOM 节点的初始化应该放在这里。

**更新**

当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：

* static getDerivedStateFromProps()
* shouldComponentUpdate()
  * 如果 [`shouldComponentUpdate()`](https://react.docschina.org/docs/react-component.html#shouldcomponentupdate) 返回值为 false，则不会调用 （性能优化方式）
* render()
* getSnapshotBeforeUpdate()
* componentDidUpdate()

**卸载**
当组件从 DOM 中移除时会调用如下方法：

* componentWillUnmount()
  * 在组件卸载及销毁之前直接调用

![ReactLiftCycle](E:\React\ReactLiftCycle.png)



### Hook

**概念**：让你在不编写 class 的情况下使用 state 以及其他的 React 特性。

* State Hook
* Effect Hook     *Effect Hook* 可以让你在函数组件中执行副作用操作



### redux

**概念**： **Redux 是 JavaScript 状态容器，提供可预测化的状态管理。**可以让你构建一致化的应用，运行于不同的环境（客户端、服务器、原生应用），并且易于测试。

包括：`动机、核心概念、三大原则`

安装：

```bash
$ npm install --save redux

# react 绑定库和开发者工具
$ npm install --save react-redux
$ npm install --save-dev redux-devtools
```

引入redux：

```js
import { createStore } from 'redux'

// 创建 Redux store 来存放应用的状态。
// API 是 { subscribe, dispatch, getState }。
const store = createStore(renducer)

// 可以手动订阅更新，也可以事件绑定到视图层。
store.subscribe(() => console.log(store.getState()))

// 改变内部 state 惟一方法是 dispatch 一个 action。

console.log(store) // dispatch-   getState等参数
// getState就是state初始化的数据的数组
```

渲染： 

1. 引入 `redux` ，创建 `store` 实例， 
2. 引入纯函数 `reducer` 关联的 `state` 和`action` ，
3. 通过父传子 `this.props.store.getState()` 方法获取到 `state `初始化的内容；
4. 创建储存内容的变量，遍历变量，绑定 key 的 `ID` ，通过 `JSX` 语法渲染



绑定事件：

1. `onClick ={}`；点击事件里面是一个函数；
2. 通过 `dispatch（`） 方法 把 action 发送到 `renducer `里面；
3. 初始化设置为空，设置`componentDidMonut()` 方法 渲染；



多个reducers时：

1. 通过新建一个 `reducers` 目录下的 `index.js` 文件
2. 从 redux 引入 `combineReducers`  进行合并

```js
import { combineReducers } from 'redux'

import  xx from './xx'

export default combineReducers({
    xx,
    ...
})
```





##### 动机

**JavaScript 需要管理比任何时候都要多的 state （状态）**state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等。



##### 核心概念

* **state**

是一个对象，保存状态数据，不能直接修改state对象属性值

* **action**

是一个普通的对象，在 action 对象中必须包含一个 type 属性，指明动作类型，修改状态时所需要使用到的数据通常在 action 对象中使用 payload 属性来携带。（修改state状态就在action里面修改。）

```js
# reducers
# 可新建reducers的文件夹 放要修改的东西
//状态初始化的内容
const initState = []	// 可能是一个对象

// 暴露出去
// 这是一个 reducer，形式为 (state, action) => state 的纯函数。
// 使用 `switch` 语句和字符串来做判断
export default (state = initState, action) => {
    // 判断，更新状态
    switch (action.type) {
        
    }
}
```





##### 三大原则

* **单一数据源**

整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中

* **State 是只读的**

唯一改变 state 的方法就是触发（dispatch） action，action 是一个用于描述已发生事件的普通对象。

* **使用纯函数来执行修改**

为了描述 action 如何改变 state tree ，你需要编写 reducers



### React redux

官网： https://react-redux.js.org

connect()	连接

provider()	共享的

```bash
# 安装
$ npm install --save react-redux
```

```js
// 引入
import { Provider,Connect } from 'react-redux'

render(
  // 通过<Proider store={}>  传输共享的数据     </Provider>
  <Provider store={store}>
    <App />
  </Provider>,
  document.querySelector("#root")
)
```



### react-router-dom

```bash
# 安装
$ npm install --save react-router-dom
```

```js
// 引用
import { HashRouter as Router } from 'react-router-dom'

render(
  <Router>
    <App />
  </Router>,
  document.querySelector("#root")
)
```

* BrowserRouter ( history 模式)

  ```js
  import { BrowserRouter } from 'react-router-dom'
  
  <BrowserRouter
    basename={optionalString}// 基名
    forceRefresh={optionalBool}// 强制刷新
    getUserConfirmation={optionalFunc}//  getUserConfirmation
    keyLength={optionalNumber}
  >
    <App/>
  </BrowserRouter>
  ```

* HashRouter（ Hash 模式 ( # )）

  ```js
  import { HashRouter } from 'react-router-dom'
  
  <HashRouter>
    <App/>
  </HashRouter>
  ```

* Link（点击跳转）

  ```js
  import { Link } from 'react-router-dom'
  
  <Link to="/about">首页</Link>
  或
  <Link to="/courses?sort=name" />
  ```

* Redirect（重定向）

  * exact 精确的

  ```js
  <Redirect to="/Home" />
  或
  <Redirect
    to={{
      pathname: "/login",
      search: "?utm=your+face",
      state: { referrer: currentLocation }
    }}
  />
  或
  <Redirect from="/accounts" to="/users" />
      
  ```

* Route 配置路由路径（设置跳转路径 path 、组件 component ）

  ```js
  import { BrowserRouter as Router, Route } from 'react-router-dom'
  
  <Router>
    <div>
      <Route exact path="/" component={Home}/>
      <Route path="/news" component={NewsFeed}/>
      <Route path="/news" render={
          () => {
              return () {
                  <div>
                  </div>
              }
          }
      }/>
    </div>
  </Router>
  ```

* Switch（类似 js中的 switch 标签）

  ```js
  <Switch>
    <Route exact path="/" component={Home}/>
    <Route path="/:user" component={User}/>
    <Route component={NoMatch}/>
        ...
  </Switch>
  ```





###  UI（Ant Design）

`antd` 是基于 Ant Design 设计体系的 React UI 组件库，主要用于研发企业级中后台产品。

**特性**：

- 提炼自企业级中后台产品的交互语言和视觉风格。
- 开箱即用的高质量 React 组件。
- 使用 TypeScript 构建，提供完整的类型定义文件。
- 全链路开发和设计工具体系。



```bash
# 安装
$ npm install antd --save
$ yarn add antd
或
使用 script 和 link 标签直接引入文件，并使用全局变量 antd。
```

* 安装 AntD 包

* 高级配置 `AntD`， 按需引入样式 ，`js` 等

  安装**`react-app-rewired customize-cra` **、

* 设置 `package.json` 弹射

* 创建 `config-overrides.js`文件

* 使用 **`babel-Pulgin-import`**（按需引入的包）

* 配置完毕后需要重启任务 `npm start`

  - 这里是配置` antd` :

  1. 先使用 cra 创建应用
  2. 添加 antd 支持

```bash
$ npm i antd -S
```

​			3.配置按需引入，先安装包

```bash
$ npm i react-app-rewired customize-cra babel-plugin-import -D
```

```js
/* package.json */
"scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test",
+   "test": "react-app-rewired test",
}
```

​		4.创建配置文件 config-overrides.js

```js
const { override, fixBabelImports } = require('customize-cra');
module.exports = override(
    fixBabelImports('import', {
        libraryName: 'antd',
      libraryDirectory: 'es',
        style: 'css',
  }),
)
```

5. 在需要使用 antd 组件的地方引入即可

6. 国际化( 中文 )

   ```js
   import { LocaleProvider } from 'antd'
   import zhCN from 'antd/es/locale-provider/zh_CN'
   
   <LocaleProvider locale={zhCN}>
   <App />
   </LocaleProvider>
   ```

   

* 若是要自定义主题

  * 安装  ` less`  和 `less-loader` (Vue里面的 `sass` 和 ` node-sass` )

    ```
    yarn add less less-loader
    ```

  * 配置  `package.json `  和  `config-overrides.js`
  
    ```
    - const { override, fixBabelImports } = require('customize-cra');
    + const { override, fixBabelImports, addLessLoader } = require('customize-cra');
    
    module.exports = override(
      fixBabelImports('import', {
        libraryName: 'antd',
        libraryDirectory: 'es',
    -   style: 'css',
    +   style: true,
      }),
    + addLessLoader({
    +   javascriptEnabled: true,
    +   modifyVars: { '@primary-color': '#1DA57A' },
    + }),
    );
    
    如果你在使用 babel-plugin-import 的 style 配置来引入样式，需要将配置值从 'css' 改为 true，这样会引入 less 文件。
    
    如果你是通过 'antd/dist/antd.css' 引入样式的，改为 antd/dist/antd.less
    ```
  
  * 修改主题的内容一般新建的文件 `  theme.js `， 最后通过 `module.export` 导出，在 `config-overrides.js `文件里面引入。
  
    ```js
    定制的样式：
    @primary-color: #1890ff; // 全局主色
    @link-color: #1890ff; // 链接色
    @success-color: #52c41a; // 成功色
    @warning-color: #faad14; // 警告色
    @error-color: #f5222d; // 错误色
    @font-size-base: 14px; // 主字号
    @heading-color: rgba(0, 0, 0, 0.85); // 标题色
    @text-color: rgba(0, 0, 0, 0.65); // 主文本色
    @text-color-secondary : rgba(0, 0, 0, .45); // 次文本色
    @disabled-color : rgba(0, 0, 0, .25); // 失效色
    @border-radius-base: 4px; // 组件/浮层圆角
    @border-color-base: #d9d9d9; // 边框色
    @box-shadow-base: 0 2px 8px rgba(0, 0, 0, 0.15); // 浮层阴影
    
    （改成字符串）
    less@
    sass $
    ```
  
    



### 复文本编辑

wangeditor 和  Ueditor

原理：` contenteditable ` 和 `document.execCommand`

```html
  <button onclick="bold()">加粗</button>
  <button onclick="bigger()">加大</button>
  <button onclick="changeColor()">变色</button>

  <script>
    function bold() {
      document.execCommand('bold')
    }

    function bigger() {
      document.execCommand('fontSize', null, '7')
    }

    function changeColor() {
      document.execCommand('foreColor', null, '#f00')
    }
  </script>
```





### Immutabe Data

​		一旦创建就不能更改的数据， 对 `immutable `对象的任何修改添加或者删除，都会创建一个新的 `immutable` 对象。

（持久化数据据结构）

npm包：`redux-immutable`

《函数式编程》



### Mobx

状态管理（类似React中的 redux）

官网： https://cn.mobx.js.org



### 可视化图表

echarts / D3 / AntV    数据可视化图

- echars.baidu.com  查看文档
- 安装 导入