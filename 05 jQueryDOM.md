# jQueryDOM

> jQuery 中非常重要的部分，就是操作 DOM 的能力。
>
> jQuery 提供一系列与 DOM 相关的方法，这使访问和操作元素和属性变得很容易。
>
> 提示：DOM = Document Object Model（文档对象模型）
>
> DOM 定义访问 HTML 和 XML 文档的标准：
>
> “W3C 文档对象模型独立于平台和语言的界面，允许程序和脚本动态访问和更新文档的内容、结构以及样式。”

## INDEX

- [x] [设置](#设置)
- [x] [添加](#添加)
- [x] [删除](#删除)
- [x] [CSS类](#CSS类)
- [x] [CSS()](#CSS())
- [x] [尺寸](#尺寸)



## 设置

```html
<div class="box">123456</div>
```

### 设置内容 

#### html()

> 设置或返回所选元素的内容（包括 HTML 标记）
>
> 可以解析HTML标签
>
> 等同于JS中的innerHTML

获得

```js
$(".box").html()//123456
```

设置

```js
$(".box").html("123").html()//123 这里采用了连缀,设置后再获得
```



#### text()

> 设置或返回所选元素的文本内容
>
> 不能解析HTML标签
>
> 等同于JS中的innerText

获得

```js
$(".box").text()//123456
```

设置

```js
$(".box").text("123").text()//123 这里采用了连缀,设置后再获得
```



#### val()

> 设置或返回表单字段的值
>
> 等同于JS中的value

获得

```js
<input type="text" name="" id="txt" value="hhhhhh">
$("#txt").val()//hhhhhh
```

设置

```js
<input type="text" name="" id="txt" value="hhhhhh">
$("#txt").val("qqqqq").val()//123 这里采用了连缀,设置后再获得
```



### 设置属性

#### attr()

> 设置/改变属性值
>
> 设置时,支持对象作为参数

获得

```js
$(".box").attr("class");
$(".box").attr("class");
```



设置

```js
$(".box").attr("class","abc");
$(".box").attr({
    a:100,
    b:200,
    c:"hello jq"
});//支持对象作为参数
```



#### removeAttr()

> 删除属性

```js
$(".box1").removeAttr(".box1")
```



## 添加

### 创建节点

```js
 $("<div>")
```



### append()

> 在被选元素的结尾插入内容

实例

```js
$("p").append($("<div>"));
```

### appendTo()

> 将创造的内容插入指定的节点中

实例

```js
$("<div>").appendTo($(".box"))//把新创建的div插入.box节点中
```



### prepend() 

>在被选元素的开头插入内容

实例

```js
$("p").prepend($("<div>"));
```

实例

```js
function appendText()
{
var txt1="<p>Text.</p>";               // 以 HTML 创建新元素
var txt2=$("<p></p>").text("Text.");   // 以 jQuery 创建新元素
var txt3=document.createElement("p");  // 以 DOM 创建新元素
txt3.innerHTML="Text.";
$("p").append(txt1,txt2,txt3);         // 追加新元素
}
```



### after()

>在被选元素之后插入内容

实例

```js
$("img").after($("<div>");

$("img").before($("<div>"));
```

### before()

>在被选元素之前插入内容

实例

```js
$("img").after($("<div>");

$("img").before($("<div>");
```



## 删除

### remove()

>`删除被选元素`（及其子元素）

实例

```js
$("#div1").remove();
```



### empty()

>从被选元素中`删除子元素`

实例

```js
$("#div1").empty();
```



## 复制

### clone()

实例

```js
$("input").clone(true)//克隆这个标签名为inpu的jq对象,clone中的参数为true时,会克隆这个input的事件
```





## CSS类

### 实例样式表

下面的样式表将用于本页的所有例子：

```css
.important
{
font-weight:bold;
font-size:xx-large;
}

.blue
{
color:blue;
}
```

### hasClass()

> 返回布尔值

### addClass()

>向被选元素添加一个或多个类

```js
$("h1,h2,p").addClass("blue");
$("div").addClass("important");
$("div").addClass("important blue");//可以在 addClass() 方法中规定多个类
```



### removeClass()

>从被选元素删除一个或多个类

```js
$("h1,h2,p").removeClass("blue");
$("div").removeClass("important");
```



### toggleClass()

>对被选元素进行`添加/删除类`的`切换操作`

```js
$("button").click(function(){
  $("h1,h2,p").toggleClass("blue");
});
```



## css()

> css() 方法设置或返回被选元素的一个或多个样式属性。

### 返回 CSS 属性

如需返回指定的 CSS 属性的值，请使用如下语法：

```js
css("propertyname");
```

下面的例子将返回首个匹配元素的 background-color 值：

实例

```js
$("p").css("background-color");
```



### 设置 CSS 属性

如需设置指定的 CSS 属性，请使用如下语法：

```js
css("propertyname","value");
```

下面的例子将为所有匹配元素设置 background-color 值：

实例

```js
$("p").css("background-color","yellow");
```



### 设置多个 CSS 属性

如需设置多个 CSS 属性，请使用如下语法：

```js
css({"propertyname":"value","propertyname":"value",...});
```

下面的例子将为所有匹配元素设置 background-color 和 font-size：

实例

```js
$("p").css({
    "background-color":"yellow",
    "font-size":"200%"
});
```



## 尺寸

### width()

> 设置或返回元素的宽度（不包括内边距、边框或外边距）

```js
$(".box").width();//获得宽度
$(".box").width(300);//设置宽度
```



### height()

> 设置或返回元素的高度（不包括内边距、边框或外边距）

```js
$(".box").height();//获得宽度
$(".box").height(300);//设置宽度
```



### innerWidth()

> 设置或返回元素的宽度（包括内边距）

```js
$(".box").innerWidth();//获得offsetWidth
$(".box").innerWidth(300);//值减去padding后设置给宽度
```



### innerHeight()

> 设置或返回元素的高度（包括内边距）

```js
$(".box").innerHeight();//获得offsetHeight
$(".box").innerHeight(300);//值减去padding后设置给高度
```



### outerWidth()

> 设置或返回元素的宽度（包括内边距,包括边框）

```js
$(".box").outerWidth();//获得clientWidth
$(".box").outerWidth(300);//值减去padding和border后设置给宽度
```



### outerHeight()

> 设置或返回元素的高度（包括内边距,包括边框）

```js
$(".box").outerHeight();//获得clientHeight
$(".box").outerHeight(300);//值减去padding和border后设置给高度
```



### offset()

> 设置或返回元素距离页面的left和top,返回一个对象(包含position+margin)

```js
console.log($(".box1").offset());       //position+margin
$(".box1").offset({left:100,top:100}) //值减去margin后设置给left和top
```



### position()

> 返回元素距离页面的left和top,返回一个对象(不margin)

```js
$(".box1").position().left;
$(".box1").position().top	;
```



### scrollTop()

> 设置或返回滚动条的高度

```js
$(".box1").scrollTop();
$(".box1").scrollTop(300);
```

