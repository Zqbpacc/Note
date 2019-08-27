## Angular

Angular 的模板语法扩展了 HTML 和 JavaScript。

* 对比各种 JS 模板引擎的设计思路
* Mustache（八字胡）语法
* 模板内的局部变量

* [] 属性绑定
* {{}} 插值表达式
* ( Click ) 事件绑定, 事件绑定是通过把事件名称包裹在圆括号 `()` 中完成的
* 双向绑定 app-modle

- 结构型指令 ***ngIf**、***ngFor**、**ngSwitch**

- 属性型指令 **NgClass**、**NgStyle**、**NgModel**

- **ng-app** 指令定义一个 AngularJS 应用程序。

  **ng-model** 指令把元素值（比如输入域的值）绑定到应用程序。

  **ng-bind** 指令把应用程序数据绑定到 HTML 视图。
  
- 管道格式化数据pipe



![](http://images.gitbook.cn/e0c611d0-acb3-11e7-9ec8-4915d3122415)

* Component（组件）是整个框架的核心，也是终极目标。“组件化”的意义有2个：第一是分治，因为有了组件之后，我们可以把各种逻辑封装在组件内部，避免混在一起；第二是复用，封装成组件之后不仅可以在项目内部复用，而且可以沉淀下来跨项目复用。
* NgModule（模块）是组织业务代码的利器，按照你自己的业务场景，把组件、服务、路由打包到模块里面，形成一个个的积木块，然后再用这些积木块来搭建出高楼大厦。
* Router（路由）的角色也非常重要，它有3个重要的作用：第一是封装浏览器的 History 操作；第二是负责异步模块的加载；第三是管理组件的生命周期。

即@Angular/core 有Component、 NgMoudle、 Router三个模块。





### 安装Angular CLI

* 要使用 `npm` 命令安装 CLI，请打开终端/控制台窗口，输入如下命令：

  ```bash
  $ npm install -g @angular/cli
  ```



* 创建工作空间和厨师应用

  1. 运行 CLI 命令 `ng new` 并提供 `my-app` 名称作为参数，如下所示：

  ```bash
  $ content_copyng new my-app
  ```

  2. `ng new` 命令会提示你提供要把哪些特性包含在初始应用中。按 Enter 或 Return 键可以接受默认值。

  Angular CLI 会安装必要的 Angular npm 包和其他依赖包。这可能要花几分钟的时间

  

* 运行应用

  Angular CLI 中包含一个服务器，方便你在本地构建和提供应用。

  1. 转到 workspace 文件夹（`my-app`）。
  2. 使用 CLI 命令 `ng serve` 和 `--open` 选项来启动服务器。

  ```
  content_copycd my-app ng serve --open
  ```

  `ng serve` 命令会启动开发服务器、监视文件，并在这些文件发生更改时重建应用。

  `--open`（或者只用 `-o` 缩写）选项会自动打开你的浏览器，并访问 `http://localhost:4200/`。



修改端口号

```bash
$  ng serve --port ###
```

构建项目

```bash
$  ng build，如果你想构建最终的产品版本，可以用 ng build --prod
```

自动创建指令

```bash
$  ng g d MyDirective
```

自动创建服务

```bash
$  ng g s MyService
```





### 项目目录文件解析

1.     e2e：终到端(End-to-End)的测试目录，包含基本的测试桩。

2.     node_modules：Node.js创建了这个文件夹，并且把package.json中列出的所有第三方模块都存放在该目录中(是由Node.js开发环境自行创建的目录)

3.     src：应用源代码目录，开发者写的代码都存储在这个目录下面

        其中包含的目录和文件有如下几类

        app文件夹：包含5个文件

               app.component.css    		 样式文件，作用于app文件夹的html
            
               app.component.html   		 网页文件
            
               app.component.spec.ts
            
               app.component.ts       	 typescript文件(功能模块)
            
               app.modules.ts            根模块.配置文件,告诉angular如何组装应用程序(引导运行应用)

4．assets: 静态资源文件夹

5．environments  ; 包含为各个目标环境准备的文件

6．index.html ：整个应用程序的根html

7．main.ts：整个web程序的入口点，也是脚本程序的入口点，有点像main方法

8．style.css：全局样式文件，作用范围是整个项目

9．polyfills.ts：用于导入一些必要的库，可以使angular可以运行在老版本浏览器

10. test.ts：用于单元测试的入口点

11. tsconfig.app.json  tsconfig.spec.json : typescript编辑器的配置文件

12.angula.cli.json : angular命令行工具的配置文件，在这个文件中可以设置一系列的默认值，也可以配置项目编译时要包含的文件。例如第三方包

13.package.json : 第三方依赖包的声明文件



### 路由

使用 Angular 的*路由器*。借助 Angular [路由器](https://www.angular.cn/guide/glossary#router)，你可以根据用户在应用中的位置向用户显示不同的组件和数据。当用户执行应用任务时，路由器可以从一个视图导航到另一个视图。

- 在地址栏中输入一个 URL，浏览器就会导航到相应的页面。

- 点击页面上的链接，浏览器会导航到新页面。

- 点击浏览器的后退和前进按钮，浏览器会在你看过的页面历史中前后导航。



**组件出口**： <router-outlet></router-outlet>

**路由链接**： <a href="#" routerLink="/"></a> 使用RouterLink - 可以让你链接到应用程序的特定部分， href - 规定链接指向的页面的URL地址，若是不使用href属性则不能使用下载、媒体、rel、目标以及类型属性

**路由传参**：

在路由中传参有3种方法：

 1.routerLink

```js
 //单一参数：
page:<a routerLink="/storeProdList/statu"></a>
router:
{   path: 'storeProdList/:statu',
    component: StoreProdListPage
}

//多个参数：queryParams携带多个参数，这个参数的格式可以是自行组织的object
routerLink=["/exampledetail",{queryParams:object}]

//也可以分开多个参数写成
routerLink=["/exampledetail",{queryParams:'id':'1','name':'yxman'}]
```

​      2.router.navigate

```js
单一参数：this.router.navigate(['/exampledetail',id])，多用在调用方法里

多个参数：this.router.navigate(['/exampledetail'],{queryParams:{'name':'helen'}})
```

​      3.router.navigateByUrl：

```js
单一参数：this.router.navigateByUrl('/exampledetail/id');

多个参数：this.router.navigateByUrl('/exampledetail',{queryParams:{'name':'yxman'}});
```

**路由守卫：**

概述：

* 路由守卫，应用在这个路由不是对所有导航都有效的，是有一些前置条件的，比如可能用户得先登录（认证）或者在显示目标组件前，你可能得先获取某些数据等等，只有当这些前置条件满足的时候，才能被导航到该页面。

* 你可以往路由配置中添加守卫，守卫返回一个boolean值，以控制路由器的行为：如果它返回 
  true，导航过程会继续,如果它返回 false，导航过程会终止，且用户会留在原页面。

* 当然这时候也可以被导航到其他页面。也可以返回一个Observable或Promise，并且路由器会等待这个可观察对象被解析为true或false。

  

路由守卫接口：

* 用CanActivate来处理导航到某路由的情况。

* 用CanActivateChild来处理导航到某子路由的情况。

* 用CanDeactivate来处理从当前路由离开的情况.

* 用Resolve在路由激活之前获取路由数据。

* 用CanLoad来处理异步导航到某特性模块的情况。

  CanActivate:  要求认证 
  CanActivateChild：保护子路由

  

Reasolve：预先获取组件数据

CanDeactivate：处理未保存的更改

CanLoad - 保护特性模块的加载

* 懒加载

  使用loadChildren属性，设置一个模块的地址， 该地址是 UserModule的文件路径（相对于app 目录的），加上一个 # 分隔符，再加上导出模块的类名 UserModule。 当路由器导航到这个路由时，它会用 loadChildren 字符串来动态加载 UserModule，然后把    UserModule添加到当前的路由配置中。

  ```js
  {
   path:"user",
   loadChildren:'myApp/views/user/user.module#UserModule',
   canload:[AnthGuard]
  }
  ```

* 预加载

  在每次成功的导航后，路由器会在自己的配置中查找尚未加载并且可以预加载的模块。 是否加载某个模块，以及要加载哪些模块，取决于预加载策略。

  Router 内置了两种预加载策略：

  * 完全不预加载，这是默认值。惰性加载的特性区仍然会按需加载。

  * 预加载所有惰性加载的特性区。
  
  ​        要为所有惰性加载模块启用预加载功能，请从 Angular 的路由模块中导入 PreloadAllModules。值得注意的是CanLoad 会阻塞预加载，即 CanLoad 守卫的优先级高于预加载策略。
  
    ```js
  RouterModule.forRoot(
    appRoutes,
    {
      enableTracing: true, // <-- debugging purposes only
      preloadingStrategy: PreloadAllModules
    }
  )
    ```



**路由配置**

一、创建 app-routing.module.ts 文件并导出；

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

二、创建 app-module.ts 文件，引入 app-routing.module.ts ;

```js
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

// 引入组件的地址 import

const routes: Routes = [];  // 配置组件 path、component、redirect、loadChildren等

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```



#### 注册路由

该应用已经设置为使用 Angular 路由器，并通过路由导航到之前修改过的商品列表组件。让我们来定义一个可以显示商品详情的路由。

1. 为商品详情生成一个新组件。把组件命名为 `product-details`。

   提示：在文件列表框中，右键单击 `app` 文件夹，选择 `Angular Generator` 和 `Component`。

   

2. 在 `app.module.ts` 中，添加一个商品详情路由，该路由的 `path` 是 `products/:productId`，`component` 是 `ProductDetailsComponent`。

   ```js
   @NgModule({
     imports: [
       BrowserModule,
       ReactiveFormsModule,
       RouterModule.forRoot([
         { path: '', component: ProductListComponent },
         { path: 'products/:productId', component: ProductDetailsComponent },
       ])
     ],
   ```

   路由会将一个或多个 URL 路径与一个组件关联起来。

   

3. 使用 `RouterLink` 指令定义一个链接。`routerLink` 定义了如何在组件模板中声明式的导航到指定路由（或 URL）。

   我们希望用户点击商品名称来显示该商品的详情。

   1. 打开 `product-list.component.html`。
   2. 修改 `*ngFor` 指令，在遍历列表的过程中把 `products` 数组中的每个索引赋值给 `productId` 变量。
   3. 修改商品名称的链接，使其包含 `routerLink`。

   ```js
   <div *ngFor="let product of products; index as productId">
   
     <h3>
       <a [title]="product.name + ' details'" [routerLink]="['/products', productId]">
         {{ product.name }}
       </a>
     </h3>
   <!-- . . . -->
   </div>
   ```

   RouterLink 指令让路由器控制了一个链接元素。在这种情况下，路由（URL）包含一个固定的区段（ `/products` ），但其最后一个区段是变量，要插入当前商品的 id 属性。例如，`id` 为 1 的商品的 URL 类似于 `https://getting-started-myfork.stackblitz.io/products/1`。

   

4. 通过单击商品名称来测试路由器。该应用会显示商品详情组件，该组件目前始终显示 “product-details works！” 

   注意，预览窗口中的 URL 会发生变化。其最后一段是 `products/1`。

![](https://www.angular.cn/generated/images/guide/start/product-details-works.png)

#### 使用路由信息

商品详情组件负责处理每个商品的显示。Angular 的路由器会根据浏览器的 URL 和你定义的这些路由来决定如何显示组件。你可以通过 Angular 的路由器来组合使用 `products` 数据和路由信息，以显示每个商品的详情。

1. 打开 `product-details.component.ts` 文件

2. 改用外部文件中的商品数据。

   1. 从 `@angular/router` 包导入 `ActivatedRoute`，从 `../products` 文件导入 `products` 数组。

      ```js
      import { Component, OnInit } from '@angular/core';
      import { ActivatedRoute } from '@angular/router';
      
      import { products } from '../products';
      ```

      

   2. 定义 `product` 属性，并把 `ActivatedRoute` 注入到构造函数中。

   3. ```js
      export class ProductDetailsComponent implements OnInit {
        product;
      
        constructor(
          private route: ActivatedRoute,
        ) { }
      
      }
      ```

      `			ActivatedRoute` 专门用于由 Angular 路由器加载的每个路由组件。它包含关于该路由，路由参数以及与该路由关联的其它数据的信息。

      

3. 在 `ngOnInit()` 方法中，*订阅（subscribe）*路由参数并根据其 `productId` 获取商品信息。

   ```js
   ngOnInit() {
     this.route.paramMap.subscribe(params => {
       this.product = products[+params.get('productId')];
     });
   }
   ```

   这个路由参数对应于路由中定义的路径变量。`productId` 是从与该路由匹配的 URL 中提供的。你可以通过 `productId` 来显示每个单独商品的详细信息。

   

4. 修改模板，在 `*ngIf` 中显示商品详情。

   ```js
   <h2>Product Details</h2>
   
   <div *ngIf="product">
     <h3>{{ product.name }}</h3>
     <h4>{{ product.price | currency }}</h4>
     <p>{{ product.description }}</p>
   
   </div>
   ```

   





### 指令

`*ngFor` 是一个 "结构型指令"。结构型指令会通过添加、删除和操纵它们的宿主元素等方式塑造或重塑 DOM 的结构。任何带有 * 的指令都是结构型指令。

```js
<div *ngFor="let product of products">

  <h3>
      {{ product.name }}
  </h3>

</div>
```



### 组件

**组件**在 UI 中定义了一些责任区，让你能重用这些 UI 功能集。

组件包含三部分：

- **一个组件类**，它用来处理数据和功能。上一节，我们在组件类中定义了商品数据和 `share()` 方法。
- **一个 HTML 模板**，它决定了用户的呈现方式。在上一节中，你修改了商品列表的 HTML 模板，以显示每个商品的名称、描述和 “Share” 按钮。
- **组件专属的样式**定义了外观和感觉。商品列表中还没有定义任何样式。

Angular 应用程序由一棵组件树组成，每个 Angular 组件都有一个明确的用途和责任。


![Online store with three components](https://www.angular.cn/generated/images/guide/start/app-components.png)

- `app-root`（橙色框）是应用的外壳。这是要加载的第一个组件，也是所有其它组件的父组件。你可以把它想象成一个基础页面。
- `app-top-bar`（蓝色背景）是商店名称和结帐按钮。
- `app-product-list`（紫色框）是你在上一节中修改过的商品列表。



### 输入

目前，商品列表会显示每个商品的名称和描述。商品列表组件还定义了一个 `products` 属性，它包含每个商品的导入数据。



创建一个新的组件

1. 创建一个新商品提醒组件。

   1. 右键单击 `app` 文件夹，使用 `Angular Generator` 生成一个名为 `product-alerts` 的新组件。

   2. 该 generator 为组件的三个部分创建了启动文件：

      - `product-alerts.component.ts`

      - `product-alerts.component.html`

      - `product-alerts.component.css`
      
        

2. 打开 `product-alerts.component.ts`。

   1. 注意 `@Component` 装饰器。这表明它下面的类是一个组件。它提供了有关该组件的元数据，包括它的模板、样式和选择器。
   
      * 该 `selector` 用于标识该组件。该选择器是当 Angular 组件在页面中渲染出 HTML 元素时使用的名字。按照惯例，Angular 组件选择器会以前缀 `app-` 开头，后跟组件名称。
      * 模板和样式文件名。它们是对另外两个生成的文件的引用。
   
    2. 组件定义中还包含一个导出类（ `ProductAlertsComponent` ），用于处理该组件的功能。
   
      
   
3. 组件定义中还包含一个导出类（ `ProductAlertsComponent` ），用于处理该组件的功能。

   1. 从 `@angular/core` 导入 `Input`。

   ```js
   content_copyimport { Component, OnInit } from '@angular/core';
   import { Input } from '@angular/core';
   ```

   2. 在 `ProductAlertsComponent` 类的定义中，定义一个带 `@Input` 装饰器的 `product` 属性。`@Input` 装饰器指出其属性值是从组件的父组件（在本例中就是商品列表组件）中传入的。

   ```ts
   content_copyexport class ProductAlertsComponent implements OnInit {
     @Input() product;
     constructor() { }
   
     ngOnInit() {
     }
   
   }
   ```

   

4. 定义这个新商品提醒组件的视图。

   打开 `product-alerts.component.html` 模板，把作为占位符的 p 替换为如果商品价格超过 700 美元就要显示出来的“通知我”按钮。

   

5. 把这个新商品提醒组件显示为该商品列表的一部分（子组件）。

   1. 打开 `product-list.component.html`。
   2. 要包含这个新组件，只要像使用 HTML 元素一样使用它的选择器（ `app-product-alert` ）就可以了。
   3. 通过属性绑定把当前商品作为输入传递给组件。





### 输出

1. 打开 `product-alerts.component.ts`。

2. 从 `@angular/core` 中导入 `Output` 和 `EventEmitter`：

   ```js
   import { Component } from '@angular/core';
   import { Input } from '@angular/core';
   import { Output, EventEmitter } from '@angular/core';
   ```

3. 在组件类中，用 `@Output` 装饰器和一个事件发射器（EventEmitter）实例定义一个名为 `notify` 的属性。这可以让商品提醒组件在 notify 属性发生变化时发出事件。

   ```js
   export class ProductAlertsComponent {
     @Input() product;
     @Output() notify = new EventEmitter();
   }
   ```

4. 在商品提醒模板（`product-alerts.component.html`）中，用事件绑定更新“Notify Me”按钮，以调用 `notify.emit()` 方法。

   ```
   <p *ngIf="product.price > 700">
     <button (click)="notify.emit()">Notify Me</button>
   </p>
   ```

5. 接下来，定义单击该按钮时应该发生的行为。回想一下，应该由父组件（商品列表组件）采取行动，而不是商品提醒组件。在 `product-list.component.ts` 文件中，定义一个 `onNotify()` 方法，类似于 `share()` 方法：

   ```js
   export class ProductListComponent {
     products = products;
   
     share() {
       window.alert('The product has been shared!');
     }
   
     onNotify() {
       window.alert('You will be notified when the product goes on sale');
     }
   }
   ```

6. 最后，修改商品列表组件以接收商品提醒组件的输出。

   在 `product-list.component.html` 中，把 `app-product-alerts` 组件（就是它显示的“Notify Me”按钮）的 `notify` 事件绑定到商品列表组件的 `onNotify()` 方法。

   ```js
   <button (click)="share()">
     Share
   </button>
   
   <app-product-alerts
     [product]="product" 
     (notify)="onNotify()">
   </app-product-alerts>
   ```

   

7. 试试“Notify Me”按钮：

   ![Product alert notification confirmation dialog](https://www.angular.cn/generated/images/guide/start/product-alert-notification.png)



### 生命周期

 使用构造函数新建一个组件或指令后，就会按下面的顺序在特定时刻调用这些生命周期钩子方法：

| 钩子                      | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| `ngOnChanges()`           | 当 Angular（重新）设置数据绑定输入属性时响应。 该方法接受当前和上一属性值的 `SimpleChanges` 对象在 `ngOnInit()` 之前以及所绑定的一个或多个输入属性的值发生变化时都会调用。 |
| `ngOnInit()`              | 在 Angular 第一次显示数据绑定和设置指令/组件的输入属性之后，初始化指令/组件。在第一轮 `ngOnChanges()` 完成之后调用，只调用**一次**。 |
| `ngDoCheck()`             | 检测，并在发生 Angular 无法或不愿意自己检测的变化时作出反应。在每个变更检测周期中，紧跟在 `ngOnChanges()` 和 `ngOnInit()` 后面调用。 |
| `ngAfterContentInit()`    | 当 Angular 把外部内容投影进组件/指令的视图之后调用。第一次 `ngDoCheck()` 之后调用，只调用一次。 |
| `ngAfterContentChecked()` | 每当 Angular 完成被投影组件内容的变更检测之后调用。`ngAfterContentInit()` 和每次 `ngDoCheck()` 之后调用 |
| `ngAfterViewInit()`       | 当 Angular 初始化完组件视图及其子视图之后调用。第一次 `ngAfterContentChecked()` 之后调用，只调用一次。 |
| `ngAfterViewChecked()`    | 每当 Angular 做完组件视图和子视图的变更检测之后调用。`ngAfterViewInit()` 和每次 `ngAfterContentChecked()` 之后调用。 |
| `ngOnDestroy()`           | 每当 Angular 每次销毁指令/组件之前调用并清扫。 在这儿反订阅可观察对象和分离事件处理器，以防内存泄漏。在 Angular 销毁指令/组件之前调用。 |



### 服务端渲染

**Angular Universal** 

标准的 Angular 应用会运行在*浏览器*中，它会在 DOM 中渲染页面，以响应用户的操作。 而 **Angular Universal** 会在*服务端*运行，生成一些*静态*的应用页面，稍后再通过客户端进行启动。 这意味着该应用的渲染通常会更快，让用户可以在应用变得完全可交互之前，先查看应用的布局。



* **创建服务端应用模块**

创建服务端应用模块 `app.server.module.ts`, 输入

```bash
$ ng add @nguniversal/express-engine --clientProject angular.io-example
```

之后该命令回城成如下结构

```src/
src /
	index.html                 *app web page*
	main.ts                    *bootstrapper for client app*
	main.server.ts             ** bootstrapper for server app*
	style.css                  *styles for the app*
	app/ ...                   *application code*
		app.server.module.ts     ** server-side application module*
server.ts                    ** express web server*
tsconfig.json                *TypeScript client configuration*
tsconfig.app.json            *TypeScript client configuration*
tsconfig.server.json         ** TypeScript server configuration*
tsconfig.spec.json           *TypeScript spec configuration*
package.json                 *npm configuration*
webpack.server.config.js     ** webpack server configuration*
```

注意： **  的文件都是新增的，不是原始的教程中的



**Angular为何需要服务端渲染？**

有三个主要的理由来为你的应用创建一个 Universal 版本。

1. 通过[搜索引擎优化(SEO)](https://static.googleusercontent.com/media/www.google.com/en//webmasters/docs/search-engine-optimization-starter-guide.pdf)来帮助网络爬虫。
2. 提升在手机和低功耗设备上的性能
3. 迅速显示出第一个支持[首次内容绘制(FCP)](https://developers.google.com/web/tools/lighthouse/audits/first-contentful-paint)的页面





### 原理图 Scheematic

**概念**：原理图是一个基于模板的支持复杂逻辑的代码生成器。它是一组通过生成代码或修改代码来转换软件项目的指令。



原理图的集合可以作为一个强大的工具，以创建、修改和维护任何软件项目，特别是当要自定义 Angular 项目以满足你自己组织的特定需求时，

比如：借助原理图来用预定义的模板或布局生成常用的 UI 模式或特定的组件。



#### Angular CLI 中的原理图

[Angular CLI](https://www.angular.cn/guide/glossary#cli) 使用原理图对 Web 应用项目进行转换。 你可以修改这些原理图，并定义新的原理图，比如更新代码以修复依赖中的重大变更，或者把新的配置项或框架添加到现有的项目中。



`@schematics/angular` 集合中的原理图是 `ng generate` 和 `ng add` 命令的默认原理图。此包里包含一些有名字的原理图，可用于配置 `ng generate` 子命令的选项，比如 `ng generate component` 和 `ng generate service` 。`ng generate` 的子命令是相应原理图的简写。你可以用长格式来指定要生成的原理图（或原理图集合）



```bash
$ ng generate my-schematic-collection:my-schematic-name ng generate my-schematic-collection:my-schematic-name
```

or

```bash
$ ng generate my-schematic-name --collection collection-name
```

#### 配置 CLI 的原理图

与原理图相关联的 JSON 模式会告诉 Angular CLI 命令和子命令都有哪些选项以及默认值。这些默认值可以通过在命令行中为该选项提供不同的值来进行覆盖。要了解如何更改代码生成选项的默认值，请参见“ [工作区配置](https://www.angular.cn/guide/workspace-config) ”。



CLI 中那些用来生成项目及其部件的默认原理图，其 JSON 模式收集在 [`@schematics/angular`](https://raw.githubusercontent.com/angular/angular-cli/v7.0.0/packages/schematics/angular/application/schema.json) 包中。该模式描述了 CLI 中每个可用的 `ng generate` 子命令选项，如 `--help` 输出中所示。



#### 编写库的原理图

作为一名库开发人员，你可以创建自己的自定义原理图集合，以便把你的库与 Angular CLI 集成在一起。

- *添加（Add）原理图*允许开发人员使用 `ng add` 在 Angular工作空间中安装你的库。

- *生成（Generation）原理图*可以告诉 `ng generate` 子命令如何修改项目、添加配置和脚本，以及为库中定义的工件提供脚手架。

- *更新（Update）原理图*可以告诉 `ng update` 命令，如何更新库的依赖，并在发布新版本时调整其中的破坏性变更。



要了解它们的更多细节以及如何创建它们，请参阅：

- [创作原理图](https://www.angular.cn/guide/schematics-authoring)
- [库的原理图](https://www.angular.cn/guide/schematics-for-libraries)



#### 添加（Add）原理图

库中通常都会提供一个添加原理图，以便通过 `ng add` 把这个库添加到现有项目中。`add` 命令会运行包管理器来下载新的依赖，并调用一个原理图形式的安装脚本。



例如，[`@angular/material`](https://material.angular.io/guide/schematics) 原理图会要求 `add` 命令安装并设置 Angular Material 及其主题，并注册可通过 `ng generate` 创建的新启动器组件。你可以把它作为自己的 "添加原理图" 的范例。



合作伙伴和第三方库也可以通过添加原理图来支持 Angular CLI。例如，`@ng-bootstrap/schematics` 会把 [ng-bootstrap](https://ng-bootstrap.github.io/) 添加到应用中，`@clr/angular`会安装并设置 [VMWare 的 Clarity](https://vmware.github.io/clarity/documentation/v1.0/get-started) 。



"添加原理图" 还可以通过更改配置、添加额外依赖（比如腻子脚本），或者添加程序包特有的初始化代码来修改项目。例如，`@angular/pwa` 原理图会通过添加一个应用清单（manifest）和 Service Worker，来把你的应用变成一个 PWA，`@angular/elements` 原理图添加了 `document-register-element.js` 腻子脚本和 Angular Elelments 的依赖项。



#### 生成（Generation）原理图

生成器原理图是 `ng generate` 的操作指令。 那些已经有文档的子命令会使用默认的 Angular 生成器原理图，但你可以在子命令中指定另一个原理图来生成你的库中定义的那些工件。



例如，Angular Material 为它定义的一些 UI 组件提供了生成器原理图。下面的命令会使用其中一个原理图来渲染一个 Angular Material 的 `<mat-table>` 组件，它预先配置了一个用于排序和分页的数据源。

```bash
$ ng generate @angular/material:table 
```



#### 更新原理图

`ng update` 命令可以用来更新工作空间的库依赖。



更新 Angular Material 库。

```bash
$ ng update @angular/material
```















