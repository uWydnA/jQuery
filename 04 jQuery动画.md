# jQuery动画

## INDEX

- [x] [内置](#内置)
- [x] [自定义](#自定义)
- [x] [全局配置](#全局配置)

## 内置

> 封装好的，固定效果，不能修改

### 显示隐藏

#### 显示 show()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").show();//瞬间显示，默认没有时间
  $(".box").show(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

#### 隐藏 hide()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").hide();//瞬间显示，默认没有时间
  $(".box").hide(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  



#### 显示／隐藏 toggle()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").toggle();//瞬间显示，默认没有时间,如果此时状态为隐藏，则显示，反之亦然
  $(".box").toggle(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  



### 上拉下拉

#### 上拉 slideUp()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").slideUp();//不传参则系统默认有一个参数，约为200
  $(".box").slideUp(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

#### 下拉 slideDown()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").slideDown();//不传参则系统默认有一个参数，约为200
  $(".box").slideDown(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

#### 上拉／下拉 slideToggle()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").slideToggle();//不传参则系统默认有一个参数，约为200
  $(".box").slideToggle(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

### 淡出淡入

#### 淡出 fadeOut()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").fadeOut();//不传参则系统默认有一个参数，约为200
  $(".box").fadeOut(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

#### 淡入 fadeIn()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").fadeIn();//不传参则系统默认有一个参数，约为200
  $(".box").fadeIn(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```

  

#### 淡出／淡入 fadeToggle()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").fadeToggle();//不传参则系统默认有一个参数，约为200
  $(".box").fadeToggle(1000);//参数为动画的毫秒数，此时动画时间为1s
  ```



#### 半透明 fadeTo()

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;}
  ```

- JS

  ```js
  $(".box").fadeTo(1000,0.2);//第一个参数为动画的毫秒数，此时动画时间为1s，第二个参数表示opacity的参数
  ```



## 自定义

> 自己设置的动画效果

### animate

- HTML

  ```html
  <div class="box">
      
  </div>
  ```

- CSS

  ```css
  .box{width:100px;height:100px;background:#f99;position:absolute;}
   /*需要注意，自定义动画如果需要操作left和top,则需要加上position:absolute;*/
  ```

- JS

  ```js
  $(".box").animation({
      width:200,
      //width: "200"
      //width: "200px"
      //width: "+=200" 此时会变成原尺寸加200的宽度
      height:300,
      left:40,
      top:100
  },1000,function(){
      alert("animate over");
  });
  //第一个参数是一个对象，表示需要改变的数值型CSSS属性
  //第二个参数是动画时间，不填写则为JQ默认的时间
  //第三个参数是一个回调函数，在动画完成后执行。
  ```



## 全局配置

> 都不推荐使用，采取默认值即可

### $.fx.interval 

​	设置动画的频率

​	$.fx.interval = 30;



### $.fx.off 

​	设置动画的关闭

​	$.fx.off = true;

## 执行顺序

### 同步

​	动画与动画之间的执行顺序是同步，逐个执行

​	动画的回调函数绝对是同步

### 链式动画

#### 分开写

> 可以操作不同元素

```js
$(".box").animate({
    left:500
})
$(".box").animate({
    top:500
})
```



#### 借助回调函数

>可以操作不同元素

```js
$(".box").animate({
    left:500
},function(){
    $(".box").animate({
        top:400
    })
})
```



#### 连缀执行

> 只能操作同一个元素

```js
$(".box").animate({
    left:500
}).animate({
    top:100
})
```



### 异步

​	动画与其他方法之间的执行顺序是异步，同时执行



### queue

> jq提供的专门做同步的方法
>
> 但queue方法存在的问题，不能继续连缀，解决方式如下

```js
$(".box").animate({
    left: 500
}).animate({
    top: 400
}).queue(function (next) {
    $(".box").css("background", "yellow")
    next();//官方提供的支持是：在queue的回调函数中接受参数，并执行，即可解决返回之前的对象伪数组
}).animate({
    left: 0
})
```



## 动画的控制

### 延迟 delay()

```js
$(".box").delay(2000).animate({
    left:500
}).delay(2000).animate({
    top:400
})
```

### 动画队列 stop()

stop(参数1,参数2)，参数都是布尔值

参数1：队列中的动画：true清空队列，false不清除队列

参数2：正在执行的动画：true立即到终点，false立即停止



