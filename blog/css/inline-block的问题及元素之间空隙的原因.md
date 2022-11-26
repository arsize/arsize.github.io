#前端/css 

2022-11-11 14:15

在html里面，元素分为两种基本类型：1.块元素 2. 内联元素；然而内联元素是没有宽和高属性的，在我们布局页面的过程中，如果需要让块元素水平排列，我们除了使用浮动(float)、弹性盒(flex)之外，我们还可以通过使用display:inline-block来让一个块元素保持自身的宽高属性并且实现水平排列。

`display:inline-block`相比于与浮动、定位最大的不同就是其没有父元素的匿名包裹特性，这使得display:inline-block属性的使用非常自由，可与文字，图片混排，可内嵌block属性元素，可以置身于inline水平的元素中。

在CSS布局中，如果我们想要将一些元素在同一行显示，其中的一种方法就是把要同行显示的元素设置display属性为inline-block。但是你会发现这些同行显示的inline-block元素之间经常会出现一定的空隙，这就是“换行符/空格间隙问题”。

![](https://raw.githubusercontent.com/arsize/pic-bed/main/obsidian/202211111431876.png)

### 空隙产生的原因(`important`)

元素被当成行内元素排版的时候，元素之间的`空白符（空格、回车换行等）`都会被浏览器处理，根据white-space的处理方式（默认是normal，合并多余空白），**原来HTML代码中的回车换行被转成一个空白符，在字体不为0的情况下，空白符占据一定宽度，所以inline-block的元素之间就出现了空隙**。这些元素之间的间距会随着字体的大小而变化，当行内元素font-size:16px时，间距为8px。

### 解决空隙的办法

### 办法一：解决元素之间的空白符

```html
<!-- 将所有子元素写在同一行 --> <div class="parent"> <div class="child">child1</div><div class="child">child2</div> </div>
```

### 方法二：为父元素中设置font-size: 0，在子元素上重置正确的font-size

```html
<div class="parent" style="font-size: 0px">
	<div class="child" style="font-size: 16px">child1</div>
	<div class="child" style="font-size: 16px">child2</div>
</div>
```

缺点：**inline-block元素必须设定字体**，不然行内元素中的字体不会显示。 增加了代码量。

### 设置父元素，display:table和word-spacing

```css
.parent{ display: table; word-spacing:-1em; }
```


---

#### inline-block会产生的其他问题

1.内部包含文本、图片的inline-block会与周围inline-block元素产生垂直方向偏移

```html
<html lang="en">
<head>
    <style>
        .fater {
            font-size: 0;
        }
        .block {
            display: inline-block;
            width: 100px;
            height: 100px;
            background-color: blue;
            font-size: 16px;
        }
        .item {
            display: inline-block;
            width: 100px;
            height: 100px;
            background-color: red;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="fater">
        <div class="block">
            <span>hello</span>
        </div>
        <div class="item">
        </div>
    </div>
</body>
</html>
```

偏移效果：

![](https://raw.githubusercontent.com/arsize/pic-bed/main/obsidian/202211111440799.png)

这其中就涉及到了`vertical-align`属性的一些性质，下一部分就来讲讲`vertical-align`，并且来说说这种现象的原因。

## 内联元素的对齐主要由哪些属性影响

我们以下所说的对齐主要是针对内联元素的。我们都知道CSS最后展现在界面中的结果，经常是由多个属性共同作用的结果。对齐主要是由`font-size`，`line-height`和`vertical-align`这三个属性共同作用的结果.

## 内联水平元素的baseline是什么

`vertical-align`属性有非常多的值，它的默认值是`baseline`即相对于基线对齐。基线的概念我们在[font-size](https://overfronted.net/posts/www.baidu.com)那部分也说过，那里解释的是文字的基线。那么对于一个`display: inline-block`，并且拥有固定宽和高的元素来说，它的基线是什么那？我可能问了一个很蠢的问题，很多人应该都知道，它的基线就是其`margin-box`即该元素的底部边界（包括margin）。如图所示，

![image](https://user-images.githubusercontent.com/13817144/55063668-71324a00-50b3-11e9-8f87-906d552a3eff.png)

但是如果在该元素中其中加入文字，它的基线还是底边界吗？实践出真知，我们还是用[实例](https://codepen.io/xwchris/pen/vjrgrE)来看下。

![image](https://user-images.githubusercontent.com/13817144/39965395-77358518-56ca-11e8-8724-c04ba573e304.png)

这种情况这个在css2.1规范里有提及

> The baseline of an 'inline-block' is the baseline of its last line box in the normal flow, unless it has either no in-flow line boxes or if its 'overflow' property has a computed value other than 'visible', in which case the baseline is the bottom margin edge

意思就是`inline-block`如果有`overflow`非`visible`的属性或者没有其中任何行盒那么它的基线就是底部的margin边界否则的话它的基线就是其中最后一个行盒的基线。

#### 最后说说关于inline、inline-block的margin和padding表现

经过测试：

1. display:inline，margin在左右方向生效，在垂直方向上不生效；设置 padding 本身生效，但是**没有把父级元素撑开**。

```css
<span class="hp">hello</span>
.hp {
	margin: 20px;
}
```

