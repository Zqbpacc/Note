## Vue项目结构

```js
# build 
	webpack构建命令目录，包括运行开发环境、项目打包等配置文件
# config 
	webpack和node基础、开发、线上环境的配置
# node_modules 
	项目中安装的依赖模块和包
# dist 
	webpack打包后生成的静态文件目录
# src 
	项目的根目录
# view
	页面文件  如：xxx.vue的文件
# assets 
	资源文件夹，里面放一些静态资源 
# router 
	路由文件，vue-router目录，定义路由跳转
# components
 	项目开发的vue组件 
# api
	项目所有接口封装目录
# base
	vue项目基础组件目录
# common
	项目公告资源目录 包括images、js、stylus（CSS预处理语言stlyus,包含样式重置，公共函数等）
# store
	vuex目录，定义项目状态管理
# App.vue 
	vue项目根组件 
# main.js 
	vue项目入口js文件 
# static
	可放静态资源文件 
# test
	测试文件夹，测试都写在这里 
# theme
	element.ui样式库
# .babelrc 
	bable相关配置、babel编译参数，vue开发需要babel编译 
# .editorconfig 
	vs code相关配置
# .eslintgnore
	eslint检测忽略的文件配置
# .gitignore 
	用来过滤和忽略的一些版本控制的文件，比如node_modules文件夹 
# index.html 
	项目的入口HTML
# .eslinttrc.js
	配置非standfixer配置
# .postcssrc.js
	css autoprefixer配置
# package.json 
	项目所需的各种模块，以及项目配置信息（如： 名称、版本、许可证等开元数据） 
# package-lock.json
	记录当前状态下实际安装的各个npm、package的具体来源和版本号
# README.md 
	介绍自己这个项目的说明
```





## React项目结构



```js
dist
public
 |--index.html
 |--manifest.json
 |-- xxx.icon
src
 |--components	// 各个组件
 |--reducers	// 全局状态
 |--routes		// 路由配置
 |--utils 		//工具类
 |--assets 		// 资源，静态
 |--common 		// 公共类
 |--views		// 视图文件，展示的页面
 |--actions		// actions操作文件
 |--App.js
 |--index.js
 |--store.js 	// redux储存
```





## 小程序项目结构

```js
assets				// 项目资源文件（图片）
config				// 项目的配置文件 如：后端的URL地址
pages				// 项目的页面 只存放TAB的页面
	|--index
		|--index.wxjs	// 页面逻辑
		|--index.wxml	// 页面结构
		|--index.wxss	// 页面样式
		|--index.json	// 页面配置
	|--detail
		|--detail.wxjs
		|--detail.wxml
		|--detail.wxss
		|--detail.json
services			// 小程序的服务调用
subpages			// 子页面，便于分包降低首次加载的时间
utils				// 项目的一些工具类
app.js				// 小程序的逻辑，生命周期、全局变量等
app.json			// 小程序的公共配置
	|--pages		// pages中视图文件的路径，第一个当作首页，是一个数组
	|--window		// 窗口表现行为（全局tittle名称、背景色、navibar颜色样式、title加载等，是一个对象）
	|--tabar		// tabbar的list数组至少两个，pagepath、text、icon、color、selectedColor/path等
	|--debug		// debug模式true、false
app.wxss			// 小程序的公共样式表
project.config.json // 小程序的项目配置
	
```

​				请求

![](E:\Note\images\network_request.pngwxChat-.png)

​				navigationBar

![](E:\Note\images\wxChat-navitabar.png)

​				tabbar

![](E:\Note\images\wxChat-tabbar.png)



![](E:\Note\images\wxChat-tabbarList.png)