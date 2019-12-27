# jQuery选择器

> 几乎支持大部分的css3选择器
>
>  q的选择器，全部返回的都是数组（伪数组）

## INDEX

- [x] [元素选择器](#元素选择器)
- [x] [属性选择器](#属性选择器)
- [x] [id选择器](#id选择器)
- [x] [群组选择器](#群组选择器)
- [x] [关系选择器](#关系选择器)
- [x] [伪类选择器](#伪类选择器)
- [x] [jQuery选择器表](#jQuery选择器表)

## 元素选择器

jQuery 使用 CSS 选择器来选取 HTML 元素。

$("p") 选取 <p> 元素。

$("p.intro") 选取所有 class="intro" 的 <p> 元素。

$("p#demo") 选取所有 id="demo" 的 <p> 元素。



## 属性选择器

jQuery 使用 XPath 表达式来选择带有给定属性的元素。

$("[href]") 选取所有带有 href 属性的元素。

$("[href='#']") 选取所有带有 href 值等于 "#" 的元素。

$("[href!='#']") 选取所有带有 href 值不等于 "#" 的元素。

$("[href$='.jpg']") 选取所有 href 值以 ".jpg" 结尾的元素。



## id选择器

```js
$(#box)
```

选择id名为box的元素，如果有多个，只选择一个，称为`id选择器的失明特性`



## 群组选择器

```js
$(".box,#cont,span").css("background","red")　　
```

​	选择多个元素，请注意，这里的如果存在多个元素均为同一id，那么会选择多个如#cont的元素。就和document.querySelectorAll一样。



## 关系选择器

### 亲儿子元素 children("li")

#### 选择器

```js
$(".list>li").css("background","red");
```

#### 方法

```js
$(".list").children("li").css("background","red");
```



### 后代元素 find("li")

#### 选择器

```js
$(".list　li")
```

#### 方法

```js
$(".list").find("li")
```



### 父元素 parent()

#### 方法

```js
$(".list").parent();
```



### 父祖先元素 parents()

#### 方法

```js
$(".list").parents();
```



### 父直到哪个祖元素 parentsUntil()

#### 方法

```js
$(".span").parentsUntil(".box1")//不包含.box1元素
```



## 伪类选择器

### 后一个兄弟元素 next()

#### 选择器

```js
$(".list+span")
```

#### 方法

```js
$(".list").next()
```



### 后面所有特定兄弟元素 nextAll("span")

#### 选择器

```js
$(".list~span")
```

#### 方法

```js
$(".list").nextAll("span")
```



### 直到后面所有特定兄弟元素 nextAllUntil("...")

#### 方法

```js
$(".box1").nextAllUntil(".red")
```



### 前一个兄弟元素 prev()

#### 选择器

```js
$(".list+span")
```

#### 方法

```js
$(".list").prev()
```



### 前面所有特定兄弟元素 prevAll("span")

#### 选择器

```js
$(".list~span").prevAll("span")
```

#### 方法

```js
$(".list").nextAll("span")
```



### 直到前面所有特定兄弟元素 prevAllUntil("...")

#### 方法

```js
$(".box1").prevAllUntil(".red")
```



### 除自己外所有兄弟元素 siblings()

#### 选择器

无

#### 方法

```js
$(".list").siblings()
```





### 第一个子元素 first()

#### 选择器

```js
$(".list li:first")
```

#### 方法

```js
$(".list li").first()
```



### 最后的子元素 last()

#### 选择器

```js
$(".list li:last")
```

#### 方法

```js
$(".list li").last()
```



### 第几个子元素  eq(n)

#### 选择器

```js
$(".list li:eq(3)")
```

#### 方法

```js
$(".list li").eq(3)
```



### 子元素内容为空 :empty

#### 选择器

```js
$(".list　li:empty")
```

#### 方法

无



### 奇数子元素 :odd

#### 选择器

```js
$(".list li:odd")
```

#### 方法

无



### 偶数子元素  :even

#### 选择器

```js
$(".list li:even")
```

#### 方法

无



### 除了该元素 not(.red)

#### 选择器

```js
$(".list li:not(.red)")//选中.list中的除了class为red的li
```

#### 方法

```js
$(".list li").not(".red")
```



### :contains() 选择器

> :contains() 选择器选取包含指定字符串的元素。
>
> 该字符串可以是直接包含在元素中的文本，或者被包含于子元素中。

#### 选择器

```js
$(".list li:contains(s)")//选中.list中的所有innerHTML里包含s字符的li
```

#### 方法

```js
$(".list li").contains("s")//选中.list中的所有innerHTML里包含s字符的li
```



### has选择器

> $(":has(*selector*)")选择器选取所有包含一个或多个元素在其内的元素，匹配指定的选择器
>
> *selector*：必需。规定要选取的元素。 `该参数接受任何类型的选择器`。

#### 选择器

```js
$(".list:has(.red)") //选择所有子元素中有.red元素的.list
```

#### 方法

```js
$(".list").has("red")
```



### hidden选择器

#### 选择器

```js
 $(".list:hidden") //选择所有display:none的.list
```

#### 方法

无



### visible选择器

#### 选择器

```js
 $(".list:visible") //选择所有可见的.list
```

#### 方法

```js
无
```



## jQuery选择器表

| 选择器                                                       | 实例                       | 选取                                       |
| ------------------------------------------------------------ | -------------------------- | ------------------------------------------ |
| [*](https://www.w3school.com.cn/jquery/selector_all.asp)     | $("*")                     | 所有元素                                   |
| [#*id*](https://www.w3school.com.cn/jquery/selector_id.asp)  | $("#lastname")             | id="lastname" 的元素                       |
| [.*class*](https://www.w3school.com.cn/jquery/selector_class.asp) | $(".intro")                | 所有 class="intro" 的元素                  |
| [*element*](https://www.w3school.com.cn/jquery/selector_element.asp) | $("p")                     | 所有 <p> 元素                              |
| .*class*.*class*                                             | $(".intro.demo")           | 所有 class="intro" 且 class="demo" 的元素  |
|                                                              |                            |                                            |
| [:first](https://www.w3school.com.cn/jquery/selector_first.asp) | $("p:first")               | 第一个 <p> 元素                            |
| [:last](https://www.w3school.com.cn/jquery/selector_last.asp) | $("p:last")                | 最后一个 <p> 元素                          |
| [:even](https://www.w3school.com.cn/jquery/selector_even.asp) | $("tr:even")               | 所有偶数 <tr> 元素                         |
| [:odd](https://www.w3school.com.cn/jquery/selector_odd.asp)  | $("tr:odd")                | 所有奇数 <tr> 元素                         |
|                                                              |                            |                                            |
| [:eq(*index*)](https://www.w3school.com.cn/jquery/selector_eq.asp) | $("ul li:eq(3)")           | 列表中的第四个元素（index 从 0 开始）      |
| [:gt(*no*)](https://www.w3school.com.cn/jquery/selector_gt.asp) | $("ul li:gt(3)")           | 列出 index 大于 3 的元素                   |
| [:lt(*no*)](https://www.w3school.com.cn/jquery/selector_lt.asp) | $("ul li:lt(3)")           | 列出 index 小于 3 的元素                   |
| :not(*selector*)                                             | $("input:not(:empty)")     | 所有不为空的 input 元素                    |
|                                                              |                            |                                            |
| [:header](https://www.w3school.com.cn/jquery/selector_header.asp) | $(":header")               | 所有标题元素 <h1> - <h6>                   |
| [:animated](https://www.w3school.com.cn/jquery/selector_animated.asp) |                            | 所有动画元素                               |
|                                                              |                            |                                            |
| [:contains(*text*)](https://www.w3school.com.cn/jquery/selector_contains.asp) | $(":contains('W3School')") | 包含指定字符串的所有元素                   |
| [:empty](https://www.w3school.com.cn/jquery/selector_empty.asp) | $(":empty")                | 无子（元素）节点的所有元素                 |
| :hidden                                                      | $("p:hidden")              | 所有隐藏的 <p> 元素                        |
| [:visible](https://www.w3school.com.cn/jquery/selector_visible.asp) | $("table:visible")         | 所有可见的表格                             |
|                                                              |                            |                                            |
| s1,s2,s3                                                     | $("th,td,.intro")          | 所有带有匹配选择的元素                     |
|                                                              |                            |                                            |
| [[*attribute*\]](https://www.w3school.com.cn/jquery/selector_attribute.asp) | $("[href]")                | 所有带有 href 属性的元素                   |
| [[*attribute*=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_equal_value.asp) | $("[href='#']")            | 所有 href 属性的值等于 "#" 的元素          |
| [[*attribute*!=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_notequal_value.asp) | $("[href!='#']")           | 所有 href 属性的值不等于 "#" 的元素        |
| [[*attribute*$=*value*\]](https://www.w3school.com.cn/jquery/selector_attribute_end_value.asp) | $("[href$='.jpg']")        | 所有 href 属性的值包含以 ".jpg" 结尾的元素 |
|                                                              |                            |                                            |
| [:input](https://www.w3school.com.cn/jquery/selector_input.asp) | $(":input")                | 所有 <input> 元素                          |
| [:text](https://www.w3school.com.cn/jquery/selector_input_text.asp) | $(":text")                 | 所有 type="text" 的 <input> 元素           |
| [:password](https://www.w3school.com.cn/jquery/selector_input_password.asp) | $(":password")             | 所有 type="password" 的 <input> 元素       |
| [:radio](https://www.w3school.com.cn/jquery/selector_input_radio.asp) | $(":radio")                | 所有 type="radio" 的 <input> 元素          |
| [:checkbox](https://www.w3school.com.cn/jquery/selector_input_checkbox.asp) | $(":checkbox")             | 所有 type="checkbox" 的 <input> 元素       |
| [:submit](https://www.w3school.com.cn/jquery/selector_input_submit.asp) | $(":submit")               | 所有 type="submit" 的 <input> 元素         |
| [:reset](https://www.w3school.com.cn/jquery/selector_input_reset.asp) | $(":reset")                | 所有 type="reset" 的 <input> 元素          |
| [:button](https://www.w3school.com.cn/jquery/selector_input_button.asp) | $(":button")               | 所有 type="button" 的 <input> 元素         |
| [:image](https://www.w3school.com.cn/jquery/selector_input_image.asp) | $(":image")                | 所有 type="image" 的 <input> 元素          |
| [:file](https://www.w3school.com.cn/jquery/selector_input_file.asp) | $(":file")                 | 所有 type="file" 的 <input> 元素           |
|                                                              |                            |                                            |
| [:enabled](https://www.w3school.com.cn/jquery/selector_input_enabled.asp) | $(":enabled")              | 所有激活的 input 元素                      |
| [:disabled](https://www.w3school.com.cn/jquery/selector_input_disabled.asp) | $(":disabled")             | 所有禁用的 input 元素                      |
| [:selected](https://www.w3school.com.cn/jquery/selector_input_selected.asp) | $(":selected")             | 所有被选取的 input 元素                    |
| [:checked](https://www.w3school.com.cn/jquery/selector_input_checked.asp) | $(":checked")              | 所有被选中的 input 元素                    |





