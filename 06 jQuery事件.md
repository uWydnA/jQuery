# jQuery事件

> jQuery 事件处理方法是 jQuery 中的核心函数。
>
> 事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。术语由事件“触发”（或“激发”）经常会被使用。

## INDEX

- [x] [注意](#注意)
- [x] [事件类型作为方法名](#事件类型作为方法名)
- [x] [bind() / unbind()](#bind() / unbind())
- [x] [on() / off()](#on() / off())
- [x] [one()](#one())
- [x] [hover()](#hover())
- [x] [ready()](#ready())
- [x] [trigger()](#trigger())

## 注意

jq的事件绑定全部都是`DOM2级`，意味着，所有事件都可以重复绑定

隐患:可能会因为一些书写代码的错误,导致重复绑定同一种事件



jQuery的事件绑定方式主要分为以下4种:

## 事件类型作为方法名

> 缺点:无法删除事件

实例

```js
$(".box").click(function(){
    console.log(1);
})
$(".box").click(function(){
    console.log(2);
})
```



## bind() / unbind()

> 缺点:没有封装事件委托

实例

```js
$(".box").bind("click.a",function(){//jQ通过事件类型.名字的方式,起到给callback函数起名字的作用
    console.log(1);
})
$(".box").bind("click.b",function(){
    console.log(2);
})
$(".box").unbind("click.a")//这样就可以删除同一个函数,从而删除这个事件
```



## on() / off()

> 优点:可以删除事件,封装了事件委托的绑定

第一个参数:字符,表示事件类型

第二个参数:字符,表示事件委托中的target,可以不传

第三个参数:事件处理函数

在事件处理函数中,jq帮我们处理了this的指向问题,处理后指向的就是事件源

```js
&(".box").on("click","li",function(){
    console.log(this)//帮我们解决了this,这里的this指向的就是事件源
})
```



## one()

> 一次性绑定事件
>
> 特点:执行1次就自动删除事件

```js
$(".box").one("click",function(){
    console.log(1);
})
```



## hover()

> 封装了鼠标的进入和离开
>
> 1. 会触发事件冒泡
>
>    onmouseover     onmouseout
>
> 2. `不会触发事件冒泡` `hover()封装的是这一组`
>
>    onmouseenter    onmouseleave

实例

```js
$(".box").hover(function(){
    console.log("进入")
},function(){
    console.log("离开")
})
```



## ready()

> 加载事件绑定

实例

```js
$(document).ready(function(){})
```



## trigger()

> trigger() 方法触发被选元素的指定事件类型。

- 触发后会触发事件冒泡

  ```js
  setInterval(() => {
      $(".box").trigger("click");
  }, 1000);
  ```

  

- 触发后不会触发事件冒泡

  ```js
  setInterval(() => {
      $(".box").triggerHandler("click");
  }, 1000);
  ```

  

