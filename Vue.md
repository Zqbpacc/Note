## Vue

vue.js : 即 **`渐进式JavaScript框架`** ;

官网：https://cn.vuejs.org/

Vue CLI ： https://cli.vuejs.org/

* 拉取2.X版本的Vue项目？

  ​	Vue CLI >= 3 和旧版使用了相同的 vue 命令，所以 Vue CLI 2 (vue-cli) 被覆盖了。如果你仍然需要使用旧版本的 vue init 功能，需要安装一个桥接工具.

  ```bash
  $ npm install -g @vue/cli-init
  # `vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
  vue init webpack my-project
  ```

  

* Vue是基于MVVM模式运行的，什么是MVVM？

```txt
MVVM 即: Model-View-ViewModel
	
​ Model :  		数据的拥有者，实现具体的业务逻辑。
​ View :  		具体的用户界面，如按钮、列表、图片。
​ ViewModel : 	校验用户输入;网络请求。展示层的逻辑，比如格式化字符串;其他不能放入 Model，与 View 无关的逻辑。
	

MVVM的优点：
​ MVVM 兼容 MVC，可以先创建一个简单的 View Model，再慢慢迁移。 
​ MVVM 使得 app 更容易测试，因为 View Model 部分不涉及 UI。

	MVVM 最好配合 binding 机制，Model 的变化需要同步到 View Model，View Model 的变化也需要同步到 View。ReactiveCocoa 就可以用来实现 binding，当然它能做的远远不止 binding。
```



* Loadsh的防抖动函数

  _debouce

  

* Loadsh的节流函数

  _lang

  

* _difference 方法

  _difference([1,2,3,4,5,], [1,2]）就会把后面数组的值有哪些就会在前面的妈的数组拿出来

  

* _pull 删除



* 层叠样式表规范OOCSS与BEM？

  ```html
  BEM代表块（Block），元素（Element），修饰符（Modifier）
  OOCSS代表面向对象的css
  ```





### 概念

​	Vue (读音 /vjuː/，类似于 view) 是一套用于 **`构建用户界面的渐进式框架`** 。与其它大型框架不同的是，Vue 被设计为可以 **`自底向上 逐层应用`**；Vue 的核心库只关注 **`视图层`**。

* 有哪些**`打包工具`**？

```html
 打包工具主要有WebPack、gulp、grout等
```

```html
WebPack和gulp对比：
	​ gulp就是为了规范前端开发流程，实现前后端分离、模块化开发、版本控制、文件合并与压缩、mock数据等功能的一个前端自动化构建工具。gulp是通过task对整个开发流程进行构建的。、
	
	​ WebPack是当下最热门的前端资源模块化管理和打包工具，他可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码块分隔，等到时机需要的时候在加载。通过loader的转换，任何形式的资源都可以视作模块，比如CommonJS模块、AMD模块、ES6模块、CSS、图片、JSON、Coffeescript、LESS等。
```



* **`生态系统`**（全家桶）

  ```html
  Core 、 Vuex 、 Vue-Router
  ```



### 响应式（双向绑定）

​	实现双向绑定**`（响应式）`**，自动修改数据：要用到 **`ES5 `** 提供的 **`Object.defineProperty()方法`** ，监控对数据的操作，从而可以自动触发数据同步。并且，由于是在不同的数据生触发同步，可以精确的将变更发送给绑定的视图，而不是所有的数据都执行一次检测。（AngularJS是采用 **`“脏值检测”`** 的方式）

​	Vue.js在 V2.x 版本里是用的 **`defineproperty`** 或者 **`defineproperties`** ，但是在新版本中用 **`proxy`** ，在IE8下的浏览器可能会用不了，这时浏览器一般会 **`特性检测`** 能否使用。

​	Vue可以被分割成一个个**复用的组件**；每个组件都有自己的css、html、js；

​	组件化和数据驱动。组件化：把整体拆分为各个可以复用的个体，数据驱动：通过数据变化直接影响bom展示，避免dom操作。	

```js
就是会自动修改：
    // 定义和设置属性
    // obj要在其上定义属性的对象  
    // prop要定义或修改的属性的名称
    // descriptor将被定义或修改的属性描述符
	​ defineProperty(obj, prop, descriptor)  // 定义一个
	​ defineProperties(obj, prop, descriptor // 可以定义多个
    
   eg: Object.defineProperty(obj, "key", {
  			enumerable: false,	// 是否可数的
  			configurable: false, // 是否可配置
 			writable: false,   	// 是否能重写
  			value: "static"
	   });
```



**defineProperty里面的原生的set和get方法**:

```js
// 在对象中添加一个属性与存取描述符的示例
var bValue;
Object.defineProperty(o, "b", {
  get : function(){
    return bValue;
  },
  set : function(newValue){
    bValue = newValue;
  },
  enumerable : true,
  configurable : true
});
	o.b = 38;
// 对象o拥有了属性b，值为38
// o.b的值现在总是与bValue相同，除非重新定义o.b
```



* **defineProperty实现响应式（操作DOM）**；

```js
<div id="app"></div>
<button onclick="setValue()">add</button>
<script>
    // 操作数据
    var xx;
    // 创建实例 方法
    const setAppText = () => {
      document.querySelector("#app").innerHTML = obj.x;
    } 
    // 创建点击之后增加的函数
    const setValue = () => {
      xx++;
      obj.x = xx;  // 给obj赋值为增加之后的值
    }
    // 创建defineproperty方法
    var obj = {};
    Object.defineProperty(obj, "x", {
     	// 每次取obj都会调用get
        get () {
        	return xx;
      	},
		// 每次设置obj都会调用set
      	set (newValue) {
       	 	xx = newValue;
        	console.log(xx);
        	setAppText();
      	}
    })
    obj.x = 20;
    // 调用方法   每次数据更新重新设置DOM
    setAppText();
</script>
```

* proxy实现响应式

  * 原生proxy

    Proxy 对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。

    ```js
    proxy的属性：
    	// handler包含陷阱（traps）的占位符对象。
    	// target 代理虚拟化的对象。它通常用作代理的存储后端。根据目标验证关于对象不可扩展性或不可配置属性的不变量（保持不变的语义）。
    	// traps 提供属性访问的方法。这类似于操作系统中陷阱的概念。
    
    let p = new Proxy({}, handler);
    let handler = {
        get: function(target, name){
            return name in target ? target[name] : 37;
        }
        
        set: function(obj, prop, value) {
        if (prop === 'age') {
          if (!Number.isInteger(value)) {
            throw new TypeError('The age is not an integer');
          }
          if (value > 200) {
            throw new RangeError('The age seems invalid');
          }
        }
    
        // The default behavior to store the value
        obj[prop] = value;
      }
    };
    ```

  * proxy响应式

    ```js
    <script>
        let pro = new Proxy({}, {
          set (obj, prop, value) {
            console.log({obj, prop, value});
            obj[prop] = value;
          },
    
          get (target, name) {
            console.log({target, name})
            return target[name]
          }
        })
        pro.x = 10;
        console.log(pro.x);
    </script>
    ```



##### 双向数据 / 单项数据

```html
单项数据：
	​ 单项数据流中，父组件给子组件传递数据，但反过来不可以传递，也就是说单项数据流是从最外层节点传递到子节点，它们只需从最外层节点获取props渲染即可，如果顶层组件的某个prop改变了，React会递归的向下遍历整个组件树，重新渲染所有使用这个属性的组件。React组件内部还具有自己的状态，这些状态只能在组件内修改；
	​ 单项数据流的数据流动方向可以跟踪，流动单一，追查问题的时候可以更快捷，缺点就是写起来不方便，要使视图发生改变就得创建各种action来维护；
	​ 在践行单向数据流的flux系的实现中，其实是在全局创建了一个单例的事件分发器，开发者必须显示的通过这个统一的事件机制做数据变更通知。


双向数据：
	​ React会递归的向下遍历整个组件树，重新渲染所有使用这个属性的组件。双向数据绑定是数据与视图双向绑定，React组件内部数据发生改变时，视图也改变，视图发生改变时，数据也将发生改变。
	​ 双向数据绑定的各种数据相互依赖，导致数据问题的源头难以被跟踪到；
	​ 双向绑定把数据变更的操作隐藏在框架内部，调用者并不会直接感知，在践行单向数据流的flux系的实现中，其实是在全局创建了一个单例的事件分发器，开发者必须显示的通过这个统一的事件机制做数据变更通知。
```



### 模板语法

​	Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析。

​	在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。

​	

​	**` bulma `**文档：

```html
官网：https://bulma.io/

Bulma是一个基于Flexbox的免费开源CSS框架，(类似于bootstrap)
```



##### 创建Vue

​	如何创建vue；

```html
<div id="id">
   	<!--内容 -->
</id>
<scripr>
const app = new Vue({
   	<!--选项 -->
    el: "#id",
    data: {},        // 数据
    methods: {}	     // 函数
    computed： {}    // 计算属性  每次数据发生改变都会重新寄算，可作为data使用
    				 // 计算属性是每次数据改变的时候才会重新计算，是会缓存的
    watch： {}    	// 监听
    filters： {}   	//过滤器
})
</scripr>
```

```js
组件树：

根实例
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```



##### 插值表达式

* 插值表达式里面代表是 **`javascript表达式`** ；

* 插值表达式不会解析html字符串，当作普通文本在渲染；

* 当指令和插值表达式同时存在的时候 **`指令`**生效；

```html
<div id="app">
    <!-- 插值表达式里面代表是javascript表达式 -->
    {{isHandsome}} 
</div>
<script>
    const app = new Vue({
      el: '#app',
      data: {
        isHandsome: true
      }
    })
</script>
```



##### 指令

​	指令 (Directives) 是带有 **`v-`** 前缀的特殊特性。指令特性的值预期是**单个 JavaScript 表达式** (`v-for` 是例外情况)。

​	指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM；

```html
指令
​ 渲染指令：
v-text		原样输出
v-html		解析html字符串
v-show		通过是否渲染来决定显示隐藏(能频繁切换显示隐藏; 通过display样式 display:none决定是否显示)
v-if		通过是否渲染来决定显示隐藏(不能频繁切换显示隐藏; 通过append，remove方法是否渲染)
v-else		渲染 (只作用于上一个兄弟的v-if; “必须写在一起，作用于上一级”)


​ 循环指令：
v-for		循环数字
            循环字符串
            循环对象
			循环数据渲染标签


​ 表单绑定
v-modle		<input>
			<textarea>
            <select>等
```



###### v-for

* 我们用 `v-for` 指令根据一组数组的选项列表进行渲染。`v-for` 指令需要使用 `item in items` 形式的特殊语法，`items` 是源数据数组并且 `item` 是数组元素迭代的别名。

  ```html
  <ul id="example-1">
    <li v-for="item in items">
      {{ item.message }}
    </li>
  </ul>
  
  <script>
  var example1 = new Vue({
    el: '#example-1',
    data: {
      items: [
        { message: 'Foo' },
        { message: 'Bar' }
      ]
    }
  })
  </script>
  ```



* 你也可以用 `of` 替代 `in` 作为分隔符，因为它是最接近 JavaScript 迭代器的语法：

  ```html
  <div v-for="item of items"></div>
  ```

  

* 在 `v-for` 块中，我们拥有对父作用域属性的完全访问权限。`v-for` 还支持一个可选的第二个参数为当前项的索引。

  ```html
  <ul id="example-2">
    <li v-for="(item, index) in items">
      {{ parentMessage }} - {{ index }} - {{ item.message }}
    </li>
  </ul>
  
  <script>
  var example2 = new Vue({
    el: '#example-2',
    data: {
      parentMessage: 'Parent',
      items: [
        { message: 'Foo' },
        { message: 'Bar' }
      ]
    }
  })
  </script>
  ```

  

* * 一个对象，你也可以用 `v-for` 通过一个对象的属性来迭代。

  ```html
  <ul id="v-for-object" class="demo">
    <li v-for="value in object">
      {{ value }}
    </li>
  </ul>
  
  <script>
  new Vue({
    el: '#v-for-object',
    data: {
      object: {
        title: 'How to do lists in Vue',
        author: 'Jane Doe',
        publishedAt: '2016-04-10'
      }
    }
  })
  </script>
  ```

  

* * 你也可以提供第二个的参数为 property 名称 (也就是键名);

  ```html
  <div v-for="(value, name) in object">
    {{ name }}: {{ value }}
  </div>
  ```



* * 第三个参数为索引；

  ```html
  <div v-for="(value, name, index) in object">
    {{ index }}. {{ name }}: {{ value }}
  </div>
  ```

  ​	在遍历对象时，是按 **`Object.keys()`** 的结果遍历，但是不能保证它的结果在不同的 JavaScript 引擎下是一致的。





###### v-model

* 你可以用 `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 `v-model` 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

* `v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

  ```html
  eg:
  ​ text和textarea元素使用value 属性和 input 事件；
  ​ checkbox和radio使用checked 属性和 change 事件；
  ​ select字段将value作为prop 并将 change 作为事件。
  ```



###### v-cloak

**解决页面卡顿**  :

​	当出现网路慢不能及时加载或者一个new Vue没有实例化的时候，div里面的模板语法是原样输出的，这时就可以用v-clock指令。

```html
<!-- 加上v-cloak这个指令以后，在vue实例化之前div身上就会有v-cloak这个属性，实例化之后这个属性就会被移除 -->
<!-- 解决页面卡顿给用户带来不好体验 -->
  <div id="app" v-cloak>
    {{msg}}
  </div>
  <script>
    // for(var i = 0; i < 1000000000000000000000; i++) {}
    setTimeout(() => {
      const app = new Vue({
      el: '#app',
      data: {
        msg: 'hello world'
      }
    })
    },2000)
  </script>
```

```html
 <style>
  [v-cloak] {
    display: none;
  }
  </style>
</head>
<body>
  <div id="app" v-cloak>
    {{msg}}
  </div>
  <script>
    setTimeout(() => {
      const app = new Vue({
        el: "#app",
        data: {
          msg: "hello world!"
        }
      })
    }, 2000);
  </script>
```





###### v-bind

简写: ：

v-bind 绑定一个属性；在绑定 `class` 或 `style` 特性时，支持其它类型的值，如数组或对象。

```html
<!-- class 绑定 -->
<div :class="[classA, { classB: isB, classC: isC }]"></div>
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">
<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>
```



```html
	<ul>
        <!-- 循环data数据，得到索引和元素值，循环渲染当前标签 -->
        <!-- 给每一个循环动态绑定一个唯一的key,这个key一般是一条数据的id,或者name,title之类的唯一标识 -->
        <li v-for="(like, index) in likes" :key="like.id">
          {{index}} : {{like.name}}
        </li>
      </ul>
```





###### v-on

简写 @;

​	绑定事件监听器(事件对象)。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。

```html
<!-- 方法处理器 -->
<button v-on:click="doThis"></button>
<!-- 缩写 -->
<button @click="doThis"></button>
```



* 事件处理函数在v-on监听的时候不写括号,函数的第一个参数就是事件对象;

* 事件处理函数在v-on监听的时候写了括号,那就可以传参,而且传一个特殊变量$event就是事件对象

```html
<!-- 内联语句 -->
<button v-on:click="doThat('hello', $event)"></button>
```



######　事件修饰符

* 在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()` 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。为了解决这个问题，Vue.js 为 `v-on` 提供了**事件修饰符**。

```html
.stop   		// 阻止冒泡
.prevent		// 默认事件
.capture		// 添加事件侦听器时使用 capture 模式。
.self			// 只当事件是从侦听器绑定的元素本身触发时才触发回调 子元素不触发
.once			// 只触发一次回调。
.passive		// {passive: true}模式添加侦听器
```

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>
```

```html
	使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。
```



* Vue 还对应 **`addEventListener `**中的 passive 选项提供了 **`.passive`** 修饰符。

```html
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

​	不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略 ;





######　按键修饰符

​	在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

```html
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```

​	你可以直接将 [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。

```html
<input v-on:keyup.page-down="onPageDown">
```





######　按键码

可以使用 `keyCode` 特性；

```html
<input v-on:keyup.13="submit">
<input v-on:keyup.enter="submit">
```

```html
常用的按键码的别名:
.enter
.tab
.delete (捕获“删除”和“退格”键)
.esc
.space
.up
.down
.left
.right
```





###### @input

v-bind可以把data数据绑定给value, @input把用户输入的值在去赋给data,这样实现了双向绑定

```html
<div id="app">
    <!-- v-bind可以把data数据绑定给value, @input把用户输入的值在去赋给data,这样实现了双向绑定 -->
   <input type="text" :value="username" @input="onInput">
   {{username}}
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        username: 'zhangsan'
      },
      methods: {
        onInput (e) {
          console.log(e.target.value)
          this.username = e.target.value
        }
      }
    })
  </script>
```





###### @change

```html
<div id="app">
    <h2>爱好</h2>
    <p><label>抽烟<input type="checkbox" value="抽烟" @change="onChange"></label></p>
    <p><label>喝酒<input type="checkbox" value="喝酒" @change="onChange"></label></p>
    <p><label>烫头<input type="checkbox" value="烫头" @change="onChange"></label></p>

    <p>{{likes.toString()}}</p>
</div>
<script>
    const app = new Vue({
      el: '#app',
      data: {
        likes: []
      },
      methods: {
        onChange (e) {
          // console.log(e.target.value)
          const val = e.target.value;
          if (this.likes.includes(val)) {
            // 这个爱好已经被选中了
            // 只留下不等于当前爱好的值(把当前的删掉)
            this.likes = this.likes.filter(like => like !== val);
          } else {
            // 这个爱好还没有选
            this.likes.push(val);
          }
        }
      }
    })
</script>
```





###### 获取焦点

原生：

```js
document.querySelector('input').focus();
```

Vue:

```js
// 在input添加实例
ref="focusInnput",

// 然后在methods函数里面表示
this.$refs.focusInput.focus()    // 获取原生对象this.$refs.
```



##### computed

computed：Vue的计算属性；

**特点** ：

* 计算属性  每次数据发生改变都会重新寄算，可作为data使用；
* 计算属性是每次数据改变的时候才会重新计算，是会缓存的；
* conputed：有一个set（）和 get（）属性和方法；

```html
<script src="vue.js"></script>
  <div id="app">
    <label>姓：<input type="text" v-model="xing"></label><br>
    <label>名：<input type="text" v-model="ming"></label><br>
    <label>姓名：<input type="text" v-model="name"></label><br>
  </div>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        xing: '',
        ming: ''
      },
      computed: {
        // 计算属性是每次数据改变的时候才会重新计算，是会缓存的
        name: {
          // return this.xing + this.ming
          get () {
            return this.xing + this.ming
          },
          set (val) {
            // val就是输入的姓名
            // 把姓名拆开设置
            console.log(val)
            this.xing = val.slice(0, 1)
            this.ming = val.slice(1)
          }
        }
      }
    })
  </script>
```





##### filter

```html
<h5>{{goods.title | toUpper}}</h5>
 <!-- 竖线之后写过滤器的名字，就会把前面值传递给过滤器，过滤器处理之后再作为插值表达式来显示 -->
<p>{{goods.price | toFix}}</p>

<script>
filters: {
        // 定义一个过滤器，接收要过滤的值，返回过滤的结果
        toFix (val) {
          return val.toFixed(2)
        },
        toUpper (val) {
          return val.toUpperCase()
        }
}
</script>
```





##### 获取数据

​	获取数据：**fetch** 、**axios**

​	开放的数据接口 : jsonplaceholder 

​	官网：https://jsonplaceholder.typicode.com/

* **fetch**

  ​	Fetch API 提供了一个 JavaScript接口，用于访问和操纵HTTP管道的部分，例如请求和响应。它还提供了一个全局 fetch()方法，该方法提供了一种简单，合理的方式来 **`跨网络异步获取资源`**。

  ​	这种功能以前是使用  **`XMLHttpRequest`**实现的。Fetch提供了一个更好的替代方法，可以很容易地被其他技术使用，例如 Service Workers。

  ```js
  fetch请求设置：
  fetch('http://example.com/movies.json')
    .then(function(response) {
      return response.json();
    })
    .then(function(myJson) {
      console.log(myJson);
    });
  ```

  

  ```js
  <script>
      // fetch返回的是一个promise
      console.log(fetch)
      // 原生支持的fetch
      // 再第一个then里得到的是fetch封装过一次的response，所以需要调用一次json()方法，解析成json数据
      // 再第二个then里就能得到后端返回回来的resp了
      fetch('https://jsonplaceholder.typicode.com/todos')
        .then(resp => resp.json())
        .then(resp => {
          console.log(resp)
        })
   </script>
  ```





* **axios**

  ```html
  引入方法：	
  ​	通过<script src="https://unpkg.com/axios/dist/axios.min.js"></script>引入；
  ​	直接安装
  	npm install axios
  ```

  

  * 使用 axios；

  ```js
  	使用axios是通过创建一个axios实例，通过这个新建的实例挂载到 Vue 的原型prototype上（Vue.prototype.$http）,这样每一个Vue的实例都可以调用$http的方法
  
  默认下axios的配置：
  var instance = axios.create({
    baseURL: 'https://some-domain.com/api/',
    timeout: 1000,
    headers: {'X-Custom-Header': 'foobar'}
  });
  ```

  ```js
  	// 创建一个axios的实例
  	// 使用这个实例可以在整个项目当中去发送axios请求
  	const ajax = axios.create({
    		// 配置所有请求的baseUrl
    		baseURL: 'https://jsonplaceholder.typicode.com'
  	})
  
  	
        // 拦截器    (在实例身上写)在axios请求发出之前和响应之后做一些预处理工作
      ajax.interceptors.request.use(config => {
        // 做一些请求发出去的时候做一些处理
        // 必须return config
        return config
      })
  
      ajax.interceptors.response.use(resp => {
        // 数据返回之后做一些全局预处理
          
        // 在请求相应的时候集中做错误处理，一般一个项目的接口返回的数据格式是基本一致的
        }
  
  
  	// 在真实项目当中我们一般会把这个实例挂载到Vue的原型上
  	// 这样每一个Vue的实例都能调用这个$http方法了
  	Vue.prototype.$http = ajax
  ```

  



### 组件

​	组件是**`可复用`**的 Vue 实例，

​	组件： component

##### 注册组件

​	注册组件可以 **`全局注册`** 和 **`局部注册`**； 

​	全局注册组件在每一个Vue实例都可以使用；局部注册组件只能在当前实例中使用

```html
全局注册：
<div id="app1">
<!-- 注册的组件大驼峰命名，在html里面使用这个组件的时候需要把大写变为小写，然后使用中线连接 -->
   <hello-vue></hello-vue>
</div>

<script>
 Vue.component('HelloWorld', {
      template: '<div>hello world</div>'
 })
</script>



局部注册：
<script>
	// 定义一个组件
    const HelloVue = {
      template: '<h2>hello Vue</h2>'
    }
    
	const app = new Vue({
      el: '#app',
      components: {
          HelloVue
      },
      // 组件的data必须是一个方法，因为每个组件的数据是独立的，使用方法可以保证不共享，return一个对象  
      data () {
          return {}
      },   
      // 组件内部的props可以直接作为data使用  []or{}
      props: [''],
      created () {}
      
    })
</script>
```



#####　props

```html
props的大小写：
1、props绑定驼峰方式要改写成中线;
2、html属性名用中线，javascript使用驼峰;
3、自定义事件也要用中线而不用驼峰;
```



prop : 处理数据传输；

```html
1. 传递数字或者boolean需要绑定，否则传递过去以后解析成字符串 
2. 它是一种单向数据流，即只能父组件向子组件传输数据，不能子组件向父组件传递，
```





##### 自定义事件

* 实现 **`父 => 子组件传输`**  props ;

* 实现 **`子 => 父组件传输`**  this.$emit ;

* 实现 **`兄 => 弟组件传输`**  event bus （事件总线）；

```html
监听子组件的自定义事件，当子组件$emit这个事件的时候，父组件的这个方法就会响应执行
```

```html
<div id="app">
    <text-areac :num="num" @add-num="onComponentNum"></text-areac>{{num}}
</div>
<script>
    const TextAreac = {
      template: '<div>{{num}}<button @click="onAddNum">Add</button></div>',
      props: ["num"],
      methods: {
        onAddNum () {
          // 子组件的props一般不允许直接修改
          this.$emit('add-num', {
            num: this.num + 1
          })
        }
      }
    }
    const app = new Vue({
      el: "#app",
      data: {
        num: "1"
      },
      components: {
        TextAreac
      },
      methods: {
        onComponentNum (data){
          this.num = data.num
        }
      }
      
    })
  </script>
```



event bus是通过 **`空的vue实例`**来进行两个兄弟组件之间的数据传输;

```html
<script>
	const bus = new Vue()
    const ge = {
      template: '<div><span @click="onDawodi">打我弟</span></div>',
      methods: {
        onDawodi () {
          // 在点击的时候触发这个wuwuwu事件，di这个组件就能响应这个事件
          // 让bus触发一个自定义事件
          bus.$emit('wuwuwu', {
            kusheng: 'yinyinyin'
          })
        }
      }
    }
    const di = {
      template: '<div><span>{{ku}}</span></div>',
      data () {
        return {
          ku: ''
        }
      },
      created () {
        // 一上来就要监听事件总线的wuwuwu事件
        bus.$on('wuwuwu', (data) => {
          // 响应ge组件里通过bus给我emit的这个wuwuwu事件
          // 接收到传递给我的参数data
          console.log(data)
          this.ku = data.kusheng
        })
      }
    }
    const app = new Vue({
      el: '#app',
      components: {
        ge,
        di
      }
    })
</script>
```



**template**

```html
<template id="tempID">
    <div>
          
    </div>
</template>
<script>
    const Temp = {
      template: "#tempID"
    }
</script>
```



##### 单页应用

页面跳转 =>js渲染

```html
优点：页面切换快
	页面每次切换跳转时，并不需要做html文件的请求，这样就节约了很多http发送时延，我们在切换页面的时候速度很快。


缺点：首屏事假稍慢，SEO差
	单页应用的首屏时间慢，首屏时需要请求一次html，同时还要发送一次js请求，两次请求回来了，首屏才会展示出来。相对于多页应用，首屏时间慢。
SEO效果差，因为搜索引擎只认识html里的内容，不认识js的内容，而单页应用的内容都是靠js渲染生成出来的，搜索引擎不识别这部分内容，也就不会给一个好的排名，会导致单页应用做出来的网页在百度和谷歌上的排名差。
```



#####  双页应用

每一次页面跳转的时候，后台服务器都会给返回一个新的`html`文档，

```html
优点：首屏时间快，SEO好
```



##### 动态组件

通过 ： **`  is` **属性设置

```html
<template id="guonei">
    <div>
      华为手机要升级了
    </div>
</template>
<template id="guoji">
      <div>
        apple Jobs deid
      </div>
</template>
<div id="app">
  <div>
      <span @click="news = 'guonei'">国内新闻</span>
      <span @click="news = 'guoji'">国际新闻</span>
  </div>
  <component :is="news"></component>
</div>

  <script>
    // 创建组件
    const guonei= {
      template: '#guonei'
    }
    // 创建组件
    const guoji= {
      template: '#guoji'
    }
    const app = new Vue({
      el: '#app',
      data: {
        news: 'guoji'
      },
      // 注册组件
      components: {
        guonei,
        guoji
      }
    })
  </script>
```



##### slot插槽

slot： **`占位`**属性

常用于电商 如是否包邮、降价等场合；

```html
slot 占位属性： <slot></slot>
	 命名： <slot name=""></slot>

1. 在使用组件的时候，决定是否需要某个DOM元素，需要的话就写在组件内部，在template里面的<slot>就会被写入的这个DOM元素替换 -->
2. 多个slot写上name属性，在使用的时候slot="slot的name"就可以对应起来了
```

```html
<template id="hello">
    <div>
      <slot name="a"></slot>
      商品名称
      <slot name="b"></slot>
    </div>
</template>

<div id="app">
    <!-- 多个slot写上name属性，用name对应，此处与书写顺序无关-->
      <hello>
      <b slot="b">包邮</b>
      <b slot="a">打九折</b>
    </hello>
</div>

  <script>
    // 定义一个组件
    const Hello = {
      template: '#hello'
    }
    const app = new Vue({
      el: '#app',
      components: {
        Hello
      }
    })
  </script>
```



##### tr

​	在组件中表单table里面的thead、tbody、tfood里面只能是tr，ul里面只能是li，所以只能用动态组件**`is属性`**来绑定；

```html
<template id="my-tr">
    <tr>
      <td>{{id}}</td>
      <td>{{name}}</td>
      <td>{{price}}</td>
    </tr>
  </template>

  <div id="app">
    <table>
      <thead>
        <tr>
          <th>编号</th>
          <th>名称</th>
          <th>价格</th>
        </tr>
      </thead>
      <tbody>
        <!-- tbody里只能是tr，所以这个地方需要使用动态组件，加上is属性 -->
        <tr
          is="my-tr"
          tag="tr"
          v-for="goods in goodsList"
          :key="goods.id"
          :id="goods.id"
          :name="goods.name"
          :price="goods.price"
        ></tr>
      </tbody>
    </table>
  </div>

<script></script>
```





##### 组件的过渡

​	Vue 提供了 **`transition`** 的封装组件，在需要添加过渡属性的标签外面加上`<transitioin>`标签就可以设置过渡属性。

```html
<transition>
   <div :is="show ? 'guonei' : 'guoji'"></div>
 </transition>
```

* 在进入/离开的过渡中，会有 6 个 class 切换 ;

```html
v-enter：定义进入过渡的开始状态。

v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。

v-enter-to:定义进入过渡的结束状态。

v-leave: 定义离开过渡的开始状态。

v-leave-active：定义离开过渡生效时的状态。

v-leave-to:定义离开过渡的结束状态。
```



* 可以通过**`name`**属性为某一个属性设置样式 ;

  ```html
  name-enter					name-leave
  name-enter-active			name-leave-active
  name-enter-to				name-leave-to
  ```



* 可以通过为transition标签设置单独的class样式自定义过渡样式； 但是当为多个标签添加transition样式时，则要设置 `name` 属性

  * 可以用 **`animate.css`**设置过渡样式

    网址 : https://daneden.github.io/animate.css/

  ```html
  <transition
        mode="out-in"
        leave-to-class="lightSpeedOut"
        enter-active-class="animated"
        leave-active-class="animated"
        enter-to-class="lightSpeedIn"
  >
      <div :is="show ? 'guonei' : 'guoji'"></div>
  </transition>
  ```



* 过渡模式： 同时生效的进入和离开的过渡不能满足所有要求;

  ```html
  in-out：新元素先进行过渡，完成之后当前元素过渡离开。
  
  out-in：当前元素先进行过渡，完成之后新元素过渡进入。
  ```





##### 生命周期

生命周期：创建  挂载  更新  销毁

​	每一个阶段都可以当作是一个函数；在实例生命周期的不同阶段被调用，如 [`mounted`](https://cn.vuejs.org/v2/api/#mounted)、[`updated`](https://cn.vuejs.org/v2/api/#updated) 和 [`destroyed`](https://cn.vuejs.org/v2/api/#destroyed)。生命周期钩子的 `this` 上下文指向调用它的 Vue 实例。 $nextTick函数在为DOM操作前放进去。



##### 虚拟DOM

```html
1、根据真实DOM构建一个虚拟DOM（js对象）
2、当DOM要修改的时候，会先修改虚拟DOM
3、用修改之后的虚拟DOM跟修改之前的进行脏检查 （diff算法）
4、把修改过后的那一部分重新渲染真实DOM
5、可以避免多次的DOM操作
```





### Vue CLI

VUE.JS标准的开发工具

1、全局安装Vue CLI；

```html
npm i -g @vue/cli
```

2、创建项目；

```html
vue create 项目名
(之后会自动安装babel：:ES6转ES5和eslint:代码规范)
```

EsLint代码规范：https://cn.eslint.org/

导入---注册--- 显示

vetur插件：sc



### router

路由作用：在单页应用中**`实现组件之间的跳转`**。

router的模式：hash  （#）、history；

```html
mode="history"
```



* **router的引入**；

```js
// 引入vue
import Vue from 'vue'
// 引入vue-router
import Router from 'vue-router'

// 引入需要配置的组件
import Home from './views/Home'

// 使用路由
Vue.use（router);

// 得到router的实例，并且导出
export default new Router({
    // 通过routes字段配置路由
  routes: [
      {
      	path： “”，  		// 地址
      	name： “”，  		// 名称
        component：“”，	// 组件名
        // 路由的嵌套
        children：[{}]
      }
  ]
```

路由的嵌套：通过**`children`**属性**`嵌套子路由`**；



* **router的渲染**；

```html
 <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
</p>


  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
<router-view></router-view>


 <!-- 进行多个渲染是可以进行命名 -->
<router-view name=""></router-view>
```



##### 命名路由

**路由传参**

```html
<router-link to="/list/man">男装</router-link>
```

**动态绑定**

传的是一个对象

```html
 <router-link :to="{ name: 'category', params: {cateName: 'woman'} }">女装</router-link>
或者
 <router-link :to="{ name: 'category', params: {cateName: 'kid', start: 0}, query: {end: 20}}">童装</router-link>
```



* **编程式的导航**

  ​	导航到不同的 URL，则使用 **`router.push`** 方法。类似于 `window.localtion.href` 打开新的网页；而当点击 `<router-link>` 时，这个方法会在内部调用，所以说，点击 `<router-link :to="...">` 等同于调用 `router.push(...)`。

  | 编程式           | 声明式                    |
  | ---------------- | ------------------------- |
  | router.push(...) | `<router-link :to="...">` |

  ```js
  // 字符串
  router.push('home')
  
  // 对象
  router.push({ path: 'home' })
  
  // 命名的路由
  router.push({ name: 'user', params: { userId: '123' }})
  
  // 带查询参数，变成 /register?plan=private
  router.push({ path: 'register', query: { plan: 'private' }})
  ```

  

##### mate

mate : 元信息

* 定义路由的时候可以配置 `meta` 字段：

```js
const router =new Router({
    routes:[
    	path: '/home',
    	alias: '/',  		// 别称
   	 	name: 'home',
   	 	meta: {isAuthRequired: false}
    ]
}) 
```



* 如何访问meta字段？

```html
	一个路由匹配到的所有路由记录会暴露为 $route 对象 (还有在导航守卫中的路由对象) 的 $route.matched 数组。因此，我们需要遍历 $route.matched 来检查路由记录中的 meta 字段。
```





##### 重定向和别名redirect

* redirect有一个 to 属性

```js
export default new Router({
  routes: [
	{
        redirect: to => {
        if (to.meta.isAuthRequired) {
          // 这个组件需要权限验证
          if (!isLogin) {			// 判断
            return '/login'    		// 没有登录就走登录页面
          } else {
            return '/list/man'		// 登录了就走list页面
          }
        }
      }
	}
  ]
 )}
```

* 重定向也是通过 `routes` 配置来完成，下面例子是从 `/a` 重定向到 `/b`：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})
```

* 甚至是一个方法，动态返回重定向目标：

```js
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```

别名： **/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。**





##### 命名视图

​	有时候想同时 (同级) 展示多个视图，而不是嵌套展示，你可以在界面中拥有多个单独命名的视图，而不是只有一个单独的出口。如果 `router-view` 没有设置名字，那么默认为 **`default`**。

```html
<router-view name="a"></router-view>
```

```js
components: {
   default: Category,
   a: Test
}
```



 ##### SCSS

lang="scss"是一个可编程css；

```html
<!-- 可以再vue文件中style属性添加lang=“scss”生成scss，此时就可以写scss代码,然后安装插件才能运行 -->
<style lang="scss">
</style>
```



转scss的插件有less-loader或者scss-loader

```html
npm install sass-loader node-sass --save-dev
```

 可用&进行拼接 (前面一样的用&表示)



* 如何保证样式只在当前页才能使用？

```html
<!-- 在style中欧添加 scoped ，这时浏览器会自动加上一个属性选择器[]，这样就只在当前应用这个样式 -->
<style scoped>
	.text {
	 	color: #a00;
	}
</style>
```



* 如何指定router-link 标签？

  router-link会自动渲染成 a 标签，我们可以指定它渲染成其他的标签，这时加上 **`tag=“ ” `** 就会成对应的标签；

  ```html
  <!-- 会渲染成span标签 -->
  <router-link tag="span" :to="{ name: 'category', params: {cateName: 'woman'} }">女装</router-link>
  ```

  

* 带有自动激活的 CSS class 的链接

  带有自动激活的 CSS，浏览器会自定添加class标签，可以单独为设置class标签样式

  



##### 导航守卫

`	vue-router` 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。

* 全局导航守卫 `router.beforeEach(to, from, next)  `,

  一般用于全局的权限验证，在每一次导航发生改变（路由跳转）之前都会进入这个钩子函数，在这个函数里只有调用了 **`next（）`**才会跳转;

```js
const router = new Router({...})

router.beforeEach((to, from, next) => {
  // console.log({ to, from, next })
  // 判断当前要跳转的那个组件是否需要权限
  if (to.meta.isAuthRequired) {
    // 验证是否已经登录
    if (isLogin) {
      next()
    } else {
      // 没有登录就中断当前导航，进入新的导航（登录）
      next({path: '/login'})
    }
  } else {
    // 不需要权限验证，直接进入当前导航
    next()
  }
})
```



* 局部导航守卫 `beforeRouteUpdate（to, from, next）`, 可以访问组件实例 `this` ，

  ```js
  // 在当前路由改变，但是该组件被复用时调用
  // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
  // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
  // 可以访问组件实例 `this`
  beforeRouteUpdate (to, from, next) {
      // console.log({to, from, next})
      // console.log(to.params.cateName)
      this.cateName = to.params.cateName
      // 调用方法
      this.getData()
      next()
    },
  methods: {
      // 发送ajax请求渲染当前分类页
      getData () {
          
      }      
  }
  ```



* 局部导航守卫 `beforeRouteEnter` ,进入路由之前渲染， 它只会在进入页面前的时候渲染一次，并且不能调用 `this`；

  *  `beforeRouteEnter`  中的 next 属性可以传递一个回调函数，可以把回调函数的形参当作 this；

  ```js
  beforeRouteEnter (to, from, next) {
      // 在渲染该组件的对应路由被 confirm 前调用
      // 不！能！获取组件实例 `this`
      // 因为当守卫执行前，组件实例还没被创建
  
      
      // 在next里可以传递一个回调函数，这个回调函数的第一个形参就是this
      next(vm => {
        console.log(vm)
        vm.cateName = to.params.cateName
        vm.getData()
      })
    }
  ```

  



##### 路由懒加载

​	**定义**： 当打包构建应用时，JavaScript 包会变得非常大，主要包括许多打包程序，影响页面加载。于是把不同路由对应的组件分割成不同的 `代码块 `，然后当路由被访问的时候才加载对应组件，这样就会更加高效。

​	**使用**： 结合 Vue 的[异步组件](https://cn.vuejs.org/v2/guide/components-dynamic-async.html#%E5%BC%82%E6%AD%A5%E7%BB%84%E4%BB%B6)和 Webpack 的[代码分割功能](https://doc.webpack-china.org/guides/code-splitting-async/#require-ensure-/)，轻松实现路由组件的懒加载。

* 可以将异步组件定义为返回一个promise的工厂函数

  ```js
  // 此时返回的是一个promise，异步
  const Home = () => import('./views/Home')
  ```

  * promise 与 import 引入组件的区别：

  ```js
  import Home from './views/Home'
  ```



#####  把组件按组分块

  	把某个路由下的所有组件都打包在同个异步块 (chunk) 中。只需要使用 [命名 chunk](https://webpack.js.org/guides/code-splitting-require/#chunkname)，一个特殊的注释语法来提供 chunk name； 

```js
const Home = () => import(/* webpackChunkName: "group-foo" */ './Home.vue')
const List = () => import(/* webpackChunkName: "group-foo" */ './List.vue')
const Baz = () => import(/* webpackChunkName: "group-foo" */ './Baz.vue')
```

Webpack 会将任何一个异步模块与相同的块名称 "group-foo" 组合到相同的异步块中。



### Vuex

​	Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

![](https://vuex.vuejs.org/flow.png)

```html
状态自管理应用的几个部分：
state: 驱动应用的数据源
view: 以声明的方式将state映射到视图
actions： 响应在view上的用户输入导致的状态变化
```

当遇到**`多个组件共享状态`**时，单个数据流的简洁性很容易被破坏：

* 多个视图来与同一状态；
* 来自不同视图的行为需要变更同一状态；

![](https://vuex.vuejs.org/vuex.png)

使用VueX：

* 创建Vue文件时选择VueX
* 通过npm安装       **`npm install vuex --save`** 或 **`yarn add vuex`**

新建store目录， 

index.js   引入Vue和VueX，

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export deault new Vue.store({
    state: {},
    moudles: {},
    getter: {},
    mutation: {},
    action: {}
})
```



辅助函数：mapState(生成计算属性)

单独引入函数

```js
import {{ mapState }} from 'vuex'
export default ({
    computed： {
    
})
```



Github：shopping-care__ https://github.com/vuejs/vuex/blob/dev/examples/shopping-cart/store/index.js

```html
state 全局状态管理

mutation： 修改state状态

action： 处理异步逻辑在通过mutation修改状态

mutationType: 状态的分类管理（集中管理：使用常量）

getter： 处理逻辑
```



##### VueX的严格模式

​	Vuex的开发环境 process.env.NODE_ENV  === "development"     true		

```js
import Vue from 'vue'
import Vuex from 'vuex'

import state from './state'

Vue.use(Vuex)

export default new Vuex.Store({
  strict: process.env.NODE_ENV === 'development',
  state,
  ..
})
```





##### VueX混入mixins

​	mixins混入用来分发Vue组件中的可复用功能

```js
Vue.mixins({
    
})
或
var mixin = {
}
new Vue({
  mixins: [mixin]
})
```



**全局混入**

```js
全局混入会影响每一个Vue实例
Vue.mixins({})
new Vue({})
```



##### 服务端渲染

​	服务端渲染 serve side render（SSR）：将组件或页面（js代码）通过服务器生成html字符串，再发送到浏览器，最后将静态标记"混合"为客户端上完全交互的应用程序。

​	此外还有：csr客户端渲染、bsr浏览器渲染

```html
SSR的优势：
1.跟利于SEO优化；
	服务端渲染返回给客户端的是已经获取了异步数据并执行JavaScript脚本的最终HTML，网络爬中就可以抓取到完整页面的信息。
2.更有利于首屏渲染；
	首屏的渲染是node发送过来的html字符串，并不依赖于js文件了，这就会使用户更快的看到页面的内容。尤其是针对大型单页应用，打包后文件体积比较大，普通客户端渲染加载所有所需文件时间较长，首页就会有一个很长的白屏等待时间。

SSR的局限：
1.服务器的压力过大；（更容易出现高并发状况，大量占用服务端CPU资源）；
2.开发条件受限；
	在服务端渲染中，只会执行到componentDidMount之前的生命周期钩子
3.学习成本相对较高；
	除了对webpack、React要熟悉，还需要掌握node、Koa2等相关技术。相对于客户端渲染，项目构建、部署过程更加复杂。
```



如何实现服务端渲染？

通过Vue可以使用**`Nuxt.js `**来使用服务器渲染；

Nuxt.js官网： https://zh.nuxtjs.org/；

* 安装

```js
npx create-nuxt-app <项目名>
    或
yarn create nuxt-app <项目名>
```

​	npx和npm类似，npx区别于若是当前没有需要安装的包，那么npx就会给你安装下来，当你使用后就会自动清除。

* 之后将会根据需求进行选择项目

  ```html
  1.在集成的服务器端框架之间进行选择:
  None (Nuxt默认服务器)
  Express
  Koa
  Hapi
  Feathers
  Micro
  Adonis (WIP)
  
  2.选择您喜欢的UI框架:
  None (无)
  Bootstrap
  Vuetify
  Bulma
  Tailwind
  Element UI
  Ant Design Vue
  Buefy
  
  3.选择你想要的Nuxt模式 (Universal or SPA)
  4.添加 axios module 以轻松地将HTTP请求发送到您的应用程序中。
  5.添加 EsLint 以在保存时代码规范和错误检查您的代码。
  6.添加 Prettier 以在保存时格式化/美化您的代码。
  ```

* 勾选完后将安装所有依赖包，启动项目

  ```js
  // 进入目录
  cd ..
  // 运行项目
  npm run dev
  ```

  - default.vue里面的组件的 `<nuxt/>` ==== #app
  - 在pages里面新建 Vue文件





##### keep-alive

标签的实例在创建的时候可以被缓存下可以用 `keep-alive` 将动态组件包裹起来	

```html
<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
```

- **Props**：

  - `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。
  - `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
  - `max` - 数字。最多可以缓存多少组件实例。

- **用法**：

  `<keep-alive>` 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 `<transition>` 相似，`<keep-alive>` 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。

  ​	当组件在 `<keep-alive>` 内被切换，它的 `activated` 和 `deactivated` 这两个生命周期钩子函数将会被对应执行。

  ​	`keep-alive` 标签同时只能一个组件能被渲染，`keep-alive`时其用在一个直属的子组件被开关的情景

  如果里面有 `v-if` ，那么则不会工作。

  ```html
  <!--外层套transition过渡-->
  <transition>
      <keep-alive>
      	<compoment :is="view"></compoment>
      </keep-alive>
   </transition>
  ```

  

  * include 和 exclude 属性允许本地有条件的缓存，两者之间可以用逗号分隔字符串，正则表达式或一个数组	

  * 匹配首先检查组件自身的 `name` 选项，如果 `name` 选项不可用，则匹配它的局部注册名称 (父组件 `components` 选项的键值)。匿名组件不能被匹配。

    ```html
    <!-- 逗号分隔字符串 -->
    <keep-alive include="a,b">
      <component :is="view"></component>
    </keep-alive>
    
    <!-- 正则表达式 (使用 `v-bind`) -->
    <keep-alive :include="/a|b/">
      <component :is="view"></component>
    </keep-alive>
    
    <!-- 数组 (使用 `v-bind`) -->
    <keep-alive :include="['a', 'b']">
      <component :is="view"></component>
    </keep-alive>
    ```



##### 异步更新

什么是异步更新？

```html
	在created()钩子函数执行的时候DOM其实并未进行任何渲染，而此时不能进行DOM操作，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。与之对应的就是mounted()钩子函数，因为该钩子函数执行时所有的DOM挂载和渲染都已完成，此时在该钩子函数中进行任何DOM操作才不会出现问题。
(ajax 或 created 执行就用 $nextTick)
```

​	

​	**`	Vue.nextTick`** 用于延迟执行一段代码，它接受2个参数（回调函数和执行回调函数的上下文环境），如果没有提供回调函数，那么将返回`promise`对象。Vue不自带 `promise` 的 `polyfill`，若是浏览器不支持`Promise`，则需要自己配置polyfill。

```JS
Vue.nextTick()
  .then(function () {
    // DOM 更新了
  })
	或
Vue.nextTick(function () {
  // DOM 更新了
})
```



### 项目上线

* DNS： 它作为将[域名](https://baike.baidu.com/item/%E5%9F%9F%E5%90%8D)和[IP地址](https://baike.baidu.com/item/IP%E5%9C%B0%E5%9D%80)相互[映射](https://baike.baidu.com/item/%E6%98%A0%E5%B0%84)的一个[分布式数据库](https://baike.baidu.com/item/%E5%88%86%E5%B8%83%E5%BC%8F%E6%95%B0%E6%8D%AE%E5%BA%93)，能够使人更方便地访问[互联网](https://baike.baidu.com/item/%E4%BA%92%E8%81%94%E7%BD%91)。DNS使用[TCP](https://baike.baidu.com/item/TCP)[UDP](https://baike.baidu.com/item/UDP)[端口](https://baike.baidu.com/item/%E7%AB%AF%E5%8F%A3)。当前，对于每一级域名长度的限制是63个字符，域名总长度则不能超过253个字符。

* 作用：解析地址和IP地址

​	域名注册：	...新网、万网 （备案 背景墙拍照）

​	云服务器ECS： 	...阿里云、腾讯云  （linux centOS）

​	密码： 自定义密码（主机密码）

​	在线监测域名或端口： http://coolaf.com/tool/port

* 命令行

  ```html
  执行的命令行：
  ​	打开服务器命令行：ssh root@自己的IP地址
  
  ​	登录： root   
  
  ​	密码：主机密码
  
  ​	查看文件：   cd /
  
  				ls
  
  ​	新建：mkdir  文件名
  
  ​	进入目录： cd
  
  ​	新建文件： touch 文件
  
  ​	打开文件：vim 文件名
  
  ​	输入内容：  i   
  
  ​	保存并推出 ：ESC ： w q
  
  ​	（查看文件： cat  文件名）
  
  ​	装插件命令：yum install  装的东西（若是安装最新版本要执行.........详情见deployment.md）
  
  ​	启动服务器：npm install http-serve -g   
  
  ​	一直运行服务器： npm install pm2 （安装）、npm start  文件名（运行）
  
  ​	查看当前所在的目录：pwd
  ```

打包: npm run build （安装完成后出现打包后的一个文件  dist文件）



**Nginx** (engine x) 是一个高性能的HTTP和反向代理web服务器，同时也提供了IMAP/POP3/SMTP服务。

* 安装nginx 

```html
yum install nginx -g
```

* 配置文件都在 `nginx.conf` 文件夹里面

conf.d    touch新建文件

* 配置文件 serve{  root、listen......}配置完成需要重启

```html
nginx -s reload
```



### 移动端布局

布局适配;

- 单位; 
  - rem（根元素大小）、em（父级元素大小）、vw、vh、百分比布局
- 事件  touch
  - touchstart、touchmove、touchend  
  - zepto.js（类似网页端的jQuery）、hammer.js



### web开发流程

web开发流程  （axure、uni-app）

产品经理设计：功能需求

交互设计：

视觉设计：

前端、后台：

运维、

测试、

发布



