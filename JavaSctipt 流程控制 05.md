# JavaSctipt 流程控制 05

标签（空格分隔）： JS

---

## 获取一组元素

> 元素.querySelectorAll('CSS选择器');

```
    <div id="box">
        <ul>
          <li class="box-item"></li>
          <li class="box-item active"></li>
          <li class="box-item"></li>
          <li class="box-item active"></li>
          <li class="box-item"></li>
        </ul>
    </div>
    <script>
    // 第一种写法
    // var lis = document.querySelectorAll('#box ul li.active');
    // console.log(lis);
    // 第二种写法
    var box = document.getElementById('box');
    var lis = box.querySelectorAll('ul li.active');
    /**
     * 获取到的是一组元素，这一组元素可以通过类似数组的方法去使用。
     */
    console.log(lis[0]);
    
    lis[0].style.background = 'red';
    lis[1].style.background = 'red';
</script>
```

> 元素.getElementsByTagName('标签名字');

```
<div id="box">
    <ul>
      <li class="box-item"></li>
      <li class="box-item active"></li>
      <li class="box-item"></li>
      <li class="box-item active"></li>
      <li class="box-item"></li>
    </ul>
</div>
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
<script>
    // 第一种写法
    // 在文档中获取到所有的li
    // var lis = document.getElementsByTagName('li');
    // 第二种写法
    var box = document.getElementById('box');
    var lis = box.getElementsByTagName('li');
    
    //console.log(lis.length);
    
    lis[0].style.background = 'blue';
</script>
```
> 元素.getElementsByClassName('class名字');

```
<div id="box">
    <ul>
      <li class="box-item"></li>
      <li class="box-item active"></li>
      <li class="box-item"></li>
      <li class="box-item active"></li>
      <li class="box-item"></li>
    </ul>
</div>
<script>
    // 第一种写法
    // 获取到页面上所有的 className 为 box-item 的元素
    // var items = document.getElementsByClassName('box-item');
    
    // 第二种写法
    // 获取到id为box下面的所有 className为 box-item的元素
    var box = document.getElementById('box');
    var items = box.getElementsByClassName('box-item');
    var actives = box.getElementsByClassName('active');
    
    console.log(items);
    
    actives[0].style.background = 'red';
    actives[1].style.background = 'red';
    
    console.log(actives.length);
</script>
```

**类数组**

凡是一组元素，并且这组元素可以被索引，并且具有length属性，就叫做类数组。


> 需求1：点击按钮，让class为list的ul下的li的背景颜色变为红色。

```
<button class="btn">按钮</button>
<ul id="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
</ul>

```


## for 循环

> 不断的重复做一件事。

```
for(初始化条件;条件的判断;条件的变化){
    循环体（当条成立的时候，依次执行这里面的代码）
}
```

1. 初始化条件：var i = 0;初始化条件在循环中只会执行一次。
2. 条件判断：例如：如果 i<5，那么条件成立了，就执行下一步。
3. 上面的条件成立，就执行循环体。
4. 执行完成循环体，会返回小括号中，按照设定好的规则进行变化 例如：i++
5. 当条件变化后，再去判断是否满足指定的条件，如果满足接着执行循环体，重复上面的 2、 3、 4 步骤
6. 如果条件改变后不再满足指定的判断条件，就结束当前循环，继续执行循环后面的代码。

```
for(var i=0; i<7; i++){
    console.log(i); // 0 1 2 3 4 5 6
}
console.log(i);  // 7
```

> 需求2：对需求1进行优化:使用for循环

```
btn.onclick = function (){
    // lis[0].style.background = 'red';
    // lis[1].style.background = 'red';
    // lis[2].style.background = 'red';
    // lis[3].style.background = 'red';
    // lis[4].style.background = 'red';
    for(var i = 0; i<lis.length; i++){
      lis[i].style.background = 'red';
    }
};
```

> 需求3：对需求1进行优化，添加隔行变色

```
<button class="btn">按钮</button>
<ul id="list">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
<script>
  var btn = document.querySelector('.btn');
  var lis = document.querySelectorAll('#list li');
  
  btn.onclick = function (){
    /*lis[0].style.background = 'red';
    lis[1].style.background = 'blue';
    lis[2].style.background = 'red';
    lis[3].style.background = 'blue';
    lis[4].style.background = 'red';*/
    var color;
    for(var i = 0; i<lis.length; i++){
      if(!(i % 2)){
        color = 'red';
      }else{
        color = 'blue';
      }
      lis[i].style.background = color;
    }
  };
  // if(0){
  //   alert(1);
  // }
</script>
```

> 需求4：向控制台打印下面数组中的每一项 1-12

```
<script>
var arr = [
  [1,2,3,4],
  [5,6,7,8],
  [9,10,11,12]
];

for(var i=0; i<arr.length; i++){
  //console.log(i);
  //console.log(arr[i]);
  for(var j=0; j<arr[i].length; j++){
    console.log(arr[i][j]);
  }
}

// for(var j=0; j<arr[0].length; j++){
//   console.log(arr[0][j]);
// }
//
// for(var j=0; j<arr[1].length; j++){
//   console.log(arr[1][j]);
// }
//
// for(var j=0; j<arr[2].length; j++){
//   console.log(arr[2][j]);
// }
</script>
```

*当for嵌套的时候，不能用同一个变量初始化。*

> 需求5：向数组的最前面添加一个数字0

```
<script>
  var arr = [1, 2, 3, 4];

  for(var i = arr.length; i>=0; i--){
    if(i){
      arr[i] = arr[i-1];
    }else{
      arr[i] = 0;
    }
  }

  /*arr[4] = arr[3];
  arr[3] = arr[2];
  arr[2] = arr[1];
  arr[1] = arr[0];
  arr[0] = 0;*/
  console.log(arr);
</script>
```

> 需求6：99乘法表

```
<head>
    <style>
    .box {
      border-left: 1px solid #000;
      border-bottom: 1px solid #000;
      width: 918px;
    }
    .box span {
      display: inline-block;
      border-top: 1px solid #000;
      border-right: 1px solid #000;
      text-align: center;
      width: 100px;
      height: 30px;
      line-height: 30px;
    }
    </style>
</head>
<body>
    <div class="box"></div>
    <script>
    var box = document.querySelector('.box');
    for(var i=1; i<=9; i++){
    for(var j=1; j<=i; j++){
      box.innerHTML += '<span>' + j + '*' + i + '=' + (i*j) + '</span>';
    }
    box.innerHTML += '<br />'
    }
    </script>
</body>
```

> 需求7：点击按钮动态生成1000个div，每个div里面的内容对应i的值。

```
<body>
  <input type="button" id="btn" value="按钮">
  <div id="box"></div>
  <script>
    var btn = document.getElementById('btn');
    var box = document.getElementById('box');
    btn.onclick = function (){
      // 不要这么写，性能不好
      /*for(var i=0; i<2000; i++){
        box.innerHTML += '<div>'+i+'</div>';
      }*/
      var str = '';
      for(var i=0; i<2000; i++){
        str += '<div>'+i+'</div>';
      }
      box.innerHTML = str;
    };
  </script>
</body>
```

> 需求8：点击生成10个div，横向依次排开。

```
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    #box {
      position: relative;
    }
    #box div{
      width: 100px;
      height: 100px;
      text-align: center;
      color: #fff;
      font: 20px/100px arial;
      position: absolute;
      background: red;
    }
  </style>
</head>
<body>
  <button class="btn">按钮</button>
  <div id="box"></div>
  <script>
    var btn = document.querySelector('.btn');
    var box = document.getElementById('box');
    
    // var flag = true;
    
    btn.onclick = function (){
      /*if(flag){
        var str = '';
        for(var i=0; i<10; i++){
          str += '<div style="left:'+(i*(100 + 10))+'px">'+i+'</div>'
        }
        box.innerHTML = str;
      }
      flag = false;*/
      
      if(box.innerHTML == ''){
        var str = '';
        for(var i=0; i<10; i++){
          str += '<div style="left:'+(i*(100 + 10))+'px">'+i+'</div>'
        }
        box.innerHTML = str;
      }
      
    };
  </script>
</body>
```

> 需求9:点击按钮生成10*10个div，组成一个方阵，要求div的颜色为红黄蓝绿依次排列。

```
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    #box div {
      width: 50px;
      height: 50px;
      border: 1px solid #000;
      position: absolute;
      text-align: center;
      color: #000;
      font: 20px/50px arial;
    }
  </style>
</head>
<body>
  <div id="box"></div>
  <script>
    var box = document.getElementById('box');
    
    var colors = ['red', 'yellow', 'blue', 'green'];
    
    var str = '';
    for(var i=0; i<100; i++){
      str += '<div style="left:'+(i%10 * 55)+'px;top:'+((i/10 + '')[0] * 55)+'px;background:'+colors[i%colors.length]+';">'+i+'</div>';
    }
    box.innerHTML = str;
    
    // 生成100个div
    /*var str = '';
    for(var i=0; i<100; i++){
      str += '<div>'+i+'</div>';
    }
    box.innerHTML = str;
    
    var divs = box.getElementsByTagName('div');
    var t = 0;
    for(var i=0; i<divs.length; i++){
      // console.log(i%10); // 0 - 9 循环
      divs[i].style.left = i%10 * 55 + 'px';
      divs[i].style.background = colors[i % colors.length];
      if(i%10 == 0){
        t++;
      }
      divs[i].style.top = (t - 1) * 55 + 'px';
    }*/
  </script>
```

> 需求10：用5个div拼成一个V字，要求动态生成。

```
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <style>
    #box div {
      width: 100px;
      height: 100px;
      background: red;
      position: absolute;
      color: #000;
      font: 40px/100px arial;
      text-align: center;
    }
  </style>
  <script>
    window.onload = function (){
      /**
       * i   l      t
       * 0   0      0
       * 1   100    100
       * 2   200    200
       * 3   300    100
       * 4   400    0
       */
      
      var box = document.getElementById('box');
      var num = 9;
      var str = '';
      var t = 0;
      for(var i=0; i<num; i++){
        if(i < num/2){
          t = i*100;
        }else{
          t = (num - i -1) * 100;
        }
        str += '<div style="left:'+(i*100)+'px;top:'+t+'px;">'+i+'</div>';
        /*console.log(t);
        str += '<div style="left:'+(i*100)+'px;top:'+(t*100)+'px;">'+i+'</div>';
        if(i < 2){
          t++;
        }else{
          t--;
        }*/
      //  console.log(t);
      }
      box.innerHTML = str;
    };
  </script>
</head>
<body>
  <div id="box">
    <div style="left:0;top:0;">0</div>
    <div style="left:100px;top:100px;">1</div>
    <div style="left:200px;top:200px;">2</div>
    <div style="left:300px;top:100px;">3</div>
    <div style="left:400px;top:0px;">4</div>
  </div>
</body>
```

## 对for循环的补充

- break：当条件成立，结束当前循环
- continue：当条件成立，结束本次循环，继续下一次。

> 一般与判断条件配合使用

```
<script>
    /*for(var i=0; i<10; i++){
      if(i%2){ // 当 i = 1的时候 条件成立 执行 break 结束本次循环
        break;
      }
      console.log(i);
      // break;
    }*/
    var arr = [1,2,3,4,5,6];
    
    var n =0;
    
    for(var i=0; i<arr.length; i++){
      if(arr[i] == 3){
        console.log(arr[i]);
        break;
      }
      n++;
    }
    console.log(n);
</script>
```

```
<script>
  for(var i=0; i<10; i++){
    if(i%2){ // 当 i = 1的时候 条件成立 执行 break 结束本次循环
      continue;
    }
    console.log(i);
    // break;
  }
</script>
```


