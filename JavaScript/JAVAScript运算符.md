#  JAVAScript运算符

[TOC]



### 1）算术运算符



**注意事项：**

1. **“+”号运算符**

   + 字符串和字符串相加拼接成新的字符串

     ```javascript
     "java" + "script";//"javascript"
     ```

   + 字符串和非字符串，非字符串转化成字符串后拼接

     ```javascript
     1 + "a";//"1a"
     false + "a";//"falsea";
     ```

   + 运算符重载，加法运算符：**"+"**,由于从左到右的运算顺序会发生重载,其他运算符则是先将所有运算子转化为数值再进行运算。

     ```javascript
     1 + 2 + "3";//"33"
     "1" + 2 + 3;//"123"
     ```

2. 对象相加，先调用对象的**valueOf()**方法，然后调用**toString()**方法，

   **Date对象优先调用toString()方法**

   ```javascript
   var obj1 = {
       valueOf：function{
       return 1;
   },
       toString:function{
           return  "hello";
       }
   }
   obj1 + 1;//2
   
   var obj2 = new Date();
   obj2.valueOf = function(){return "1"};
   obj2.toString = function(){return "hello"};
   obj2 + 1;//"hello1"
   ```

3. 自增自减运算符

   **前置先加后取值**，**后置先取值后加**。

   ```javascript
   var x = 1;
   ++x//x = 2，先执行++后取值x = 2
   x++//先取值x = 1，然后执行++
   ```

4. 赋值运算符可以将任何类型的值转化为数值(参考Number)

   ```javascript
   + true;//1
   +[];//0
   +{};//NaN
   ```



### 2）比较运算符



+ **非相等比较符**

  1. **字符串比较** 转换成ASCII码进行比较

     ~~~javascript
     //非数字字符串比较
     console.log("cat">"dog");//false
     console.log("cat的ASCII码值："+"cat".charCodeAt());//99
     console.log("dog的ASCII码值："+"dog".charCodeAt());//100
     //数字字符串比较
     console.log("5" > "11" );//true
     console.log("5的ASCII码值："+"5".charCodeAt());//53
     console.log("11的ASCII码值："+"11".charCodeAt());//49
     ~~~

  2. 

     + **数字字符串**与数字比较，字符串转化为数字后比较

       ~~~javascript
       "11" > 1;//true
       ~~~

     + **非数字字符串**与数字比较，非数字字符串转化为**NaN**,**NaN**比较都返回false

       ~~~javascript
       "dora" > 1;//false
       ~~~

  3. **非字符串比较**

     + 若运算子为原始类型的值将全部转化为数值后比较

       ~~~javascript
       5 > "4";//true
       //相当于5 > Number("4");
       //相当于5 > 4
       fasle < 1;//true
       //相当于Number(false)<1;
       //相当于0 < 1
       ~~~

     + **NaN**与任何值都返回**false**

  4. **对象比较**(先调用valueOf()方法后调用toString()方法。)

     ~~~javascript
     var x = [2];
     console.log(x > "11");//true
     //相当于[2].valueOf().toString();
     //相当于"2">"11";
     ~~~



### 3) 严格相等运算符比较



  + **NaN**与任何值都不相等
  ~~~javascript
  console.log(+0 === -0)；//true
  ~~~
  + 同一类型的原始类型的值（数值、字符串、布尔值）比较时，值相同就返回**true**，值不同就返回**false**
  + 复合类型值相互比较时比较的是它的地址
  ~~~javascript
  console.log({} === {});//false
  console.log([] === []);//false
  ~~~


### 4) 相等运算符比较




  1. 比较相同类型的值时等同于严格相等运算符

     ~~~javascript
     1 == 1.0；//false
     //等同于1 === 1.0
     false == "false";//false
     //等同于false === "false"
     ~~~

  2. 比较不同原始类型值（转化为Number后进行比较）

     ~~~javascript
     false == false;//false
     //等同于Number(false) == Number(false);
     //Number(false) = NaN;
     //NaN与任何值都不相等，包括它本身
     ~~~

  3. 对象与原始类型值比较

     + 对象与数值比较，对象转化为数值后比较

       ~~~javascript
       [1] == 1;//true
       //相当于Number([1]) == 1
       //相当于1 == 1
       ~~~

     + 对象与字符串比较，对象转化为字符串后比较

       ~~~javascript
       [1] == "1";//true
       //相当于String([1]) == "1"
       //相当于"1" == "1"
       ~~~

     + 对象与布尔值比较，双双转化为数值后比较

       ~~~javascript
       [1] == true;//true
       //相当于Number([1]) == Number(true);
       //相当于1 == 1
       ~~~



### 5) void运算符



void运算符执行一个表达式不返回任何值（返回undefined）

~~~javascript
var x = 3;
void(x=5);//undefined
console.log(x);//5
~~~



### 6）逗号运算符","

逗号运算符对两个表达式求值并返回后一个表达式的值

~~~javascript
var x = 0;
var y = (x++,10);
console.log("x");//1
console.log("y");/10
~~~



### 7）其他注意事项

​	**1.** 圆括号"()"

**圆括号中的表达式会第一个运算**

~~~javascript
（1+2）*3;//括号内先计算
~~~



​	**2.**运算顺序

**赋值运算符（`=`）和三元条件运算符（`?:`）从右往左运算**

~~~JavaScript
x = y = z;//运算顺序：x = (y = z);
~~~

