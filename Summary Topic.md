 

###  介绍webpack和gulp，及在项目中的具体使用？

```
webpack和gulp等项目构建工具
webpack:静态模块打包器
gulp：自动化构建工具

相同点：都可用于项目打包，文件压缩，文件监测等功能。

不同点：两种工具的侧重点不同，webpack主要侧重于模块的打包，适合于单页面的项目，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。而gulp侧重于前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。
```

###  ES6的了解？

```
一、新的变量声明方式 let/const
	let： 块级作用域，不会变量提升，暂时性死区
	const： 声明常量
二、箭头函数的使用
三、模板字符串
四、解构赋值
五、扩展运算符
六、Class
七、Promise
八、继承extends  super（）构造函数的继承
在ES6中，会默认采用严格模式
```

###  介绍Vue, React, Angular，及其区别？

```
VUE渐进式框架
react快速构建用户界面的JS库

Vue与Angular相同点：
	指令和自定义指令；
	支持双向绑定；
	都支持过滤器；
  不同点：
	在性能上，AngularJS依赖对数据做脏检查，所以Watcher越多越慢；
	Vue.js使用基于依赖追踪的观察并且使用异步队列更新。所有的数据都是独立触发的；
	
Vue与React的相同点：
	一切都是组件，组件实例之间可以嵌套；
	在组件开发中都支持mixins的特性；
	都提供合理的钩子函数，可以让开发者定制化地去处理需求
  不同点：
  	Vue用js插值表达式，react是JSX；
  	React依赖Virtual DOM,而Vue.js使用的是DOM模板。React采用的Virtual DOM会对渲染出来的结果做脏检查
```

###  CSS引入的方式？link和import的区别？

```
1. link属于XHTML标签，而@import是CSS提供的一种方式
2. 当一个页面被加载时link引用的CSS会同时被加载，@import引用的CSS会等到页面加载完毕后加载
3. @import是CSS2.1时提出的，所以老的浏览器不支持， 而link无此问题
4. 当使用js控制DOM 去改变样式时必须用link，因为@import不是DOM可以控制的
```

###  用promise 写ajax？

```js
/* ajax方法
	 * @param  url <string> 请求的地址
	 * @param  query <object>  请求携带的参数
	 * @param  isJson <boolean>  是否是json格式的数据	
	*/

	ajaxGetPromise : function (url, query, isJson) {
		isJson = isJson === undefined ? true : isJson;
		// 如果有query再url后面拼接query
		if(query){
			url += "?";
			for(var key in query){
				url += key+"="+query[key]+"&";
			}
			url = url.slice(0, -1);
		}
		return new Promise((resolve, reject) => {
			let ajax = new XMLHttpRequest();
			ajax.open("GET", url, true);
			ajax.send(null);
			ajax.onreadystatechange = function () {
				if(ajax.readyState === 4){
					if(ajax.status === 200){
						// 数据成功返回了
						resolve(isJson ? JSON.parse(ajax.responseText) : ajax.responseText);
					}else{
						reject();
					}
				}
			}
		})
	}
}
```

###  描述 call 和 apply 函数的作用及用法?

###  并发和并行的区别

```
	并发是宏观概念，我分别有任务 A 和任务 B，在一段时间内通过任务间的切换完成了这两个任务，这种情况就可以称之为并发。(node  不使用密集型应用)
	并行是微观概念，假设 CPU 中存在两个核心，那么我就可以同时完成任务 A、B。同时完成多个任务的情况就可以称之为并行。
```

###  什么是回调函数、特点、如何解决回调地狱？

```
回调函数： callback

概念： 回调函数就是一个通过函数指针调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。

回调函数：
	不能使用try catch捕获错误；
	不能return
	
回调地狱：
	嵌套函数存在耦合性，一旦有所改动就可能影响某些代码功能；
	嵌套函数一般很难处理错误；
```



###  **async 和 await的特点，await的原理？**
async： 异步、await： 等待

一个函数加上async，该函数就会返回一个promise；

```js
// async语法： 在函数前面添加async关键字
   async function timeout() {
       return 'hello world'
   }
   timeout();
   console.log('虽然在后面，但是我先执行');
```

await只能配套async使用；

常用定时器函数

```js
 setTimeout（超时定时器）、setInterval（间隔定时器）、requestAnimationFrame（循环定时器）

 setTimeout 会比 promise后执行
```



### vue的seo优化

```
1.SSR服务器渲染；
2.静态化；
3.预渲染prerender-spa-plugin；
4.使用Phantomjs针对爬虫做处理。

预渲染
安装插件
1. npm install vue-meta-info --save
2. npm install prerender-spa-plugin --save-dev
```





### 什么是ajax？

```
AJAX 是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。

AJAX的优点：
1）不需要插件支持（一般浏览器且默认开启JavaScript即可）；
2）用户体验极佳（不刷新页面即可获取可更新的数据）；
3）提升Web程序的性能（在传递数据方面做到按需放松，不必整体提交）；
4）减轻服务器和带宽的负担（将服务器的一些操作转移到客户端）；

Ajax的不足：
1）不同版本的浏览器度XMLHttpRequest对象支持度不足(比如IE5之前)；
2）前进、后退的功能被破坏（因为Ajax永远在当前页，不会记录前后页面）；
```





###  **进程与线程区别？JS 单线程带来的好处？**

```
   进程描述了 CPU 在运行指令及加载和保存上下文所需的时间，放在应用上来说就代表了一个程序。
线程是进程中的更小单位，描述了执行一段指令所需的时间。
   JS单线程可以达到节省内存，节约上下文切换时间，没有锁的问题的好处；    
   
   把这些概念拿到浏览器中来说，当你打开一个 Tab 页时，其实就是创建了一个进程，一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。
```



###  **什么是执行栈？**

```
 栈： 一种存放数据的内存区域；

   调用栈
   （1）当脚本要调用一个函数时，解析器把该函数添加到栈中并且执行这个函数。并形成一个栈帧 
   （2）任何被这个函数调用的函数会进一步添加到调用栈中，形成另一个栈帧,并且运行到它们被上个程序调用的位置。 
	（3）当执行完这个函数后，如果它没有调用其他函数，则它会从调用栈中推出。然后调用栈继续运行其他部门。 
    （4) 异步函数的回调函数一般都会被添加到运行队列里面，如settimeout会在响应的时间后把回调函数放入队列中，队列里的函数需要等栈为空时才会被推入栈中执行。如果队列中有其他函数，需要等队列前面的函数被堆入调用栈中之后才会运行。
```



###  **new 的原理是什么？通过 new 的方式创建对象和通过字面量创建有什么区别？ **

```
在调用 new 的过程中会发生以上四件事情：

   新生成了一个对象
   链接到原型
   绑定 this
   返回新对象

   使用 new Object() 的方式创建对象需要通过作用域链一层层找到 Object，但是你使用字面量的方式就没这个问题，所以更推荐使用字面量的方式创建对象。
```



###  **跨域请求资源的几种方式**

```
由于浏览器同源策略，凡是发送请求URL的协议、域名、端口三者之间任意一与当前页面地址不同即为跨域。

（1）JSONP（jsonp跨域get请求） 
    这种方式主要是通过动态创建一个script标签，浏览器对script的资源引用没有同源限制，同时资源加载到页面后会立即执行；（创建script标签向不同域提交http请求的不会被拒绝的方法，jsonp标签的src属性是没有跨域限制的）
    实际项目中JSONP通常用来获取json格式数据，这时前后端通常约定一个参数callback，该参数的值，就是处理返回数据的函数名称；

缺点：这种方式无法发送post请求，另外要确定jsonp的请求是否失败并不容易，大多数框架的实现都是结合超时时间来判断。


（2）proxy 代理
这种方式首先将请求发送给后台服务器，通过服务器来发送请求，然后将请求的结果传递给前端；需要注意的是如果你代理的是https协议的请求，那么你的proxy首先需要信任该证书或者忽略证书检查，否则你的请求无法成功。

（3）cors
当你使用XMLHttpRequest发送请求时，浏览器发现该请求不符合同源策略，会给该请求头origin，后台进行一系列处理，如果确定接受请求则在返回结果加入一个响应头Access-Control-Allow-Origin；浏览器判断该响应头中是否包含Origin的值，如果有则浏览器会处理响应，我们就可以拿到响应数据，如果不0这时我们无法拿到响应数据； 
```

###  监控

```
页面埋点、性能监控、异常监控。

页面埋点 {
	PV / UV
	停留时长
	流量来源
	用户交互
	（归纳为手写埋点和无埋点的方式）
}

性能监控{
	只需要调用 performance.getEntriesByType('navigation')
}

异常监控{
	代码报错、接口异常上报。
}
```

###  UDP 与 TCP 的区别是什么？

```
传输的两个协议：UDP  TCP；

1. UDP 协议是面向无连接的，也就是说不需要在正式传递数据之前先连接起双方。
2. UDP 不支持一对一的传输方式，支持一对多，多对多，多对一的方式（单播，多播，广播）。
3. UDP 的头部开销小，只有八字节，相比 TCP 的至少二十字节要少得多，在传输数据报文时是很高效的。

TCP
1. 链接需要三次握手（状态机）

ARQ 超时重传机制（ARQ 协议包含停止等待 ARQ 和连续 ARQ 两种协议。）

	面向无连接：
在发送端，应用层将数据传递给传输层的 UDP 协议，UDP 只会给数据增加一个 UDP 头标识下是 UDP 协议，然后就传递给网络层了
在接收端，网络层将数据传递给传输层，UDP 只去除 IP 报文头就传递给应用层，不会任何拼接操作
	UDP 头部包含了以下几个数据
两个十六位的端口号，分别为源端口（可选字段）和目标端口
整个数据报文的长度
整个数据报文的检验和（IPv4 可选 字段），该字段用于发现头部信息和数据中的错误
```

###  HTTP 及 TLS？

```
HTTP 请求由三部分构成，分别为：

请求行
首部
实体

HTTPS 还是通过了 HTTP 来传输信息，但是信息通过 TLS 协议进行了加密。

TLS 协议位于传输层之上，应用层之下,首次进行 TLS 协议传输需要两个 RTT ，接下来可以通过 Session Resumption 减少到一个 RTT。
在 TLS 中使用了两种加密技术，分别为：对称加密和非对称加密
```

###  Post 和 Get 的区别？

```
1. Get 请求能缓存，Post 不能
2. Post 相对 Get 安全一点点，因为Get 请求都包含在 URL 里（当然你想写到 body 里也是可以的），且会被浏览器保存历史纪录。Post 不会，但是在抓包的情况下都是一样的。
3. URL有长度限制，会影响 Get 请求，但是这个长度限制是浏览器规定的，不是 RFC 规定的
4. Post 支持更多的编码类型且不对数据类型限制
```

###  常见状态码？

```
2XX 成功
200 OK，表示从客户端发来的请求在服务器端被正确处理
204 No content，表示请求成功，但响应报文不含实体的主体部分
205 Reset Content，表示请求成功，但响应报文不含实体的主体部分，但是与 204 响应不同在于要求请求方重置内容
206 Partial Content，进行范围请求

3XX 重定向
301 moved permanently，永久性重定向，表示资源已被分配了新的 URL
302 found，临时性重定向，表示资源临时被分配了新的 URL
303 see other，表示资源存在着另一个 URL，应使用 GET 方法获取资源
304 not modified，表示服务器允许访问资源，但因发生请求未满足条件的情况
307 temporary redirect，临时重定向，和302含义类似，但是期望客户端保持请求方法不变向新的地址发出请求

4XX 客户端错误
400 bad request，请求报文存在语法错误
401 unauthorized，表示发送的请求需要有通过 HTTP 认证的认证信息
403 forbidden，表示对请求资源的访问被服务器拒绝
404 not found，表示在服务器上没有找到请求的资源

5XX 服务器错误
500 internal sever error，表示服务器端在执行请求时发生了错误
501 Not Implemented，表示服务器不支持当前请求所需要的某个功能
503 service unavailable，表明服务器暂时处于超负载或正在停机维护，无法处理请求
```

###  http1.1和http2？

```
http/1:因为浏览器限制了同一个域名下的请求数量（Chrome 下一般是限制六个连接），当页面中需要请求很多资源的时候，队头阻塞（Head of line blocking）会导致在达到最大请求数量时，剩余的资源需要等待其他资源请求完成后才能发起请求。（对头阻塞）

在 HTTP/2 中引入了多路复用的技术，这个技术可以只通过一个 TCP 连接就可以传输所有的请求数据。多路复用很好的解决了浏览器限制同一个域名下的请求数量的问题，同时也接更容易实现全速传输(多路复用)

HTTP/2 通过多路复用、二进制流、Header 压缩等等技术，极大地提高了性能，但是还是存在着问题的
QUIC 基于 UDP 实现，是 HTTP/3 中的底层支撑协议，该协议基于 UDP，又取了 TCP 中的精华，实现了即快又可靠的协议
```

###  输入 URL 到页面渲染的整个流程？

```
简介：
DNS：就是通过域名查询到的具体的IP，而 IP 存在数字和英文的组合（IPv6），很不利于人类记忆，所以就出现了域名。在TCP握手之前就进行了DNS查询；
www.google.com
1. 操作系统会首先在本地缓存中查询 IP
2. 没有的话会去系统配置的 DNS 服务器中查询
3. 如果这时候还没得话，会直接去 DNS 根服务器查询，这一步查询会找出负责 com 这个一3级域名的服务器
4. 然后去该服务器查询 google 这个二级域名
5. 接下来三级域名的查询其实是我们配置的，你可以给 www 这个域名配置一个 IP，然后还可以给别的三级域名配置一个 IP  
(迭代查询（客户端做请求）/递归查询（DNS服务器请求的结果返回客户端）)
6. TCP握手， 应用层下发数据给传输层，此时TCP协议指明两段的端口号然后下发给网路层；网络层中的 IP 协议会确定 IP 地址，并且指示了数据传输中如何跳转路由器。
7. 数据在进入服务端之前，可能还会先经过负责负载均衡的服务器，它的作用就是将请求合理的分发到多台服务器上，判断当前的状态码，200继续解析、500 400就会报错、300就会重定向
8. 开始渲染
```

###  渲染流程？

```
1. 渲染流程，先会根据 HTML 构建 DOM 树，有 CSS 的话会去构建 CSSOM 树。如果遇到 script 标签的话，会判断是否存在 async 或者 defer ，前者会并行进行下载并执行 JS，后者会先下载文件，然后等待 HTML 解析完成后顺序执行。

2. CSSOM 树和 DOM 树构建完成后会开始生成 Render 树，这一步就是确定页面元素的布局、样式等等诸多方面的东西

3. 在生成 Render 树的过程中，浏览器就开始调用 GPU 绘制，合成图层，将内容显示在屏幕上了。
```

###  设计模式有哪些？

```
1. 工厂模式（Vue创建异步组件）
2. 单例模式（全局缓存、全局状态管理等等这些只需要一个对象）
3. 适配器模式（适配器用来解决两个接口不兼容的情况，不需要改变已有的接口，通过包装一层的方式实现两个接口的正常协作。）
4. 装饰模式（装饰模式不需要改变已有的接口，作用是给对象添加功能）
5. 代理模式（控制对象的访问，不让外部直接访问对象）
6. 发布-订阅模式（观察者模式： 点击事件）
7. 外观模式（提供一个接口，隐藏内部的逻辑，更加方便外部的调用）（添加事件）
```

###  斐波那契数列？

```
function fib(n) {
  if (n < 2 && n >= 0) return n
  return fib(n - 1) + fib(n - 2)
}
fib(10)
```

###  export default 和 module.export 的区别？

CommonJS规范：

CommonJS定义的模块分为: 模块标识(module)、模块定义(exports) 、模块引用(require)

```txt
require: node 和 es6 都支持的引入(CommonJS规范)
export / import : 只有es6 支持的导出引入
module.exports / exports: 只有 node 支持的导出(CommonJS规范)
exports = module.exports 都指向同一个内存地址

1. require方法用于加载模块;
2. module变量代表当前模块。这个变量是一个对象，module对象会创建一个叫exports的属性，这个属性的默认值是一个空的对象：
3. export 对应的 import，相当于 export { default as }  from "";
4. export default在一个模块中只能有一个，当然也可以没有。export在一个模块中可以有多个。
5. export default的对象、变量、函数、类，可以没有名字。export的必须有名字。
6. export default对应的import和export有所区别
```

```
ES6
export 和 export default的区别:

1. 在一个文件或模块中，export、import可以有多个，export default仅有一个
2. 通过export方式导出，在导入时要加{ }，export default则不需要
3. export能直接导出变量表达式，export default不行。
```



###  **浏览器储存的方式？优缺点？**

cookie，localStorage，sessionStorage，indexDB

|   特性   |             cookie             |      localStorage      | sessionStorage |        indexDB         |
| :------: | :----------------------------: | :--------------------: | :------------: | :--------------------: |
| 生命周期 | 由服务器生成，可以设置过期时间 | 除非被清理否则一直存在 | 页面关闭就清理 | 除非被清理否则一直存在 |
|   大小   |               4K               |           5M           |       5M       |           5M           |

Service Worker 是运行在浏览器背后的**独立线程**，一般可以用来实现缓存功能。使用 Service Worker的话，传输协议必须为 **HTTPS**。因为 Service Worker 中涉及到请求拦截，所以必须使用 HTTPS 协议来保障安全。

Service Worker 实现缓存功能一般分为三个步骤：首先需要先注册 Service Worker，然后监听到 `install` 事件以后就可以缓存需要的文件，那么在下次用户访问的时候就可以通过拦截请求的方式查询是否存在缓存，存在缓存的话就可以直接读取缓存文件，否则就去请求数据。



###  **缓存策略?**

**强缓存**：强缓存可以通过设置两种 HTTP Header 实现：`Expires` 和 `Cache-Control` 。强缓存表示在缓存期间不需要请求，`state code` 为 200。

**协商缓存**： 如果缓存过期了，就需要发起请求验证资源是否有更新。协商缓存可以通过设置两种 HTTP Header 实现：`Last-Modified` ：`Last-Modified` 表示本地文件最后修改日期和 `ETag` 。

缓存策略都是通过设置 HTTP Header 来实现的。



###  **什么是 XSS 攻击？如何防范 XSS 攻击？什么是 CSP？**

XXS 跨站脚本攻击

XSS 可以分为：**持久型和非持久型**。

XSS是一种在web应用中的计算机安全漏洞，它允许恶意web用户将代码植入到提供给其它用户使用的页面中。

**危害**： 

- 盗取用户账号
- 非法转账
- 强制发sing电子邮件
- 盗窃资料等

**如何防御**

- 转义字符
- CSP
  - 设置 HTTP Header 中的 `Content-Security-Policy`
  - 设置 `meta` 标签的方式 `<meta http-equiv="Content-Security-Policy">`

**CSP** :  加密服务提供者

1. CSP是真正执行密码运算的独立模块
2. 物理上一个CSP由两部分组成：一个动态连接库，一个签名文件
3. 签名文件保证密码服务提供者经过了认证，以防出现攻击者冒充CSP
4. 若加密算法用硬件实现，则CSP还包括硬件装置
5. Microsoft通过捆绑RSA Base Provider，在操作系统中提供一个CSP，使用RSA公司的公钥加密算法，更多的CSP可以根据需要增加到应用中。
6. Windows 2000以后自带了多种不同的CSP.



###  **什么是 CSRF 攻击？如何防范 CSRF 攻击？**

​	CSRF 中文名为 **跨站请求伪造** 。原理就是攻击者构造出一个后端请求地址，诱导用户点击或者通过某些途径自动发起请求。如果用户是在登录状态下的话，后端就以为是用户在操作，从而进行相应的逻辑。

**如何防御**

防范 CSRF 攻击可以遵循以下几种规则：

1. Get 请求不对数据进行修改
2. 不让第三方网站访问到用户 Cookie
3. 阻止第三方网站请求接口
4. 请求时附带验证信息，比如验证码或者 Token



###  **什么是点击劫持？如何防范点击劫持？**

**`点击劫持`**  是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 `iframe` 嵌套的方式嵌入自己的网页中，并将 `iframe` 设置为透明，在页面中透出一个按钮诱导用户点击。

- X-FRAME-OPTIONS
- JS防御





###  **图片加载优化**

- 多使用精灵图，将多个图片文件整合到一张图片中
- 选择正确的图片格式（小图使用png，照片使用jpeg）

减少图片大小： 

- **减少像素点**
- **减少每个像素点能够显示的颜色**



###  **DNS解析**

DNS 解析也是需要时间的，可以通过预解析的方式来预先获得域名所对应的 IP。



###  **预加载**

当有些资源不需要马上用到，但是希望尽早获取，这时候就可以使用预加载。

预加载其实是声明式的 `fetch` ，强制浏览器请求资源，并且不会阻塞 `onload` 事件，可以使用以下代码开启预加载

```html
<link rel="preload" href="http://example.com">
```

特点;

- 预加载可以降低首屏的加载时间，
- 可以将不影响首屏但重要的文件延后加载
- 兼容性差



###  **什么是 MVVM？比之 MVC 有什么区别？**

ViewModel 将视图中的状态和用户的行为分离出一个抽象，

即模型-视图-视图模型。【模型】指的是后端传递的数据。【视图】指的是所看到的页面。【视图模型】mvvm模式的核心，它是连接view和model的桥梁.



###  **什么是 Virtual DOM？为什么 Virtual DOM 比原生 DOM 快？**

vdom可以看作是一个使用javascript模拟了DOM结构的树形结构，这个树结构包含整个DOM结构的信息

特点：

1. 将 Virtual DOM 作为一个兼容层，还能对接非 Web 端的系统，实现跨端开发。
2. 同样的，通过 Virtual DOM 我们可以渲染到其他的平台，比如实现 SSR（服务端渲染）、同构渲染等等。
3. 实现组件的高度抽象化



###  **路由原理**

监听URL的变化：

- hash模式  -------当 `#` 后面的哈希值发生变化时，可以通过 `hashchange` 事件来监听到 URL 的变化，从而进行跳转页面，
- history模式  --------主要使用 `history.pushState` 和 `history.replaceState` 改变 URL。

两种模式的对比：

- Hash 模式只可以更改 `#` 后面的内容，History 模式可以通过 API 设置任意的同源 URL
- History 模式可以通过 API 添加任意类型的数据到历史记录中，Hash 模式只能更改哈希值，也就是字符串
- Hash 模式无需后端配置，并且兼容性好。History 模式在用户手动输入地址或者刷新页面的时候会发起 URL 请求，后端需要配置 `index.html` 页面用于匹配不到静态资源的时候



###  **Vue和React之间的区别**

- Vue实现双向绑定，修改状态比较简单，react需要使用setState来改变状态
- Vue使用了模板语法，相比react使用的 `JSX` 没有那么灵活
- Vue一开始的定位就是尽可能的讲的开发者的门槛，而react更多的是改变用户去接受它的思想和概念



###  **Vue生命周期钩子函数**

- 初始化`initState`时是获取不到` props `和` data` 的数据的 ;  如：beforeCreate;
- 执行created函数（此时为挂载）;
- 执行`beforeMount `，开始创建`VDOM`, 最后执行mounted钩子， 并将`VDOM` 渲染为真实的DOM;
- 数据更新时调用` beforeUpdate` 和 `Upadte`;
- keep-alive独有的生命周期； `activated` 和`deactivated` ； 用`keep-alive` 包裹的组件不会被销毁， 而是缓存到` deactivated钩子` 函数

​    

###  **并发和并行的区别 **

- 并发是宏观概念，我分别有任务 A 和任务 B，在一段时间内通过任务间的切换完成了这两个任务，这种情况就可以称之为并发。
- 并行是微观概念，假设 CPU 中存在两个核心，那么我就可
- 以同时完成任务 A、B。同时完成多个任务的情况就可以称之为并行。



###   **什么是回调函数、特点、如何解决回调地狱？ **

回调函数： callback

概念： 回调函数就是一个通过[函数指针](https://baike.baidu.com/item/%E5%87%BD%E6%95%B0%E6%8C%87%E9%92%88/2674905)调用的函数。如果你把函数的[指针](https://baike.baidu.com/item/%E6%8C%87%E9%92%88/2878304)（地址）作为[参数传递](https://baike.baidu.com/item/%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92/9019335)给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。

回调函数：

1. 不能使用try catch捕获错误；
2. 不能return

回调地狱：

1. 嵌套函数存在耦合性，一旦有所改动就可能影响某些代码功能；
2. 嵌套函数一般很难处理错误；



###   **async和await的特点，await的原理？ **

async： 异步、await： 等待

- 一个函数加上async，该函数就会返回一个promise；

```js
// async语法： 在函数前面添加async关键字
async function timeout() {
    return 'hello world'
}
timeout();
console.log('虽然在后面，但是我先执行');
```

- await只能配套async使用；



###   **常用定时器函数 **

setTimeout（超时定时器）、setInterval（间隔定时器）、requestAnimationFrame（循环定时器）

setTimeout 会比 promise后执行



###   **进程与线程区别？JS 单线程带来的好处？ **

- 进程描述了 CPU 在**运行指令及加载和保存上下文所需的时间**，放在应用上来说就代表了一个程序。
- 线程是进程中的更小单位，描述了执行一段指令所需的时间。
- JS单线程可以达到节省内存，节约上下文切换时间，没有锁的问题的好处；

```htlml
	把这些概念拿到浏览器中来说，当你打开一个 Tab 页时，其实就是创建了一个进程，一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。
```



### **什么是执行栈？ **

栈： 一种存放数据的内存区域；

调用栈

（1）当脚本要调用一个函数时，解析器把该函数添加到栈中并且执行这个函数。并形成一个栈帧
（2）任何被这个函数调用的函数会进一步添加到调用栈中，形成另一个栈帧,并且运行到它们被上个程序调用的位置。
（3）当执行完这个函数后，如果它没有调用其他函数，则它会从调用栈中推出。然后调用栈继续运行其他部门。
（4) 异步函数的回调函数一般都会被添加到运行队列里面，如settimeout会在响应的时间后把回调函数放入队列中，队列里的函数需要等栈为空时才会被推入栈中执行。如果队列中有其他函数，需要等队列前面的函数被堆入调用栈中之后才会运行。

   

###    **Jquery的事件绑定方式有几种，说明其优缺点？ **

   jQuery目前有四种绑定方式：`on()`,   `bind()`,   `delegate()`,   `live()`；

*  `bind() `的事件绑定是只对当前页面选中的元素有效，不能对动态创建的元素绑定事件，使用 `unbind() ` 取消事件；

* `on() `绑定单事件、多事件、多事件多函数绑定、使用 `on `进行事件委托；使用 `0ff() ` 取消事件；

  ```js
  <button id="add" type="button">add DIV</button>
  
  $("button").on("mouseover click",function(){
  console.log($(this).html())
  })；
  ```

* `delegate() `的事件是利用事件冒泡，事件绑在父元素上，获得目标元素

```bash
不同点：
1.绑定位置：bind直接绑定在目标元素（子元素上）
delegate绑在父元素上
2.监听个数：bind监听个数多
delegate监听个数少
3.动态生成子元素
delegate动态生成的新子元素可自动获得父元素上的事件处理函数
bind动态生成的新子元素必须反复绑定
```



### css浏览器兼容性的写法

- *， ie6,ie7可以识别；
-    _和- ，  ie6可以识别；
- ​    !important  ,表示高优先级，ie7及以上，firefox都支持，ie6认识带!important的样式属性，但不认识!important的优先级；
- -webkit- ，针对safari，chrome浏览器的内核CSS写法
- -moz-，针对firefox浏览器的内核CSS写法
- -ms-，针对ie内核的CSS写法
- -o-，针对Opera内核的CSS写法



### 常见的CSSbug和CSShack

1、图片间隙 

display：block

2、dt ,li中图片间隙,

将img转为快长元素添加声明display：block

3、双倍浮向

display：inline

4、图片在IE中有蓝色边框

给imgde边写成0，img{border：0}

5、默认高度

IE6及以下版本部分元素快有默认高度

font-size：0；overflow：hidden；

6、表单元素距离顶部间距不一致

float：left‘

7、按钮元素默认大小不一

统一大小，input外边套一个标签

8、百分比BUG  

clear：right；

9、鼠标指针BUD

corsor:pointer;

10、子元素没有设置浮动，设置margin-top属性后会错误的吧margin-top的属性添加给父元素

overflow:hidden;



### 五大浏览器内核

Trident（MSHTML）：IE 遨游、腾讯、360

Gecko：Linux、  MacOS X   开源

Presto：opera

Webkit ： safari、chrome  开源

blink:  Google



### 元素类型有哪些？

1、块状元素

自上而下，块状元素会占据一行不会出现并列情况；并且可以设置width和height；是其他元素的容器。自上而下

eg: div  dl  , dd,  dt,  ol,  ul , fieldset, h1-h6 ,p, form ,hr,colgroup,col,table,tr,td;

2、行内元素

始终以行内逐个显示，不能设置width和height；横向；

eg;  a, span, i ,em ,strong,

3、内联块状元素

其他元素都在一行，height和width可以设置；横向；

eg ; img,  input，select;



### 多列布局

规定多列布局之间呃价格 colum-gap

规定多列布局之间列于列的边框 column-rule

设置元素是否可以横跨所有列 column-span

规定元素被分隔的次数 column-count

设置多列布局的列宽 colum-with 



### 什么是垫片？

不满足AMD规范有依赖别的环境的插件

AMD : 依赖前置 require.j

CMD：就近依赖 sea.js

CommonJS



### gulp常见的命令行语句

查看是否安装成功：node -v 

进入环境： node

退出当前运行： 两次Ctrl+V

进入某一目录： cd 

进入上一目录： cd ..

新建文件： touch

新建目录：mkdir

删除文件： rm-rf （ 先删文件再删目录）

重启服务器： connect.reload



### 常见的SEO方式有哪些？

1. 使用隐藏文本和链接（如： 将文本和链接的颜色设置与背景一样；使用CSS隐藏文本）
2. 关键词叠加（如： 一般在标题[title标签](http://www.wzhseo.com/seorumenjiaocheng/titletag.html)、描述标签、图片[ALT标签](http://www.wzhseo.com/seorumenjiaocheng/alt.html)里大量的堆砌关键词，引起搜索引擎的注意）
3. 群发外链，
4. 站群手法
5. 网页劫持
6. PR劫持



### 伪代码快速排序

```js
 伪代码（Pseudocode）是一种非正式的，类似于英语结构的，用于描述模块结构图的语言.
 1 quicksort(A, lo, hi)
 2   if lo < hi
 3     p = partition(A, lo, hi)
 4     quicksort(A, lo, p - 1)
 5     quicksort(A, p + 1, hi)
 6 
 7 partition(A, lo, hi)
 8     pivot = A[hi]
 9     i = lo 						//place for swapping
10     for j = lo to hi - 1
11         if A[j] <= pivot
12             swap A[i] with A[j]
13             i = i + 1
14     swap A[i] with A[hi]
15     return i
```



### 简述CSS盒模型

1. 盒模型是css布局的一个基础或者叫基石；

2. 盒模型的组成：border（边框）、margin（边界、外边距）、padding（填充、内边距、补白）、content（宽和高） 

3. 盒模型规定了网页中的元素如何显示以及元素相互之间的关系；



### 如何启用`JavaScript`的严格模式

"use strict":   严格模式通过在脚本或函数的头部添加 "use strict"; 表达式来声明。



* 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
* 消除代码运行的一些不安全之处，保证代码运行的安全；
* 提高编译器效率，增加运行速度；
* 为未来新版本的Javascript做好铺垫。
* "严格模式"体现了Javascript更合理、更安全、更严谨的发展方向，包括IE 10在内的主流浏览器，都已经支持它，许多大项目已经开始全面拥抱它。



###  怎样阻止默认事件和冒泡事件？

默认事件  `window.event ? window.event.returnValue = false : e.preventDefault()`

阻止冒泡  `window.event ? window.event.cancelBubble = true : e.stopPropagation();`

```js
//阻止浏览器的默认行为 
function stopDefault( e ) { 
    //阻止默认浏览器动作(W3C) 
    if ( e && e.preventDefault ) 
        e.preventDefault(); 
    //IE中阻止函数器默认动作的方式 
    else 
        window.event.returnValue = false; 
    return false; 
}

// 阻止冒泡
function stopBubble(e) { 
//如果提供了事件对象，则这是一个非IE浏览器 
if ( e && e.stopPropagation ) 
    //因此它支持W3C的stopPropagation()方法 
    e.stopPropagation(); 
else 
    //否则，我们需要使用IE的方式来取消事件冒泡 
    window.event.cancelBubble = true; 
}
```



### Sass、LESS是什么？大家为什么要使用他们？

​     sass和less是CSS 的预处理器，是CSS的抽象层，他们赋予CSS一些动态语言的特性，如变量、继承、运算、函数等，既可以在客户端上运行，也可以在服务端运行（node.js）。

​    结构清晰，便于扩展；

​	减少无意义的机械劳动，

​	轻松实现继承；

​	兼容老的CSS代码；

Less是基于JavaScript，是在客户端处理的。

Sass是基于Ruby的，是在服务器端处理的。



### 创建函数的方式

1. 函数表达式
2. 函数声明
3. Class构造器

```js
// 函数表达式
var fn = function () {}
// 函数声明
function fn () {}
// class构造器
var fn = new Function()
```



### 创建对象的方式

​	1、字面量  var obj = {}

​    2、通过new运算符 var obj = new Object()

​    3、构造函数

​            用来构造（创建）对象的函数

​            他在声明的时候跟普通函数没有区别

​            用new运算符加上函数的调用，调用的结果就是一个对象

​            构造函数中的this指的是即将要new的那个对象

​    4、ES6语法糖



### 什么是模块化

​		函数封装   --->  对象   --->  立即执行函数   --->  模块化规范

​		是一种项目的构架模式， 这种构架模式让JS代码重用性变得非常高，让项目构架的一些复杂问题全部得以解决。如：多个script标签不会再出现了，我们只要用一个script标签进行引入就可以了。

AMD规范、CMD规范、COMMONJS



### Vue.nextTick

​		在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。



### 原生 JS **中 call()、apply()、bind() **方法有什么区别

三个方法都可以改变函数运行时的 this 指向。

三个方法第一个参数都是函数调用执行时this 指向的对象。call() 方法第二个参数是个可变参数，是函数调用执行时本身所需要的参数，apply() 方法第二个参数是数组或arguments。call()与apply()都是立即调用函数执行，在运行时修改this指向。bind()是返回一个新的函数，新函数的函数主体与原函数的函数主体一致，当新函数被调用时，函数体中 this 指向的是 bind() 方法第一个参数传递的对象，而bind() 方法不会影响原函数本身的this 指向。



### vue-组件间的通信

#### **1.父子组件的通信**

- **1.父组件利用props向子组件传输数据**

  ​		当props中接收的是父组件传递的引用类型（对象或者是数组）时，在子组件中对数据改变时，父组件中的数据也会相应的改变，因为两者是指向的同一地址内存。如果不想子组件的改变影响父组件可以利用深拷贝，将接受的数据进行深拷贝后在子组件中使用，而不直接操作接受的数据。

- **2.子组件向父组件传递参数利用事件机制**
  子组件通过`this.$emit()`派发事件，父组件利用`v-on`对事件进行监听，实现参数的传递

  ```js
  //子组件：
     this.$emit('changeCart',event.target)/*向父组件派发事件，同时传递参数event.target,后面的参数的个数不限*/
  //父组件：
  <v-cartcontrol :food="food" v-on:changeCart="changeCart"></v-cartcontrol>
  <v-cartcontrol :food="food" @changeCart="changeCart"></v-cartcontrol>
  ```

- **3.利用ref属性可以获取到dom元素或者是子组件，从而可以调用子组件的方法（注意2.0版本用ref取代了el）**
  1、当ref直接定义在dom元素上时，则通过`this.$refs.name`可以获取到dom对dom进行原生的操作.(ref属性不崩使用驼峰命名，获取元素也是)

#### **2.非父子组件的通信**

- **使用eventBus**

  ```js
  //非父子关系的两个组件之间也需要通信。在简单的场景下，可以使用一个空的 Vue 实例作为事件总线：
  var bus = new Vue()  
  // 触发组件 A 中的事件  
  bus.$emit('id-selected', 1)  
  // 在组件 B 创建的钩子中监听事件  
  bus.$on('id-selected', function (id) {  
    // ...  
  }) 
  ```



### 前端优化方法

（1） 减少http请求次数：CSS Sprites, JS、CSS源码压缩、图片大小控制合适；网页Gzip，CDN托管，data缓存 ，图片服务器。代码重构

（2） 前端模板 JS+数据，减少由于HTML标签导致的带宽浪费，前端用变量保存AJAX请求结果，每次操作本地变量，不用请求，减少请求次数

（3） 用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能。

（4） 当需要设置的样式很多时设置className而不是直接操作style。

（5） 少用全局变量、缓存DOM节点查找的结果。减少IO读取操作。

（6） 避免使用CSS Expression（css表达式)又称Dynamic properties(动态属性)。

（7）图片预加载，将样式表放在顶部，将脚本放在底部，加上时间戳



## vue面试题

一：什么是MVVM

MVVM是是Model-View-ViewModel的缩写，Model代表数据模型，定义数据操作的业务逻辑，View代表视图层，负责将数据模型渲染到页面上，ViewModel通过双向绑定把View和Model进行同步交互，不需要手动操作DOM的一种设计思想。

二：MVVM和MVC区别？和其他框架(jquery)区别？那些场景适用？

MVVM和MVC都是一种设计思想，主要就是MVC中的Controller演变成ViewModel,，MVVM主要通过数据来显示视图层而不是操作节点，解决了MVC中大量的DOM操作使页面渲染性能降低，加载速度慢，影响用户体验问题。主要用于数据操作比较多的场景。

三：Vue的优缺点是什么

优点：低耦合，可重用性，独立开发，可测试，渐进式

缺点：不利于SEO，社区维护力度不强，相比还不够成熟

三：组件之间传值

父向子传值：属性传值，父组件通过给子组件标签上定义属性，子组件通过props方法接收数据；

子向父传值：事件传值，子组件通过$emit(‘自定义事件名’，值)，父组件通过子组件上的@自定义事件名=“函数”接收

非父子组件传值：全局定义bus，var bus=new Vue() ; 发送者， bus.$emit(‘自定义名’，值) ；接受者，bus.$on(‘自定义名’，(值)=>{})

四：路由之间传参

路由字典中：routes={path:’/detail/:id’,component:Detail}

标签中：<router-link :to=”‘/detail/’+item.id ”>

Js中：this.$route.params.id

五：axios的特点和使用

特点：基于promise的Http库，支持promise的所有API，用来请求和响应数据的，而且对响应回来的数据自动转化为json类型，安全性较高，客户端支持防御XRSF(跨站请求伪造)，默认不携带cookie;

使用：下载包后引入 import axios from ‘axios’ , 让其携带cookie ，axios.defaults.withCredentials=true, 然后添加到prototype中，Vue.prototype.$axios=axios ,组建中不用引入直接使用this.$axios.get(url,{params:{id:1}})。

六：Vuex是什么？怎么使用？用于哪些场景？

Vuex是框架中状态管理；新建目录store...export,然后main.js引入store再注入到vue实例中；用于购物车，登录状态，单页应用等。

七：Vuex有哪几种属性？

五种：state，action，mutation，getter，module

State：数据源存放地，数据是响应式的

Action: 逻辑处理，提交的是mutation,包含任意异步操作

Mutation: 修改state里的公共数据

Getter: 相当于计算属性，可以复用，可缓存

Module: 模块化

八：Vuex取值

This.$store.state.city

This.$store.commit(‘getData’)

this.$store.dispath(‘getData’)

This.$store.getters.getData

九：不使用vuex会带来什么问题？

可维护性下降，可读性下降，增加耦合

十：v-show和v-if指令的共同点和不同点

V-show指令是通过修改元素的display的css样式使其显示隐藏

V-if指令是销毁和重建DOM达到让元素显示隐藏

十一：如何让css只在当前组件中起作用?

将当前组件的<style>修改为<style scoped>

十二：<keep-alive></keep-alive>的作用是什么，如何使用？

包裹动态组件时，会缓存不活动的组件实例，主要用于保留组件状态或避免重新渲染；

使用：简单页面时

缓存：  <keep-alive include=”组件名”></keep-alive>

不缓存：<keep-alive exclude=”组件名”></keep-alive>

使用：复杂项目时

路由字典中定义{path:’/detail’,meta:{keepAlive:false/true}} 是否缓存

根目录中：

<keep-alive><router-view v-if=”$route.meta.keepAlive”></router-view></keep-alive>

<keep-alive><router-view v-if=” ! $route.meta.keepAlive”></router-view></keep-alive>

 

十三：Vue数据双向绑定原理

Vue数据双向绑定是通过数据劫持结合发布者-订阅者模式方式来实现的，语法主要有{{}}和v-model。首先用递归方法遍历所有的属性值，再用Object.defineProperty()给属性绑定getter和setter方法添加一个observe(val)监听器对数据进行劫持监听;然后创建一个订阅器来在getter里收集订阅者并创建和绑定watcher，如果数据变化，订阅者就会执行自己对应的更新函数;watcher就是在自身实例化的时候往订阅器里添加自己，自身必须有一个update的数据，是监听器和模板渲染的通信桥梁;最后创建解析模板指令compile，替换数据，初始化视图。最终observer来监听自己的model数据变化通过compile解析编译模板指令，利用watcher搭起observer和compile之间的通信桥梁，达到数据变化->视图更新双向绑定效果。

十四：Vue生命周期

vue生命周期就是从开始创建，初始化数据，编译模板，挂载DOM，渲染->更新->渲染，销毁等一系列过程。生命周期钩子如下：

组件实例周期：

BeforeCreate：实例初始化后，无法访问方法和数据；

Created：实例创建完成，可访问数据和方法，注意，假如有某些数据必须获取才允许进入页面的话，并不适合；

beforeMonut：挂载DOM之前

Mounted :el被新创建的vm.$el替换，可获取dom，改变data，注意，beforeRouterEnter的next的钩子比mountend触发靠后；

beforeUpdate：数据更新时调用，发生在虚拟DOM重新渲染前；

Updated：数据更改后，可以执行依赖于DOM的操作，注意，应该避免在此期间更改状态，可能会导致更新无限循环；

beforeDestroy：实例销毁之前，这一步还可以用this获取实例，一般在这一步做重置操作，比如清定时器监听dom事件；

Destroyed：实例销毁后，会解除绑定，移除监听。

十五：路由钩子

全局路由钩子：

Router.beforeEach((to,from,next)=>{... next()})

注意：一定要调用next(),否则页面卡在那，一般用于对路由跳转前进行拦截，参数：

To：即将要进入的目标路由对象    From：当前导航正要离开的路由

Next()：跳转下一个页面      next(‘/path’)：跳转指定路由

Next(false)：返回原来页面  next((vm)=>{})：且在beforeRouterEnter用

比如根据登录状态跳转页面判断(to.name->name是路由名)

Router.beforeEach(function(to,from,next){if(to.name==’login’){..}next();})

Router.afterEach((to,from)=>{}) 跳转后调用没有next方法

组件路有钩子：

beforeRouteEnter(to,from,next){next(vm=>{...})} 路由跳转时

注意：此钩子在beforeCreate之前执行，但是next在组件mounted周期之后,无法直接调用this访问组件实例，可用next访问vm实例，修改数据；

beforeRouteLeave(to,from,next){...next()} 离开路由时

注意：可以直接访问this,next不可回调

beforeRouteUpdate 路由切换时

十六：指令周期

Bind：一次初始化调用          inserted：被绑定元素插入父节点调用

Update：模板更新调用         unbind：指令与元素解绑时

Vue.nextTick：在dom更新后执行，一般用于dom操作

Vue.$nextTick：一直到真实的dom渲染结束后执行

Ex:created(){this.$nextTick(()=>{...})}

十七：生命周期的作用是什么？

它的生命周期有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。

十八：第一次加载会触发哪几个钩子？

会触发beforeCreate , created ,beforeMount ,mounted

十九：说出至少4种vue当中的指令和用法？

V-if：判断是否隐藏         v-for：数据循环                v-bind：绑定属性

v-model：双向绑定          v-is：动态组件特殊特性 v-on：事件绑定

二十：vue-loader是什么？用途有哪些？

是解析vue文件的一个加载器，用途是js可以写es6，style样式可以scss或less，template可以加jade

二十一：active-class是那个组件属性？

Vue-router模块的router-link组件,设置激活时样式

二十二：vue中使用插件的步骤是什么？

Inport ... from ... 引入插件，Vue.use(...)全局注册

二十三：为什么使用key？

当有相同标签名和元素切换时，需要通过key特性设置唯一的值来标记让vue区分它们，否则vue为了效率只会替换相同标签内部的内容

二十三：为什么避免v-if和v-for用在一起？

当vue处理指令时，v-for比v-if具有更高的优先级，通过v-if移动到容器的元素，不会在重复遍历列表中的每个值，取而代之的是，我们只检查它一次，且不会v-if为否的时候运算v-for

二十四：VNode是什么？虚拟DOM是什么？

Vue在页面上渲染的节点，及其子节点称为虚拟节点，简称VNode；虚拟DOM时由组件树建立起来的整个VNode树的称呼

二十五：scss是什么？有哪些特性？怎么使用？

是css的预编译，特新有可以用变量($变量名=值)，可以用混合器()，可以嵌套，可以继承，可以运算，安装先装css-loader，node-loader，sass-loader，在webpack.base配置，style标签上加lang=”scss”

二十五：Vue router如何实现跳转

<router-link></router-link>   router.push(‘/’)      router.go(0)

二十六：vue router跳转和location.href有什么区别？

Router是hash改变；location.href是页面跳转，刷新页面

 二十七：v-model原理

<input v-model="sth">

==相当于通过oninput(用户输入时触发)把表单值给到变量

<input v-bind:value="sth" v-on:input="sth=$event.target.value">

二十八：vue的template的理解

通过compile编译template生成AST语法树，AST语法树经过generate转化为render function字符串后返回虚拟DOM节点(Vnode)的过程

二十九：vue和react区别

相同点：

都鼓励组件化，都有’props’的概念，都有自己的构建工具，Reat与Vue只有框架的骨架，其他的功能如路由、状态管理等是框架分离的组件。

不同点：

React：数据流单向，语法—JSX，在React中你需要使用setState()方法去更新状态

Vue：数据双向绑定，语法--HTML，state对象并不是必须的，数据由data属性在Vue对象中进行管理。适用于小型应用，但对于对于大型应用而言不太适合。

三十：单页面和多页面的区别

单页面：

整个项目中只有一个完整的HTML页面，其它"页面"只是一段HTML片断而已

优: 请求少

缺: 不利于搜索引擎优化

页面跳转本质：把当前DOM树中某个DIV删除，下载并挂载另一个div片断

多页面：

项目中有多个独立的完整的HTML页面

缺: 请求次数多，效率低

页面跳转本质:

删除旧的DOM树，重新下载新的DOM树

 三十一：Vue的SPA如何优化加载速度

减少入口文件体积，静态资源本地缓存，开启Gzip压缩，使用SSR，nuxt.js

三十二：Axios发送post请求

Import qs from ‘qs’

Var data=qs.stringify({

Number : ’1’

})

Axios.post(url,data).then()

VUE如何自定义属性

全局自定义：

Vue.directive(‘focus’,{

         Inserted:function(el){
    
                   el.focus()  //聚焦函数

}       

})

三十三：组件自定义

directive{

         inserted:function(el){
    
                   el.focus() 

}

}

三十四：Vue和vuex 有什么区别

Vue是框架，vuex是插件，vuex是专门为vue应用程序开发的状态管理模式

三十五：.Vuex中actions和mutations的区别

Mutations的更改是同步更改，用于用户执行直接数据更改，this.$store.commit(‘名’)触发

Actions的更改是异步操作，用于需要与后端交互的数据更改,this.$store.dispath(“名”)触发

注意：

1)：定义actions方法创建一个更改函数时，这个函数必须携带一个context参数，用于触发mutations方法，context.commit(‘修改函数名’ , ’异步请求值’)；

2)：mutations第一个参数必须传入state，第二个参数是新值



**1.css只在当前组件起作用**
答：在style标签中写入**scoped**即可 例如：<style scoped></style>

**2.v-if 和 v-show 区别**
答：v-if按照条件是否渲染，v-show是display的block或none；

**3.$route和$router的区别**
答：$route是“路由信息对象”，包括path，params，hash，query，fullPath，matched，name等路由信息参数。而$router是“路由实例”对象包括了路由的跳转方法，钩子函数等。

**4.vue.js的两个核心是什么？**
答：数据驱动、组件系统

**5.vue几种常用的指令**
答：v-for 、 v-if 、v-bind、v-on、v-show、v-else

**6.vue常用的修饰符？**
答：.prevent: 提交事件不再重载页面；.stop: 阻止单击事件冒泡；.self: 当事件发生在该元素本身而不是子元素的时候会触发；.capture: 事件侦听，事件发生的时候会调用

**7.v-on 可以绑定多个方法吗？**
答：可以

**8.vue中 key 值的作用？**
答：当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。key的作用主要是为了高效的更新虚拟DOM。

**9.什么是vue的计算属性？**
答：在模板中放入太多的逻辑会让模板过重且难以维护，在需要对数据进行复杂处理，且可能多次使用的情况下，尽量采取计算属性的方式。好处：①使得数据处理结构清晰；②依赖于数据，数据更新，处理结果自动更新；③计算属性内部this指向vm实例；④在template调用时，直接写计算属性名即可；⑤常用的是getter方法，获取数据，也可以使用set方法改变数据；⑥相较于methods，不管依赖的数据变不变，methods都会重新计算，但是依赖数据不变的时候computed从缓存中获取，不会重新计算。

**10.vue等单页面应用及其优缺点**
答：优点：Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件，核心是一个响应的数据绑定系统。MVVM、数据驱动、组件化、轻量、简洁、高效、快速、模块友好。
缺点：不支持低版本的浏览器，最低只支持到IE9；不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；第一次加载首页耗时相对长一些；不可以使用浏览器的导航按钮需要自行实现前进、后退。

**11.怎么定义 vue-router 的动态路由? 怎么获取传过来的值**
答：在 router 目录下的 index.js 文件中，对 path 属性加上 /:id，使用 router 对象的 params.id 获取。



### Vue的路由实现：hash模式 和 history模式

**hash模式：**在浏览器中符号“#”，#以及#后面的字符称之为hash，用window.location.hash读取；
特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
hash 模式下，仅 hash 符号之前的内容会被包含在请求中，如 [http://www.xxx.com](http://www.xxx.com/)，因此对于后端来说，即使没有做到对路由的全覆盖，也不会返回 404 错误。

**history模式：**history采用HTML5的新特性；且提供了两个新方法：pushState（），replaceState（）可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更。
history 模式下，前端的 URL 必须和实际向后端发起请求的 URL 一致，如 <http://www.xxx.com/items/id>。后端如果缺少对 /items/id 的路由处理，将返回 404 错误。**Vue-Router 官网里如此描述：**“不过这种模式要玩好，还需要后台配置支持……所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。”



### 什么是keep-alive

**keep-alive**是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。





### js的延迟加载有哪些？

**1.defer属性**

**2.async属性**

**3.动态创建DOM方式**

**4.使用Jquery的getScript()方法**

**5.使用setTimeout延迟方法的加载时间**

**6.让js最后加载**



### null和undefined的区别？

null： Null类型，代表“空值”，代表一个空对象指针，使用typeof运算得到 “object”，所以你可以认为它是一个特殊的对象值。

undefined： Undefined类型，当一个声明了一个变量未初始化时，得到的就是undefined。

null是javascript的**关键字，**可以认为是对象类型，它是一个空对象指针，和其它语言一样都是代表“空值”，不过 undefined 却是javascript才有的。undefined是在ECMAScript第三版引入的，为了区分空指针对象和未初始化的变量，它是一个预定义的**全局变量**。没有返回值的函数返回为undefined，没有实参的形参也是undefined。



### 浅谈深拷贝和浅拷贝，如何实现深拷贝？

深拷贝:

​		深拷贝就是能够实现真正意义上的数组和对象的拷贝。递归调用"浅拷贝"。（深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象）

- 直接遍历
- slice（）
- concat（）
- ES6 的Object.assign
- 复制粘贴
- 扩展运算符...

浅拷贝：

​		浅拷贝只是拷贝基本类型的数据，如果父对象的属性等于数组或另一个对象，那么实际上，子对象获得的只是一个内存地址，因此存在父对象被篡改的可能，浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存



### XHTML和HTML的区别

1.XHTML 元素必须被正确地嵌套。

2.XHTML 元素必须被关闭。

3.标签名必须用小写字母。

4.XHTML 文档必须拥有根元素



### 网页优化

1.网站结构优化（重构），网页中的结构、表现、行为三者分离

2.H1标签的的使用，一个页面设置一个H1标签，有助于搜索引擎明白网站架构，因为H1标签的搜索权重比其他标签高，一般用于logo区域。

3.页面头部优化（meta）

4.超链接优化

​	采用纯文本链接，少用，最好是别用Flash动画设置链接，因为搜索引擎无法识别Flash上的文字。

​	按规范书写超链接

​	最好别使用图片热点链接

5.图片优化

6.避免大“体积”的页面

7.命名规则化，使用公共代码；



### BFC

​		BFC全称 `Block Formatting Context` ，中文直译为块级格式上下文。它是`W3C CSS 2.1 `规范中的一个概念，**它决定了元素如何对其内容进行定位，以及与其他元素的关系和相互作用。**

* BFC布局规则
  1.在BFC下，内部的Box会在垂直方向，一个接一个地放置。

  2.Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠 

  3.在BFC中，每一个盒子的左外边缘（margin-left）会触碰到容器（父元素）的左边缘(border-left)（对于从右到左的格式来说，则触碰到右边缘），即使存在浮动也是如此。

  4.BFC的区域不会与float box重叠。例子：两个div，一个进行浮动，一个不浮动，这时浮动的元素会覆盖没有浮动的元素。给没有浮动的元素加overflow：hidden。就不会重合。

  5.计算BFC的高度时，浮动元素也参与计算

* 如何触发 BFC

  1.浮动元素，float 除 none 以外的值

  2.position的值不为static或者relative

  3.display为inline-block、table-cell、table-caption

  4.overflow 除了 visible 以外的值

* BFC的应用

  1.解决浮动塌陷问题

  2.自适应两栏布局（我们还可以运用BFC可以阻止元素被浮动元素覆盖的特性来实现自适应两栏布	局。方法：给没有浮动的元素加overflow：hidden。）

  3.解决设置margin值重叠问题。



### H5和CSS3新特性

1.语义化标签

2.新的表单控件

3.媒体播放 （video、audio）

4.本地存储（localStorage、sessionStorage、cookie）

5.新的选择器

6.动画

7.媒体查询

8.阴影、渐变



### post和get的区别

1.GET请求只能进行url编码，而POST支持多种编码方式。

2.GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。

3.GET请求在URL中传送的参数是有长度限制的，而POST没有。

4.GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。

5.GET能缓存，post不能





### js截取字符串的方法有哪些？ 区别？

* 函数：substring()
  定义：substring(start,end)表示从start到end之间的字符串，包括start位置的字符但是不包括end位置的字符。
* 函数：substr()
  定义：substr(start,length)表示从start位置开始，截取length长度的字符串。
*  函数：split()
  功能：使用一个指定的分隔符把一个字符串分割存储到数组
* 函数：indexOf()
  功能：返回字符串中匹配子串的第一个字符的下标
* 函数：lastIndexOf()
  定义：lastIndexOf()方法返回从右向左出现某个字符或字符串的首个字符索引值（与indexOf相反）
* 函数：John()
  功能：使用您选择的分隔符将一个数组合并为一个字符串



### src和href的区别

src用于替换当前元素，href用于在当前文档和引用资源之间确立联系。

src是source的缩写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。

<script src =”js.js”></script>
当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。

href是Hypertext Reference的缩写，指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，如果我们在文档中添加

<link href=”common.css” rel=”stylesheet”/>

那么浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。这也是为什么建议使用link方式来加载css，而不是使用@import方式。



### iframe的优缺点？

优点：

1. 解决加载缓慢的第三方内容如图标和广告等的加载问题

2. Security sandbox

3. 并行加载脚本

缺点：

1. iframe会阻塞主页面的Onload事件

2. 即时内容为空，加载也需要时间

3. 没有语意

 

### DOM操作——怎样添加、移除、移动、复制、创建和查找节点。

1. 创建新节点

createDocumentFragment() // 创建一个DOM片段

createElement() // 创建一个具体的元素

createTextNode() // 创建一个文本节点

2. 添加、移除、替换、插入

appendChild()

removeChild()

replaceChild()

insertBefore() // 在已有的子节点前插入一个新的子节点

3. 查找

getElementsByTagName() // 通过标签名称

getElementsByName() // 通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)

getElementById() // 通过元素Id，唯一性





   

   

   

   

   

   

   

   

   

   

   

   

   