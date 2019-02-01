# let&const

[TOC]



#### 1）不能重复声明

使用var声明的变量可以重复声明且后声明的变量覆盖先声明的变量

let,const不可以重复声明。

~~~javascript

var a = 1;
var a = 2;
console.log(a);//2

let a = 1;
let a = 2;
console.log(a);//报错，a is undefined


~~~



#### 2）不存在变量提升

使用var声明的变量存在变量提升

let,const不存在变量提升

~~~javascript
console.log(a)//undefined
var a = 1;

console.log(a)//报错
let a = 1;
~~~



#### 3）暂时性死区（temporal dead zone，简称 TDZ）

在使用let变量声明之前使用变量都不可用

~~~javascript
{
    console.log(a)；//报错
    let a = 1;
}

~~~



#### 4）块级作用域

ES6新增了块级作用域

**没有块级作用域会发生什么**

+ for语句中的循环变量变为全局变量，在循环结束后任然存在在内存中

~~~javascript
//ES5
var a =[];
for(var i=1;i<5;i++){
    a[i]=function(){
        console.log(i);//5
    };
}
a[2]();//5
console.log(i);//5

//ES6
var a =[];
for(let i=1;i<5;i++){
    a[i]=function(){
        console.log(i);
    };
}
a[2]();//2
console.log(i);//报错
~~~

**注意事项**

+ 外层变量无法调用内层变量

  ~~~javascript
  {
      {
          let i = 1;
      }
      console.log(i);//报错
  }
  ~~~

+ 内层作用域可以定义与外层作用于相同的同名变量

  ~~~javascript
  {let a = 1;
      {
      let a = 2;
      console.log(a);//2
  	}
  }
  ~~~
