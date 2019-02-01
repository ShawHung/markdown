# JavaScript数值类型转换

[TOC]



### 1) Number()

​	**1.**使用Number()转化**基本类型值**

~~~JavaScript
//1.字符串可以被解析成数值转化为数值，字符串不能解析为数值转化为NaN
console.log(Number（"123"));//123
console.log(Number("123abcd"));//NaN

//2.空字符串转化为0，布尔值true转化为1，false转化为0，null转化为0，undefined转化为NaN
console.log(Number(""));//0
console.log(Number(true));//1
console.log(Number(false));//0
console.log(Number(null));//0
console.log(Number(undefined));//NaN

//parseInt()方法和Number()方法都会忽略前置空格和后置空格
~~~

​	**2.**使用Number()转化**对象**

~~~javascript
//除了包含单个数值的数组均转化为NaN
console.log(Number({a:1}));
console.log(Number([1,2,3]));
console.log(Number([1]));

//转化规则是
//1.调用对象的valueOf()方法，若转化为基本类型按照基本类型的规则来转换
//2.若第一步转化后为对象，调用toString()方法。按照字符串转化规则转化
//3.第二步若为对象，则报错
//toString()方法和valueOf()方法可以重写

console.log(Number({}));//NaN
//对于上述代码
//1.valueOf()方法返回对象本身
//2.toString()方法返回[object,Object]
//3.使用Number()转化为NaN

//重写valueOf()方法和toString()方法

//重写valueOf()方法
console.log(Number({
    valueOf:function(){
    	return 1;
}
}));//1

//重写toString()方法
console.log(Number({
    toString:function(){
        return 2;
    }
}));//2

//两个方法优先级
console.log(Number(
  valueOf: function () {
    return 2;
  },
  toString: function () {
    return 3;
  }
));//2
//valueOf()方法优先级高于toString()


~~~



### 2) String()

​	**1.**转化基本类型值

~~~javascript
//数字转化为数字字符串
console.log(String(123)); // "123"

//字符串保持字符串形式
console.log(String('abc')); // "abc"

//布尔值true转化为字符串"true",布尔值false转化为字符串"false"
console.log(String(true)) // "true"
console.log(String(false));//false

//undefined转化为字符串"undefined"
console.logString((undefined));// "undefined"

//null转化为字符串"null"
console.logString((null));// "null"
~~~

​	**2.**转化对象

~~~javascript
//转化规则是
//1.调用对象的toString()方法，若转化为基本类型按照基本类型的规则来转换
//2.若第一步转化后为对象，调用valueOf()方法。按照字符串转化规则转化
//3.第二步若为对象，则报错
//toString()方法和valueOf()方法可以重写

//重写valueOf()方法
console.log(Number({
    valueOf:function(){
    	return 1;
}
}));//1

//重写toString()方法
console.log(Number({
    toString:function(){
        return 2;
    }
}));//2

//两个方法优先级
console.log(Number(
  valueOf: function () {
    return 2;
  },
  toString: function () {
    return 3;
  }
));//3
//toString()方法优先级高于valueOf()方法
~~~



### 3) Boolean()

转换规则是除了以下五种转化为false，其他均转化为true

 	1. **undefined**
 	2. **null**
 	3. **+0**和**-0**	
 	4. **NaN**
 	5. **空字符串""**



### 4) 其他注意事项



+ 自动转化为布尔值（比如if语句），规则同Boolean()

+ **"+"**加号运算符运算中若一个值为字符串，后一个值转化为字符串

  ~~~javascript
  '5' + 1 // '51'
  '5' + true // "5true"
  '5' + false // "5false"
  '5' + {} // "5[object Object]"
  '5' + [] // "5"
  '5' + function (){} // "5function (){}"
  '5' + undefined // "5undefined"
  '5' + null // "5null"
  ~~~

+ 一元运算符和除了加号运算符之外的运算符会将运算子转化为数值

  ~~~javascript
  '5' - '2' // 3
  '5' * '2' // 10
  true - 1  // 0
  false - 1 // -1
  '1' - 1   // 0
  '5' * []    // 0
  false / '5' // 0
  'abc' - 1   // NaN
  null + 1 // 1
  undefined + 1 // NaN
  
  +'abc' // NaN
  -'abc' // NaN
  +true // 1
  -false // 0
  ~~~
