看到一个用JavaScript生成随机字符串的方法：

```javascript
Math.random().toString(36).substring(2);
```

其中的`toString(36)`是什么意思呢？

[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toString)上说，`Number.prototype.toString()`有一个可选的参数`radix`，就是`进制`：

> radix：指定要用于数字到字符串的转换的基数(从2到36)。如果未指定 radix 参数，则默认值为 10。

> 如果转换的基数大于10，则会**使用字母**来表示大于9的数字，比如基数为16的情况，则使用a到f的字母来表示10到15。

也就是说，如果`radix`是`36`，就会把数字表示为由`0-9, a-z`组成的的`36进制`字符串。

不用管36进制是什么，只要知道，由`Math.random`产生的数字会被表示成看起来随机的字符串，类似`hg7znok52x`，就像`10`表示成二进制是`1010`一个道理。