## HTML5-画布canvas

> 菜鸟地址：https://www.runoob.com/w3cnote/html5-canvas-intro.html
> MDN文档：https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial

​	`Canvas` 是由 `HTML` 代码配合高度和宽度属性而定义出的可绘制区域。`JavaScript` 代码可以访问该区域，类似于其他通用的二维 `API`，通过一套完整的绘图函数来动态生成图形。



### <canvas> 元素

建议直接在 <canvas> 元素中设置 width、height 属性来设置 canvas 的宽度与高度，若要设置在低版本下不支持canvas，则在标签里面填写内容。

```html
<canvas>
    你的浏览器不支持 canvas，请升级你的浏览器。
</canvas>
```

注意：结束标签 </canvas> 不可省略



### 渲染上下文

渲染上下文(画笔)的获取：

```js
// 获取画布
const canvas = document.querySelector('#tutorial')
// 获取渲染上下文（画笔）
const ctx = canvas.getContext('2d')
```



### 检测支持性

```js
var canvas = document.getElementById('tutorial');

if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```



### 绘制形状

#### 设置样式

1. ctx.fillStyle()
2. ctx.strokeStyle()

#### 绘制矩形

1. ctx.fillRect(x, y, width, height)
2. ctx.strokeRect(x, y, width, height)
3. ctx.clearRect(x, y, width, height)

#### 绘制路径

1. beginPath()
2. moveTo()
3. closePath()
4. stroke()
5. fill()

##### 线段

ctx.lineTo(x, y)

ctx.moveTo(x, y)

##### 弧

ctx.arc(x, y, r, startAngle, endAngle, anticlockwise)

x,y 圆中心点坐标
r   半径
startAngle, endAngle  起点与终点的弧度
anticlockwise  是否逆时针    true: 逆时针   false: 顺时针

角度转换为弧度的公式：

radians = (Math.PI / 180) * degrees

##### 文本

ctx.fillText(text, x, y)
ctx.strokeText(text, x, y)

##### 图像

ctx.drawImage(image, x, y, width, height)

注意：通常绘制图像会在图像内容加载结束后再绘制

```js
// 创建图像元素
const img = new Image()
img.src = './images/1.jpg'
// 图像资源加载完毕，再渲染
img.onload = function() {
  // 在 canvas 上绘制图像
  ctx.drawImage(img, 0, 0, 300, 300)
}
```

##### 变形

ctx.translate(x, y)
ctx.rotate(x)

##### 动画

动画的基本步骤

**清空 canvas** 在绘制每一帧动画之前，需要清空所有。清空所有最简单的做法就是 clearRect() 方法。

**保存 canvas 状态** 如果在绘制的过程中会更改 canvas 的状态(颜色、移动了坐标原点等),又在绘制每一帧时都是原始状态的话，则最好保存下 canvas 的状态

**绘制** 动画图形这一步才是真正的绘制动画帧

**恢复** canvas 状态如果你前面保存了 canvas 状态，则应该在绘制完成一帧之后恢复 canvas 状态。