# jQuery

> jQuery 是一个 JavaScript 库。

## INDEX

- [x] [版本介绍](#版本介绍)
- [x] [功能](#功能)

## 版本介绍

#### 1.xx.xx

​	常用：1.11完善了所有的功能

​	最终版本：1.12.4



#### 2.xx.xx

​	常用：2.2.4

​	最终版本：2.2.4

​	1-2做的重大修改：删除兼容处理



#### 3.xx.xx

​	重构了内核不太稳定



#### 版本代码的意义

​	第一个数字：重大修改

​	第二个数字：新增或删除或修改了某个功能

​	第三个数字：修复了bug或优化了一些使用



## 功能

- HTML 元素选取
- HTML 元素操作
- CSS 操作
- HTML 事件函数
- JavaScript 特效和动画
- HTML DOM 遍历和修改
- AJAX
- Utilities



## 源码分析

#### 模块入口的暴露方式

JQ的代码是在一个匿名函数下运行的，理应拿不到内部的变量，因此需要做模块入口的暴露方式

1. 通过函数的返回值传参
2. **通过在匿名函数的最后声明全局变量实现**          **(jq的采取的是window的暴露方式**


```js
;(function(){
    function fn(){
        console.log("hello")
    }
    var a = "world"
    // return fn;
    window.fn = fn;
    window.a = a;
})();

fn()//可以拿到fn();
```
