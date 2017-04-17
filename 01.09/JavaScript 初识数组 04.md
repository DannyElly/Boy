# JavaScript 初识数组 04

标签（空格分隔）： JS

---

## 数组的基本概念

**什么是数组**

> 是一种储存数据的有序列表，并且每个数据可以被索引，与一次只能存储一个数据的变量不同，数组可以存储“任意”多个数据，而且可以使任意类型的数据。


**创建数组：**

```
var arr = []; // 创建数组

var arr2 = ['a','b','c','d','e'];

```

**使用数组：**

|0|1|2|3|4|
|:---:|:---:|:---:|:---:|:---:|
|'a'|'b'|'c'|'d'|'e'|

> 可以通过索引值（下标）的方式取到数组中对应的数据。

```
var arr = ['a','b','c','d','e'];

console.log(arr[2]); // 'c';
console.log(arr[0]); // 'a';
```

**数组的属性**

> 数组.length，可以获取到数组的长度，并且可读可写，当设置length属性的时候，如果小于原来的长度，那么就会截去多余的部分，如果大于原来的长度，默认以undefinied进行填充。

```
var arr = ['a','b','c','d','e'];

console.log(arr.length); 
```

如果想直接拿到数组的第一位那么使用arr[0]，如果想直接拿到数组的最后一位，那么使用arr[arr.length - 1];

**增加和修改数组的元素：**

- 数组的长度（length属性）会随着数组的增加或减少动态的改变。
- 数组的修改方法：直接用  数组[下标] = 新的值。

```
<script>
    var arr = ['a','b','c','d','e'];
    // 增加数组的数据
    /*arr[5] = '123';
    alert(arr[5]);
    console.log(arr);*/
    // arr[arr.length] = 新的值; 向数组中最后的位置后面添加一个新的数组
    
    /*arr[arr.length] = 1;
    console.log(arr.length);
    arr[arr.length] = 2;
    console.log(arr.length);
    arr[arr.length] = 3;
    
    console.log(arr.length);
    console.log(arr);*/
    
    // 数组的修改方法：直接用  数组[下标] = 新的值
    arr[0] = 'A';
    console.log(arr);
</script>
```

**删除数组的元素**

> 通过 delete 数组[对应的下标];

通过delete可以删除数组里面的数据，删除后数据变为undefeined

```
<script>
    var arr = ['a','b','c','d','e'];
    delete arr[2];
    console.log(arr); // ['a','b',undefined,'d','e'];
</script>
```

## 数组中的数组

> 进一步理解数据，可以储存任意数据类型，包括数组本身。

```
<script>
// var arr = [[1,2,3,4],['a','b','c'],100,400];
var arr = [[1,2,3,4],['a','b',['c','arr','abc']],100,400];
console.log(arr[1][2][2]);
</script>
```

## 为什么使用数组？

**以图片切换的案例为例：**

```
<button id="prev">上一张</button><button id="next">下一张</button>
<img id="img" src="images/loading.gif" width="600"/>
<script>
	
	var prev = document.getElementById('prev');
	var next = document.getElementById('next');
	var img = document.getElementById('img');
	
	var n = 0;
	
var arrImg = ['asd123.jpg','asdasdg.jpg','gsdfsd.jpg','rtert.jpg'];

imgTab();

function imgTab(){
img.src = 'images/' + arrImg[n];
}

next.onclick = function (){
n++;
if(n > arrImg.length - 1){
  n = 0;
}
console.log(n);
imgTab();
};

prev.onclick = function (){
n--;
if(n < 0){
  n = arrImg.length -1;
}
console.log(n);
imgTab();
}
</script>
```

## 对数组的总结

- 数组就是一种数据格式
- 数组中的每个数据都是可以被索引的，并且索引值是从0开始的。
- 数组具有length属性，代表数组的长度，并且这个属性可读可写。
- 数组可以动态的添加和删除或者修改对应的数据，同时其长度也会动态的跟着改变。





