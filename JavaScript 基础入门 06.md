# JavaScript 基础入门 06

标签（空格分隔）： JS

---

## 回顾 window 

> window 是JS中全局对象，凡是在全局中声明的变量，或者函数，最终都会成为它的属性（方法）。

- 全局：在JS中在script内，并且在函数外都算全局的范围。
- 对象：在现实中，对象是一个抽象的概念，可以指人或者事物，在JS中可以指标签元素等，都可以算是对象。
- 属性：一般都是名词，用来描述元素的特性的。
- 方法：在JS中就是指函数。

## 回顾for循环

**对for循环使用的一些补充：**

```
<script>
  /*var i;
  for(i=0; i<3; i++){
    console.log(i);  // 0 1 2
  }*/
  // 循环完成后i的结果
  // console.log(i); // 3
  
  /*for(var i=0; i<3; i++){
  // 相当于调用了3次函数 每次弹出i的值
    fn1();  // 0 1 2
  }
  
  function fn1() {
    alert(i);
  }
  // 在这调用函数 循环已经结束，此时i的值是3
  fn1(); //3*/
  
  /*for(var i=0; i<3; i++){
    function fn1() {
      alert(i);  // 3
    }
  }
  // 上面这种写法，相当于我特别傻的写了3次重复的下面的函数
  function fn1() {
    alert(i);
  }
  function fn1() {
    alert(i);
  }
  function fn1() {
    alert(i);
  }
  // 在这调用函数 for循环已经结束此时i是3
  fn1();*/
  
  for(var i=0; i<3; i++){
  // 相当于用重复了3次下面的代码，但是这个函数并没有触发
    document.onclick = function() {
      alert(i);
    }
  }
  
  console.log(1);  // 1
  
  /*doucment.onclick = function() {
    alert(i);
  }
  
  doucment.onclick = function() {
    alert(i);
  }
  
  doucment.onclick = function() {
    alert(i);
  }*/
</script>
```

> 需求1：class为list的ul下面有5个li，每个li里面的内容分别是0、1、2、3、4，点击每个li弹出其对应的内容。

```
<body>
<ul class="list">
    <li>0</li>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>
<script>
    var lis = document.querySelectorAll('.list li');
    
    console.log(lis);
    
    /*lis[0].onclick = function (){
      alert(lis[0].innerHTML);
    };
    lis[1].onclick = function (){
      alert(lis[1].innerHTML);
    };
    lis[2].onclick = function (){
      alert(lis[2].innerHTML);
    };
    lis[3].onclick = function (){
      alert(lis[3].innerHTML);
    };
    lis[4].onclick = function (){
      alert(lis[4].innerHTML);
    };*/
    
    for(var i=0; i<lis.length; i++){
      lis[i].onclick = function (){
        //alert(i)
        //因为这里的i是循环完成i的值
        alert(lis[/*填什么呢？*/].innerHTML);
      }
    }
</script>
```

## 初识 this

> this 是JS中的一个关键字，是预先定义好的一个变量，并且这个变量储存的永远是一个对象，这个变量this储存的对象会随着不同的环境改变，也就是说它不是定值。这个this只能读，不能写。

**关于this指向：(初步)**

- 在全局下 this 就代表 window
- 对象.函数 函数里面的this就是这个对象。
- 元素.事件 = 函数，此时函数内的this就是这个元素对象。

```
// 全局
alert(this);
var a = 1;
alert(this.a)
```

```
// 通过.的方式调用函数
function fn(){
   alert(this);  // window
}
window.fn()
```

```
// 事件调用
var btn = document.getElementById('btn');
btn.onclick = function (){
  alert(this);  // btn
};
```

**对需求1进行完善：**

```
<script>
  var lis = document.querySelectorAll('.list li');
  for(var i=0; i<lis.length; i++){
    lis[i].onclick = function (){
      console.log(this);
      alert(this.innerHTML);
    }
  }
</script>
```

> 需求2：现有5个50*50的span，默认没有背景颜色，只有边框，点击其中一个span，当前被点击的这个背景颜色变为半透明的粉色，其它不做改变，变成粉色后再点击本身不做改变。再次点击另外一个，另外一个背景颜色变成半透明的粉色。其它的都变回没有颜色。

```
  <style>
    span {
      display: inline-block;
      width: 50px;
      height: 50px;
      border: 1px solid #000;
      margin: 5px;
    }
    .active {
      background: rgba(245, 61, 182, 0.64);
    }
  </style>
  <script>
    window.onload = function (){
      var spans = document.querySelectorAll('span');
      
      /**
       * 第一种思路：点击当前的span给当前的span添加class
       * 在添加class之前 先把所有的span的class清空
       *
       * 第二种思路：定义一个上一个，点击当前的时候
       * 先清空上一个，然后给当前的添加class，然后把
       * 当前的变成上一个。
       */
      
      // 思路1
      /*for(var i=0; i<spans.length; i++){
        spans[i].onclick = function (){
          // 清空一组span的class
          for(var i=0; i<spans.length; i++){
            spans[i].className = '';
          }
          // 给当前的点击的span添加class
          this.className = 'active';
        }
      }*/
      
      // 思路2
      var prev = spans[0];
      
      for(var i=0; i<spans.length; i++){
        spans[i].onclick = function (){
          prev.className = '';
          this.className = 'active';
          prev = this;
        };
      }
      
      // for(var i=0; i<3; i++){
      //   for(var i=0; i<3; i++){
      //     console.log(i);
      //   }
      // }
      // console.log(i);
    };
  </script>
</head>
<body>
  <span></span>
  <span></span>
  <span></span>
  <span></span>
  <span></span>
</body>
```

> 需求3：生成10*10方阵，拼成一张完整的图片，默认每个方块透明度为0.1，鼠标移入，让当前方块透明度变为1，同时放大1.2倍，移出后恢复为1倍，透明度还为1。

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
      position: relative;
    }
    .box div {
      position: absolute;
      left: 0;
      top: 0;
      width: 50px;
      height: 50px;
      background-size: 500px 500px;
      background: url(pic.jpg) no-repeat;
      opacity: 0.3;
      transition: 500ms;
    }
  </style>
  <script>
    window.onload = function (){
      var box = document.querySelector('.box');
      
      var str = '';
      var t = -1;
      for(var i=0; i<100; i++){
        if(i%10 == 0){
          t++;
        }
        str += '<div style="left:'+(i%10 * 51)+'px;top:'+(t*51)+'px;background-position:'+(-i%10 * 50)+'px '+(-t*50)+'px;"></div>'
      }
      
      box.innerHTML = str;
      
      var divs = document.querySelectorAll('.box div');
      
      /**
       * 移入每一个div 让当前移入的这个 透明度变为1 同时放大1.2倍
       * 移出当前移入的这个div 让它变回1倍
       */
      
      for(var i=0; i<divs.length; i++){
        divs[i].onmouseover = function (){
          this.style.opacity = 1;
          this.style.transform = 'scale(1.2)';
        };
        divs[i].onmouseout = function (){
          this.style.transform = 'scale(1)';
        };
      }
    };
  </script>
</head>
<body>
  <div class="box"></div>
</body>
</html>
```

## 从数组到对象

> 想找到数组中的元素，需要通过对应的索引值（0、1、2），这个索引值实质上就是这个元素对应的key。

|0|1|2|3|
|:---:|:---:|:---:|:---:|
|'a'|'b'|'c'|'d'|

> 对象和数组非常类似，但是可以自己去定义每个数据对应的名字（key/属性名）。

**创建自定义对象**

> var obj = {key:value};

```
var obj = {
  a: 'a',
  b: 'b',
  c: 'c',
  d: 'd'
};
```

对象里面的数据包括 属性的名字（key），和属性对应的值（value），对象里面可以储存任意类型的数据，但是每个数据都必须对应一个名字。

**给对象添加属性和方法**

1. 在创建的时候直接写到对象里面
```
var obj2 = {
  arr:[1,2,3,4],
  str:'abc',
  num:10,
  o:{},
  fn:function (){  // 对象里面写函数 需要这么写，不用写名字了。
    
  }
}
```

2. 通过 对象.属性（方法）的方式给对象添加属性或者方法。

**使用对象中的数据**

> 通过 对象.属性名（方法名）

```
var obj = {};
    
// 给obj添加一个属性a，对应的值是1
obj.a = 1;

// 给obj添加一个方法
obj.fn = function (){
  alert(1);
}

//alert(obj.fn);
```

## 元素的自定义属性

**从需求开始：**

> 需求4：点击一个50*50的span，默认只有边框，没有背景颜色的，点击的时候添加背景颜色，再次点击取消背景颜色。

```
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    span {
      display: block;
      width: 50px;
      height: 50px;
      border: 1px solid #000;
      margin: 5px;
    }
    .active {
      background: rgb(250, 191, 15);
    }
  </style>
</head>
<body>
  <span class=""></span>
  <script>
    var span = document.querySelector('span');
    var flag = true;
    span.onclick = function (){
      if(flag){
        this.className = 'active';
      }else{
        this.className = '';
      }
      flag = !flag;
    };
  </script>
</body>
```

> 需求5：class为box的div，里面有5个span，默认只有边框，没有背景颜色的，点击某一个span的时候添加背景颜色，再次点击添加过背景颜色的取消背景颜色。

```

```

> 需求6：在需求2的基础上，添加点击被选中的可以取消选中，点击其它未被选中的，已经被选中的取消被选中的（去掉背景颜色）。

```
<body>
  <span></span>
  <span></span>
  <span></span>
  <span></span>
  <span></span>
  <script>
    // 获取到5个spans
    var spans = document.querySelectorAll('span'); // {flag:true}
    
    // 定义上一个
    var prev = spans[0];
    
    // 循环所有的span
    for(var i=0; i<spans.length; i++){
      // 给每个span添加自定义属性 flag 默认为true
      spans[i].flag = true;
      // 给每个span添加点击事件
      spans[i].onclick = function (){
        // 如果当前点击的这个span身上的自定义flag 为true就执行
        if(this.flag){
          // 先清空上一个的className
          prev.className = '';
          // 由于上一个className被清空了，但是实际上没有className的时候
          // 上一个的自定义属性flag对应的应该是个true，
          // 所有要给它变回true
          prev.flag = true;
          // 给当前的这个点击的span添加一个className active
          this.className = 'active';
          // 让当前点击的这个span 变成上一个
          // 以便下次点击的时候 可以找到正确的上一个
          prev = this;
        }else{
          // 当这个span有className的时候，再次点击 由于 this.flag 变为了false
          // 那么就执行清空className的操作
          this.className = '';
        }
        // 切换它的这个 开关
        this.flag = !this.flag;
      }
    }
  </script>
</body>
```

## 自定义属性的应用

**选项卡**

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    button {
      width: 70px;
      height: 40px;
    }
    .active {
      background: rgba(58, 219, 65, 0.65);
    }
    div {
      width: 220px;
      height: 220px;
      font: 49px/220px arial;
      text-align: center;
      border: 2px solid #000;
      margin-top: 5px;
      display: none;
    }
    .show {
      display: block;
    }
  </style>
</head>
<body>
  <button class="active">1</button>
  <button>2</button>
  <button>3</button>
  <div class="show">1111</div>
  <div>2222</div>
  <div>3333</div>
  <script>
    /**
     * 需求：选项卡
     *  当鼠标移入对应的按钮的时候，让对应的div显示出来，然后不是对应的div隐藏
     */
     var btns = document.querySelectorAll('button');
     var divs = document.querySelectorAll('div');
     
     /**
      * btns
      *  0     btns[0]
      *  1     btns[1]
      *  2     btns[2]
      */
     
      /**
       * divs
       *  0     divs[0]
       *  1     divs[1]
       *  2     divs[2]
       */
      
      // 1 先做鼠标移入按钮  移入的按钮 有背景颜色 其它没有
      // 2 将所有的btns 和 div 对应起来
      
      for(var i=0; i<btns.length; i++){
        // 给每个btns添加一个自定义的属性 叫 indedx，每次循环正好等于当前这个i的值
        btns[i].index = i; // 自定义索引值
        // 给每个btns添加鼠标移入事件
        btns[i].onmouseover = function (){
          //console.log(this.index);
          // 先清空所有btns的className，以及让所有的div都隐藏（清空所有div的className）
          for(var i=0; i<btns.length; i++){
            btns[i].className = '';
            divs[i].className = '';
          }
          //给当前的按钮添加背景 也就是 className为active
          this.className = 'active';
          //给当前这个按钮对应的这个div添加一个用来显示出来的className为show
          divs[this.index].className = 'show';
        };
      }
  </script>
</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    button {
      width: 70px;
      height: 40px;
    }
    .active {
      background: rgba(58, 219, 65, 0.65);
    }
    div {
      width: 220px;
      height: 220px;
      font: 49px/220px arial;
      text-align: center;
      border: 2px solid #000;
      margin-top: 5px;
      display: none;
    }
    .show {
      display: block;
    }
  </style>
</head>
<body>
  <button class="active">1</button>
  <button>2</button>
  <button>3</button>
  <div class="show">1111</div>
  <div>2222</div>
  <div>3333</div>
  <script>
    /**
     * 需求：选项卡
     *  当鼠标移入对应的按钮的时候，让对应的div显示出来，然后不是对应的div隐藏
     */
     var btns = document.querySelectorAll('button');
     var divs = document.querySelectorAll('div');
     
     // 清空上一个
     
     var prevBtn = btns[0];
     var prevDiv = divs[0];
     
     for(var i=0; i<btns.length; i++){
       /**
        * 什么时候用自定义索引值：
        *  当一组元素去控制另外一组元素的时候，首先想到自定义属性（索引值）
        *  给控制的一组元素添加索引值，而不是被控制的。
        */
       // 给每个按钮添加一个自定义索引值 0 1 2
       btns[i].index = i;
       btns[i].onmouseover = function (){
         // 清空上一个（第一个，默认显示的那个）的className
         prevBtn.className = '';
         // 让上一个（默认显示的div）的className 清空
         prevDiv.className = '';
         // 给当前的按钮添加className
         this.className = 'active';
         // 让当前这个按钮对应的div显示出来（添加className为show）
         divs[this.index].className = 'show';
         // 更新上一个
         prevBtn = this;
         prevDiv = divs[this.index];
       };
     }
  </script>
</body>
</html>
```










