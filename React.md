## 概念

**react 是用于构建用户界面的 javascript 库**

react 三件套：react 、react-dom 、react-scripts、    react-rn（原生DOM）



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





