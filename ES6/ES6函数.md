# ES6函数扩展

## :blue_book:函数参数默认值

### ES6指定默认参数

```javascript
function log1(x,y="xiaohuang!"){
  return x + y;
}
console.log(log1("hello"));
console.log(log1("hello",""));
console.log(log1("hello","world"));
console.log(log1("hello",undefined));
console.log(log1("hello",null));
//输出结果依次为：
//helloxiaohuang!
//hello
//helloworld
//helloxiaohuang!
//hellonull
```

### ES6函数默认参数与解构赋值

```javascript
function log2({x,y}) {
  console.log(x+y);
}
log2({x:"xiao",y:"huang"});
log2({x:"xiao"});
log2({y:"huang"});
log2({});
//输出结果依次为：
//xiaohuang
//xiaoundefined
//undefinedhuang
//NaN
```

### 两种写法

```javascript
function log3({x=0,y=0}) {
  console.log(x,y);
}

function log4({x,y}={x:0,y:0}) {
    console.log(x,y);
}
log3({ x: "xiao", y: "huang" });
log3({ x: "xiao" });//y为默认值
log3({ y: "huang" });
log3({});//x,y均为默认值
//输出结果：
// xiao huang
// xiao 0
// 0 'huang'
// 0 0

log4({ x: "xiao", y: "huang" });
log4({ x: "xiao" });//y为undeifined
log4({ y: "huang" });//x为undefined
log4({});//x,y均为undefined
//输出结果：
// xiao huang
// xiao undefined
// undefined 'huang'
// undefined undefined

```

### ES6函数参数的位置

```javascript
function log5(x = 1 ,y) {
    console.log(x,y);
  };
  //log5(,1);此种情况报错
  log5(1);//1,undefined
  log5(1,2);//1,2
  log5(undefined,2);//1,2

```

### ES6 函数length属性

**设置了默认参数的函数的length属性将失真**

```javascript
console.log((function a(x, y) { }).length);//2
console.log((function a(x , y = 1) {}).length);//1
//默认参数不是为函数，后面的参数也不计入length属性
console.log((function a(x = 1 , y ) { }).length);//0
//rest参数不计入length属性
console.log((function a(...args) { }).length);//0
```

### 作用域

**当函数参数设置了默认值，在函数声明初始化的时候，参数就会形成单独作用域，改作用域直到初始化结束消失，不设置函数参数默认值不会出现该情况**

```javascript
//案例一
var x = 1;
function f(x,y=x) {
  console.log(y);
}
f(2);//2 x赋值为2，y赋值为x,x=2,y=2.y指向参数x

f()//1，调用时未赋值，所以取到全局变量x x = 1,y = x,y = 1，若此时不声明全局变量则报错
//在本例中，函数设置了参数默认值y，调用f时参数形成了单独的作用域，此时x指向参数x，所以输出2

//下面这种情况也会报错
// var x = 1;
// function f(x = x) {
//   console.log(x);
// }//此时相当于let x = x;出现暂时性死区（x未赋值就调用）

//案例二
let foo = "outside";
function g(func = x=>foo ) {
  let foo  = "inner";
  console.log(func());
};
g();//outside
//此例中g函数参数func为匿名函数，返回值为foo,当调用函数g,函数参数形成单独作用域，该作用域内不存在foo,所以调用全局变量foo,输出结果为outside
//此时不声明foo将报错


// let foo = "outside";
// function g(func = x => foo) {
//   foo = "inner";
//   console.log(func());
// };
// g();//inner
//这里因为函数内部foo指向函数参数foo，所以返回inner


//案例三
var x ="out";
function m(x,y=function(){x = 2;}) {
  var x = "in";
  y();
  console.log(x);
}
m();//in
//在本例中，m函数调用时参数形成单独作用域，改作用域中的x和函数内部的x不是同一个，所以输出的是函数内部的x
```

## :blue_book:rest参数

**形式为（...变量名）**

```javascript
function add(...args){
    let count = 0;
    for( var val of args){
        count+=val;
    }
    return count;
}
console.log(1,2,3);//6
```

## :blue_book:严格模式

+ 在ES6中如果函数设置了参数默认值，解构赋值，扩展运算符，函数内部就不能显示声明严格模式，否则报错

  **可用以下两种方法避免此限制**

  + 在全局模式下时声明严格模式

    ```javascript
    'use strict'
    function(){
        
    }
    ```

  + 在无参数立即调用函数内声明

    ```javascript
    const strictFunc = (funcion(){
                        return function(){
        
    }
                        })()
    ```

## :blue_book:name属性

+ 匿名函数赋值给变量返回实际函数名

  ```javascript
  //ES6
  let f = function(){};
  f.name;//"f"
  
  //ES5
  let f = function(){};
  f.name;//""
  
  ```

### :blue_book:箭头函数

