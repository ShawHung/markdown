# ES6 Generator	

## :book:Generator是什么

是ES6提出来的异步编程解决方案。可以理解为一个状态机，封装了多个内部状态，执行Generator函数返回一个遍历器对象，返回的遍历器对象可以依次遍历Generator函数内部的每一个状态。



## :book:如何创建一个Generator函数

+ 和普通函数创建不同，需要在function关键字和函数名之间加上<code>*</code>符

+ Generator函数函数体内使用yield语句定义不同的状态

+ 调用该函数的方式和调用普通函数相同

  + **不同的是Generator函数调用后不会执行，也不会返回函数执行结果，而是返回一个遍历器对象，指向函数内部的状态**	
  + **使用遍历器的next方法可以使指针指向内部下一条状态，每次调用next方法直到遇到yield语句或者return语句才会停止执行。也就是Generator函数是分段执行的**

  ~~~javascript
  function *helloGenerator(){
      yield "hello"
      yield "Generator"
      return "bye"
  }
  
  var gen1 = helloGenerator()
  //并不会返回函数执行结果，而是返回一个遍历器对象
  
  gen1.next()////{value:hello done:false}//直到遇到第一条yield语句未知，返回一个对象，value值是yield语句的值
  gen1.next()////{value:Generator done:false}
  gen1.next()////{value:bye: done:true}//遍历结束
  gen1.next()////{value:undefined done:false}//以后调用next方法均返回该值。
  
  ~~~



## :book:yield语句

**因为Generator函数返回的遍历器对象调用next方法才会遍历下一个状态，yield语句就是暂停标志，使遍历暂时停止**

**next方法工作逻辑**

+ 遇到yield语句，先暂时停止执行后续操作，并将yield语句表达式的值作为返回对象的value属性值

+ 如果没有遇到新的yield语句，就运行到函数结束，直到遇到return语句，并将return语句表达式的值作为返回对象的value属性值

+ 如果没有return语句，对象的value值为undefined

+ 在Generator函数中可以不使用yield语句，但是不可以再普通函数中使用yield函数。且如果需要在另一个语句中使用yield函数，需要用括号括起来

  ~~~javascript
  function* demo(){
      //console.log("hello"+yield "world")//wrong
   	console.log("hello"+(yield "world"))//yes   
  }
  ~~~

+ yield语句也可以作为函数参数或者赋值表达式右边而不加括号使用

  ~~~JavaScript
  function* demo(){
      func(yield 'a',yield 'b')
      let foo = yield 
  }
  ~~~




**:heavy_check_mark:只有调用了next方法才会执行yield语句表达式，即“惰性求值”**

~~~javascript
function* hello(){
    yield "hello"
}
~~~

**上面代码中yield语句后的表达式并不会马上执行，而是会在next方法指针指向该语句时才会执行**



**:heavy_check_mark:return语句与yield语句的异同**

+ 相同之处是都能返回语句后表达式的值
+ 不同之处是return语句不具有记忆性，且只能在一个函数里执行一次。yield语句可以执行多次，并可以暂停执行，执行完当前yield语句后表达时候继续执行下一条



## :book:与iterator接口关系

+ 可以通过把Generator函数赋值给对象的Symbol.iterator属性使对象具有iterator接口（可遍历）（因为Generator函数返回一个遍历器对象，是遍历器对象生成函数）
+ Generator函数执行后返回的遍历器对象也具有Symbol.iterator属性，该属性返回该对象本身





## :book:next()方法参数

**对next方法传入参数会作为上一条yield语句的返回值**

~~~javascript
function* model(x){
   let a = yield x
   let b = yield (a+x)
   return (a+b+x)
}

let mod = model(1)
//不加参数
console.log(mod.next())
console.log(mod.next())
console.log(mod.next())
// { value: 1, done: false }
// { value: NaN, done: false }
// { value: NaN, done: true }

//加参数
console.log(mod.next())
console.log(mod.next(2))
console.log(mod.next(3))
// { value: 1, done: false }
// { value: 3, done: false }
// { value: 6, done: true }
~~~

**但是传入的参数不能作为第一个next方法的传入值**



## :book:for...of循环

**可以使用for...of循环自动遍历Generator函数生成的遍历器对象，从而不需要调用next方法**

~~~javascript
function* model(){
  yield 1
  yield 2
  yield 3
  return 4
}

for(let val of model()){
  console.log(val);//1,2,3
}
~~~

**一旦遍历器对象的done状态（return）为true，for...of就会立刻停止遍历**



**:heavy_check_mark:除了for...of循环，扩展运算符，解构赋值，Array.from()都是内部调用遍历器接口，说明其可以将GEnerator函数返回的遍历器对象作为参数**

~~~javascript
function* model() {
  yield 1
  yield 2
  yield 3
  return 4//此处done为true,所有遍历到这里停止
  yield 5
}

//扩展运算符
console.log([...model()]) //[ 1, 2, 3 ]

console.log(Array.from(model()))//[1,2,3]
let [x, y, z, m] = model()

console.log([x, y, z, m]) //[ 1, 2, 3, undefined ]
~~~





## :book:yield*语句

**用于在一个Generator函数内调用另外一个Generator函数**

~~~javascript
//yield*
function* model1(){
  yield 1
  yield 2
}

function* model2(){
  yield 3
  yield model1()
  yield* model1()
  yield 4
  return 5
}

for(let i of model2()){
  console.log(i) //3,Object [Generator] {},1,2,4
}
~~~

上述代码中使用yield语句返回的是一个遍历器对象，yield*语句返回的是遍历器对象内部的值



**:heavy_check_mark:yield*语句也可以遍历部署了iterator接口的数据结构**

~~~javascript
let arr = [1,2,3,4]
let str = "hello"
function* iterator(){
  yield arr
  yield* arr

  yield str
  yield* str
}

let ite = iterator()

//使用yield语句
console.log(ite.next()) //第一条yield语句返回值：{ value: [ 1, 2, 3, 4 ], done: false }

//使用yield*语句是遍历数组
console.log(ite.next())
console.log(ite.next())
console.log(ite.next())
console.log(ite.next())
// { value: 1, done: false }
// { value: 2, done: false }
// { value: 3, done: false }
// { value: 4, done: false }


//遍历字符串

//使用yield语句
console.log(ite.next()) //{ value: 'hello', done: false }


//使用yield*语句
console.log(ite.next())
console.log(ite.next())
console.log(ite.next())
console.log(ite.next())
console.log(ite.next())
// { value: 'h', done: false }
// { value: 'e', done: false }
// { value: 'l', done: false }
// { value: 'l', done: false }
// { value: 'o', done: false }
~~~

**:book:如果被代理的Generator函数有return语句，就可以向代理的Generator函数返回数据**