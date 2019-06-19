# CommonJS

### 概念

CommonJS API将通过定义处理许多常见应用程序需求的API来填补这一空白，最终提供与Python，Ruby和Java一样丰富的标准库，`CommonJs 是服务器端模块的规范`。

目的是应用程序开发人员能够使用CommonJS API编写应用程序，然后跨不同的JavaScript解释器和主机环境运行该应用程序。使用CommonJS兼容系统，您可以使用JavaScript编写：

- 服务器端JavaScript应用程序
- 命令行工具
- 基于桌面GUI的应用程序
- 混合应用程序（Titanium，Adobe AIR）



### 模块

* 模块引用（require）
* 模块定义（exports）
* 模块表示（module )

ComminJS加载是 **`同步` **的，所以只有加载完成才能执行后面的操作。

```html
SO:
​	 一个文件就是一个模块，拥有单独的作用域；

​    普通方式定义的变量、函数、对象都属于该模块内；

​    通过require来加载模块；

​    通过exports和modul.exports来暴露模块中的内容；
```





# AMD

### 概念

AMD: ( **Asynchromous Module Definition**异步模块定义 )   它就主要为前端JS的表现制定规范

`require.js`  依赖前置



### 配置

```js
require.config({
    baseUrl: "",		// 绝对路径
    path: {			
        a: "",
        b: "",
        ...
    }
})
```



### 定义

```js
define(function () {
    ...
    return
})

或者

// 没有依赖
define(['dep1','dep2'], function (dep1,dep2) {
    ...
    return
});
```



### 引入

```js
// module 若是多个模块yoga逗号隔开，不加后缀名
// 回调函数先执行，在执行模块
require(['module1', 'module2'], function () {
    ...
    callback
})
```





# CMD

### 概念

CMD: ( **Common Module Definition**异步模块定义 )   `sea.js`  就近依赖



### 配置

`````js
define(function (require, exports, module) {
    ...
});
`````





# CMD和AMD的区别

* 对于依赖的模块AMD是提前执行，CMD是延迟执行。不过RequireJS从2.0开始，也改成可以延迟执行（根据写法不同，处理方式不通过）。 

* CMD推崇依赖就近，AMD推崇依赖前置。   





# NPM加载机制

NPM的模块加载机制：

​      如果require的是绝对路径文件，查找不会去遍历每个node_modules目录，其速度最快

　　1）.从module.paths数组中（由当前执行文件目录到磁盘根目录）取出第一个目录作为查找基准

　　2）.直接从目录中查找该文件，如果存在则结束查找，如果不存在则进行下一条查找

　　3）.尝试添加.js、.node、.json后缀之后查找，如果存在文件则结束查找，如果不存在则进行下一条查找

　　4）.尝试将require的参数作为一个包来进行查找，读取目录下的package.json文件，取得Main参数指定的文件

　　5）.尝试查找该文件，如果存在则结束查找，如果不存在则进行第3条查找

　　6）.如果继续失败，则取出module.paths数组中的下一目录作为基准查找，循环第1-5个步骤

　　7）.如果继续失败，循环第1-6个步骤，直到module.paths中的最后一个值

　　8）.如果继续失败，则抛出异常