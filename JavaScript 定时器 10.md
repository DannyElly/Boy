# JavaScript 定时器 10

标签（空格分隔）： JS

---

## 定时器是什么

javaScript中系统提供的函数，用来每隔一段时间或者延迟一段时间执行一段指定的代码，分为两种：

- 重复执行定时器 `setInterval`
- 延迟执行定时器 `setTimeout`


## 定时器的语法

**重复执行定时器**

```
//setInterval('要做的事儿','间隔时间');
//每个 间隔时间 做一次 要做的事。
// 间隔时间的单位事毫秒， 没有单位  1s == 1000ms
```

> 需求1：设置一个变量初始为0，让其每隔1秒自增依次，并且打印到控制台中。

```
var a = 0;
    
/*setInterval(fn, 1000);

function fn(){
  a++;
  console.log(a);
}*/

setInterval(function (){
  a++;
  console.log(a);
}, 1000);

/*setInterval('fn()', 1000);  // 虽然可以，不要这么写

function fn(){
  a++;
  console.log(a);
}*/
```

**延迟执行定时器**

> 需求2：页面上一个div，让其在3秒之后背景颜色由红色变为蓝色。

```
var box = document.querySelector('.box');
    
setTimeout(function() {
  box.style.backgroundColor = 'blue';
}, 3000);
```

## 清除定时器

```
// 清除定时器也分为两种分别是
    
//clearInterval();
//clearTimeout();

// 它们都有一个共同的特性，就是脾气特别好，给我什么都可以。
// 如果参数是某个定时器的编号，那么就会清除对应的定时器
// 由于定时器的编号在跨浏览器的时候会有兼容性问题，所以通常使用一个变量来存储定时器的返回值
```

> 需求3：设置一个变量初始为0，让其每隔1秒自增依次，并且打印到控制台中，当变量增加到5的时候停止定时器。

```
var a = 0;
    
var timer = setInterval(function() {
  console.log(a++);
  if(a == 5){
    clearInterval(timer);
  }
}, 1000);
```
> 需求4：延时菜单，使用以下结构，当移入按钮，让div显示，此时鼠标从按钮移开到div身上，div可以继续显示，当移开div之后，div消失，如果移开按钮的时候没有移入到div身上，div消失。

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>延时菜单</title>
  <style>
    .box {
      width: 100px;
      height: 100px;
      background: red;
      display: none;
    }
  </style>
</head>
<body>
  <input type="button" value="按钮" class="btn">
  <div class="box"></div>
</body>
</html>
```

## 关于定时器的最小时间间隔

定时器的时间间隔并不精确，不同的浏览器都有各自的最小间隔，最新的HTML5的规范规定了最小间隔为4ms。

## 获取元素计算后样式的数据

> `getComputedStyle(元素).属性`

注意：无法获取`transform`的样式

### 封装CSS函数（初步）

```
function css(){
  var len = arguments.length;
  if(len < 2){
    return false;
  }
  if(len == 2){
    return Number.parseFloat(getComputedStyle(arguments[0])[arguments[1]]);
  }
  if(len == 3){
    arguments[0].style[arguments[1]] = arguments[2];
  }
}
```

> 需求5：点击按钮让div向右以`1px/20ms`的速度运动。

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .box {
      width: 100px;
      height: 100px;
      position: relative;
      background: red;
      left: 0;
      top: 10px;
    }
  </style>
</head>
<body>
  <input type="button" value="按钮" class="btn">
  <div class="box"></div>
  <script>
    var btn = document.querySelector('.btn');
    var box = document.querySelector('.box');
    
    var t = null;
    
    btn.onclick = function (){
      // 让box向右运动
      clearInterval(t);
      t = setInterval(function() {
        box.style.left = css(box, 'left') + 1 + 'px';
      }, 20);
      console.log(t);
    };
  </script>
</body>
</html>
```








