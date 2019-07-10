什么是预处理器？

​		**CSS 预处理器是一种语言用来为 CSS 增加一些编程的的特性，无需考虑浏览器的兼容性问题。**可以在 CSS 中使用变量、简单的程序逻辑、函数等等在编程语言中的一些基本技巧，可以让你的 CSS 更见简洁，适应性更强，代码更直观等诸多好处。



它们的后缀名？

​		Sass 和 Less 都使用的是标准的 CSS 语法，因此如果你可以很方便的将已有的 CSS 代码转为预处理器代码，默认 Sass 使用 ` .sass ` 扩展名，而 Less 使用 ` .less`  扩展名.



SASS和less的**变量声明**？

​		Sass 的变量必须是 $ 开始，然后变量名和值使用冒号隔开，跟 CSS 的属性一致；

```scss
$mainColor: #0982c1;
 
body {
  color: $mainColor;
}
```

​		 Less 的变量名使用 @ 符号开始：

```less
@mainColor: #0982c1;
 
body {
  color: @mainColor;
}
```



**Mixins (混入)**、 继承、导入 (@Import)