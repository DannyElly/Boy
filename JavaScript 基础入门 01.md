# JavaScript 基础入门 01

标签（空格分隔）： JS

---

### 了解JS能做些什么

- 与用户进行交互
- 图像处理
- WebApp
- 音频和视频的播放处理
- ......

### 分析JS特效的基本原理

> 动态的改变元素的行间CSS样式或者属性
> 动态的修改数据与服务器进行交互

---

### 第一个案例：

> 需求：鼠标点击按钮弹出对话框，同时显示：hello world!

#### 编写 HTML + CSS

```
<input type="button" value="按钮">
```

#### 需求分解

> * 找到按钮
> * 点击按钮
> * 弹出对话框

#### 如何书写注释

```
// 多行注释 
/*找到按钮
点击按钮
弹出对话框*/
/**
 * 注释1
 * 注释2
 * ....
 */
// 注释内容  单行注释
```

#### 第一个语法规则

> 语句： 一行代码;(分号不能是中文的)

#### 通过ID获取元素

> document.getElementById('元素的id');

* document 文档
* get 获取
* Element 元素
* By 通过
* Id  元素的Id

除了get的g小写，其他的单词首字母都要大写

#### 了解事件

> 事件：初步的理解成用户对浏览器的操作。

鼠标事件：

* onclick 当鼠标点击的时候
* onmouseover 当鼠标移入的时候
* onmouseout 当鼠标移出的时候

#### 初识函数

> 函数：本质上是一种代码的分组形式。可以通过这种形式赋予某组代码一个名字，以便于之后的调用。函数可以在任何时候和任意地方去调用。

- 可以理解成对事件的一个响应

#### 函数的基本组成（初步）

* function  声明函数的关键字
* 函数的名 比如 abc 、 fn、
* ()
* { 写上对应的代码，就是需求 }

#### 函数的调用

> 放在函数内的代码不会主动执行。

* 通过函数的名字 + ()  abc();
* 通过事件去调用

#### 对话框之 alert()

> 带确定按钮的对话框。

如果括号内写的是一个数字，那么可以不加引号，如果是一句自己写的内容，那么就必须加上引号，单引号和双引号都可以。

---

#### 关于JS中的 “=”

“=” 不是数学上的相当，而是赋值的意思，就是将其右边的“东西”给其左边的“东西”。

### 关于如何书写JS代码

* 行间: 在HTML标签上写JS，不利于维护和管理，最好不要这么写。
* 内嵌: 可以在当前页面的`<script></script>`标签中写，可以方便复用，但是其他页面无法使用。
* 外链: 和CSS外链的形式类似，通过script标签的src属性将js文件的路径链接到页面。可以方便代码的维护和管理。也可以让多个页面进行复用。

```
<input id="btn" onclick="alert(1)" type="button" value="按钮">
```

```
<input id="btn" type="button" value="按钮">
<input id="btn2" type="button" value="按钮2">
<script>
document.getElementById('btn').onclick = abc;
document.getElementById('btn2').onclick = abc;
//  abc();
function abc() {
  alert('hello world!');
}

// abc();
</script>
```

```
// 04.js
document.getElementById('btn').onclick = abc;
document.getElementById('btn2').onclick = abc;

function abc() {
  alert('hello world!');
}

```

```
// 04.html
<input id="btn" type="button" value="按钮">
<input id="btn2" type="button" value="按钮2">
<script src="js/04.js"></script>
```

---

### 第二个案例

> 需求：鼠标移入div让div由200px得宽高变为400px，让背景颜色变为蓝色，同时旋转360度，移出后恢复原来的状态。

#### 编写 HTML + CSS

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    #duoduo {
      width: 200px;
      height: 200px;
      background: goldenrod;
      transition: 1s;
    }
  </style>
</head>
<body>
  <div id="duoduo"></div>
</body>
</html>
```

#### 需求分解

> * 通过ID找到对应的div元素
> * 给这个div元素添加一个鼠标移入事件
> * 让这个div变个样子
> * 给这个div元素添加一个鼠标移出事件
> * 让这个div恢复原来的样子

#### 元素的属性

> 属性：是用来描述元素特征的，包括属性的名字和属性的值。

#### 编写JS代码

```
<script>
// 通过ID找到对应的div元素
// 给这个div元素添加一个鼠标移入事件
document.getElementById('duoduo').onmouseover = fnOver;
/**
 * 给这个div元素添加一个鼠标移出事件
 * 让这个div恢复原来的样子
 */
document.getElementById('duoduo').onmouseout = fnOut;

// 鼠标移入的时候让div变个样子
function fnOver() {
  document.getElementById('duoduo').style.width = '400px'; // 字符串
  document.getElementById('duoduo').style.height = '400px';
  document.getElementById('duoduo').style.background = 'blue';
  document.getElementById('duoduo').style.transform = 'rotate(360deg)';
}

// 鼠标移出的时候让div恢复原来的样子
function fnOut () {
  document.getElementById('duoduo').style.width = '200px';
  document.getElementById('duoduo').style.height = '200px';
  document.getElementById('duoduo').style.background = 'goldenrod';
  document.getElementById('duoduo').style.transform = 'rotate(0deg)';
}
</script>
```

---

### 变量

> 定义：通常是用来储存数据的，即它是存放具体数据的容器。当我们编写程序时，用变量来标识实际数据会更方便些，尤其是多次使用某个数据的时候。

#### 使用变量的步骤：

* var 变量声明;
* 变量的初始化；

```
var a;
var b;
var c = 1; // 声明+初始化
```

#### 关于undefined类型

当变量声明未赋值的时候默认就是undefined；

#### 变量的命名规则

> 由数字字母下划线还有美元符($)组成，并且首字符不能是数字。不能使用关键字和保留字。

```
var a1;
var 1223ccc;  // 不符合规则
var $ = 0;
var _ = 100;
```

尽量使用类似JS本身的命名规则：

```
getElementById // 驼峰命名法
```

#### 关键字和保留字

> 关键字：用来定义JS的基本语法的语句

![屏幕快照 2016-12-18 下午9.17.12.png-59.5kB][1]


 > 保留字：将来JS这门语言在发展的过程中可能会用到词
 
![屏幕快照 2016-12-18 下午9.18.14.png-111.7kB][2]

 ---
 
### 调试代码（一）
 
 > console.log(code)  向控制台打印输出指定的内容。
 
 ---
 
### 全局对象：window
 
 window 是JS里面的顶级对象，是JS所有变量函数等的老大。
 
 ```
 var a = 1;
 
 alert(window.a);
 ```
 
### window的系统事件
 
> onload 当加载完成的时候

```
window.onload = fnLoad;

function fnLoad(){
    // do some thing...
}
```

上面的代码的意思可以理解成，当页面所有元素都加载完成的时候会触发 fnLoad 这个函数，那么函数里面就可以写上你所需要的需求。这样就可以把你的代码写在所有元素的上面了。
  
 
 

 
 
 
 
 
 
 
 
 
 
 
   [1]: http://static.zybuluo.com/maxleader/l69srcwk8zwo9vilxvope949/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-18%20%E4%B8%8B%E5%8D%889.17.12.png
  [2]: http://static.zybuluo.com/maxleader/2s92tcluh3n5p22gh1988tib/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-12-18%20%E4%B8%8B%E5%8D%889.18.14.png