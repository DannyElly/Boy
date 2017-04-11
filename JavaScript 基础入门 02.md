# JavaScript 基础入门 02

标签（空格分隔）： JS

---

## cssText

> 是元素style的一个属性，用来批量设置元素的css样式。

```
ele.style.cssText = ''; // 将元素的行间样式清空
ele.style.cssText = 'width:300px;height:300px;background:red;'; // 批量设置元素的行间CSS样式。
```

## 匿名函数

匿名函数的声明：

- 关键字 function
- ()
- { 代码 }

不能单独的写一个匿名函数，否则会报错。

匿名函数的调用的第一种方式：

```
// 通过事件去调用

元素.事件 = function (){
    代码。。。
};
```

> 案例：鼠标移入按钮让div旋转360deg，移出让div恢复。

```
<style>
    #box {
      width: 200px;
      height: 200px;
      background: goldenrod;
      transition: 1s;
    }
</style>
</head>
<body>
  <input id="btn" type="button" name="" value="按钮">
  <div id="box"></div>
  <script>
    var btn = document.getElementById('btn');
    var box = document.getElementById('box');
    
    // 匿名函数 通过事件去调用的写法
    // btn.onclick = function (){
    //   console.log('hello');
    // };
    
    // 鼠标移入div旋转360deg
    btn.onmouseover = function (){
      box.style.transform = 'rotate(360deg)';
    };
    // 鼠标移出 恢复
    btn.onmouseout = function (){
      box.style.transform = 'rotate(0deg)';
    };
 </script>
```

## 函数的嵌套

```
// 案例：
function fn1(){
  alert(1);
}

function fn2(){
  fn1();
}

fn2();

btn.onclick = function (){
  fn2();
};
```

## 通过CSS选择器来获取元素

> document.querySelector('CSS选择器');

* document  文档
* query  查询
* Selector 选择器
* 在文档中通过选择器（css）求查询对应的元素

```
<ul id="list">
    <li class="li1 li">1</li>
    <li>2</li>
    <li>3</li>
    <li class="li4 li">4</li>
    <li>5</li>
    <li>6</li>
</ul>

<script>
    //  var li4 = document.querySelector('.li4');
    //
    //  console.log(li4);
    
    // 当有多个相同的class的时候或者单个标签的时候，只选第一个
    // var li = document.querySelector('li');
    //
    // console.log(li);
</script>
```

> 需求1：用两种方法获取以下结构中的第二个span。然后当鼠标点击它的时候向控制台打印“找到了目标”。

```
<div class="box">
    <p>aaa</p>
    <span>span1</span>
    <div>111</div>
    <span>我在这！</span>
    <div>222</div>
</div>
```

```
<script>
// var span = document.querySelector('.box span:nth-of-type(2)');
var span = document.querySelector('.box span:nth-child(4)');
span.onclick = function (){
  console.log('找到了目标');
};
</script>
```

[关于更多CSS选择器](http://www.w3school.com.cn/cssref/css_selectors.asp)

> 需求2：用三种方法获取以下结构中的第二个li中name以d2结尾的按钮，点击这个按钮弹出'hello'

```
<ul class="list">
    <li>
      <input type="button" name="abc1" value="按钮1">
      <input type="button" name="abc2" value="按钮2">
      <input type="button" name="abc3" value="按钮3">
    </li>
    <li>
      <input type="button" name="abcd1" value="按钮4">
      <input type="button" name="abcd2" value="按钮5">
      <input type="button" name="abcd3" value="按钮6">
    </li>
    <li>
      <input type="button" name="abce1" value="按钮7">
      <input type="button" name="abce2" value="按钮8">
      <input type="button" name="abce3" value="按钮9">
    </li>
</ul>
```

```
<script>
// var btn = document.querySelector('#list li:nth-of-type(even) input:nth-of-type(2)');

// var btn = document.querySelector('#list li:nth-of-type(even) input:nth-child(2)');

// var btn = document.querySelector('#list li:nth-of-type(even) input[name $=d2]');

//var btn = document.querySelector('#list li:nth-of-type(even) input[name ^=sab]');

console.log(btn);
</script>
```

  
## JS的属性操作

> 属性操作主要是操作元素的属性，包括属性的读取和写入（获取和修改）

### 属性的获取（读）

属性读取的方法：

- 通过 元素.元素的属性名 可以获取到这个属性对应的值
- 通过 ['属性名字'] 的方式来获取属性的值

凡是能用 . 的地方都能用 [], 但是能用 [] 的地方不一定能用 .

示例：

```
<style>
    #box {
      width: 200px;
      height: 200px;
      background: red;
    }
</style>
<input type="button" id="btn" value="按钮">
<div id="box"></div>
<script>
// 获取到id为btn的按钮
var btn = document.querySelector('#btn');
var box = document.querySelector('#box');

btn.onclick = function (){
  alert(btn['type']);
};

// btn.onclick = function (){
//   // box.style.background-color = 'blue';  // 错误的写法
//   // box.style.backgroundColor = 'blue';
//   box.style['background-color'] = 'blue';
// };
</script>
```

> 需求1：点击按钮获取文本框内的value值，并且弹出输入的内容。

编写HTML结构:

```
<input id="text" type="text">
<input type="button" name="" value="按钮">
```

需求分解：

* 找到按钮
* 给按钮添加点击事件
* 找到text文本框
* alert(text.value)

```

```


### 属性的修改（写）

所谓的属性修改就是：元素.元素的属性 = 新的值；

> 需求1：点击按钮让“按钮”变为“button”。

```
<input type="button" value="按钮" id="btn">
<script type="text/javascript">
// 元素.元素的属性 = 新的值
var btn = document.querySelector('#btn');

btn.onclick = function (){
  btn.value = 'button';
};
</script>
```

> 需求2：点击按钮弹出文本框中的值，并且自动清空文本框。

```
<input type="text" id="text" value="">
<input type="button" value="按钮" id="btn">
<script type="text/javascript">
// 元素.元素的属性 = 新的值
var btn = document.querySelector('#btn');
var text = document.getElementById('text');

btn.onclick = function (){
  var val = text.value;
  alert(val);
  val = 'new val';
  alert(val)
};

</script>
```

> 需求3：点击按钮获取输入框中属性名称和属性值，对div设置。

```
<head>
<style>
	#box{
		width: 100px;
		height: 100px;
		background: red;
	}
</style>
</head>
<body>
	<input type="text" id="text1" />
	<input type="text"  id="text2" />
	<input type="button" id="btn"  value="设置" />
	<div id="box"></div>
	<script>

	</script>
</body>
```

需求4：点击按钮将div的class从red变为blue。

```

```

> 一些补充：在JS中声明相同的变量或者函数，那么后面的会覆盖前面的。使用 on的形式给元素添加事件，如果添加多个 后面的同样会覆盖前面的。

```
// 下面的代码点击div会弹出2
div.onclick = function (){
    alert(1);
};
div.onclick = function (){
    alert(2);
};
```

```
var a = 1;
var a = 2;
// 上面的两行 最终 a 的变量的值 存的是2， 这叫作覆盖。
```

```
var a = 1;
a = 2;
// 上面的两行 最终 a 的变量的值 存的是2， 这叫作修改。
```

### 属性操作的注意事项：

> JS操作的是元素的行间样式，如果行间没有任何样式的属性，那么是无法通过属性的操作读取其样式表里面的值的。但是不影响对其的设置。

- class：不能使用class需要使用className
- src：获取到的是绝对路径，不一定是实际的值。但是设置的时候不用一定要设置绝对路径，设置相对路径也是可以得。
- background：获取到的颜色值不一定是写的格式，不同浏览器不一样。
- cssText：先清空元素之前的所有样式，然后再设置新的样式。

```
<input type="button" id="btn" value="button">
<div class="red"></div>
<script>
    var btn = document.getElementById('btn');
    var div = document.querySelector('.red');
    
    btn.onclick = function (){
     // JS中操作元素的class不能使用元素.class需要使用 ele.className
      console.log(div.className);
      div.className = 'blue';
    };
</script>
```

```
<img src="img/1.jpg" id="img" alt="abc">
<script>
var img = document.getElementById('img');

// console.log(img.src);  // 获取到的是文件的绝对路径

img.onclick = function (){
  img.src = 'img/2.jpg';  // 修改是没问题的
};
</script>
```

```
<div style="background:#f00;width:100px;height:100px;"></div>
<script>
var div = document.querySelector('div');
console.log(div.style.background); // 获取到的不一定是写的颜色类型

div.style.cssText = 'width:200px;height:200px;border:1px solid #000;';

// 先清空元素之前的所有样式，然后再设置新的样式。
</script>
```

## 元素的HTML内容

> innerHTML

- 通过 元素.innerHTML 可以获取到标签内的HTML内容
- 通过 元素.innerHTML = 新的值 可以修改元素内的HTML内容。

> 需求1：点击按钮向控制台打印元素内的HTML内容

```
<button id="btn">按钮</button>
<div id="box">duoduo</div>
<div class="box2">
    <img src="img/1.jpg" alt="">
    1111
</div>
<script>
    var box = document.getElementById('box');
    // console.log(box.innerHTML);
    box.innerHTML = 'momo';
    
    // 通过 元素.innerHTML 可以获取到标签内的HTML内容
    // 通过 元素.innerHTML = 新的值 可以修改元素内的HTML内容。
    
    var box2 = document.querySelector('.box2');
    console.log(box2.innerHTML); //  '内容'
    var btn = document.getElementById('btn');
    btn.onclick = function (){
      console.log(box2.innerHTML);
    };
</script>
```

> 需求2：点击按钮将文本框内的值写到p标签内。

```
<input type="button" id="btn" name="" value="按钮">
<input type="text" id="text" name="" value="">
<p>1</p>
<script>
    var btn = document.getElementById('btn');
    var text = document.getElementById('text');
    var p = document.querySelector('p');
    
    btn.onclick = function (){
      var val = text.value;
      console.log(val);
      p.innerHTML = val;
    };
    console.log(p.innerHTML == '1');
    
    // innerHTML  会先清空元素之前的内容，然后再添加新的内容。
    // innerHTML 不仅仅能写文字还能写HTML标签
    // 例如： 在文本框内写一个<img src="img/1.jpg">
</script>
```

## 字符串

> 由0个或者多个字符组成的集合，并且放在一对双引号或者单引号中，就叫做字符串。

```
var str1 = '1';
var str2 = 'abc';
var str3 = 100; // 不是字符串 是个 数字
var str4 = '';
```

凡是元素自带的属性获取到的值都是字符串，innerHTML获取到的值也是字符串。

```

```

### 字符串的属性

> 字符串.length

字符串一旦声明就不可以再被更改，所以length是一个只读属性（只能读，不能修改）。

### 字符串的拼接

> 将2个或者2个以上的字符串拼接到一起，需要用 "+"。

```
<script>
var str1 = 'abc';
var str2 = '456';

var str3 = str1 + str2;

console.log(str3);  // 'abc456'

// console.log('hello' + ' ' + 'world' + '!'); // 'hello world!'

// 当一个字符串和一个数字做拼接的时候
console.log('abc' + 1); // 'abc1'
// 当两个数字做+的时候
console.log(1 + 1); // 2

var s = '1' + 1; // 11

console.log(s == '11'); //true

var a = 100;

// 
console.log('我的成绩是' + a + '分');

var stra = "abc";
var strb = 'abc';

console.log(stra == strb); // true

console.log('<div style='width:200px'>'); // 报错

// 引号一定是成对儿出现的
// 如果说外面的是单引号，而里面的数据需要加上引号的情况
// 那么这个数据需要加上双引号

</script>
```

> 需求1：点击按钮向已有的div中添加一个新的div元素，并且这个新的div元素的宽高是文本框中的值。

需求分解：

1. 获取到对应的元素：按钮，2个文本框，div
2. 点击按钮，给按钮添加点击事件
3. 拿到2个文本框里面的数值
4. 给div里面添加HTML内容，这个内容是一个div元素，同时设置这个div元素的宽高是拿到的2个文本框内的内容。


```
<input id="t1" type="text" value="">
<input id="t2" type="text" value="">
<input id="btn" type="button" name="" value="button">
<div id="box"></div>
<script>
    var btn =document.getElementById('btn');
    var t1 = document.getElementById('t1');
    var t2 = document.getElementById('t2');
    var box = document.getElementById('box');
    
    /*btn.onclick = function (){
      var w = t1.value;
      var h = t2.value;
      console.log(w, h);
      box.innerHTML = '<div style="width:' + w + 'px;height:' + h + 'px;"></div>';
    };*/
    
    /*btn.onclick = function (){
      var w = t1.value;
      var h = t2.value;
      box.innerHTML = '<div id="box2"></div>';
      var box2 = document.getElementById('box2');
      console.log(box2);
      box2.style.cssText = 'width:'+w+'px;height:'+h+'px;';
    };*/
    
    btn.onclick = function (){
      box.innerHTML = '<div style="width:' + t1.value + 'px;height:' + t2.value + 'px;"></div>';
    };
</script>
```

## 实例：留言板

需求：点击按钮进行留言




