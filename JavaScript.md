

## 原生JavaScript

### JS概念

Javascript是一门**面向对象的、跨平台的脚本语言**；

**对象**：

```html
	属性和方法的结合；

​	类是对象的抽象，对象是类的实例； ( 你做事，我放心 ) ；
```

**跨平台**：JS代码；（浏览器windows 、linux、unix、Android、IOS）；
**脚本语言**：即依赖外部环境才能运行的语言。

脚本语言特点：

```html
	HTML文件必须在浏览器里执行；
​	JS文件嵌入到HTML文件里才能执行；
​	凡是不能独立执行需要依赖其他程序的，通常都叫做脚本，也叫动态语言。（宿主语言）；

（浏览器>HTML文件>JS文件）
    真+假=假
    学习逻辑方法：类比、归类；
```



### 学习内容

```html
	完全掌握各版本的-JS-ES3，5，6；（ECMAscript）
​	利用JS完成复杂编程  -页面交互效果；
​	面向游戏对象编程思想  -游戏的制作；
​	后端交互方式  -AJAX；
​	交互化构建工程化前段  -gulp。
```



### JS历史

```html
1995年，网景公司Netscape由brendan eich设计，
	IE 的脚本语言：Jscript；
Nombas:cenvi中的scriptEase。

1997年，ECMA发布262号标准文件（ECMA-262）的第一版；
1999年，ECMAScript 3.0发布；
2015年6月，ECMAScript 6 正式通过（ES6）；
```



### JS标准

​	ECMAScript 可以为不同种类的宿主环境提供核心的脚本编程能力，因此核心的脚本语言是与任何特定的宿主环境分开进行规定的

```html
	标准化：
		W3C；
		ECMAscript
​	组成:
		ECMAScript；
		BOM;
		DOM；
​	用途：
		视觉交互、数据交互、node.js
		​​嵌入动态文本于HTML页面;
		​​对浏览器事件做出响应;
		​​读写HTML元素;
		​​在数据被提交到服务器之前验证数据;
		​​检测访客的浏览器信息（可以使用js代码判断浏览器类型）;
		​​控制cookies，包括创建和修改等;
		​​基于Node.js技术进行服务器端编程;
```



### JS和H5的关系

```html
页面三要素
​	结构：HTML
​	表现：CSS
​	行为：JS

 	H5是一种新的技术，就目前而言，我们所知的H5都是一些标签，但是有了JS之后，这些标签深层的扩展功能才得以实现。 比如video标签；我们对其理解为一个简单的标签；但是实际上，video标签还有更深层次的扩展功能；
```



### JS基础

##### 书写

* 内部JS

```js
<script>
		document.write("hello world"); // 文本显示

		console.log("hello world"); // 控制台显示

		alert("hello world");  // 弹窗显示

		document.write("<h1>hello world</h1>");

		/* 多行注释 */
</script>
```



* 外部JS

```js
index.js文件   document.write("hello world");

内部引入：<script src="path:to/index.js"></script>；

<script src="01.js"><！--这里不能写js代码，因为这个script是用来引入外部js文件的--></script>
```



##### 页面输出内容

```js
document.write(""); // 文本显示

console.log(""); // 控制台显示

alert("");  // 弹窗显示
```



##### 转义字符

```js
&lt； || &gt；
document.write("&lt;strong&gt;我很man&lt;/strong&gt;");
```



##### 声明变量

​	我们通常使用**`关键字var `**声明一个变量的时候，这时计算机会从内存中留出一定储存空间，为我们存放不同类型的内容。

```js
// 左值：在等号左侧，是声明一个变量并且起名；
// 右值 ：在等号右侧，是存放进变量中的东西（给变量赋值）；

var a = "hello world"；  // 把"hello world'赋值给右边的 a 
```



### 变量类型

##### 变量

```html
变量：存储数据的容器（可变的量）

​	注意：再次修改变量的值的不是不需要再写 var
```



##### 变量类型

```html
	数字类型(number)：1234567890   int：整型  float：浮点型（小数）
​	字符类型(string)：'123456',"字符串类型",.....（有单引号或者双引号）
​	未定义类型(undefined)：这是一种特殊类型，当变量被声明但是没有被赋值的时候，那么该变量的类型为undefined；
​	布尔值类型（boolean）：true，false；(boolean会隐式转换，true会转换成1、false会转换成0；)
​	对象类型：object；
​	函数类型：Function；
​	引用类型：Function：object
```



#####  判断类型

关键字：**`typeof`**；用typeof后得到的是字符串；  

```html
 typeof返回有六种值： number、string、boolean、undefined、object（数组也是对象）、function；
​ js有五种基本数据类型：number、string、boolean、undefined、null、symbol；
​ 两种引用类型：object、function；
​ 两种特殊数据类型：null、undefined；
```



##### 弱类型

```html
	声明变量的时候无需声明类型, 同一个变量可以修改存储不同类型的数据
```

```js
 var a = "hello world";
 a = 123;
类比强类型语言，
如：Java
       String a = "Hello world";
       a = 123; // 报错！！！
```



##### 变量类型转换

分为**`隐式转换`**、**`显式转换`**;

```html
 parseInt(    ) 
	方法首先查看位置 0 处的字符，判断它是否是个有效数字；如果不是，该方法将返回 NaN，不再继续执行其他操作。 但如果该字符是有效数字，该方法将查看位置 1 处的字符，进行同样的测试。这一过程将持续到发现非有效数字的字符为止，此时 parseInt() 将把该字符之前的字符串转换成数字。
	(从左往右看，直到特殊符号和字母结束，保留前面的整数，若是前面第一位出现字母或字符这回不出现NaN,)

​ parseFloat(    )
	跟parseInt()极其相似，不过第一个出现的小数点是有效字符。如果有两个小数点，第二个小数点将被看作无效的。parseFloat (    ) 会把这个小数点之前的字符转换成数字。
	（与parseint一样，但会保留一个小数）

NaN：Not a Number：
​	是一个特殊值，说明某些算术运算（如求负数的平方根）的结果不是数字（本来期望得到一个数字，但是结果没有计算成功）。方法 parseInt() 和 parseFloat() 在不能解析指定的字符串时就返回这个值。
	判断是否是NAN时必须要用 isnan 来判断；
number:（整数小数可以转换，但有字符就会出现NAN）
```



#####  强制类型转换

```html
 Boolean(value) - 把给定的值转换成 Boolean 型；
​ Number(value) - 把给定的值转换成数字（可以是整数或浮点数）；
​ String(value) - 把给定的值转换成字符串；
```



#####  变量命名规范

匈牙利命名法：**`驼峰命名法`**；

​	或者

```html
 变量名首字符必须为字母(a-z A-Z)，下划线( _ )，或者美元符号( $ )开始  
     
​ 余下的字符可以是下划线、美元符号或任何字母或数字字符

​ 变量名大小写敏感（var a 和  var A 是不一样的两个变量）
```



### 关键字

关键字用于**`执行特定操作`**等。按照规则，关键字也是`语言保留`的，不能用作`标识符`。

| break     | do       | instanceof | typeof |
| --------- | -------- | ---------- | ------ |
| case      | else     | new        | var    |
| catch     | finally  | return     | void   |
| continue  | for      | switch     | while  |
| debugger* | function | this       | with   |
| default   | if       | throw      | delete |
| in        | try      |            |        |



### new 操作符

new操作符具体操作了什么？

​	1、创建了一个空对象，并且this变量引用该对象，同事还继承了该函数的原型；

​	2、属性和方法被加入到this引用的对象中；

​	3、新创建的对象由this所引用； 并且隐式返回this



### 保留字

未来可能作为`标识符`存在

| abstract | enum       | int       | short        |
| -------- | ---------- | --------- | ------------ |
| boolean  | export     | interface | static       |
| byte     | extends    | long      | super        |
| char     | final      | native    | synchronized |
| class    | float      | package   | throws       |
| const    | goto       | private   | transient    |
| debugger | implements | protected | volatile     |
| double   | import     | public    | name         |

### 运算符

```js
	算数运算符
	加、减、乘、除、求余/取模（+ 、- 、* 、/ 、%）；
	"+"：加好除了做数字运算还能字符串连接，数组跟字符相加，会把数字转换为字符串并且连接到一起；
	取余：大数对小的那个数取余结果为整除之后的余数；小的那个数对大数求余的结果就是小的那个数本身；

​ 	关系运算符
	= =（相等） 、! =（不等于）、<（小于） 、>（大于） 、< =（小于或者等于） 、> =（大于或者等于）
	**判断运算符两侧的结果是否满足规则，满足结果即为true，否则false；

​ 	逻辑运算符
	逻辑与：&&, “和”的意思；必须两个条件均为true结果才为true；
	逻辑或：||, “或”的意思 ；只要有一个条件为true结果就为true，必须两个条件均为false结果才为false；
	逻辑非：! , “不”的意思， 对本身的结果取反。
与逻辑在两个条件均为true时结果才为true，其余情况均为false；
或逻辑在两个条件均为false时结果才为false，其余情况均为true；
补充：
	异或：两个条件结果不同时（一个true，一个false），结果才为true。
    
​ 	三目运算符 
	？
写法：条件？ 条件成立时：条件不成立时	；
```



###  自增

```js
++a     a++    --a    a- 
```

自增自减前置后置是不一样的，**`前置是先加后用`**，**`后置的先用后加`**。

 

### = 和 == 以及 ===

```html
= 赋值 、== 相等 、=== 全等、！== 不全等 ；

   （1）一个等号是赋值，将等号右边的值赋给左边；
   （2）两个等号是判断相等，相等结果为true，不等为false，不考虑数据类型，只判断值；
   （3）三个等号要求全等，不仅值要相等，类型也必须相等；
```



### JS程序执行结构 

```html
	分支结构：根据不同的条件判断来决定程序执行走向的结构（也叫选择结构）
​	循环结构：需要重复执行同一操作的程序结构称为循环结构。
​	顺序结构：按照由上到下的顺序一行一行地执行的程序结构。

​​​ 注意：0、-0、null、""、false、undefined 或者 NaN在if条件里结果为false；
```



##### if

```js
// 单分支

if(true){
    //会执行的语句
}

if(false){
    //会跳过不执行的语句
}



if(判断条件){ //当if括号中结果为true时执行语句1，否则执行语句2
    //语句1
}else{
    //语句2
}


// 多分支

if(判断条件1){ //当条件1结果为true时执行语句1
    //语句1
}else if(判断条件2){ //当条件1结果为false而且条件2结果为true时执行语句2
    //语句2
}else{ //当条件1条件2结果都为false时执行语句3
    //语句3
}
```

if 括号中只需要布尔类型值。那么在if判断中，所有的数据类型都会被`隐式转换`为`布尔类型`。



##### switch  case 

```js
switch(语句){  //语句的结果与每一条case内容进行匹配
    case 1:
       alert(1);
           break;
    case 2:
        alert(2);
           break;
    case 3:
        alert(3);
           break;
    default:
        alert(0);
}
```

```html
 注意switch的应用场景（有多个确定值需要判断的时候）；
​ 注意case穿透，要加break语句（如果程序没有发现break语句，那么解析器会继续向下解析）;
```

```html
 break：跳出循环体，整个循环结束；
​ continue：结束本次循环，但继续下次循环；
```



##### while

```js
while(条件){
    //条件成立就会反复执行这里的代码
}
```

`死循环`： 没有终止条件的循环即为死循环，在代码中应尽量避免死循环



##### do while

```js
do{
    //先执行一遍代码
    //while条件成立再继续反复执行
}while(条件)
```



##### for

```js
// 执行步骤：var i= 0;    i< 10;    console;   i++；
//    		i< 10;    console;   i++。。。。。。
//    		i< 10;    console;   i++。。。。。。
for (var i = 0; i < 10; i++) {
    console.log(i);
}
```



##### **三种循环的联系和区别**

```html
1、都是会反复执行的代码块；
2、大部分情况下可以互相替换；
3、do...while至少执行一次，while和for有可能0次，while不太能确定执行次数，for可以。
```



### 函数

函数在创建的时候会创建两个对象，一个是函数**`对象本身`**，另一个是**`作用域链对象`**

函数在调用的时候会创建**`一个执行环境对象`**（活动对象）



**`系统函数`**（封装、调用）、**`自定义函数`**:

```html
系统函数：
parseInt()   alert()  prompt()  eval()  //Eval：把字符串当作js代码去执行

var str = "1+1";
var res = eval(str);
console.log(res);
```

**封装**：一个工具，被封装好可重复执行的一段代码块，函数的功能相对单一；

**调用**: 计算机编译或运行时，使用某个函数来完成相关命令。对无参函数调用时则无实际参数表。实际参数表中的参数可以是常数、变量或其它构造类型数据及表达式。各实参之间用逗号分隔。

```js
function   fn （    传递参数  形参    ）{  
    函数体（可重复执行）  
  }；
如何调用函数：fn (    实参    )；

// 回调函数：把函数作为参数
```

```js
立即函数表达式(自调用函数)：

（function（）{    }）（）；只能调用一次
```



**函数参数**

```html
形参、实参；
​ 形参：形式参数，声明函数的时候写在小括号里面的参数，无需var;
​ 实参：实际参数，在函数调用的时候需要传递实际有值得参数;
​ 实参个数大于形参，多余实参自动舍弃;
​ 形参个数大于形参，多余形参默认为undefined;
​ 调用的时候讲实参传递形参，形参的值就是实参的值。
```



**函数的声明和使用**

```js
//通过function关键字声明一个函数，跟上函数名，一堆小括号，一堆花括号，花括号里面放代码块
//提升到顶部
function test(){
    //可重复执行的代码块
}  
test();
test();
test();


//表达式定义法
//不会提升
var test1 = function(){
    //可重复执行的代码块

}
for (var i = 0; i < 10; i++) {
    test1();
}
```



#####  作用域

`作用域`：变量的作用范围.

```txt
全局变量

​    作用范围为整个程序的执行范围

​    在函数体外部定义的变量就是全局变量

​    在函数体内部不使用var定义的也是全局变量



局部变量

​    作用范围是某个函数体内部

​    在函数体内部通过var关键字定义的变量或者形参，都是局部变量

​    当局部变量与全局变量重名时，在函数体内部局部变量优先于全局变量



变量提升

​    变量的声明会提升至当前作用域的最顶端，但不会提升赋值

	解释器会扫描代码进行预编译查看是否有语法错误。
	变量和函数提升当前作用域的顶部，但是变量的赋值不会提升。
（函数与变量冲突时会保留函数，两个函数冲突时会按照书写顺序，顺序靠后的会覆盖前面的。）
```



##### return关键字

```html
 1.结束函数的执行
 2.交回函数执行权
 3.返回一个结果函数调用位置
```



##### JSON

JSON是一种数据格式（对象和数组互相嵌套）



##### 堆栈

**`堆栈`**： 是一种数据结构，指的是数据存取的方式，当定义一个变量时，内存会开辟一段空间。

```html
   栈（ Stack）：先进后出（FILO），在栈顶做插入（压栈）和删除操作（出栈）。

​   队列：先进先出（FIFO），在队头做删除操作,在队尾做插入操作。
```

**` 堆`**和它们不同，代码执行时系统动态分配，不存在是先进后出还是先进先出。

即

```html
栈：先进后出              栈底删除，插入
队列：先进先出            对头删除，对位插入
```



##### 执行环境执行栈

**`执行环境执行栈 `**也称 **`执行上下文 `** – execution context

​	当JavaScript解释器初始化执行代码时，它首先默认进入全局执行环境，从此刻开始，**函数的每次调用都会创建一个新的执行环境，**每一个执行环境都会创建一个新的环境对象压入栈中*。 

​        当执行流进入一个函数时，函数的环境对象就会被压入一个`环境栈`中（execution stack）。在函数执行完后，`栈`将其环境弹出，把控制权返回给之前的执行环境。



##### 作用域链

​	  **`内层环境`**可以访问`外层`中的`变量`和`函数`，而**`外层环境`**不能访问`内层的变量和函数`。



#####  递归

​	**`程序调用自身的编程技巧`**称为递归（recursion）。

​	递归，就是在运行的过程中**`调用自己`**，本质就是循环。

递归具备的条件:

```html
	子问题须与原始问题为同样的事，且更为简单；
​	不能无限制地调用本身，须有个出口，化简为非递归状况处理。

由于递归是函数本身一层一层压栈，导致先入栈的不能出栈，空间占满以后就会造成堆栈溢出。
```



#####  变量提升

```html
 解释器会扫描代码进行预编译查看是否有语法错误。
​ 变量和函数提升当前作用域的顶部，但是变量的赋值不会提升。
（函数与变量冲突时会保留函数，两个函数冲突时会按照书写顺序，顺序靠后的会覆盖前面的。）
```



##### 逻辑短路

```html
如果第一部分已经能够决定真个表达式的结果，那第二部分就不会执行
与逻辑：  一部分false下一步就不会执行；
或逻辑：  一部分false下一步会继续执行；
```



##### JS运行和编译

```html
 语法分析：
查找基本语法有没有错误。

​ 预解析：
执行之前进行预解析。
var、function关键字提前到当前作用域的顶部，变量默认值为undefined，函数默认值为函数体代码块，当函数与变量重名时，保留函数。

​ 解释执行
```



##### 变量的生命周期

```txt
 全局变量的生命周期直至浏览器卸载页面才会结束。
​ 局部变量只在函数的执行过程中存在，而在这个过程中会为局部变量在栈或堆上分配相应的空间，以存储它们的值，然后再函数中使用这些变量，直至函数结束.
```



##### 事件

```html
用户的行为：onclick、ondblclick、onfocus、onblur、window.onload
    是用户跟页面的交互，当用户跟页面进行一些“交流”的时候，页面通过js就会触发一些事件，比如鼠标点击的时候就会触发onclick事件，给这个事件绑定一个函数，那么这个时候函数就会被调用，代码就会被执行

​ 文本框事件：onchange
​ 元素失去焦点：onblur
​ 元素获得焦点：onfocus

​ 鼠标事件
    click，dbclick，mousedown，mouseup，mouseover，mouseout，mouseenter、mouseleave、mousemove   
    scroll    mousewheel    鼠标滚轮
    contextmenu  鼠标右键（上下文菜单：在不同环境下右键菜单不一样）
    mouseover：鼠标在元素身上移动穿过子元素的时候会被反复触发
    mouseenter：只是在进入元素的时候触发

​ 键盘事件
    keydown，keyup，keypress

​ 表单
	表单事件：对表单元素操作之后会触发的事件
    单选框、多选框、下拉菜单   状态改变的时候会触发onchange 事件
 	表单提交的时候会触发 onsubmit    触发在<form>元素身上
```



##### this关键字

this关键字:事件函数里面的this指的是**`事件触发对象`**;

**`this指向`**

```html
 全局this指向window；
​ 对象方法的this指向对象的本身；（谁调用就指谁）
​ 构造函数的this指即将new的对象本身；
​ 自调用函数指向window；  	“IIFE，立即执行函数(function( ){})( )”
​ 事件里的this指向事件触发事件；
​ 箭头函数没有自己的this；
​ 定时器的this指向window；
```

```HTML
call()、apply()、bind()  可以改变this的指向。

​ call传参依次传参，第一个参数数对应第二个数的下标；
	obj1.say.call(obj2, 1, 2);
​ apply传参是一个数组，第一个参数对应数组的下标；
	obj1.say.apply(obj2, [2,2]);
​ bind在函数封装绑定bind；bind绑定谁就是谁;
```





### Math内置对象

##### **Math 对象属性**

| 属性          | 描述                                              |
| ------------- | ------------------------------------------------- |
| Math.E        | 返回算术常量 e，即自然对数的底数（约等于2.718）。 |
| Math.LN2      | 返回 2 的自然对数（约等于0.693）。                |
| Math.LN10     | 返回 10 的自然对数（约等于2.302）。               |
| Math.LOG2E    | 返回以 2 为底的 e 的对数（约等于 1.414）。        |
| Math.LOG10E   | 返回以 10 为底的 e 的对数（约等于0.434）。        |
| Math.PI       | 返回圆周率（约等于3.14159）。                     |
| Math.SQRT1_2  | 返回返回 2 的平方根的倒数（约等于 0.707）。       |
| SQRT1_2.SQRT2 | 返回 2 的平方根（约等于 1.414）。                 |



#####  Math对象方法

| 方法     | 描述                                    |
| -------- | --------------------------------------- |
| abs(x)   | 返回数的绝对值。                        |
| sin(x)   | 返回数的正弦。                          |
| cos(x)   | 返回数的余弦。                          |
| tan(x)   | 返回角的正切。                          |
| ceil(x)  | 对数进行上舍入。                        |
| floor(x) | 对数进行下舍入。                        |
| round(x) | 把数四舍五入为最接近的整数。            |
| max(x,y) | 返回 x 和 y 中的最高值。                |
| min(x,y) | 返回 x 和 y 中的最低值。                |
| pow(x,y) | 返回 x 的 y 次幂。                      |
| sqrt(x)  | 返回数的算术平方根。                    |
| random() | 返回 0 ~ 1 之间的随机小数，包含0不包含1 |



##### 随机数

Math.random()生成一个从0-1（包含0不包含1）的随机小数

生成 min ~ max （min < max）的随机数公式：


```html
Math.random()*(max - min) + min
```

```html
参数对应的是弧度：Math.PI / 180;

Eg：Math.sin(30 *Math.PI / 180 )就等于sin30的值。
```



### Date内置对象

**`时间戳`**：是指`格林威治时间`1970年01月01日00时00分00秒`(北京时间1970年01月01日08时00分00秒)`起至现在的总毫秒数.



##### 日期对象创建

```js
//当前时间的日期对象
var date = new Date();
```



##### get系列API

| getFullYear() | 返回年                                           |
| ------------- | ------------------------------------------------ |
| getMonth()    | 返回月份0--11                                    |
| getDate()     | 返回某一天                                       |
| getDay()      | 返回星期0-6                                      |
| getHours()    | 返回小时                                         |
| getMinutes()  | 返回分钟                                         |
| getSeconds()  | 返回秒                                           |
| getTime()     | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数 |



##### set系列API

| setFullYear() | 设置年份                   |
| ------------- | -------------------------- |
| setMonth()    | 设置月                     |
| setDate()     | 设置天                     |
| setHours()    | 设置小时                   |
| setMinutes()  | 设置分钟                   |
| setSeconds()  | 设置秒                     |
| setTime()     | 使用毫秒的形式设置时间对象 |

```html
 setDay( 这个真没有!!!!,星期是通过设定日期自动计算的 )
​ set系列API可以设置比当前范围更精细的时间
    比如：setFullYear（2012，3，5）  设置日期为2018年4月5号
         setHours（13，30，0）  设置时间为13:30:00
```

```html
1秒=1000毫秒

1分钟=60秒

1小时=60分=3600秒

1天=24小时=1440分=86400秒
```

```js
 year：必需，表示年份的四位整数

​ month：可选,介于 0 ~ 11 之间：如果不填，取系统当月
-1 为去年的最后一个月
12 为明年的第一个月
13 为明年的第二个月

​ date：可选,表示月中某一天的数值。如果不填，取系统当日
	用本地时间表示。介于 1 ~ 31 之间：
	0 为上个月最后一天
	-1 为上个月最后一天之前的天数
如果当月有31天： 32 为下个月的第一天
如果当月有30天： 32 为下一个月的第二天
```

```js
例：现在时间：13:11:43

var date = new Date(2012, 2, 15, 13, 11, 43);
2012年3月15日 13:11:43


date.setFullYear(2013, 5);
2013年6月15日 13:11:43


date.setFullYear(2012, 20, 5);
2013年9月5日 13:11:43
```



### **对象**

对象的`类型`是Object。


JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...


javaScript中万事万物皆对象;



##### 创建对象

创建方法：**`字面量`** 和 **` new 运算符`**；

```js
// new
var obj = new Object();

//找到对象了  >>>  第一个想到的就是属性；
//给对象添加一个属性；

obj.bianmei='哇真的变漂亮了' ;
obj.say=function(){
    alert(this.bianmei);
}

obj.say();
```

obj的属性可以是一个函数，这个时候也叫方法；obj函数内的指针this，指向obj对象本身；



##### 删除对象的属性

​	delete obj.jian；



##### JS内置对象

```html
1.Object对象          是所有JavaScript对象的超类(基类)

2. Array对象          数组对象--定义数组属性和方法

3. Boolean对象        布尔对象--布尔值相关

4. Date对象           日期对象--日期时间相关

5. Error对象          错误对象--处理程序错误

6. Function对象     	函数对象--定义函数属性和方法

7.Math对象            数学对象--各种数学运算工具(不是构造函数)

8.Number对象          数字对象--定义数字属性和方法

9.RegExp对象          正则表达式对象--定义文本匹配与筛选规则

10.String对象         字符串对象--定义字符串属性和方法
```



### 数组

​	一列就是一个数组，一个数组里面有很多个元素（一个变量来承载）；

​	数组是**`引用类型`**;



分类：稀疏数组、二维数组；

```js
// 稀疏数组
var arr1= new A rray（n）；                 // “此时两位数组长度”
arr1[3] = 10；                             //  “给第四个赋值”
```

```js
// 二维数组
<script>
			var arr = [
				[1,2,3],
				[4,5,6],
				[7,8,9]
			];
			console.log(arr[1][1]);
			
			for(var i = 0; i < arr.length; i++){
				for(var j = 0 ; j < arr[i].length; j++){
					console.log(arr[i][j]);
				}
			}
</script>
```



##### 创建数组

创建方法：**`字面量`** 和 **` 构造函数方式`**；

```js
var arr = [];
//字面量的方式

var arr = new Array();
//构造函数的方式
var arr = new Array(10);//一个参数指数组长度为10
var arr = new Array(10，20，30);//多个参数指定义数组元素
```

```js
 数组的长度    			 arr.length
​ 数组的索引（下标）   	  arr[0]  - arr[arr.length-1]
```



##### 数组遍历

```js
// for循环
var arr = [9,2,35,5,74,12,43,4];
for(var i = 0; i < arr.length; i++){
    console.log(arr[i]);
}

// for...in (ES5)    遍历稀疏数组的时候不会遍历到undefined
var arr = [9,2,35,5,74,12,43,4];
for(var key in arr){

    console.log(typeof key); //string
    console.log(arr[key]);
}

// for...of（ES6）
var arr = [9,2,35,5,74,12,43,4];
for(var value of arr){
    console.log(value);
}
```



##### for..in/for..of

```html
	For in可以遍历对象，for of不能变量对象
​	For of可以遍历map集合，for-in不能遍历map集合
​	For-in遍历数组得到的是数组的下标，for of遍历数组得到是数组的元素
​	For in遍历键，for of遍历值；
```



##### **函数的值传递和引用传递**数组API

| **方法**   | **描述**                                                     |
| ---------- | :----------------------------------------------------------- |
| concat()   | 连接两个或更多的数组，并返回结果。                           |
| join()     | 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。 |
| pop()      | 删除并返回数组的最后一个元素                                 |
| push()     | 向数组的末尾添加一个或更多元素，并返回新的长度。             |
| shift()    | 删除并返回数组的第一个元素                                   |
| unshift()  | 向数组的开头添加一个或更多元素，并返回新的长度。             |
| reverse()  | 颠倒数组中元素的顺序。                                       |
| slice()    | 从某个已有的数组返回选定的元素                               |
| sort()     | 对数组的元素进行排序                                         |
| splice()   | 删除元素，并向数组添加新元素。                               |
| toString() | 把数组转换为字符串，并返回结果。                             |



##### **排序**

**`冒泡排序`**：“相邻两个元素进行比较，若是小于当前比较数值则向左换序，直至最后一个”

```js
<script>
function bubble(arr){
			for(var i=0; i<arr.length-1; i++){
				for(j=0; j<arr.length-1-i; j++){
					if(arr[j]>arr[j+1]){
						var temp=arr[j];
						arr[j]=arr[j+1];
						arr[j+1]=temp;
						}
					}
				}
				return arr;
			}	
			console.log(bubble([12,12,32,54,02,78,54,41]));
</script>
```

**`选择排序`**：“左边数值为单位向右查找小于的数，第一个值先记录直至搜索完毕找到最小的值，然后排序”。

```js
<script>
			function choose(arr){
				for(var i=0; i<arr.length-1; i++){
					var minIndex=i;
					for(var j=i+1; j<arr.length; j++){
						if(arr[minIndex]>arr[j]){
							minIndex=j;
						}
					}
					var temp=arr[i];
					arr[i]=arr[minIndex];
					arr[minIndex]=temp;
				}
				return arr;
			}
			console.log(choose([12,20,15,56,24,34]));
</script>
```

**`快速排序`**：

**`插入排序`**：





##### **去重**

**`查找数组中是否有两个数有则删除`**:

```js
<script>
			function distinct (arr){
				for(var i=0; i<arr.length-1; i++){
					for(var j=i+1;j<arr.length;j++){
						if(arr[i] === arr[j]){
							arr.splice(j--,1);
						}
					}
				}
				return arr ;
			}
			console.log(distinct([1,2,3,4,2,1,2,1]));
</script>
```

**`通过对象的属性值不能重复的特点去重：`**

```js
<script>
			function distinct(arr){
				var obj={};
				obj.name;
				obj["name"];
				for(var i=0; i<arr.length; i++){
					if(obj[arr[i]] === undefined){
						obj[arr[i]]=1;
					}else{
						arr.splice(i--,1);
					}
				}
				return arr;
			}
			console.log(distinct([1,2,3,4,2,1,2,1]));
</script>
```

**`直接去重`**:

```js
<script>
			function distinct(arr){
				return Array.from(new Set(arr));
			}
			console.log(distinct([           ]));
</script>
```

**`reduce去重`**:

```js
var arr=[      ];
var arr1= arr.reduce(function(perv,next){
if(!perv.includes(next) perv.push(next);
	return perv; 
},[])
console.log(arr);
```

**`set结构去重：`**

```js
var newarr = [...new Set(array)];
```



##### **ES5新增数组常见方法**

```js
 2个索引方法：indexOf() 和 lastIndexOf()；
​ 5个迭代方法：forEach()、map()、filter()、some()、every()；
​ 2个归并方法：reduce()、reduceRight()；
```





### string

字符串的两种创建方式: **`常量`** 和 **`构造函数`**;

字符串常见API(charAt\ indexOf\substring\slice\split\replace);



API

| 方法           | 描述                                                 |
| -------------- | ---------------------------------------------------- |
| charAt()       | 返回在指定位置的字符。                               |
| indexOf()      | 检索字符串，返回下标                                 |
| lastIndexOf()  | 从后向前搜索字符串。                                 |
| charCodeAt()   | 返回在指定的位置的字符的 Unicode 编码。              |
| fromCharCode() | 从字符编码创建一个字符串。                           |
| concat()       | 连接字符串。                                         |
| *match*()      | 找到一个或多个（正则表达式的）匹配。                 |
| replace()      | 替换与正则表达式匹配的子串。                         |
| *search*()     | 检索与正则表达式相匹配的值。                         |
| slice()        | 提取字符串的片断，并在新的字符串中返回被提取的部分。 |
| split()        | 把字符串分割为字符串数组。                           |
| substr()       | 从起始索引号提取字符串中指定数目的字符。             |
| substring()    | 提取字符串中两个指定的索引号之间的字符。             |
| toLowerCase()  | 把字符串转换为小写。                                 |
| toUpperCase()  | 把字符串转换为大写。                                 |
| trim()         | 去掉字符串前后空格（ES5）                            |
| startsWith()   | 字符串是否以某个字符开头（ES6）                      |
| endsWith()     | 字符串是否以某个字符结尾（ES6）                      |
| includes()     | 字符串是否包含某个字符（ES6）                        |
| repeat()       | 重复某个字符串几次（ES6）                            |



##### ASCII码和字符集

字符串常见API :   统计字符串字数

charCodeAt   \   fromCharCode

敏感词过滤 :   replace（  ， ）

铭感词过滤主要适用于注册登录验证，QQ号验证；



##### 遍历字符串

For-in语句

For-of语句

For循环       



### BOM / DOM

##### BOM

BOM ： **`Browser Object Model 浏览器对象模型`**

window是**`全局浏览器内置顶级对象`**

 	   表示浏览器中打开的窗口（没有应用于window对象的公开标准，不过所有浏览器都支持该对象）

Window 对象表示一个**`浏览器窗口` **或  **`一个框架`**。

   	 在客户端 JavaScript 中，Window 对象是**`全局对象`**，所有的表达式都在当前的环境中计算。也就是说，要引用当前窗口根本不需要特殊的语法，可以把那个窗口的属性作为全局变量来使用。

(例如，可以只写 document，而不必写 window.document。)

* 全局默认对象是挂在windows上面的

  ```html
  window -> document  -->  anchors/ forms/ images/ limks/ location
  		 frames
  		 history
  		 lacation
  		 navigator
  		 screen
  ```

  ```js
  var  a = 123;
  
  alert(window.a)//123
  ```

* windows下的子对象

  * location

    ```js
     window.location.href                 当前页面的 URL，可以获取，可以修改（页面跳转）。
    ​ window.location.hostname     		   web 主机的域名
    ​ window.location.pathname      	   当前页面的路径和文件名
    ​ window.location.port                 web 主机的端口 （80 或 443）
    ​ window.location.protocol       	   所使用的 web 协议（http:// 或 https://）
    ​ window.location.search          	   请求参数（？后面的内容）
    ```

  * window.navigator

    ```js
     navigator.appName       				返回获取当前浏览器的名称。
    ​ navigator.appVersion     				返回获取当前浏览器的版本号。
    ​ navigator.platform        			返回当前计算机的操作系统。
    ​ navigator.userAgent   	  			返回浏览器信息
    ```

  * history

    ```js
     history.go(1)    		  				参数可写任意整数，正数前进，负数后退
    ​ history.back( )   		 			后退
    ​ history.forward( ) 		  			前进
    ```

  * screen:( 屏幕 ）

    ```js
     window.screen.width 		  			返回当前屏幕宽度(分辨率值)
    ​ window.screen.height 	  				返回当前屏幕高度(分辨率值)
    ```

  * window下的弹框方法

    ```js
    alert( )   	prompt( )  	confirm( )
    ```

  * 定时器

    ```js
    超时定时器       	 间隔定时器
    setTimeout         setInterval
    clearTimeout       clearInterval
    
    ```

  * window.onload   页面加载

  * window.onscroll  滚动条兼容

    ```js
    var scrolltop=document.documentElement.scrollTop||document.body.scrollTop; //兼容
    ```

  * window.onresize  浏览器窗口大小触发事件

  * 判断当前浏览器类型的代码

    ```js
    function isBrowser() {
        var userAgent = navigator.userAgent;
        //微信内置浏览器
        if(userAgent.match(/MicroMessenger/i) == 'MicroMessenger') {
            return "MicroMessenger";
        }
        //QQ内置浏览器
        else if(userAgent.match(/QQ/i) == 'QQ') {
            return "QQ";
        }
        //Chrome
        else if(userAgent.match(/Chrome/i) == 'Chrome') {
            return "Chrome";
        }
        //Opera
        else if(userAgent.match(/Opera/i) == 'Opera') {
            return "Opera";
        }
        //Firefox
        else if(userAgent.match(/Firefox/i) == 'Firefox') {
            return "Firefox";
        }
        //Safari
        else if(userAgent.match(/Safari/i) == 'Safari') {
            return "Safari";
        }
        //IE
        else if(!!window.ActiveXObject || "ActiveXObject" in window) {
            return "IE";
        }
        else {
            return "未定义:"+userAgent;
        }
    }
    
    ```



##### DOM

DOM :**`Document Object Model 文档对象模型`**

DOM定义了**`表示`**和**`修改文档所需的对象`**、**`行为 `** 和 **`属性`** ，以及这些**` 对象之间的关系`**。

****

**DOM树**

​	根据文档对象模型（即：DOM），每个HTML标签事实上都是一个**对象**。嵌套的标签被称为**子**元素（或子标签）。除此之外，标签内的**文本**也是一个对象。而这些对象都可以使用JavaScript访问。

**DOM操作**

* 获取DOM节点

  ```js
   document.getElementById(id名)
  
  ​ getElementsByTagName(标签名)
  	得到的是一个集合（不止一个，是一堆）
      
  ​ getElementsByName( ) 通过Name值获取元素，返回值是集合，通常用来获取有name的input的值；
   注：1、不是所有的标签都有name值；
   	2、低版本的浏览器会有兼容问题；
      
  ​ children属性，获得DOM元素的所有子元素；返回值是集合
  ​ parentNode属性，获得DOM元素的父级元素
  ​ getElementsByClassName(class名称)，但是：IE8以下不能用
  
  ​ ES5选择器：
  document.querySelector (  )   			一旦匹配成功一个元素，就不往后匹配了
  document.querySelectorAll (  )   		匹配到所有满足的元素, 支持IE8+；
  
  ```

* 属性获取和操作

  ```js
  	getAttribute( )获取元素的属性值，他是节点的方法！所以前缀必须是节点！
    	document.getElementById( ID值 ).getAttribute( )
      什么是元素属性呢？ class就是元素属性，写在标签内的所有东西都是标签属性， 比如link的href比如img的src....都是元素属性。
     元素自带的属性可以直接用语法获取，但是自定义属性需要 getAttribute() 和 setAttribute( ) 方法。 
     
  ​	setAttribute( )设置元素的属性。同上；
  	有些小小的兼容性问题，低版本IE不兼容；
  	设置的属性永远都是字符串类型
  
  ​	removeAttribute( )删除属性；同上；
  	兼容性问题同上；
  ```

* DOM元素类型

  ```js
  （元素、文本和属性）
  1、node.Name   		节点名称
  2、node.Type   		1=元素节点、2=属性节点、3=文本节点	
  元素节点：标签名（大写）
  属性节点：属性名称
  文本节点：#text
  
  适用场所：网页换肤、隔行变色。
  ```

* 操作DOM

  ```js
  操作DOM的作用：增、删、克隆节点
  
  ​ 创建节点
  var oDiv = document.createElement("div");
  
  ​克隆节点
  clonedNode = Node.cloneNode(boolean)
  只有一个参数，传入一个布尔值，true表示深客隆，复制该节点下的所有子节点；false表示浅克隆，只复制该节点
  
  ​ 插入节点
  parentNode.appendChild(childNode);            		将新节点追加到子节点列表的末尾
  parentNode.insertBefore(newNode, targetNode);   	将newNode插入targetNode之前
  
  ​ 替换节点
  parentNode.replaceChild(newNode, targetNode);   	使用newNode替换targetNode
  
  ​ 移除节点
  parentNode.removeChild(childNode);            		移除目标节点
  node.parentNode.removeChild(node);    		    	在不清楚父节点的情况下使用
  
  ​ childNode.remove( )                         		IE不支持
  ```



##### node节点

node节点 ： **更详细的获取（设置）页面中所有的内容**；

​	根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点： **`元素是节点的别称`**，节点包含元素，当然节点还有好多细化的种类；



**根节点**：root  >>>>  HTML没有父节点；

**节点操作**：（通过父子系关系）

```js
 childNodes      获取当前元素的所有子节点；

​ nodeType       节点种类，返回值是数字；

​ nodeValue      获取（文字）节点的文本内容；

​ nodeName       返回node节点名称（#text，注释，标签....）；
```



**常见的节点类型**

| **nodeType值** | **含义**                              |
| -------------- | ------------------------------------- |
| 1              | 元素（DIV、BODY、LI、SPAN....... ）   |
| 2              | 属性代表属性节点 （class，src，href） |
| 3              | 文本节点（text节点）                  |
| 8              | 代表注释节点                          |
| 9              | 代表document节点；                    |



**获取节点元素**

```js
 nodeValue           	不会进行解析，会将标签名转译成字符串，直接输出；
​ innerHTML       		解析标签，获取元素节点标签间的元素内容  前面的内容满足条件则输出HTML文本。

即：
box.innerHTML = '<strong>abc</strong>';

box.childNodes[0].nodeValue = '<strong>abc</strong>';
// innerHTML会将标签解析；
// nodeValue不会进行解析，会将标签名转译成字符串，直接输出；
outerHTML/innerText (非W3C)
```



**attributes属性**

```js
 var oBox = document.getElementById('box');
		console.log(oBox.attributes)                       //获取所有，该节点的属性信息；
        console.log(oBox.attributes.length);               //返回属性节点个数
        console.log(oBox.attributes[0]);                   //返回第一个属性节点
        console.log(oBox.attributes[0].nodeType);          //2，属性
        console.log(oBox.attributes[0].nodeValue);         //属性值
        console.log(oBox.attributes['id']);                //返回属性为 id 的节点
 
        console.log(oBox.attributes.getNamedItem('id'));   //获取 id 的节点；

   	    attributes属性 一般只用作获取，设置使用setAttribute()
```



**HTML文本**

```js
 innerTEXT 		 				表示节点及其后代的“呈现”文本内容。
​ tagName				 			获取元素节点间的标签名

​ childNodes 		 				获取当前元素节点的所有子节点
​ firstChild		 				获取当前元素节点的第一个子节点
​ lastChild 		 				获取当前元素节点的最后一个子节点
​ previousSibling    				获取当前节点的前一个同级节点
​ nextSibling 		 				获取当前节点的后一个同级节点

​ firstElementChild   				获取当前元素节点的第一个元素子节点
​ lastElementChild   		 		获取当前元素节点的最后一个元素子节点
​ ownerDocument       				获取该节点的文档根节点，相当与 document
​ parentNode 		  				获取当前节点的父元素
```



##### **DOM尺寸和位置**

* **DOM尺寸**

| 属性                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| box.style.widthbox.style.height                              | 只能获取到内联style属性的CSS样式中的宽和高，如果有，获取;如果没有，则返回空 |
| getStyle(box,"width")getStyle(box,"width")//如下getStyle方法的封装 | 通过计算获取元素的大小，无关你是否是行内、内联或者链接，它经过计算后得到的结果返回出来。如果本身设置大小，它会返回元素的大小，如果本身没有设置，非IE浏览器会返回默认的大小，IE浏览器返回auto。 |
| box.clientWidthbox.clientHeight                              | 返回了元素大小，但没有单位，默认单位是px，如果设置了其他的单位，比如100em之类，返回出来的结果还会转换为px像素（不含边框） |
| box.scrollWidthbox.scrollHeight                              | 获取滚动内容的元素大小（当元素出现滚动条时，此属性指全部滚动内容的宽高）返回了元素大小，默认单位是px。如果没有设置任何CSS的宽和高度，它会得到计算后的宽度和高度 |
| box.offsetWidthbox.offsetHeight                              | 返回了元素大小，默认单位是px。如果没有设置任何CSS的宽和高度，他会得到计算后的宽度和高度包含盒模型中除margin以外的宽高（包含边框）最稳定，使用最频繁 |

以上这三对方法都是只读的；

* **位置坐标**

  | 属性                        | 说明                                                         |
  | --------------------------- | ------------------------------------------------------------ |
  | box.clientLeftbox.clientTop | 获取左边框和上边框的宽度                                     |
  | box.offsetLeftbox.offsetTop | 获取元素当前相对于offsetParent父元素的位置                   |
  | box.scrollTopbox.scrollLeft | 获取滚动内容上方的位置(就是隐藏的内容的高度)获取滚动内容左方的位置 |
  | **offsetParent**            | 这个属性的返回值是它根据谁定位的，如果它的所有父元素都没有定位，那么返回 |

* **获取非行内样式（兼容问题）**

  ```js
  function getStyle(obj,attr){    //获取非行间样式，obj是对象，attr是值
        if(obj.currentStyle){   //针对ie获取非行间样式
              return obj.currentStyle[attr];
        }else{
              return getComputedStyle(obj,false)[attr];   //针对非ie
        };
  };
  ```



##### 创建文档碎片

document.createDocumentaFragment(  )

```js
var cache = document.createDocumentFragment();
for( var i = 0 ; i < 1000; i ++ ){
    var opt = document.createElement("input");
    opt.type="button";
    opt.value = "删除";
    cache.appendChild(opt);
}
document.body.appendChild(cache);
```



### 事件

**事件的绑定**

​	w3c标准：事件写在行内，但是因为结构和行为要分离，所以我们一般情况下用JavaScript的方法来绑定事件，只有再极少数情况下，才将事件写在行内，事件的绑定方法：

```js
浏览器中的节点(对象).on+事件句柄 = function( ){
     要干什么？（放在浏览器中，不执行，当事件发生的时候再执行。）
}

oDiv.onclick=function(){     
     alert（1）
}
```



**事件总结** : 事件是给浏览器定义一个预处理函数，当事件触发的时候，执行函数，这就是事件。

​	当事件被触发的时候奥特曼会得到一个信息（事件对象），包含了跟事件相关的一些属性和方法的封装（如：事件发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态等），只有事件在触发的时候才会得到。

```js
oDiv.onmousedown=function(e){
     alert（e）;
}
```

**`JS缺德定律`**：事件对象有兼容问题；

```js
做好兼容再去使用事件对象：
e=e || window.event;

alert (e.buttons)观察.buttons的返回值；
```



##### 鼠标事件及方法

| 属性名              | 含义                                        |
| ------------------- | ------------------------------------------- |
| e.buttons           | 返回鼠标点击按键（1左键，2右键，4中键滚轮） |
| e.offsetX / offsetY | 获取事件触发最近的盒子（事件源）的坐标      |
| e.clientX / clientY | 获取可视区的坐标（根据浏览器的定位）        |
| e.screenX / screenY | 获取整个屏幕的坐标                          |
| e.pageX / e.pageY   | 获取文档的坐标（包含滚动条）                |



##### 可视化宽高

```js
/* 获取整个body的宽高
*/ @return <object> {width, height}

getBody : function () {
	return {
		width : document.documentElement.clientWidth || document.body.clientWidth,
		height : document.documentElement.clientHeight || document.body.clientHeight
	}
}
```



#####  键盘事件

keydown、keyup、keypress

```js
document.onkeydown = function(e){    
	console.log(e.keyCode)   
}
```

​	键盘上每一个键都有一个唯一的**`编码`**，用来识别当前用户正在操作的是键盘上哪一个键，

有**`兼容问题`**；e.keyCode || e.which;



​	特殊键码：是否按下alt  ctrl  和 shift;

```js
 e.altKey
​ e.ctrlKey
​ e.返回值是布尔值；
// 返回值是布尔值；

可以用来判断组合键
if（e.keyCode==13&&e.altKey）{
     alert('同时按下了enter和alt')；
}
```



##### 判断当前键码

```js
document.onkeydown=function(e){
	e=e || window.event;
	var cade=e.keyCode || e.which;
	console.log(code);
}
```



 ##### 默认行为

默认事件（浏览器）

​	有一些html元素默认的行为，比如说a标签，点击后有跳转动作；form表单中的submit类型的input有一个默认提交跳转事件；reset类型的input有重置表单行为。

但是，有些时候我们是不需要默认事件的，所以就需要阻止默认事件：

```js
if(e.preventDefault) {

   e.preventDefault();

}else {

    window.event.returnValue = false;    
    //return false;

}
```



##### 事件流

子元素的事件被触发时，父级也会被触发（冒泡）

一个完整事件流包含  捕获阶段 ---> 目标阶段  --->冒泡阶段

**`事件冒泡 `**： 

Netscape认为，石头先扔进河里，再从河里确定了一个扔石头的点，从外往内逐渐精确的过程（捕获）;

w3c认为，石头扔进去先到达准确的那个点，涟漪从内往外扩散（冒泡）;

**`事件流`**：事件执行的顺序

```html
捕获阶段：
	document-- 
		element  （html）---
			element  （body） ----
				element   （div） -----

冒泡阶段：
	element   （div）--
		element  （body） ---
			element  （html）----
				document ------
```

冒泡是可以阻止的；



##### 阻止冒泡

```js
if(e.stopPropagation) e.stopPropagation();
else e.cancelBubble = true;  // 兼容IE
```



##### 事件监听

DOM0级事件处理，是一种**`赋值`**方式，是被所有浏览器所支持的，简单易懂容易操作；

DOM2级事件处理是所有DOM节点中的方法，可以**`重复监听`**，但是**`浏览器兼容`**存在问题；

```js
oDiv.onclick = function(){ .... }    //DOM0级

//DOM2级
if(window.attachEvent){
    oDiv.attachEvent("onclick", function(){ ... });  // IE只有冒泡阶段,所以没有第三个参数，而且需要加on；
}else{
    oDiv.addEventListener( "click", function(){ ... },false);  // false指冒泡阶段
}


//移除事件监听，第二个参数为必须，移除的事件处理函数
oDiv.removeEventListener( "click",fn）
oDiv.detachEvent("onclick",fn)
```



##### 事件委托

**事件委托** 又叫**`事件代理`** 或者**`事件委派`**;

​	事件委托就是**`利用事件冒泡`**，只指定一个事件处理程序，就可以处理某一类型的所有事件，使用场景主要用于**`事件源不确定`**的情况，可以把**`事件委托给父级`**;

​	特点： 

```html
 减少了事件绑定浏览器重绘的次数，提高了程序的执行效率；
​ 减少了事件的亢余绑定，节约了事件资源；
​ 可以解决动态添加元素节点无法绑定事件的问题；
```



**判断事件源**

```js
    e.target || e.srcElement
```



##### 拖拽

拖拽应用到了三个点击事件 ：

```html
拖拽：
​ 鼠标按下 onmousedown
​ 鼠标移动 onmousemove
​ 鼠标抬起 onmouseup
```



```js
<body>
		<div></div>
		<script>
			var div = document.querySelector("div");
			div.onmousedown = function (e) {
				e = e || event;
				// 记录鼠标跟元素的偏移量
				var disX = e.offsetX,
					disY = e.offsetY;
				document.onmousemove = function (e) {
					console.log(disX, disY);
					e = e || event;
					// 获取鼠标坐标
					div.style.left = e.clientX - disX + "px";
					div.style.top = e.clientY - disY + "px";
				}
				document.onmouseup = function () {
					// 停止拖动 --- move事件解绑
					document.onmousemove = null;
				}
				return false; // 阻止默认圈选文字事件
			}
		</script>
</body>
```



### 正则表达式

regExp：定义字符串规则的表达式。

正则表达式其实就是一种规则，其实把正则称作规则表达式更为恰当。

```js
 test方法：
	该方法用来测试某个字符串是否与正则匹配，匹配就返回true，否则返回false；
    
​ compile方法：
	该方法的作用是能够对正则表达式进行编译，被编译过的正则在使用的时候效率会更高，适合于对一个正则多次调用的情况下，如果对一个正则只使用一两次，那么该方法没有特别显著的效应；
    
​ exec方法：
	返回的是一个数组，数组元素为匹配的子字符串
```



**写法**： 

```js
// 字面量

var reg=new RegExp('a');
var str='abcdefg';
alert(reg.test(str));   //返回bool值，代表是否匹配成功
```

```js
// perl风格

var re = /a/

var str='abcdefg';
re.test(str);
```



##### 转义字符

转义字符又元字符

```html
[ ]  中括号：匹配其中的某一个字符
( )  小括号：分组：小括号里面的内容作为整体进行匹配；小括号、竖线不要放在 [ ] 内（无意义）
| ：或，跟js中的(||)一样
^ ：排除（除了） 类似js中的（!）	
^ ：(不在中括号里)匹配字符串开头
$  匹配结尾
/^  $/ 完整匹配全等匹配


d  ---- [0-9]				数字
\w -----[a-z0-9_A-Z]			数字，字母，下划线
\s  -----空白字符
\D  -----[^0-9]				非数字
\W -----[^a-z0-9_]			非数字，字母，下划线
\ S -----非空白字符
.  -----全部字符

\b -----匹配单词边界
\B -----匹配 非 单词边界
\0(数字0) -----匹配 NUL 字符
\n -----匹配 换行符
\f -----匹配 换页符
\r -----匹配 回车符
\t -----匹配 制表符
\v -----匹配 垂直制表符
```



##### 量词

```html
{n}  ---匹配n次
{n,m} ---最少n次，最多m次； 
{n,} ---最少n次，最多不限
+	{1,}
?	{0,1} 可有可无，最多一个
*  {0,} 可以有也可以没有，个数不限

i：忽略大小写
g：全局查找
m：多行查找
```



##### 直接量字符

```js
\/ 匹配 /
\\ 匹配 \
\. 匹配 .
\* 匹配 *
\+ 匹配 +
\? 匹配 ?
\| 匹配 |
\( 匹配 (
\) 匹配 )
\[ 匹配 [
\] 匹配 ]
\{ 匹配 {
\ } 匹配 }
\’ 匹配 单引号
\” 匹配 双引号
 
\xxx 查找以八进制数 xxx 规定的字符
\xdd 查找以十六进制数 dd 规定的字符
\uxxxx 查找以十六进制数 xxxx 规定的 Unicode 字符
\u4e00 - \u9fa5    验证中文
```

**贪婪模式和惰性模式**

```js
贪婪： /[ab]+b/ 	结果：abbbb

惰性： /[ab]+?b/	结果：ab
```



##### 支持字符串方法

```htm
 search
	查找第一次匹配的子字符串的位置，如果找到就返回一个number类型的index值，否则返回-1

​ replace
	该方法用来将字符串中的某些子串替换为需要的内容，接受两个参数，第一个参数可以为正则或者子字符串，表示匹配需要被替换的内容，第二个参数为被替换的新的子字符串

​ split
	将一个字符串拆分成一个数组，它接受一个正则或者子字符（串）作为参数，返回一个数组

​ match
	接受一个正则作为参数，用来匹配一个字符串，返回一个数组。
```



##### 正则扩展

```html
1.u
ES6对正则表达式添加了u修饰符，含义为“Unicode模式”，用来正确处理大于\uFFFF的Unicode字符。也就是说，会正确处理四个字节的UTF-16编码。
/^\u{61}$/.test('a')  		// false   {61}会识别成量词
/^\u{61}$/u.test('a')     // true    {61}识别大括号的Unicode字符

2.y (“粘连”修饰符)
ES6添加了y修饰符和g类似，不过y 修饰符在下次匹配的时候需要紧跟上次匹配成功之后的结果匹配，确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的含义。而g则是全局匹配，只需要剩余位置中存在匹配就可;
实际上，y 修饰符号隐含了头部匹配的标识 ^，y修饰符的设计本意，就是让头部匹配的标识 ^ 在全局匹配中都有效。

exec( ) 方法在匹配全局对象的时候，多次匹配会在上一次结束的地方继续匹配;
```



### ES5 严格模式

​	除了正常运行模式，ECMAscript 5 添加了第二种运行模式："严格模式"（strict mode）。顾名思义，这种模式使得Javascript在更严格的条件下运行。

​	**特点**

```html
1.消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
2.消除代码运行的一些不安全之处，保证代码运行的安全；
3.提高编译器效率，增加运行速度；
4.为未来新版本的Javascript做好铺垫。
```

​	"严格模式"体现了Javascript**`更合理、更安全、更严谨`**的发展方向，包括**`IE 10`**在内的主流浏览器，都已经支持它。

​	另一方面，同样的代码，在"严格模式"中，可能会有不一样的运行结果；一些在"正常模式"下可以运行的语句，在"严格模式"下将不能运行。



#####  进入严格模式 :

"use strict"

```js
<script>
        "use strict"
        console.log("已经进入严格模式");
</script> 
```



##### **严格模式行为变更：**

* 全局变量声明时 必须加var;

  ```js
  <script>
  
      "use strict"
                 
      a = 10;//报错 因为 a没有被var 声明
  
       //Uncaught ReferenceError: a is not defined; 引用错误： a 没有被声明
                           
  </script>
  ```

* this 无法指向全局对象;

  ```js
  <script>
          "use strict"
           // console.log("已经进入严格模式");
          function a(){
              this.b = 10; //报错 ， 因为this指向了window对象;
              //Uncaught TypeError: Cannot set property 'b' of undefined; 类型错误 ： 不能给undefined设置属性b；
  
          }
          window.a()；
  </script>
  ```

* 函数内重名属性；

  ````js
  <script>
      "use strict";
      function a(b,b,c){ //报错
  
              // Uncaught SyntaxError: Duplicate parameter name not allowed in this context   ;语法错误：在此上下文中不允许重复的参数名称
  
      }
  </script>
  ````

* arguments对象;

  * arguments对象不允许被动态改变;

    ```js
    <script>
        function fn1(a) {
            a = 2;
            return [a, arguments[0]];
        }
        console.log(fn1(1)); // 正常模式为[2,2]
        function fn2(a) {
            "use strict";
            a = 2;
            return [a, arguments[0]];
        }
        console.log(fn2(1)); // 严格模式为[2,1]
    </script>
    ```

  * arguments对象不允许被自调用;

    ```js
    <script>
            "use strict";
            var f = function() { return arguments.callee; };
            f(); // 报错
    
            //Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode functions or the arguments objects for calls to them
    
            //类型错误：“caller ”，“arguments.callee ”，不能在严格模式中使用;
    
            //caller返回调用当前函数的函数的引用  （正在执行的函数的属性）
           // callee返回正在执行的函数本身的引用 （arguments的属性）
    
    </script>
    ```

* 新增保留字； implements, interface, let, package, private, protected, public, static, yield。

  ```js
  <script>
  	"use strict";
  	function package(protected) { // 语法错误
      	var implements; // 语法错误
  	}
  	package();
  </script>
  ```



##### ES5 新增常见方法

```js
数组：
2个索引方法：indexOf() 和 lastIndexOf()；
5个迭代方法：forEach()、map()、filter()、some()、every()；
2个归并方法：reduce()、reduceRight()；


字符串：
    trim();// 去掉字符串前后空格
    trimLeft()
    trimRIght()


Date.now();  							//日期对象得到当前日期的毫秒数


JSON.parse(str);  						//json序列化，将符合json格式的字符串转换为json
JSON.stringify(); 						//json转换为字符串


对象：
Object.defineProperties(obj, props); 	//给obj设置属性
Object.keys(obj);  						//获取obj的所有属性名称，返回数组
Object.values(obj);  					// 获取obj的所有属性值，返回数组
Object.assign       					// 合并对象
```



举例：

```js
var obj = new Object();

Object.defineProperty(obj, 'name', {
configurable: false, // 表示能否通过delete删除此属性
writable: true, // 能否修改属性的值
enumerable: true, // 表示该属性是否可枚举，即是否通过for-in循环或Object.keys()返回属性
value: '张三'
})

console.log(obj.name)

或者：

var obj = new Object();
Object.defineProperties(obj, { 
    name: {
        value: '张三',
        configurable: false,
        writable: true,
        enumerable: true
    }, 
    age: {
        value: 18,
        configurable: true
    }
})

console.log(obj.name, obj.age) // 张三, 18
```



### ES6

ES6 ： ECMAScript2015；



##### let / const

let --**`块级作用域`**：一种普遍存在于各个语言中的作用域范围；

```js
     {
          var a = 10;
          let b = 20;
     }
     
     console.log(a)//10
     console.log(b)// a is not defined
// 我们可以发现，在一个大括号中用let声明的变量在外部不可访问了，每个大括号都是独立的作用域
```

* **`let不存在声明提升`**;

```js
console.log(a); // undefined;
     var a = 10;
console.log(b)   // b is not defined;
	let b = 10;
```

* **暂时性死区；**

  ```js
   var a = 10;
       if(true){
           console.log(a);//ReferenceError(引用错误): a is not defined;
           let a = 20;
  	 }
  ```

  ​	 ES6规定在某个区块中， 一旦用**let或const声明一个变量**，那么这个区块就变成**`块级作用域`**，用let或者const声明的变量即为该区块绑定， 该变量不受任何变量影响。 **在该变量使用let声明前不可以用**。在语法上，我们叫这种情况为：暂时性死区 (temporal dead zone，简称 TDZ)



**const** : 声明常量

```js
const a = 20;

a = 30;    // Uncaught TypeError: Assignment to constant variable.
		   // 未捕获的类型错误：分配给常量变量。
```



##### **扩展运算符  ...**

三个点号，功能是把**`数组`**或**`类数组对象`**展开成一系列**`用逗号隔开的值`**;

```js
var foo = function(a, b, c) {
console.log(a);
console.log(b);
console.log(c);
}

var arr = [1, 2, 3];

//传统写法
foo(arr[0], arr[1], arr[2]);

//使用扩展运算符
foo(...arr);
//1
//2
//3
```



##### rest运算符 ...

rest运算符也是三个点号，不过其功能与扩展运算符恰好相反，把**`逗号隔开的值`**序列**`组合成一个数组`**;

```js
//主要用于不定参数，所以ES6开始可以不再使用arguments对象
var bar = function(a, ...args) {
    console.log(a);
    console.log(args);
}

bar(1, 2, 3, 4);
//1
//[ 2, 3, 4 ]
```



##### 字符串扩展



* **字符串的 Unicode 表示**;  规则为\u + 四位十六进制;

  ```js
  这种新的字符表示方式只能表示  \u 0000 ~ \u ffff 之间的数字。 
  
  如果超出范围必须用双字节表示;
  console.log("\uD842\uDFB6"); 
  ```

  

*  如果想要**`一次性表示超出范围的字符`**那么我们可以使用{ }来表示；

  ```js
  console.log("\u20BB9");  这个的打印结果是 拆分开来的 ₻9
  
  console.log("\u{20BB9}"); 这个打印的结果是一个完整的字符
  ```

  

* ES6**`支持多种格式的字符`**表示;





##### 字符串新增的方法

* **repeat()重复功能**

  ```js
  'x'.repeat(3)  //xxx；
  
  重复字符串;
  ```

  

* **includes()  startsWith() endsWith()  ;判定字符串中是否存在某个字符串;**

  ```js
  var s = 'Hello world!';
  
    s.startsWith('Hello') // true   		以参数开头
    s.endsWith('!')  		// true         以参数结尾
    s.includes('o') 		// true         包括参数;
  
  
  第二种方法接受第二个参数，第二个参数表示从第几位开始;
  var s = 'Hello world!';
  
    s.startsWith('world', 6) // true
    s.endsWith('Hello', 5)   // true
    s.includes('Hello', 6)   // false       
  ```

  

* **for of** 

  一种新的遍历方式 ; for of 可以用于遍历字符串：

  ```js
  for of 可以用于遍历字符串：       
            var s = "abc";
            for(let  b  of s){               
                 console.log(b) 	// "a"  "b"  "c"
             }
  ```





##### **字符串模板扩展**

```js
	ES6中存在一种新的字符串， 这种字符串是 以 ` `  (波浪线上的那个字符 > 反引号)括起来表示的；
通常我们想要拼接一个带有标签的字符串， 是用这样的方式:
     bianliang + " <strong>这是一个文字" + obj.name + "</strong> " + bianliang


但是
	有了ES6字符串一切都变得非常简单了;
      `  ${bianliang} <strong>这是一个文字${obj.name}</strong>${bianliang} `
	1.用 ${ } 扩住变量让拼接变得非常容易;

	2.当我们想要在字符串中使用 `反引号的时候我们需要进行转义；
	`\`Yo\` World!`    //"`Yo` World!"

	3.模板还可以调用函数；
          function fn() {
   			 return "Hello World";
  		  }
  		`foo ${fn()} bar`
```





##### 箭头函数

**使用**：

```js
var  函数名 = 参数 => 运算规则;  

// 参数只有一个时可以省略括号，运算规则只有一句话时可以省略大括号和return。
(形参) =＞｛
｝

eg:
var obj = {    
	left : 200,     
	move : function(){         
		setTimeout( ()=>{          
		this.left = 100;      
	 },1000);    
} }
```

​	箭头函数this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this,导致内部的this就是外层代码块的this。正是因为这个，所以**`箭头函数也不能做构造函数`**。



**特点**

```js
1、箭头函数自绑this，	this = window；function的this = function的父元素，
2、箭头函数不能New；
3、箭头函数如果要返回一个JSON对象，json函数用小括号把键值对括起来 “（{}）”，或者大括号+ return “{return{ }}”；
4、自动绑定this；
5、箭头函数的代码的可读性伤害太大；
```



##### 解构赋值

**作用**：

```html
1、一次性可以定义多个变量；
2、可以作用在函数传参上，以对象的方式传递，参数顺序也无需保持一致；
3、可以轻松实现两个数的交换；
4、可以实现剩余和扩展运算；
```

```js
var arr = [2,4,5,6];
	var [a,b] = arr;
console.log(a,b);
var [p1, {userName,ag:[a,b]}] = json;
```



##### **Symbol类型**

​	Symbol函数会生成一个唯一的值可以理解为Symbol类型跟字符串是接近的 , 但每次生成唯一的值，也就是每次都不相等，

```js
const TYPE = {    

SMALL: Symbol(),  
MIDDLE: Symbol(), 
LARGE: Symbol()

}

//以前我们可能会把SMALL、MIDDLE、LARGE赋值为数字或字符串
//案例： 点击div切换四种颜色
//还要确保它们的值不能发生重复，但现在不用担心了

function Create(type){   

          switch(type){       
                case TYPE.SMALL:  {console.log("SMALL")}  break;       
                case TYPE.MIDDLE: {console.log("MIDDLE")}  break;               
                case TYPE.LARGE:  {console.log("LARGE")}  break;     
            }
        }

var s = Create(TYPE.MIDDLE);
```



##### **Set和Map结构**

Set集合，本质上就是**`对数组的一种包装`** ;

Set集合是**`默认去重`**的，但前提是两个添加的元素严格相等 所以5和"5"不相等，两个new出来的字符串不相等 ;

```js
let imgs = new Set();
imgs.add(1）;
imgs.add(1）;
imgs.add(5）;
imgs.add("5"）;
imgs.add(new String("abc")）;
imgs.add(new String("abc")）;

// 打印的结果： 1  5  '5'  'abc'  'abc'
```

```js
// set去重
var newarr = [...new Set(array)];
```



Set集合本质上还是一个map,因此会有以下几种奇怪的遍历方法：

```js
var imgs = new Set(['a','b','c']); 

 //根据KEY遍历
for(let item of imgs.keys()){
    console.log(item);
} //a //b //c
```

```js
//根据VALUE遍历
for(let item of imgs.values()){
    console.log(item);
} //a //b //c
```

```js
//根据KEY-VALUE遍历
for(let item of imgs.entries()){
    console.log(item);
 } //['a','a'] //['b','b'] //['c','c']
```

```js
//普通for...of循环(for...of跟for-in的区别很明显，就是直接取值，而不再取下标了)
for(let item of imgs){  
  console.log(item);
} //a //b //c
```



**Map集合,即映射** ；

```js
let map = new Map();

map.set("S230", "张三");
map.set("S231", "李四");
map.set("S232", "王五");

//获取某一个元素 
map.get("s232"); //王五

//循环遍历，配合解构赋值 
for(let [key,value] of map){    console.log(key,value);  }
```



##### Class语法糖

Class保留字终于成了关键字；

​	其中constructor被称之为构造方法，在我们new 一个对象的时候，自动被调用 ；不过本质上，JS依然使用了原型来实现，也就是说，这不过是一个新的写法而已 跟以前的构造函数没有区别。要注意的是，使用了class来定义类，必须先定义再使用。

```js
class Iphone{
    constructor(color, size){
            this.color = color;
            this.size = size;    
     }    
	playgame(){
           //.............    
	}    
	toString(){
          return `这台手机的颜色是${this.color} 屏幕大小是${this.size}`;
    }
    new Iphone();
}

或者
class Fn {
		constructor (name) {
			this.name = name;
		}
		say () {
			console.log(this.name);
		}
}
var num=new Num（“name”）;
num.say();
```



#####  兼容问题

```html
1、事件对象的创建；
2、事件冒泡
3、浏览器的默认行为
4、事件委托中事件源的获取
```

```js
// 事件对象的创建；
e=e || window.event;

// 事件冒泡
if(e.stopPropagation) e.stopPropagation();
else e.cancelBubble = true;  // 兼容IE

// 浏览器的默认行为
if(e.preventDefault) {
   e.preventDefault();
}else {
    window.event.returnValue = false;    
    //return false;
}

// 事件委托中事件源的获取
e.target || e.srcElement

// 判断键码
e.keyCode || e.which;
```





### 面向对象

对象的本质：

​	属性和方法的集合；

​	结论：万事万物皆为对象

**对象的三大特点** :   **封装、继承、多态**

```html
封装：
    1、写对象
    2、用对象
把一些相关的对象和属性放到一起，用一个变量抽象出来，那么这就完成了这个对象的封装


继承：
    1、子承父业
    2、子对象可以使用父对象的一些属性和方法


多态：重载，重写
    重载就是根据不同的参数类型，参数个数实现不同的功能
    重写就是父类的方法不好用，我自己重新定义一个方法名相同的不同方法
类和对象的关系： -->  模板  -->  产品;
```



##### **创建对象**

```html
1、字面量  var obj = {}

2、通过new运算符 var obj = new Object()

3、构造函数
      用来构造（创建）对象的函数
      他在声明的时候跟普通函数没有区别
      用new运算符加上函数的调用，调用的结果就是一个对象
      构造函数中的this指的是即将要new的那个对象

4、ES6语法糖
```





##### **原型**

​	原型是**`函数的伴生体`**；我们创建的每个函数都有一个**`prototype(原型)属性`**，这个属性是一个**`指针`**，指向一个对象，而这个对象的用途是包含可以由特定类型的所有**`实例共享的属性和方法`** ;

​	prototype（原型）属性 指向的对象就是**`原型对象`**;



​	**属性和方法：**

```txt
属性和方法:
​ constructor    			prototype里面的constructor指向当前对象的构造函数

​ __proto__   				===  [[prototype]]   指向父类的prototype

​ prototype      			指向当前对象的原型对象

​ instanceof     			运算符，判断当前对象是否是另一个对象的实例

​ hasOwnProperty  			判断对象上是否存在某个属性，并且这个方法会过滤到原型上的属性

​ isPrototypeOf      		检查一个对象是否存在于另一个对象的原型链上
```

​	**注意的问题**

```html
1.改写面向对象程序，要让所有函数不能嵌套；

2.提取变量，让函数正常运行；

3.改写面向对象，将方法写在prototype上；

4.注意this指向问题。
```





##### **OOA、OOD、OOP**

```html
OOA、OOD、OOP
​	OOA面向对象分析
	面向对象分析: 将大问题拆分成小问题，并试图用分工协作来完成 的思维方式。
	面向对象不是编程独有思维方式。
	面向对象分析方法（Object-Oriented Analysis，OOA），是在一个系统的开发过程中进行了系统业务调查以后，按照面向对象的思想来分析问题。OOA与结构化分析有较大的区别。OOA所强调的是在系统调查资料的基础上，针对OO方法所需要的素材进行的归类分析和整理，而不是对管理业务现状和方法的分析。
OOA（面向对象的分析）模型由5个层次（主题层、对象类层、结构层、属性层和服务层）和5个活动（标识对象类、标识结构、定义主题、定义属性和定义服务）组成。在这种方法中定义了两种对象类之间的结构，一种称为分类结构，一种称为组装结构。分类结构就是所谓的一般与特殊的关系。组装结构则反映了对象之间的整体与部分的关系。

​	OOD面向事件设计
1、分析模块后，确定职责。
2、确定耦合关系；
3、为OOP做准备。

​	OOP面向事件编程
将内容包含在对象中  --> 信息传递速度更快，效率更高
系统升级 --> 通过增加和删除组件实现需求。（某个软件中的组件）
```
























