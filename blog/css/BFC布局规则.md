#前端/css

2022-11-11 13:55

## 前言

BFC在css的学习中是重要的但不易理解的概念，BFC也牵扯了很多其他问题，如浮动、定位、盒模型等，因此弄懂BFC是很有必要的。本文对BFC进行总结，希望对你有所帮助。

## BFC是什么？

先看看MDN的定义：

> 块格式化上下文（Block Formatting Context，BFC） 是Web页面的可视化CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

官方文档的说法很难理解，查阅多方资料后，得到以下的结论：

> BFC(block formatting context)块级格式化上下文，它是页面中的一块渲染区域，并且有一套属于自己的渲染规则，它决定了元素如何对齐内容进行布局，以及与其他元素的关系和相互作用。 当涉及到可视化布局的时候，BFC提供了一个环境，HTML元素在这个环境中按照一定规则进行布局

简短的总结：**BFC是一个独立的布局环境，BFC内部的元素布局与外部互不影响**

## BFC的布局规则

1.  内部的Box会在垂直方向一个接着一个地放置。
2.  Box垂直方向上的距离由margin决定。属于同一个BFC的两个相邻的Box的margin会发生重叠。
3.  所有属于BFC中的盒子默认左对齐，并且它们的左边距可以触及到容器的左边线。最后一个盒子，尽管是浮动的，但依然遵循这个原则。
4.  BFC的区域不会与float box重叠。
5.  BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。
6.  计算BFC的高度时，浮动子元素也参与计算。

## 如何触发BFC？

这里只记录常用方法，想要了解全部触发BFC的方法请点击此[链接](https://link.zhihu.com/?target=https%3A//developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

1. 浮动元素，float 除 none 以外的值；   
2. 定位元素，position（absolute，fixed）；   
3. display 为以下其中之一的值 inline-block，table-cell，table-caption；   
4. overflow 除了 visible 以外的值（hidden，auto，scroll）；

## BFC可以解决哪些问题？

-   解决浮动元素令父元素高度坍塌的问题

方法：给父元素开启BFC

原理：计算BFC的高度时，浮动子元素也参与计算

![动图](https://pic3.zhimg.com/v2-880519f91bd0d58be798fb1bb2c79702_b.webp)

-   非浮动元素被浮动元素覆盖

方法：给非浮动元素开启BFC

原理：BFC的区域不会与float box重叠

演示：
![动图](https://pic4.zhimg.com/v2-829a36f238d40c395b82bdc182cda59f_b.webp)

-   两栏自适应布局

方法：给固定栏设置固定宽度，给不固定栏开启BFC。

原理：BFC的区域不会与float box重叠

演示：

![动图](https://pic4.zhimg.com/v2-e66bd46e2f5ebbd9b2b0885e44ed2883_b.webp)


-   外边距垂直方向重合的问题

方法：给上box或者下box任意一个包裹新的box并开启BFC

原理：属于同一个BFC的两个相邻的Box的margin会发生重叠。

演示：

![动图](https://pic1.zhimg.com/v2-b009cd8730013634c885f2ebb76b0710_b.webp)

## 参考

[BFC官方文档](https://link.zhihu.com/?target=https%3A//developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
[BFC](https://juejin.cn/post/7147928538811727880)