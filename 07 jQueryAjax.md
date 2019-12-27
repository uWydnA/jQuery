# jQueryAjax

## INDEX

- [x] [注意](#注意)
- [x] [事件类型作为方法名](#事件类型作为方法名)
- [x] [bind() / unbind()](#bind() / unbind())
- [x] [on() / off()](#on() / off())
- [x] [one()](#one())
- [x] [hover()](#hover())
- [x] [ready()](#ready())
- [x] [trigger()](#trigger())



## $.get() / $post()

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