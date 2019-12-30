# jQueryAjax

## INDEX

- [x] [$().get() / $()post()](#$().get() / $()post())
- [x] [$().load](#$().load)
- [x] [$().ajax()](#$().ajax())
- [x] [ajax的全局事件](#ajax的全局事件)
- [x] [one()](#one())
- [x] [hover()](#hover())
- [x] [ready()](#ready())
- [x] [trigger()](#trigger())



## $().get() / $()post()

> $.get() 方法通过 HTTP GET 请求从服务器上请求数据。
>
> $.post() 方法通过 HTTP POST 请求从服务器上请求数据。
>
> 二者用法都是一样的

### 语法

```js
$.get(URL,callback);
```

必需的 *URL* 参数规定您希望请求的 URL。

可选的 *callback* 参数是请求成功后所执行的函数名。

下面的例子使用 $.get() 方法从服务器上的一个文件中取回数据：

### 实例

```js
$(document).on("click", function () {
    $.get(url, {
        user: "retr0",
        pass: "Qh5#"
    }).then(function (res) {
        console.log(res)
    })
})
```

### 返回值

$.get() 的返回值是一个`类promise对象`,身上有例如:

- then()
- success()
- error()
- ...

并且还包含了XHR对象身上的一些属性和方法,例如:

- getResponseHeader()
- readyState
- state
- status
- ...





## $().load

> load() 方法通过 AJAX 请求从服务器加载数据，并把返回的数据放置到指定的元素中。

### 语法

```js
load(url,data,function(response,status,xhr))
```

| 参数                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| *url*                           | 规定要将请求发送到哪个 URL。                                 |
| *data*                          | 可选。规定连同请求发送到服务器的数据。                       |
| *function(response,status,xhr)* | 可选。规定当请求完成时运行的函数。额外的参数：*response* - 包含来自请求的结果数据*status* - 包含请求的状态（"success", "notmodified", "error", "timeout" 或 "parsererror"）*xhr* - 包含 XMLHttpRequest 对象 |

### 详细说明

该方法是最简单的从服务器获取数据的方法。它几乎与 $.get(url, data, success) 等价，不同的是它不是全局函数，并且它拥有隐式的回调函数。当侦测到成功的响应时（比如，当 textStatus 为 "success" 或 "notmodified" 时），.load() 将匹配元素的 HTML 内容设置为返回的数据。这意味着该方法的大多数使用会非常简单：

```js
$("#result").load("ajax/test.html");
```

如果提供回调函数，则会在执行 post-processing 之后执行该函数：

```js
$("#result").load("ajax/test.html", function() {
  alert("Load was performed.");
});
```

上面的两个例子中，如果当前文档不包含 "result" ID，则不会执行 .load() 方法。

如果提供的数据是对象，则使用 POST 方法；否则使用 GET 方法。

### 加载页面片段

.load() 方法，与 $.get() 不同，允许我们规定要插入的远程文档的某个部分。这一点是通过 url 参数的特殊语法实现的。如果该字符串中包含一个或多个空格，紧接第一个空格的字符串则是决定所加载内容的 jQuery 选择器。

我们可以修改上面的例子，这样就可以使用所获得文档的某部分：

```js
$("#result").load("ajax/test.html #container");
```

如果执行该方法，则会取回 ajax/test.html 的内容，不过然后，jQuery 会解析被返回的文档，来查找带有容器 ID 的元素。该元素，连同其内容，会被插入带有结果 ID 的元素中，所取回文档的其余部分会被丢弃。

jQuery 使用浏览器的 .innerHTML 属性来解析被取回的文档，并把它插入当前文档。在此过程中，浏览器常会从文档中过滤掉元素，比如 <html>, <title> 或 <head> 元素。结果是，由 .load() 取回的元素可能与由浏览器直接取回的文档不完全相同。

注释：由于浏览器安全方面的限制，大多数 "Ajax" 请求遵守同源策略；请求无法从不同的域、子域或协议成功地取回数据。

实例

- HTML

  ```html
  <div class="top">
      <h1>子页</h1>
  </div>
  <div class="box"></div>
  <div class="footer"></div>
  ```

- JS

  用法是在load()方法中传入绝对坐标的URL地址字符，地址后`空格加CSS选择器字符`可以实现选择具体的元素插入

  ```js
  $(".box").load("http://localhost/1912-server/jq-ajax/data/page.html .nav");
  $(".footer").load("http://localhost/1912-server/jq-ajax/data/page.html p");
  ```

- 外部HTML

  ```html
  <div class="nav">导航</div>
  <p>页脚</p>
  ```

  



## $().ajax()

### 实例

通过 AJAX 加载一段文本：

jQuery 代码：

```JS
$(document).ready(function(){
  $("#b01").click(function(){
  htmlobj=$.ajax({url:"/jquery/test1.txt",async:false});
  $("#myDiv").html(htmlobj.responseText);
  });
});
```

HTML 代码：

```HTML
<div id="myDiv"><h2>Let AJAX change this text</h2></div>
<button id="b01" type="button">Change Content</button>
```



#### 最简AJAX

```JS
//最简化的ajax
var xhr = $.ajax({
    url:"http://localhost/1912-server/jq-ajax/data/data.php",
    success:function(res,b,c){
        console.log(res)
        console.log(b)
        console.log(c)
    }
})
console.log(xhr)
```



#### JSONP请求

```js
$.ajax({
    url:"https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su",
    dateType:"jsonp",//定义传输方式是jsonp，但这不代表JSONP跟AJAX有什么关系，JSONP和AJAX无关
    jsonp:"cb",
    data:{
        wb : "html",
    }
    success:function(res){
    	console.log(res);
	}
})
```



#### 超时报错

```js
$.ajax({
    url:"https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su",
    dataType:"jsonp",
    jsonp:"cb",
    data:{
        wb:"html"
    },
    success:function(res,status,xhr){
		console.log(res); 
    	console.log(status);
    	console.log(xhr);
	},
    error:function(xhr,status,res){
    	console.log(xhr);
    	console.log(status);
    	console.log(res);
	}
	timeOut:100,//数值单位为毫秒，超时会执行error函数,status和res会输出timeOut字符串
})
```



#### loading效果

```js
$(document).click(function () {
    var xhr = $.ajax({
        url: "http://127.0.0.1/myown/jq-ajax/data/loading.php",
        success: function (res) {
            console.log(res)
            $("img").hide();
        },
        beforeSend: function () {
            if (!$("img")[0]) {
                $("body").append($("<img src = '1.jpg' class = 'loading'>"))
            } else {
                $("img").show();
            }
        }
    })
})
```





### 定义和用法

ajax() 方法通过 HTTP 请求加载远程数据。

该方法是 jQuery 底层 AJAX 实现。简单易用的高层实现见 $.get, $.post 等。$.ajax() 返回其创建的 XMLHttpRequest 对象。大多数情况下你无需直接操作该函数，除非你需要操作不常用的选项，以获得更多的灵活性。

最简单的情况下，$.ajax() 可以不带任何参数直接使用。

注意：所有的选项都可以通过 $.ajaxSetup() 函数来全局设置。

#### 语法

```js
jQuery.ajax([settings])
```

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| *settings* | 可选。用于配置 Ajax 请求的键值对集合。可以通过 $.ajaxSetup() 设置任何选项的默认值。 |

#### 参数

- options

  类型：Object可选。AJAX 请求设置。所有选项都是可选的。

- async

  类型：Boolean默认值: true。默认设置下，所有请求均为异步请求。如果需要发送同步请求，请将此选项设置为 false。注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行。

- beforeSend(XHR)

  类型：Function发送请求前可修改 XMLHttpRequest 对象的函数，如添加自定义 HTTP 头。XMLHttpRequest 对象是唯一的参数。这是一个 Ajax 事件。如果返回 false 可以取消本次 ajax 请求。

- cache

  类型：Boolean默认值: true，dataType 为 script 和 jsonp 时默认为 false。设置为 false 将不缓存此页面。jQuery 1.2 新功能。

- complete(XHR, TS)

  类型：Function请求完成后回调函数 (请求成功或失败之后均调用)。参数： XMLHttpRequest 对象和一个描述请求类型的字符串。这是一个 Ajax 事件。

- contentType

  类型：String默认值: "application/x-www-form-urlencoded"。发送信息至服务器时内容编码类型。默认值适合大多数情况。如果你明确地传递了一个 content-type 给 $.ajax() 那么它必定会发送给服务器（即使没有数据要发送）。

- context

  类型：Object这个对象用于设置 Ajax 相关回调函数的上下文。也就是说，让回调函数内 this 指向这个对象（如果不设定这个参数，那么 this 就指向调用本次 AJAX 请求时传递的 options 参数）。比如指定一个 DOM 元素作为 context 参数，这样就设置了 success 回调函数的上下文为这个 DOM 元素。就像这样：`$.ajax({ url: "test.html", context: document.body, success: function(){         $(this).addClass("done");       }}); `

- `data`

  类型：String发送到服务器的数据。将自动转换为请求字符串格式。GET 请求中将附加在 URL 后。查看 processData 选项说明以禁止此自动转换。必须为 Key/Value 格式。如果为数组，jQuery 将自动为不同值对应同一个名称。如 {foo:["bar1", "bar2"]} 转换为 '&foo=bar1&foo=bar2'。

- dataFilter

  类型：Function给 Ajax 返回的原始数据的进行预处理的函数。提供 data 和 type 两个参数：data 是 Ajax 返回的原始数据，type 是调用 jQuery.ajax 时提供的 dataType 参数。函数返回的值将由 jQuery 进一步处理。

- dataType

  类型：String预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断，比如 XML MIME 类型就被识别为 XML。在 1.4 中，JSON 就会生成一个 JavaScript 对象，而 script 则会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数。可用值:"xml": 返回 XML 文档，可用 jQuery 处理。"html": 返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。"script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 "cache" 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）"json": 返回 JSON 数据 。"jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。"text": 返回纯文本字符串

- `error`

  类型：Function默认值: 自动判断 (xml 或 html)。请求失败时调用此函数。有以下三个参数：XMLHttpRequest 对象、错误信息、（可选）捕获的异常对象。如果发生了错误，错误信息（第二个参数）除了得到 null 之外，还可能是 "timeout", "error", "notmodified" 和 "parsererror"。这是一个 Ajax 事件。

- `global`

  类型：Boolean是否触发全局 AJAX 事件。默认值: true。设置为 false 将不会触发全局 AJAX 事件，如 ajaxStart 或 ajaxStop 可用于控制不同的 Ajax 事件。

- ifModified

  类型：Boolean仅在服务器数据改变时获取新数据。默认值: false。使用 HTTP 包 Last-Modified 头信息判断。在 jQuery 1.4 中，它也会检查服务器指定的 'etag' 来确定数据没有被修改过。

- `jsonp`

  类型：String在一个 jsonp 请求中重写回调函数的名字。这个值用来替代在 "callback=?" 这种 GET 或 POST 请求中 URL 参数里的 "callback" 部分，比如 {jsonp:'onJsonPLoad'} 会导致将 "onJsonPLoad=?" 传给服务器。

- `jsonpCallback`

  类型：String为 jsonp 请求指定一个回调函数名。这个值将用来取代 jQuery 自动生成的随机函数名。这主要用来让 jQuery 生成度独特的函数名，这样管理请求更容易，也能方便地提供回调函数和错误处理。你也可以在想让浏览器缓存 GET 请求的时候，指定这个回调函数名。

- password

  类型：String用于响应 HTTP 访问认证请求的密码

- processData

  类型：Boolean默认值: true。默认情况下，通过data选项传递进来的数据，如果是一个对象(技术上讲只要不是字符串)，都会处理转化成一个查询字符串，以配合默认内容类型 "application/x-www-form-urlencoded"。如果要发送 DOM 树信息或其它不希望转换的信息，请设置为 false。

- scriptCharset

  类型：String只有当请求时 dataType 为 "jsonp" 或 "script"，并且 type 是 "GET" 才会用于强制修改 charset。通常只在本地和远程的内容编码不同时使用。

- `success`

  类型：Function请求成功后的回调函数。参数：由服务器返回，并根据 dataType 参数进行处理后的数据；描述状态的字符串。这是一个 Ajax 事件。

- traditional

  类型：Boolean如果你想要用传统的方式来序列化数据，那么就设置为 true。请参考工具分类下面的 jQuery.param 方法。

- `timeout`

  类型：Number设置请求超时时间（毫秒）。此设置将覆盖全局设置。

- `ype`

  类型：String默认值: "GET")。请求方式 ("POST" 或 "GET")， 默认为 "GET"。注意：其它 HTTP 请求方法，如 PUT 和 DELETE 也可以使用，但仅部分浏览器支持。

- `url`

  类型：String默认值: 当前页地址。发送请求的地址。

- username

  类型：String用于响应 HTTP 访问认证请求的用户名。

- xhr

  类型：Function需要返回一个 XMLHttpRequest 对象。默认在 IE 下是 ActiveXObject 而其他情况下是 XMLHttpRequest 。用于重写或者提供一个增强的 XMLHttpRequest 对象。这个参数在 jQuery 1.3 以前不可用。

### 回调函数

> 如果要处理 $.ajax() 得到的数据，则需要使用回调函数：beforeSend、error、dataFilter、success、complete。

#### beforeSend

在发送请求之前调用，并且传入一个 XMLHttpRequest 作为参数。

#### error

在请求出错时调用。传入 XMLHttpRequest 对象，描述错误类型的字符串以及一个异常对象（如果有的话）

#### dataFilter

在请求成功之后调用。传入返回的数据以及 "dataType" 参数的值。并且必须返回新的数据（可能是处理过的）传递给 success 回调函数。

#### success

当请求之后调用。传入返回后的数据，以及包含成功代码的字符串。

#### complete

当请求完成之后调用这个函数，无论成功或失败。传入 XMLHttpRequest 对象，以及一个包含成功或错误代码的字符串。

### 数据类型

$.ajax() 函数依赖服务器提供的信息来处理返回的数据。如果服务器报告说返回的数据是 XML，那么返回的结果就可以用普通的 XML 方法或者 jQuery 的选择器来遍历。如果见得到其他类型，比如 HTML，则数据就以文本形式来对待。

通过 dataType 选项还可以指定其他不同数据处理方式。除了单纯的 XML，还可以指定 html、json、jsonp、script 或者 text。

其中，text 和 xml 类型返回的数据不会经过处理。数据仅仅简单的将 XMLHttpRequest 的 responseText 或 responseHTML 属性传递给 success 回调函数。

注意：我们必须确保网页服务器报告的 MIME 类型与我们选择的 dataType 所匹配。比如说，XML的话，服务器端就必须声明 text/xml 或者 application/xml 来获得一致的结果。

如果指定为 html 类型，任何内嵌的 JavaScript 都会在 HTML 作为一个字符串返回之前执行。类似地，指定 script 类型的话，也会先执行服务器端生成 JavaScript，然后再把脚本作为一个文本数据返回。

如果指定为 json 类型，则会把获取到的数据作为一个 JavaScript 对象来解析，并且把构建好的对象作为结果返回。为了实现这个目的，它首先尝试使用 JSON.parse()。如果浏览器不支持，则使用一个函数来构建。

JSON 数据是一种能很方便通过 JavaScript 解析的结构化数据。如果获取的数据文件存放在远程服务器上（域名不同，也就是跨域获取数据），则需要使用 jsonp 类型。使用这种类型的话，会创建一个查询字符串参数 callback=? ，这个参数会加在请求的 URL 后面。服务器端应当在 JSON 数据前加上回调函数名，以便完成一个有效的 JSONP 请求。如果要指定回调函数的参数名来取代默认的 callback，可以通过设置 $.ajax() 的 jsonp 参数。

注意：JSONP 是 JSON 格式的扩展。它要求一些服务器端的代码来检测并处理查询字符串参数。

如果指定了 script 或者 jsonp 类型，那么当从服务器接收到数据时，实际上是用了 <script> 标签而不是 XMLHttpRequest 对象。这种情况下，$.ajax() 不再返回一个 XMLHttpRequest 对象，并且也不会传递事件处理函数，比如 beforeSend。

### 发送数据到服务器

默认情况下，Ajax 请求使用 GET 方法。如果要使用 POST 方法，可以设定 type 参数值。这个选项也会影响 data 选项中的内容如何发送到服务器。

data 选项既可以包含一个查询字符串，比如 key1=value1&key2=value2 ，也可以是一个映射，比如 {key1: 'value1', key2: 'value2'} 。如果使用了后者的形式，则数据再发送器会被转换成查询字符串。这个处理过程也可以通过设置 processData 选项为 false 来回避。如果我们希望发送一个 XML 对象给服务器时，这种处理可能并不合适。并且在这种情况下，我们也应当改变 contentType 选项的值，用其他合适的 MIME 类型来取代默认的 application/x-www-form-urlencoded 。

### 高级选项

global 选项用于阻止响应注册的回调函数，比如 .ajaxSend，或者 ajaxError，以及类似的方法。这在有些时候很有用，比如发送的请求非常频繁且简短的时候，就可以在 ajaxSend 里禁用这个。

如果服务器需要 HTTP 认证，可以使用用户名和密码可以通过 username 和 password 选项来设置。

Ajax 请求是限时的，所以错误警告被捕获并处理后，可以用来提升用户体验。请求超时这个参数通常就保留其默认值，要不就通过 jQuery.ajaxSetup 来全局设定，很少为特定的请求重新设置 timeout 选项。

默认情况下，请求总会被发出去，但浏览器有可能从它的缓存中调取数据。要禁止使用缓存的结果，可以设置 cache 参数为 false。如果希望判断数据自从上次请求后没有更改过就报告出错的话，可以设置 ifModified 为 true。

scriptCharset 允许给 <script> 标签的请求设定一个特定的字符集，用于 script 或者 jsonp 类似的数据。当脚本和页面字符集不同时，这特别好用。

Ajax 的第一个字母是 asynchronous 的开头字母，这意味着所有的操作都是并行的，完成的顺序没有前后关系。$.ajax() 的 async 参数总是设置成true，这标志着在请求开始后，其他代码依然能够执行。强烈不建议把这个选项设置成 false，这意味着所有的请求都不再是异步的了，这也会导致浏览器被锁死。

$.ajax 函数返回它创建的 XMLHttpRequest 对象。通常 jQuery 只在内部处理并创建这个对象，但用户也可以通过 xhr 选项来传递一个自己创建的 xhr 对象。返回的对象通常已经被丢弃了，但依然提供一个底层接口来观察和操控请求。比如说，调用对象上的 .abort() 可以在请求完成前挂起请求。



## ajax的全局事件

### ajaxStart()

#### 定义和用法

ajaxStart() 方法在 AJAX 请求发送前执行函数。它是一个 Ajax 事件。

#### 详细说明

无论在何时发送 Ajax 请求，jQuery 都会检查是否存在其他 Ajax 请求。如果不存在，则 jQuery 会触发该 ajaxStart 事件。在此时，由 .ajaxStart() 方法注册的任何函数都会被执行。

#### 语法

```js
.ajaxStart(function())
```

| 参数         | 描述                               |
| ------------ | ---------------------------------- |
| *function()* | 规定当 AJAX 请求开始时运行的函数。 |

#### 示例

AJAX 请求开始时显示信息：

```js
$("#loading").ajaxStart(function(){
  $(this).show();
});
```



### ajaxStop()

#### 定义和用法

ajaxStop() 方法在 AJAX 请求结束时执行函数。它是一个 Ajax 事件。

#### 详细说明

无论 Ajax 请求在何时完成 ，jQuery 都会检查是否存在其他 Ajax 请求。如果不存在，则 jQuery 会触发该 ajaxStop 事件。在此时，由 .ajaxStop() 方法注册的任何函数都会被执行。

#### 语法

```js
.ajaxStop(function())
```

| 参数         | 描述                               |
| ------------ | ---------------------------------- |
| *function()* | 规定当 AJAX 请求完成时运行的函数。 |

#### 示例

AJAX 请求结束后隐藏信息：

```js
$("#loading").ajaxStop(function(){
  $(this).hide();
});
```



## jQuery Ajax 操作函数

jQuery 库拥有完整的 Ajax 兼容套件。其中的函数和方法允许我们在不刷新浏览器的情况下从服务器加载数据。

| 函数                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [jQuery.ajax()](https://www.w3school.com.cn/jquery/ajax_ajax.asp) | 执行异步 HTTP (Ajax) 请求。                                  |
| [.ajaxComplete()](https://www.w3school.com.cn/jquery/ajax_ajaxcomplete.asp) | 当 Ajax 请求完成时注册要调用的处理程序。这是一个 Ajax 事件。 |
| [.ajaxError()](https://www.w3school.com.cn/jquery/ajax_ajaxerror.asp) | 当 Ajax 请求完成且出现错误时注册要调用的处理程序。这是一个 Ajax 事件。 |
| [.ajaxSend()](https://www.w3school.com.cn/jquery/ajax_ajaxsend.asp) | 在 Ajax 请求发送之前显示一条消息。                           |
| [jQuery.ajaxSetup()](https://www.w3school.com.cn/jquery/ajax_ajaxsetup.asp) | 设置将来的 Ajax 请求的默认值。                               |
| [.ajaxStart()](https://www.w3school.com.cn/jquery/ajax_ajaxstart.asp) | 当首个 Ajax 请求完成开始时注册要调用的处理程序。这是一个 Ajax 事件。 |
| [.ajaxStop()](https://www.w3school.com.cn/jquery/ajax_ajaxstop.asp) | 当所有 Ajax 请求完成时注册要调用的处理程序。这是一个 Ajax 事件。 |
| [.ajaxSuccess()](https://www.w3school.com.cn/jquery/ajax_ajaxsuccess.asp) | 当 Ajax 请求成功完成时显示一条消息。                         |
| [jQuery.get()](https://www.w3school.com.cn/jquery/ajax_get.asp) | 使用 HTTP GET 请求从服务器加载数据。                         |
| [jQuery.getJSON()](https://www.w3school.com.cn/jquery/ajax_getjson.asp) | 使用 HTTP GET 请求从服务器加载 JSON 编码数据。               |
| [jQuery.getScript()](https://www.w3school.com.cn/jquery/ajax_getscript.asp) | 使用 HTTP GET 请求从服务器加载 JavaScript 文件，然后执行该文件。 |
| [.load()](https://www.w3school.com.cn/jquery/ajax_load.asp)  | 从服务器加载数据，然后把返回到 HTML 放入匹配元素。           |
| [jQuery.param()](https://www.w3school.com.cn/jquery/ajax_param.asp) | 创建数组或对象的序列化表示，适合在 URL 查询字符串或 Ajax 请求中使用。 |
| [jQuery.post()](https://www.w3school.com.cn/jquery/ajax_post.asp) | 使用 HTTP POST 请求从服务器加载数据。                        |
| [.serialize()](https://www.w3school.com.cn/jquery/ajax_serialize.asp) | 将表单内容序列化为字符串。                                   |
| [.serializeArray()](https://www.w3school.com.cn/jquery/ajax_serializearray.asp) | 序列化表单元素，返回 JSON 数据结构数据。                     |