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















