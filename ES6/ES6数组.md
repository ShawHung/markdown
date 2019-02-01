# ES6数组

## :book:扩展运算符

**相当于rest（...）的逆运算，用于将数组展开成逗号分隔的参数序列**

**作用：**

+ 替代数组apply方法

+ 通过push方法将另外一个数组添加到另外一个数组后面

+ 合并数组

+ 解构赋值(扩展运算符只能放在最后)

+ 将字符串转化成数组

+ 其他作用

```javascript
  function f(x,y,z) {
    console.log(x+y+z);
  }
  f.apply(null,array);
  f(...array);
  
  console.log("apply方法："+Math.max.apply(null,[3,5,8]));
  console.log("扩展运算符："+Math.max(...[3, 5, 8]));
  
  
  //通过push方法将另外一个数组添加到另外一个数组后面
  var arr1 = [1,2,3];
  var arr2 = [2,3,4];
  arr1.push(...arr2);
  console.log("push之后:" + arr1); //push之后:1,2,3,2,3,4
  
  
  console.log(new Date(...[2018,12,28]));
  
  
  //合并数组
  var arr1 = [1, 2, 3];
  var arr2 = [2, 3, 4];
  var newArr = [...arr1,...arr2];
  console.log("拼接后新数组:" + newArr); //拼接后新数组:1,2,3,2,3,4
  
  //解构赋值(扩展运算符只能放在最后)
  const [a,...rest] = [1,2,3,4];
  console.log("a的值是:" + a); //a的值是:1
  console.log("rest的值是:" + rest); //rest的值是:2,3,4
  
  const [x,...y] = [];
  console.log("x的值是:" + x); //x的值是:undefined
  console.log("y的值是:" + y); //y的值是:
  
  //将字符串转化成数组
  const str = [..."hello"];
  console.log("转化后:"+str);
  
  //将类数组转化为数组
  
  //1.nodeList集合
  [...document.querySelector("p")];
  
  //arguements对象
  function foo(){
      var args = [...arguments];
      //...do sonmething
  }
  
```

## :book:Array.from()

**用于将类数组转化为数组**

```javascript
let arrLike = {
  0:1,
  1:2,
  2:3,
  length:3
};

//ES5写法
let arr1 = [].slice.call(arrLike);
console.log("ES5写法:"+arr1);
//ES6写法
let arr2 = Array.from(arrLike);
console.log("ES6写法:" + arr1);
//类数组元素
console.log(Array.from({length: 4})); //[ undefined, undefined, undefined, undefined ]


//NodeList集合
let ps = document.querySelector("p");
Array.from(ps).forEach(function(p){
    console.log(p);
})

//arguements对象
function foo(){
    var args = Array.from(arguements);
    //...do something
}

//转化字符串
console.log(Array.from("hello"));//["h","e","l","l","o"]

//类数组元素
console.log(Array.from({length: 4})); //[ undefined, undefined, undefined, undefined ]


```

**接受第二个参数，类似于map，对数组进行处理**

```javascript
function typesOf(){
    return Array.from(arguments,value=>typeof value);
}
typesof([1,"hello",[],{}]);//number,string,object,object
```

## :book:Array.of()

**用于将一组值转化为数组**

```javascript
Array.of(3);//[3]
Array.of();//[]



console.log("数组是："+Array.of(3));//[3]
console.log("长度是："+Array.of(3).length); //1
//和Array的不同是参数个数的不同带来的差异
console.log("数组是："+Array(3));//[,,]
console.log("长度是："+Array(3).length); //3

console.log("数组是："+Array.of(1, 23, 3));//[1,23,3]
console.log("长度是："+Array.of(1, 23, 3).length);//3

console.log("数组是："+Array(1, 23, 3));//[1,23,3]
console.log("长度是："+Array(1, 23, 3).length);//3

console.log("数组是："+Array.of());//0
console.log("长度是："+Array.of().length);//0

//实现

function ArrOf() {

  return [].slice.call(arguments);

}

console.log(ArrOf(1,2));


```

## :book:copyWithin()方法

**用于将数组内部指定位置的成员复制到指定位置并覆盖，该方法会修改原数组**

```javascript
let arr = [1,2,3,4,5];

//演示复制数组第二个位置到第一个位置
let newArr1 = arr.copyWithin(0,1,2);
console.log("新数组："+newArr1); //[ 2, 2, 3, 4, 5 ]
console.log("原数组：" + arr); //[ 2, 2, 3, 4, 5 ]

//如果第二第三个参数为负值则从倒数开始计算
//演示数组第二位到数组第三位替换数组第一位
let newArr2 = arr.copyWithin(0, -3, -2);
console.log("新数组：" + newArr2); //[ 3, 2, 3, 4, 5 ]
console.log("原数组：" + arr); //[ 3, 2, 3, 4, 5 ]
//省略第三个参数则是从第二个参数到数组尾部
//演示复制数组1到4位从0好位置开始替换
let newArr3 = arr.copyWithin(0, 1);
console.log("新数组：" + newArr3); //[ 2, 3, 4, 5, 5 ]
console.log("原数组：" + arr); //[ 2, 3, 4, 5, 5 ]
```

## :book:find()方法和findIndex()方法

+ **find()方法接受一个回调函数作为参数，对每一个数组成员运行回调函数直到找到第一个返回值为true的成员**
+ **findIndex()方法接受一个回调函数，对每一个数组成员运行回调函数直到找到第一个返回值为true的成员的索引**
+ **回调函数接受三个参数(分别为当前值，当前位置，原数组)**
+ **两种方法均接受第二个参数用于绑定回调函数的this对象**
+ **两种方法可以识别NaN，弥补了indexOf（）方法的不足**

```javascript
let arr = [1,-5,3,-6,8];

let arr1 = arr.find(function(value,index,arr){
  return value < 0;
});
console.log(arr1);//-5

let arr2 = arr.findIndex(function (value, index, arr) {
  return value < 0;
});
console.log(arr2);//1
```
## :book:fill()方法

**fill()方法用于使用给定值填充数组，原数组会被覆盖**

```javascript
let arr = [1,2,3];

let newArr = arr.fill(7);
console.log("新数组：" + newArr); //新数组：7,7,7
console.log("原数组：" + arr); //原数组：7,7,7


//接受第二和第三个参数表示填充的开始位置和结束位置

let arr1 = [1, 2, 3];

let newArr1= arr1.fill(7,1,2);
console.log("新数组：" + newArr1); //新数组：1,7,3
console.log("原数组：" + arr1);//原数组：1,7,3

```

## :book:keys(),values()，entries()

+ **keys()返回键名**

+ **values()返回键值**

+ **entires()返回键值对**

```javascript
  let arr = [1,2,3];
  for (let index of arr.keys()){
    console.log("键名："+index);
  }
  // 键名： 0
  // 键名： 1
  // 键名： 2
  for (let value of arr.values()) {
    console.log("键值：" + value);
  }
  // 键值： 1
  // 键值： 2
  // 键值： 3
  for (let [index,value] of arr.entries()) {
    console.log("[键名:" + index+"键值："+value+"]");
  }
  // [键名: 0 键值： 1]
  // [键名: 1 键值： 2]
  // [键名: 2 键值： 3]
```


## :book:includes()

**用于判断数组是否包含某个值，接受两个参数，第一个参数表示给定值，第二个参数表示搜索起始位置，返回一个布尔值**

```javascript
let arr = [1,3,4,5];

let result1 = arr.includes(1);
console.log("返回值：" + result1); //返回值：true

let result2 = arr.includes(8);
console.log("返回值：" + result2); //返回值：false

let result3 = arr.includes(1,0);
console.log("返回值：" + result3); //返回值：true


let result4 = arr.includes(1,3);
console.log("返回值：" + result4); //返回值：falses
```

## :book:数组空位

**在ES6中数组空位处理为undefined**



