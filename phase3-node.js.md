## 第三阶段

### node.js

##### 安装

node安装：下载安装、nvm、Chocolaty

##### 常用属性

1.OS系统

2.FS系统文件
	writeFile 写文件 

​	appendFile 追加文件 

​	readFile 读文件（读出的文件是一个16#的流，用buffer 可转成正常的文字）

3.http模块（可以创建一个服务器）

```js
http.createServer((req,resp), =>{

}.listen()
```
4.path路径

  ```js
  path.resolve()
  ```

##### server

**node.js模块规范是`commonJS`;**

* 创建一个服务器（接受请求require，返回数据响应response）；

```js
//引入核心模块
const http = require("http");
http.createServer = ((req,resp) =>{
    console.log(req.url);  //路径
    resp.write("");
    resp.end()
}).listen(8080); //监听  服务器端口号
```

* 配置路径渲染模块

* 模块化配置一个router对象；

  导出(暴露)模块：module.exports = router

```js
// 路由
const router = {
    "/" : "index.html",
    "/list": "list.html",
    "/detail": "detail.html",
    "/index": "../index1.html"
}

 // 导出（暴露）模块
module.exports = router
```

* 配置地址引入
  通过path.resolve()配置，上一目录或者引入目录

```js
// 引入需要依赖的核心模块
const http = require('http'),
        fs = require('fs'),
        path = require('path'),
        router = require('./router')

// request response
http.createServer((req, resp) => {
    if(req.url === '/favicon.ico'){
        resp.end();
        return;
    }
    fs.readFile(path.resolve('./static', router[req.url]), (err, data) => {
        if(err) throw err;  //抛出异常
        else resp.end(data);  //渲染数据
    })
}).listen(8080)
```



### express

**概念：express  是基于Node.js平台，快速、开放、极简的 Web 开发框架(Node.js框架)**

​	express是一个保持最小规模的灵活的Node.js Web应用程序开发框架，为Web和移动应用程序提供一组强大的功能。使用您所选择的各种 HTTP 实用工具和中间件，快速方便地创建强大的 API。

官网：http://www.expressjs.com.cn/
安装：npm install express --save

##### Express应用程序生成器

通过应用生成器工具 express-generator 可以快速创建一个应用的骨架。

**新建文件myapp**

* 假定你已经安装了 Node.js，接下来为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。

```JS
mkdir myapp
```

* 进入myApp文件夹

```JS
cd myapp
```

* 通过 npm init 命令为你的应用创建一个 package.json 文件。

```JS
npm init -y
```

* 安装express

```JS
npm install express --save
```

* main.js      通过node main命令，在浏览器输入端口号访问

```js
// 引入express模块
const express = require('express')
// 创建express的实例
const app = express()
// 处理来自根目录的get请求
app.get('/', (req, resp) => resp.send('Hello World!'))
// 监听3000端口
app.listen(3000, () => console.log('Example app listening on port 3000!'))
```

**新建ExApp文件**

* express-generator 包含了 express 命令行工具。通过如下命令即可安装：

```js
npm install express-generator -g
```

* 帮助参数

```js
express -h
```

* 回上一级（exApp文件夹里）

```js
cd ..
```

* 创建了一个名称为 myapp 的 Express 应用。此应用将在当前目录下的 exApp 目录中（文件名自定）创建,并且设置为使用 ejs模板引擎；

```js
express --view=ejs exApp
```

* 进入目录

```js
cd exApp/
```

* 安装npm install

```js
npm i
```

* 执行express

```js
npm start
```

* 执行前可以自行配置端口号(8090)

```js
port=8090 npm start
```



**app.js文件夹内容的注释**

```js
// 引入http报错模块
var createError = require('http-errors');

// 引入express模块
var express = require('express');

// 引入核心path模块
var path = require('path');

// 引入处理cookie的模块
var cookieParser = require('cookie-parser');

// 引入日志模块
var logger = require('morgan');

// 引入路由文件模块
var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');

// 创建express实例
var app = express();

// 设置模板引擎， 如果要加载视图文件，就去views目录
// __dirname 当前路径 C:\1902-node\express-project\exApp\views
app.set('views', path.join(__dirname, 'views'));

// 设置模板引擎为 ejs
app.set('view engine', 'ejs');

// app.use 中间件
// 使用日志的中间件
app.use(logger('dev'));

// 使用处理json格式数据的中间件
app.use(express.json());

// 使用解析url的中间件
app.use(express.urlencoded({ extended: false }));

// 使用cookie解析器的中间件
app.use(cookieParser());

// 处理静态文件的中间件（静态资源从public里面获取）
app.use(express.static(path.join(__dirname, 'public')));

// 使用路由
app.use('/', indexRouter);
app.use('/users', usersRouter);

// 处理404错误
app.use(function(req, res, next) {
    next(createError(404));
});

// 处理500错误
app.use(function(err, req, res, next) {
    // set locals, only providing error in development
    res.locals.message = err.message;
    res.locals.error = req.app.get('env') === 'development' ? err : {};


// render the error page
res.status(err.status || 500);
res.render('error');

});

// 暴露app
module.exports = app;
```

##### 自动重启

nodemon

1 全局安装    npm install -g nodemon;

2 在scripts添加自己的nodemon;

```js
{
   "scripts": {
    "start": "node ./bin/www",
    "st": "nodemon ./bin/www"
  }
}
```

3 运行代码：npm run st（属性名）.



#####　ejs 模板引擎

ejs:类似前后端使用的air-template模板引擎。

官网：https://ejs.bootcss.com/

书写方式：<%=   ?   %>  **`语句中没有等号`**


### mongoDB

mongoDB是一个**非关系型数据库**
mySQL是一个**关系型数据库**

**特点**：

| mysql     | mongoDB    |
| --------- | ---------- |
| database  | database   |
| table     | collection |
| col(列)   | field      |
| row（行） | document   |

mongoDB官网：https://www.mongodb.com/
安装教程：https://www.runoob.com/mongodb/mongodb-window-install.html
下载网址（V3.1.4）：https://www.mongodb.com/download-center/community

**安装完成需要的设置：**
（1）设置环境变量：把bin的目录设置到环境变量中
                        （右键计算机--高级系统设置--高级--环境变量）

（2）新建自己的服务器运行的地址

（3）开启服务：

​        	1 在bin目录下选择命令行（或者git bash）；
​        	2 命令行中输入：

mongod --dbpath 自己新建的文件路径

```js
mongod --dbpath 自己新建的文件路径
```

**什么是MongoDB？**

* MongoDB是一个文档数据库，具有您需要的可查询性和索引所需的可伸缩性和灵活性。
* 文档模型映射到应用程序代码中的对象，使数据易于使用。
* 即席查询，索引和实时聚合提供了访问和分析数据的强大方法。
* MongoDB是一个分布式数据库，因此内置了高可用性，水平扩展和地理分布，并且易于使用。



#####　可视化工具 robo 3T

还有Navicat MongoDB等其他可视化工具。

官网：https://robomongo.org/
下载：https://robomongo.org/download

**默认端口号port：27017**；

安装可能出现的问题
win 7 下安装robo 3t遇到“无法启动程序，引文计算机丢失api-ms-win-crt-runtime-|1-1-1.dll”;
解决办法：安装VC_redist;



##### Navicat MongoDB

开启服务：

```txt
在bin目录下打开命令行输入命令：mongod --dbpath 自己服务器的地址
```

##### mongoose包

官网：https://mongoosejs.com/
**mongoose：基于node.js的优雅mongodb对象建模.**



##### 使用mongoose 
* 接下来使用npm以下命令从命令行安装Mongoose ：

```js
npm install mongoose
```

* 我们需要做的第一件事是在项目中包含mongoose，并test在我们本地运行的MongoDB实例上打开与数据库的连接。

```js
// getting-started.js
//  引入模块
const mongoose = require('mongoose');

// 连接数据库
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true});
```

* 我们与在localhost上运行的测试数据库有挂起的连接。如果我们成功连接或发生连接错误，我们现在需要收到通知：

```js
//得到了连接实例
let db = mongoose.connection;

// 处理连接错误输出
db.on('error', console.error.bind(console, 'connection error:'));

//监听一次打开事件
db.once('open', function() {
  // we're connected!
});
```

* 使用Mongoose，一切都来自Schema。
          Schema：把非关系型数据库转换成关系型结构。

```js
let kittySchema = new mongoose.Schema({
  name: String,
    ...
});
```

* 一个带有一个属性的模式name，它将是一个 String。下一步是将模式编译为模型。

```js
var Kitten = mongoose.model('Kitten', kittySchema);
```

* 模型是用于构造文档的类。

```js
var silence = new Kitten({ name: 'Silence' });
console.log(silence.name); // 'Silence'
```

* 向MongoDB保存内容

```js
 // 存数据    异步方法
silence.save(function (err, silence) {
    if (err) return console.error(err);   // 报错
    fluffy.speak();
});
```

* 查找

```js
// model的kitten
Kitten.find(function (err, kittens) {
  if (err) return console.error(err);
  console.log(kittens);
})
```

#####　mongooseDB增删改查

```js
// 引入mongoose模块
const mongoose = require('mongoose');

// 连接本地数据库服务器，打开1902数据库
mongoose.connect('mongodb://localhost/1902', {useNewUrlParser: true});

// 得到连接实例
let db = mongoose.connection;

// 处理连接错误输出
db.on('error', console.error.bind(console, 'connection error:'));

// 监听一次打开事件
db.once('open', function() {
  console.log("we're connected!");
});

// schema把非关系型数据库转换成关系型结构
let usersSchema = new mongoose.Schema({
  username: String,
  password: String
});

// 根据usersSchema得到了一个model,这个model是一个抽象，他是没有值的，只是代表这个collection的抽象的模型
let Users = mongoose.model('Users', usersSchema);

const userModel = {
  /*
   * 插入document
   * @param userInfo <object>  {username, password}
  */
  insert: (userInfo) => {
    //往模型当中去填值，得到一个实例的document
    let user = new Users(userInfo)
    return new Promise((resolve, reject) => {
      // 存数据
      user.save((err, user) => {
        if(err) reject(err);
        else resolve(user);
      })
    })
  },
  /*
   * @param where 查询条件 <object>
   * @param isOne 是否查一条 默认为false
  */
  find: (where, isOne = false) => {
    if(isOne) {
      return new Promise((resolve, reject) => {
        Users.findOne(where, (err, docs) => {
          if(err) reject(err)
          else resolve(docs)
        })
      })
      
    }else{
      return new Promise((resolve, reject) => {
        Users.find(where, (err, docs) => {
          if(err) reject(err)
          else resolve(docs)
        })
      })
    }
  },

  /*
   * 删除
   * @param where <object> 删除条件
   * @param [isOne] <Boolean> 是否删一条 默认值true
  */
 delete: (where, isOne=true) => {
  return new Promise((resolve, reject) => {
    if (isOne) {
      // 只删除一条
      Users.deleteOne(where, err => {
        if(err) reject(err);
        else resolve();
      })
    }else {
      Users.deleteMany(where, err => {
        if(err) reject(err);
        else resolve();
      })
    }
  })
 },

  /*
    * 更新
    * @param where <object> 更新条件
    * @param updatedData <object> 更新之后的数据
    * @param [isOne] <Boolean> 是否一条 默认值true
  */
  update: (where, updatedData, isOne = true) => {
    return new Promise((resolve, reject) => {
      if(isOne) {
        Users.updateOne(where, updatedData, (err, res) => {
          if(err) reject(err);
          else resolve(res);
        })
      }else {
        Users.updateMany(where, updatedData, (err, res) => {
          if(err) reject(err);
          else resolve(res);
        })
      }
    })
  }

}
// 暴露出去（导出模块）
module.exports = userModel;
```



##### MVC 框架

模型module    视图   控制器controller

controller    渲染到前端
module        写的逻辑
db                 引入mongoose模块，连接服务器

用promise来处理异步( ES7: await / async )



### 前后端跨域

服务器与服务器之间不存在兼容问题，只有浏览器之间才存在兼容问题

#####　什么是跨域?

```
当协议、域名、端口有其中任意一项不一致时则为跨域（非同源）。
```

##### 前端解决跨域

```txt
a.CORS
	前端：ajax（解决get/post跨域需求）
	后端：设置要请求的源  设置相应开头信息： Access-Control-Allow-Origin:*（PHP）

b.jsonp
	利用<script>在引入外部JS时不受同源策略限制的特性，src的开放性原则来实现跨域。
	前端：
		1. 创建 <script> 元素
        2. 设置 src 属性，传递 callback 参数指明全局回调函数的名称
        3. 添加到 body 中
        4. 创建全局函数，用于处理响应数据
        5. 删除 <script> 元素
        （在src里面写接口地址）
    后端：
    	由服务器端构建一个字符串：字符串中的内容是能够在 JS 中执行的函数调用的结构
```

#####　原生ajax

```js
// 创建一个ajax原生对象
var ajax = new XMLHttpRequest();

// open方法打开连接（请求方式get\post，请求的地址url，是否异步true代表异步
ajax.open("POST","url",true);

// send方法，发送请求
ajax.send("name=zhangsan&age=18");

// 监听状态的变化
ajax.onreadystatechange = function(){
if(ajax.readyState == 4 && ajax.status == 200){
     var json = JSON.parse(ajax.responseText);
    fn(json);
}
```



##### postman工具

官网：https://www.getpostman.com/

作用：

​	1.检测接口；

​	2.当返回数据慢时可以通过postman工具检测接口所需要的时间，方便判断是前端渲染数据慢或者是后端的接口问题；	

**jquery托管在线地址**：  http://code.jquery.com/jquery-3.2.1.min.js



##### 实现跨域

* cors

  * 安装cors跨域插件 

    * npm i cors

  * 引入相关模块

    ```js
    // 引入模块
    var express = require('express');
    var path = require('path');
    const cors = require('cors');
    
    // 创建express的实例
    var app = express();
    
    // 使用中间件  use方法
    app.use(cors());
    
    // list.html  需要引入jQuery文件
    $.get('/api/goods?subject_id=5571&page=1&size=3', function (resp) {
          console.log(resp);
    })
    
    // list.js
    router.post('/', function(req, res, next) {
      res.json({
        "res_code": 200,
        "res_body": [
          {"id":1, title: "商品1"},
            ...
        ]
      });
    });
    ```

    

* 代理（proxy）

  * 代理跨域  

    ```html
    http-proxy-middleware
    ```

  * 安装插件

    ```html
    npm install --save-dev http-proxy-middleware
    ```

  * 引入依赖

  * 根据options创建一个代理的实例

  * 使用中间件

  * 代理配置项

    * 设置目标源的主机
    * 修改源为true
    * 把前端的地址重写为真实接口的地址

    ```js
    // 引入依赖
    const express = require('express')
    const proxy = require('http-proxy-middleware')
    const path = require('path')
    
    // 根据options创建一个代理的实例
    var goodsProxy = proxy(options)
     
    // 得到一个express实例
    var app = express()
    
    // 设置默认访问静态页面public     __dirname为当前目录
    app.use(express.static(path.join(__dirname, 'public')));
    
    // 使用goodsProxy代理中间件
    app.use('/api', goodsProxy);
    app.listen(3000);
    
    // 代理配置项
    var options = {
      target: 'https://apiv2.pinduoduo.com',  // 目标源的host
      changeOrigin: true,  // 修改源
      ws: true,  // 常连接
      pathRewrite: {
        // 把前端的虚拟地址/api/goods重写为真实接口地址/api/fiora/subject/goods
        '^/api/goods': '/api/fiora/subject/goods' 
      },
        
      router: {
        // when request.headers.host == 'dev.localhost:3000',
        // override target 'http://www.example.org' to 'http://localhost:8000'
        'dev.localhost:3000': 'http://localhost:8000'
      }
    }
    
    // HTML部分
     $.get('/api/goods?subject_id=5571&page=1&size=3', function (resp) {
          console.log(resp);
        })
      })
    ```




##### 前后端交互方式

* 利用cookie

  ```html
  前端通过登录存储cookie，后端通过req.cookie（）获取cookie
  ```


* 利用ajax

  ```js
  a  可以利用原生ajax的XMLHttpRequest创建可信对象
  b  jquery的方法$ajax   
      $.ajax({
          url:"",
          methon:"",
          data:"",
          success:(function(){
  
          }),
          dataType:"jsonp",
      })
  （post、get、jsonp）
  ```

* jsonp

* 服务端渲染

  * 在php中实现服务端渲染：

    在php文件中可以放入html代码，访问php文件的时候就相当于访问这个对应的html文件，因为在php文件中，所以可以写一些php的代码来渲染数据.

  * 在Node中实现服务端渲染：

    利用模板引擎，node在渲染模板的时候给模板传入数据，在模板中就可以使用特定的语法来渲染dom了 例如：ejs,

  ```js
  <?php
  	echo "Hello world!这是正文";
  ?>
  ```

*  webSocket 和 Socket.io

```html
	WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。
	WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。
	在 WebSocket API 中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。

	Sockets应用层通过传输层进行数据通信时，TCP和UDP会遇到同时为多个应用程序进程提供并发服务的问题。多个TCP连接或多个应用程序进程可能需要 通过同一个TCP协议端口传输数据。为了区别不同的应用程序进程和连接，许多计算机操作系统为应用程序与TCP／IP协议交互提供了称为套接字 (Socket)的接口，区分不同应用程序进程间的网络通信和连接。
	生成套接字，主要有3个参数：通信的目的IP地址、使用的传输 层协议(TCP或UDP)和使用的端口号。Socket原意是"插座"。通过将这3个参数结合起来，与一个"插座"Socket绑定，应用层就可以和传输 层通过套接字接口，区分来自不同应用程序进程或网络连接的通信，实现数据传输的并发服务。
```





### 登录

登录流程：

* 浏览器向后台发送post请求提交登录信息
* 后台接收用户名密码，访问数据库验证登录信息
* 登录成功后台将会向前端发送一个随机的字符串" token "，返回前端存在cookie里面
* 前端跳转页面，前端首页会验证是否登录成功，就会带上cookie，发送给后端对比数据库的登陆信息是否匹配，若是匹配则登录成功（可能：则把用户名密码返回到首页）
* 前端首页就会显示登录状态

##### cookie

存cookie

```html
npm install cookie-session
```

引入模块使用

```js
var cookieSession = require('cookie-session')
```

| 对象 |  数组  |
| :--: | :----: |
| null | length |

我可以取到用户的密码吗？

```txt
	注册后的密码将会通过create-hash包进行加密，甚至多次加密，只有将用户的密码再次加密后与原来的加密的数据进行对比，若是匹配成功，才会验证成功。
```

加密包:

```js
create-hash
```



### 搭建假数据

搭建假数据会需要一个工具包

```js
mock.js
```

安装模块

```js
npm i mockjs
```



* 如何自己简易搭建假数据？

app.js部分

```js
// 引用模块
var listRouter = require('./routes/list');
var detailRouter = require('./routes/detail');

// 使用中间件
app.use('/api/list', listRouter);
app.use('/api/detail', detailRouter);

// 暴露
module.exports = app;
```

router的list.js

```js
// 引入相关模块
var express = require('express');
var router = express.Router();
const Mock = require('mockjs')

// 请求列表页所有商品
router.get('/', function(req, resp, next) {
  let goodList = Mock.mock({
    "res_code|1": [200, 200, 200, 200, 200, 200, 200, 201],
    "res_body": {
      "list|10": [
        {
          "id|+1": 1,
          "title": "@ctitle( 10, 20 )",
          "img": "@image('200x100', @color, #FFF, png, @word)",
          "price": "@float(100,1000,2,2)"
        }
      ]
    }
  })
  resp.json(goodList);
});

module.exports = router;
```

router的detail

```js
// 引入相关模块
var express = require('express');
var router = express.Router();
const Mock = require('mockjs')

/* 取id. */           
router.get('/', function(req, resp, next) {
  let id = req.query.id;
  console.log(req.query)
  let detail = Mock.mock({
    "id": id,
    "title": "@ctitle( 10, 20 )",
    "img": "@image('200x100', @color, #FFF, png, @word)",
    "price": "@float(100,1000,2,2)"
  })
  resp.json(detail)
});

module.exports = router;
```



* 如何使用自己搭建的假数据？

```txt
把自己的localhost地址驾到项目的baseUrl；此涉及跨域（cros、proxy）
```



### 文件上传

常用的**处理文件的模块**：formidable、multer；

​	上传文件可以用from（页面提交，必须要写enctype）、ajax（files:fileList）前后端传送文件会把发送的文件转换成二进制的流（buffer）。

**buffer**:

```html
- buffer也已在全局状态下使用；
- buffer是用来处理二进制的数据的流；
- buffer类的实例类似于整数数组；
```

* 安装模块

```txt
npm i -S formidable
```

* 新建文件夹保存图片的位置

```js
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="ie=edge">
<title>Document</title>
</head>
<body>

    <h1>上传图片</h1>
    <form>
        <input type="file" id="fileInput">
        <button>上传</button>
        <div id="imgWrap"></div>
    </form>


<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script>
$('form').on('submit', function (e) {
    e.preventDefault();

    // 使用FormData来上传文件
    var formData = new FormData();

    // 把从原生对象上获取得到的files 添加到formData里
    formData.append('file', $("#fileInput").get(0).files[0]);


    $.ajax({
        url: '/upload',
        method: 'post',
        data: formData,
        processData: false, // 不处理数据
        contentType: false, // 不设置内容类型
        success: function (resp) {

            // console.log(resp);
            var {path} = JSON.parse(resp);
            console.log(path);
            let img = $(`<img src="${path}">`);
            $("#imgWrap").append(img);
         }
    })
})
</script>
</body>
</html>
```



##### 图片裁剪

查找iquery插件

官网：www.jq22.com



### WebSocket

作用：聊天、在线直播、游戏（热更新）

可以实现socket通讯的语言有：java、 php 、 node；

WebSocket分为：**轮询**、**WebSocket**；

* 轮询：

```html
长轮询： 每隔一段时间想服务器发出请求；即使没有发生变化

短轮询： 服务器会挂起，在这段时间内检测是否发生变化，检测到变化就会立即返回，否则就一直等到超时为止。
```

* WebSocket



#####　chat

实现chat聊天需依赖于node.js + express的**socket.io**插件。



* 创建package.jsson文件

  ```html
  npm init -y
  ```

* 需要再一次局部啊安装express

  ```html
  npm install --save express
  ```

* 以下步骤见官网

  见官网
  创建步骤：https://socket.io/get-started/chat/

  ...

  ...

  

##### socket

socket定义：

```html
socket是进程通信的一种方式，即调用这个网络库的一些API函数实现分布在不同主机的相关进程。
	IP地址：即依照TCP/IP协议分配给本地主机的网络地址，两个进程要通讯，任一进程首先要知道通讯对方的位置，即对方的IP；
	端口号:用来辨别本地通讯进程，一个本地的进程在通讯时均会占用一个端口号，不同的进程端口号不同，因此在通讯前必须要分配一个没有被访问的端口号。
	连接：指两个进程间的通讯链路。
```

