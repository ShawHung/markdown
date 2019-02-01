# ES6函数声明与块级作用域

**一个例子的解析**

根据阮一峰老师教程：

- 允许在块级作用域内声明函数。
- 函数声明类似于`var`，即会提升到全局作用域或函数作用域的头部。
- 同时，函数声明还会提升到所在的块级作用域的头部。

**考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。**

**eg1"**

~~~javascript
function f() {
  console.log("outside");
}

(function () {
  if(false){
    function f() {
      console.log("inside");
    }
    f();
  }
  f();
}());
~~~

+ 在ES5环境下上例解析成如下代码（**如果是严格模式则报错，因为ES5严格模式不允许在代码块内部声明函数**）

  ~~~javascript
  function f() {
    console.log("outside");
  }
  
  (function () {
   function f() {
        console.log("inside");
      }
   if(false){
   	 f();
    }
    f();
  }());//inside inside
  ~~~

+ 在ES6环境下

+ **ES6非严格模式下函数提升到外围函数或者全局环境的顶部，严格模式下提升到代码块顶部**

  + false
  + true
  + false+'use strict'
  + true+'use strict'

  **false**

  ~~~javascript
  function f() {
    console.log("outside");
  }
  
  (function () {
    if(false){
      function f() {
        console.log("inside");
      }
      f();
    }
    f();
  }());
  
  //相当于
  function f() {
    console.log("outside");
  }
  
  (function () {
    var f = undefined;
    if (false) {
      function f() {
        console.log("inside");
      }
      f();
    }
    f();
  }());//报错
  ~~~

  **true**

  ~~~javascript
  function f() {
    console.log("outside");
  }
  
  (function () {
    if (true) {
      function f() {
        console.log("inside");
      }
      f();
    }
    f();
  }());//inside inside
  
  //相当于
  function f() {
    console.log("outside");
  }
  
  (function () {
    var f = undefined;
    if (true) {
      function f() {
        console.log("inside");
      }
      f();
    }
    f();}());//inside inside
  ~~~

  **false+'use strict'**

  ~~~javascript
  function f() {
    console.log("outside");
  }
  
  (function () {
    'use strict'
    if (false) {
      function f() {
        console.log("inside");
      }
      f();
    }
    f();
  }());//outside
  ~~~

  **true+'use strict'**

  ~~~javascript
  function f() {
    console.log("outside");
  }
  
  (function () {
    'use strict'
    if (true) {
      function f() {
        console.log("inside");
      }
      f();
    }
    f();}());//inside outside
  ~~~
