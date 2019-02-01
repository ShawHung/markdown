# ES6 Symbol

[TOC]



## <code>Symbol</code>概述

+ <code>Symbol</code>是一种基本数据类型，可以解决对象属性名冲突问题。Symbol值是独一无二的。

+ <code>Symbol</code>值通过<code>Symbol</code>函数生成,symbol是基本数据类型，所以不能使用new操作符来创建。

  ```javascript
  let sy = Symbol();
  console.log(typeof(sy));//symbol
  ```

+ 若<code>Symbol</code>参数是一个字符串，输出时是<code>"Symbol("string")"</code>形式。

  ```javascript
  let sy1 = Symbol("hello");
  let sy2 = Symbol("world");
  console.log(sy1);//Symbol(hello)
  console.log(sy2);//Symbol(world)
  ```

+ 若<code>Symbol</code>函数参数是一个对象，会调用该对象的toString()方法转化为字符串后生成<code>Symbol</code>值。

  ~~~javascript
  let obj1 ={
    name:"xiaohuang",
  }
  let a1 = Symbol(obj1);
  console.log(a1); //Symbol([object Object])
  
  
  let obj2 = [1],
  let a2 = Symbol(obj2);
  console.log(a2);//Symbol(1)
  ~~~

+ <code>Symbol</code>函数接受相同参数返回值不同

  ```javascript
  var sy1 = Symbol();
  var sy2 = Symbol();
  console.log(sy1 === sy2);//false
  
  
  var sy1 = Symbol("hello");
  var sy2 = Symbol("hello");
  console.log(sy1 === sy2);//false
  ```

+ <code>Symbol</code>值可以转换成字符串和<code>Boolean</code>但是不能转化为数值。且<code>Symbol</code>值不能与其他类型进行运算。



## symbol作为属性名

+ 由于<code>Symbol</code>值的唯一性，可保证对象属性名的唯一性

+ <code>Symbol</code>值作为属性名有以下三种方式定义。

  ~~~javascript
  var s = Symbol();
  var obj = {},
  //方法一
  obj[s] = "hello";
  
  //方法二
  var obj = {
      [s]:"hello",
  }
  
  //方法三
  Object.defineProperty(obj,s,{value:"hello"});
  console.log(obj[s]);//hello
  ~~~

+ <code>Symbol</code>值作为对象属性名不能使用点操作符，因为点操作符后面是字符串，导致属性名会是字符串而不是<code>Symbol</code>值。**所以使用<code>Symbol</code>值定义对象时必须放在方括号内**

  ~~~javascript
  var s = Symbol();
  var obj = {},
  //方法一
  obj.s = "hello";
  console.log(obj[s]);//undefined
  console.log(obj["s"]);//hello
  ~~~

## 消除魔术字符串

魔术字符串是指在代码中多次出现的字符串或数值，应该避免魔术字符串的出现。使用<code>Symbol</code>值就很好消除魔术字符串。因为不会与其他只产生冲突。



## 属性名的遍历

+ <code>Symbol</code>值作为属性不能被<code>for...in,for..of，Object.getOwnPropertyNames()</code>返回

+ 可以使用<code>Object.getOwnPropertySymbols()</code>方法获取到所有的<code>Symbol</code>值属性。返回值是一个数组。

  ```javascript
  var s1 = Symbol('hello');
  var s2 = Symbol('world');
  var obj = {};
  
  obj[s1] = 'hello';
  obj[s2] = 'world';
  obj.name = 'xiaohuang';
  obj.age = 21;
  
  var res1 = Object.getOwnPropertySymbols(obj);
  console.log(res1); //[ Symbol(hello), Symbol(world) ]
  
  var res2 = Object.getOwnPropertyNames(obj);
  console.log(res2); //[ 'name', 'age' ]
  
  for(key in obj){
    console.log(key);
  }//name age
  
  
  for (key of Object.keys(obj)) {
    console.log(key);
  }//name age
  
  
  ```

+ 使用<code>Reflect.ownKeys()</code>返回所有类型的键名，包括SYmbol类型和其他类型。

  ~~~javascript
  var res3 = Reflect.ownKeys(obj);
  console.log(res3); //[ 'name', 'age', Symbol(hello), Symbol(world) ]
  ~~~

+ 可以利用这个特性创造非私有但仅对象内部可用的属性。



## Symbol.for()和Symbol.keyfor()方法

+ <code>**Symbol.for():**</code>方法用于创建同<code>Symbol</code>值。接受一个字符串作为参数，若无以该参数作为名称的<code>Symbol</code>值，则新创建一个，若存在就返回该值。和<code>Symbol</code>函数区别是<code>Symbol.for()</code>会在全局环境中登记，即不会重复创建，若存在给定key的<code>Symbol</code>值，会返回该值，而<cods>Symbol</code>会重新创建。

  ~~~javascript
  let s1 = Symbol.for("hello");
  let s2 = Symbol.for("hello");
  console.log(s1 === s2);//true
  
  
  let s1 = Symbol("hello");
  let s2 = Symbol("hello");
  console.log(s1 === s2);//false
  
  ~~~

+ <code>Symbol.keyFor()</code>方法返回一个已经登记的<code>Symbol</code>值的key

  ~~~javascript
  let s1 = Symbol.for("hello");
  console.log(Symbol.keyFor(s1));//"hello"
  
  let s1 = Symbol("hello");
  console.log(Symbol.keyFor(s1));//undefined
  ~~~
