# ES6 Map&WeakMap

## Map

### 概述

+ **:book::Map结构可以接受任何类型的值作为键用以解决JS对象只能接受字符串作为键名的问题**

+ **:book::通过Map构造函数新建一个Map实例对象,可以接受任何值作为键名**

~~~javascript
const newMap = new Map();
let o = {};

newMap.set(o,'content');
netMap.get(o);//'content'
~~~

+ **:book::Map接受一个数组成员是一个个表示键值对的数组的数组作为参数**

  ~~~javascript
  const nMap2 = new Map([[1,2],[3,[4,5]]]);
  console.log(nMap2); //Map { 1 => 2, 3 => [ 4, 5 ] }
  console.log(nMap2.get(1));//2
  console.log(nMap2.get(3)); //[4,5]
  
  
  const nMap3 = new Map([
    [1, 2],
    [3, 4, 5]
  ]);
  console.log(nMap3); //Map { 1 => 2, 3 => 4 }
  console.log(nMap3.get(1)); //2
  console.log(nMap3.get(3)); //4
  ~~~

+ **:book::如果定义相同的键名，后定义的会覆盖先定义的。**

+ **:book::如果读取未定义的键名，返回undefined**

+ **📖:如果接受对象作为键名，只有键名是相同对象的引用才会返回同一个值，否则就算对象值相同也代表不同的键名，因为对象地址值不同**

+ **:book::如果接受基本类型的值作为键名，只要键名严格相等，Map就将其视为一个键。例如+0和-0，Map也接受NaN作为键名。**

  ~~~javascript
  const nMap4 = new Map();
  nMap4.set(NaN,"1");
  nMap4.set(NaN, "2");
  console.log(nMap4); //Map { NaN => '2' }
  //NaN被覆盖。说明在Map内和Set内一样，NaN被认为等于自身。
  ~~~

### 属性和方法

+ <code>size</code>属性，返回Map实例对象成员个数
+ <code>set(key,value)</code>方法用于设置key所对应的键值，有则更新，无则新增
+ <code>get(key)</code>方法用于获取key所对应的键值。未找到key值返回undefined
+ <code>dalete(key)</code>方法用于删除key所对应的键值，删除成功返回true，否则返回false
+ <code>has(key)</code>方法用于判断是否含有lkey对应键值，有则返回true,否则返回false
+ <code>clear()</code>方法用于清楚所有的Map实例对象成员





### 遍历

参考Set



## WeakMap

### 概述：

**WeakMap也只接受对象（null除外）作为参数，WeakMap键不在引用他所指向的对象的时候，对象的内存会自动释放，而不需要手动释放，同Set。**



