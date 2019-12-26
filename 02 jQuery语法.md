# jQuery 语法

> 通过 jQuery，您可以选取（查询，query） HTML 元素，并对它们执行"操作"（actions）。

jQuery 语法是通过选取 HTML 元素，并对选取的元素执行某些操作。

## INDEX

- [x] [注意](#注意)
- [x] [执行方式](#执行方式)
- [x] [jQuery.fn.init {}](#jQuery.fn.init {})
- [x] [文档就绪事件](#文档就绪事件)

## 注意

语法可以通用，那么一个程序中，能不能即出现jq又出现原生js？

- jq封装的对象身上的方法不能给非jq封装的对象使用

- 非jq封装的对象身上的方法不能给jq封装的对象使用

- 除非进行对象转换

  - js用jq的方法

    ```js
    var obox1 = document.getElementById("box");
    $(obox1).css(...)
    ```

  - jq用js的方法

    `jQuery.fn.init {}`对象返回的数字的０个索引，就是ＤＯＭ节点

    ```js
    var obox2 = $("#box");
    obox2[0].style.display = "none";
    ```

    

## 执行方式

### $()

返回的是`jQuery.fn.init {}`对象

### $(...)

返回的是`jQuery.fn.init {...}`对象

实例

```js
$(div)//选用当前界面所有的div元素
//jQuery.fn.init [div.box, prevObject: jQuery.fn.init(1), context: document, selector: "div"]
//{
//	0: div.box
//	context: document
//	length: 1
//	prevObject: jQuery.fn.init [document, context: document]
//	selector: "div"
//	__proto__: Object(0)
//}

```



### $.ajax()



### $(...).css(...)

1. 基础语法： `$(selector).action()`
2. 美元符号定义 jQuery
3. 选择符（selector）"查询"和"查找" HTML 元素
4. jQuery 的 action() 执行对元素的操作
5. 实例:

```js
$(this).hide() - 隐藏当前元素
$("p").hide() - 隐藏所有 <p> 元素
$("p.test").hide() - 隐藏所有 class="test" 的 <p> 元素
$("#test").hide() - 隐藏所有 id="test" 的元素
```





## jQuery.fn.init {}

> jQuery.fn.init {}是一个伪数组

通过一个实例来证明如下：

```html
<div class="box1"></div>
<div class="box1"></div>
<div class="box2"></div>
```

通过jQuery来选择：

```js
$(".box1");
```

### length

- 返回值

  返回的是当前选择的DOM元素的个数

  ```js
  console.log(${".box"}.length);//2
  ```

### 索引

- 返回值

  返回的是当前选择DOM元素节点

  ```js
  console.log($(".box1"}[0]);//第一个class="box1"的DOM元素
  console.log($(".box1"}[1]);//第二个class="box1"的DOM元素
  console.log($(".box1"}[2]);//undefined,因为只有2个class="box1"的DOM元素
  ```



## 文档就绪事件

> 这是为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作。
>
> 如果在文档没有完全加载之前就运行函数，操作可能失败。下面是两个具体的例子：
>
> - 试图隐藏一个不存在的元素
> - 获得未完全加载的图像的大小
>
> 注意：$(document).ready()与window.onload()的区别咋与，onload()是`页面和资源都加载完成`，ready()是`页面加载完成`，因此他可能无法获得图片的尺寸我可爱的宝贝

```js
$(document).ready(function(){
 
   // 开始写 jQuery 代码...
 
});
```



简洁写法（与以上写法效果相同):

```js
$(function(){
 
   // 开始写 jQuery 代码...
 
});
```

