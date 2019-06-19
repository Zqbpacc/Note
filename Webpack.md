# Webpack

>官网：<https://www.webpackjs.com/>
>
>指南：<https://www.webpackjs.com/guides/>

是一个模块打包器



## 概念

**webpack：静态模块打包器**

概念：当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。



**四个核心概念：**

- 入口(entry)
- 输出(output)
- loader
- 插件(plugins)



检测是否可以使用  can i use

官网：https://www.caniuse.com/



**Webpack配置**

 webpack 配置是标准的 Node.js    ` CommonJS`  模块

* 通过 `require(...)` 导入其他文件
* 通过 `require(...)` 使用 npm 的工具函数
* 使用 JavaScript 控制流表达式，例如 `?:` 操作符
* 对常用值使用常量或变量
* 编写并执行函数来生成部分配置



## 使用

1. 安装

   ```bash
   $ npm i webpack webpack-cli -D
   # 等价于
   $ npm install webpack webpack-cli --save-dev
   ```

   

2. package.json

   ```json
   script: {
     "start": "webpack --mode development"  // 开发模式
     // 构建模式 production（build  默认）
   }
   ```

   

3. 打包

   ```bash
   $ npm start
   # 默认 webpack 中入口文件在 './src/index.js' ，出口文件在 './dist/main.js'
   # 默认执行 webpack 命令是 production 模式 （生产模式），可以改为 development 模式
   ```

   

4. 多入口

   ```json
   module.exports = {
     entry: {
       index: './src/index.js',
       home: './src/home.js',
       cart: './src/cart.js',
     },
     output: {
       path: path.join(__dirname, "./dist"),
       // hash模式下文件的随机字符串会随着文件的修改hash字符串也会跟着修改，为使当我们将js文件引入html时hash字符串也会跟着修改，需要插件：http-webpack-plogin
       filename: '[name].[chunkHash].js'
     }
   }
   ```

   

5. 插件：html-webpack-plugin

   ```bash
   $ npm i --save-dev html-webpack-plugin
   ```

   

6. 使用插件：

   ```js
   // 引入模块
   const HtmlWebpackPlugin = require('html-webpack-plugin')
   
   module.exports = {
     .....,
     plugins: [
       new HtmlWebpackPlugin({
         // 模板
         template: './src/index.html'
       })
     ]
   }
   ```

   

7. ` script`  或 ` config ` 配置目录

   ​	一般 webpack.config.js 配置文件都放在 `script ` 后者 ` config ` 文件夹目录里面；这时会改变webpack的默认设置（src  index.js   /   dist  main.js）;所以要修改output路径和package.json里面的 script ；

   ```json
   # package.json
   
   // 修改前
   "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1",
   "start": "webpack --mode development"
   },
   
   // 修改后
   "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1",
   "start": "webpack --mode development --config scripts/webpack.config.js"
   },
   ```

   ```js
   # webpack.config.js
   
   // 修改前
   module.export = {
       ....
       output: {
           path:  path.join(__dirname, '../dist'),
           filename: 'js/index.[chunkHash].js
       }
   }
   
   //  修改后
   module.export = {
       ....
       output: {
           path:  path.join(__dirname, '../dist'),    // 上一级的dist目录
               或者
           path:  path.join(process.cwd(), 'dist'),   // path的方法
           filename: 'js/index.[chunkHash].js
       }
   }
   ```

   

8. CSS样式打包

   ```bash
   # 安装 mini-css-extract-plugin
   $ npm install --save-dev mini-css-extract-plugin
   ```

   ```bash
   # 安装 css-loader
   $ npm install --save-dev css-loader
   
   # 安装 style-loader
   $ npm install style-loader --save-dev
   ```

   

9. webpack服务器

   ```bash
   # 安装 webpack-dev-server
   $ npm install webpack-dev-server --save-dev
   ```

   在package.json里 `script ` 配置

   ```json
   "script"： {
   	"dev": "webpack-dev-server --mode development --config scripts/webpack.config.js"
   }
   ```

   

10. SASS样式打包

    ```bash
    # 安装 sass-loader 自动添加浏览器前缀postcss-loader
    $ sass-loader node-sass --save-dev
    $ npm i -D postcss-loader
    ```

    

11. ES6转ES5

    ```bash
    # 安装 babel-loader
    $ npm install -D babel-loader @babel/core @babel/preset-env webpack
    ```

    

