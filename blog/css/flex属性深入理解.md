#前端/css 

2022-11-11 15:34

`flex`属性是`flex-grow`，`flex-shrink`和`flex-basis`这3个CSS属性的缩写,按照以往的经验，`flex`属性只有一个值的时候，另外缺省的值应该使用默认值才对，但是`flex`属性并不是这样的。

-   `flex:1`等同于`flex:1 1 0%`，`flex:1 2`等同于`flex:1 2 0%`，即`flex-basis`使用的不是默认值`auto`，而是使用的`0%`；
-   `flex:100px`等同于`flex:1 1 100px`，即`flex-grow`使用的不是默认值`0`，而是使用的`1`；

这就是上面提到的`flex`属性站在实用主义的角度对缩写属性的计算值进行了优化。

然后，还有一个重要原因，flex属性的长语法需要理解深刻，反复使用才能驾驭，门槛比较好，因此，实际开发，如果可以，建议使用flex缩写。

#### flex:1和flex:auto的区别和各自适用场景

`flex:1`等同于设置`flex: 1 1 0%`，`flex:auto`等同于设置`flex: 1 1 auto`。

结合flex属性值的描述，我们可以得出`flex:1`和`flex:auto`的行为表现：

> 元素尺寸可以弹性增大，也可以弹性变小，具有十足的弹性，但是`flex:1`在尺寸不足时会优先最小化内容尺寸，`flex:auto`在尺寸不足时会优先最大化内容尺寸。

上面的描述可以通过一个例子明白是什么意思，这一次是仅仅设置第1项的文字内容很多，HTML代码如下所示：

```html
<h4>flex:1</h4>
<div class="container flex-1">
    <item>范张范张范张范张范张范张范张范张范张</item>
    <item>范鑫</item>
    <item>范旭</item>
    <item>范帅</item>
    <item>范哥</item>
</div>
<h4>flex:auto</h4>
<div class="container flex-auto">
    <item>范张范张范张范张范张范张范张范张范张</item>
    <item>范鑫</item>
    <item>范旭</item>
    <item>范帅</item>
    <item>范哥</item>
</div>
```

可以看出两段HTML结构和内容都是一样的，现在，对上下两端HTML设置不同的CSS样式，代码如下所示：

```css
.flex-1 item {
    flex: 1;
}
.flex-auto item {
    flex: auto;
}
```

结果就会看到如下图所示的布局效果。

![flex:1和flex:auto的对比效果示意](https://image.zhangxinxu.com/image/blog/202010/6-43_flex-1-auto.png)

上图鲜明地体现了`flex:1`和`flex:auto`的区别，虽然都是充分分配容器的尺寸，但是`flex:1`的尺寸表现更为内敛（优先牺牲自己的尺寸），`flex:auto`的尺寸表现则更为霸道（优先扩展自己的尺寸）。

从某种程度上讲，`flex:1`的表现神似`table-layout:fixed`，`flex:auto`的表现神似`table-layout:auto`。

##### 适合使用flex:1的场景

当希望元素充分利用剩余空间，同时不会侵占其他元素应有的宽度的时候，适合使用`flex:1`，这样的场景在Flex布局中非常的多。

例如所有的等分列表，或者等比例列表都适合使用`flex:1`或者其他flex数值，适合的布局效果轮廓如下图所示。

![flex:1适合用在固定比例的列表中](https://image.zhangxinxu.com/image/blog/202010/6-54-insert-_flex-1-suitable.png)

以及适用于无规律布局中动态内容元素，我们不妨继续使用`flex:none`那里演示的例子进行说明。

```html
<div class="item">
    <img src="1.jpg">
    <p>右侧按钮没有设置flex:none，表现为最小内容宽度。</p>
    <button>按钮</button>
</div>
```

```css
.container {
    display: flex;
    padding: .5rem;
    border: 1px solid lightgray;
    background-color: #fff;
}
img {
    width: 3rem; height: 3rem;
    margin-right: .5rem;
}
button {
    align-self: center;
    padding: 5px;
    margin-left: .5rem;
}
```

除了设置`<button>`元素`flex:none`以外，在这个例子中，我们还可以设置`<p>`元素`flex:1`实现类似的效果。

结果就有如下图所示，`<p>`元素设置了`flex:1`之后，按钮元素正常显示了。

![主体动态的文本元素设置flex:1之后的效果对比示意](https://image.zhangxinxu.com/image/blog/202010/6-56-insert-_flex-1-suitable2.png)

##### 适合使用flex:auto的场景

当希望元素充分利用剩余空间，但是各自的尺寸按照各自内容进行分配的时候，适合使用`flex:auto`。

`flex:auto`多用于内容固定，或者内容可控的布局场景，例如导航数量不固定，每个导航文字数量也不固定的导航效果就适合使用`flex:auto`效果来实现，我做了个很简单的示意，代码如下所示：

```html
<nav class="flex">
  <span>首页</span>
  <span>排行榜</span>
  <span>我的订单</span>
  <span>个人中心</span>
</nav>
```

```css
nav span {
    flex: auto;
    line-height: 3rem;
    background: #444;
    color: #fff;
    text-align:center;
}
span + span {
    border-left: 1px solid #eee;
}
```

此时大家就可以看到一个基于内容自动分配宽度的自适应导航效果了，效果如下图所示，文字越多的导航占据的宽度越大，这完全是浏览器自动分配的。

![flex:auto实现的基于内容宽度自动分配的导航效果示意](https://image.zhangxinxu.com/image/blog/202010/6-57-insert-_flex-auto-suitable.png)

最后总结一下：

-   `flex:initial`表示默认的flex状态，无需专门设置，适合小控件元素的分布布局，或者某一项内容动态变化的布局；
-   `flex:0`适用场景较少，适合设置在替换元素的父元素上；
-   `flex:none`适用于不换行的内容固定或者较少的小控件元素上，如按钮。
-   `flex:1`适合等分布局；
-   `flex:auto`适合基于内容动态适配的布局；


参考：
[CSS新世界](https://www.zhangxinxu.com/wordpress/2020/10/css-flex-0-1-none/)