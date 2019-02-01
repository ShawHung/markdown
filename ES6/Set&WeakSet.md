# ES6 Set&WeakSet

## ES6 Set

**:book:概述：是ES6提供的一种新的数据结构，成员值唯一不重复（即不能添加重复值），类似于数组。本身是一个构造函数用来生成Set数据结构。**

+ 可以接受一个数组作为参数用以初始化。（数组去重）。

  ~~~javascript
  var s = new Set();
  [1,1,1,2,2,4,3,2,3,2,4].forEach(x => s.add(x));
  console.log(s);//Set {1,2,3,4}
  
  const s1 = new Set([6,4,6,5,6,4,3,3,2]);
  console.log([...s1]);
  //[ 6, 4, 5, 3, 2 ]
  ~~~

+ 向Set中加入值不会发生数值类型转换。类似于”===“，并且NaN被认为等于自身。两个对象也被认为不相等。

  ```javascript
  const set1 = new Set();
  let a = NaN;
  let b = NaN;
  set1.add(a);
  set1.add(b);
  
  console.log(set1);//Set{NaN}
  ```





### 属性和方法

+ <code>Set.prototype.constructor</code>构造函数，默认为Set函数

+ <code>Set.prototype.size</code>返回Set实例成员数量

+ <code>add(value)</code>添加值，返回Set实例

+ <code>delete(value）</code>删除值，返回布尔值表示是否删除成功。

+ <code>has(value)</code>返回一个布尔值，表示参数是否是Set的实例

+ <code>clear()</code>清除所有成员，没有返回值。

  ~~~javascript
  const set2 = new Set();
  
  set2.add(1);
  set2.add(1);//重复
  set2.add(2);
  console.log(set2); //Set { 1, 2 }
  
  
  console.log(set2.has(1));//true
  
  let res1 = set2.delete(1);
  console.log(res1);//true
  
  console.log(set2.has(1));//false
  
  set2.clear();
  console.log(set2); //Set {}
  ~~~

+ 使用<code>Array.from()</code>方法可以将Set转化为数组。

  ~~~javascript
  const setArr = new Set([1,2,3]);
  var result = Array.from(setArr);
  console.log(result);//[1,2,3]
  ~~~

### 遍历

+ <code>keys()</code>:返回键名遍历器
+ <code>values()</code>返回键值遍历器
+ <code>entries()</code>返回键值对遍历器
+ <code>forEach()</code>对每个成员调用回调函数

**由于Set只有键值没有键名，所以键值和键名行为保持一致。（可用for...of直接遍历Set）**

~~~javascript
const nSet1 = new Set([1,2,3,4]);

for( let key of nSet1.keys()){
  console.log(key);
}
//1
//2
//3
//4

for (let val of nSet1.values()) {
  console.log(val);
}
//1
//2
//3
//4

//省略values方法直接使用for...of遍历。
for (let val of nSet1) {
  console.log(val);
}
//1
//2
//3
//4

for ( let ent1 of nSet1.entries()) {
  console.log(ent1);
}
// [1, 1]
// [2, 2]
// [3, 3]
// [4, 4]


nSet1.forEach((val,keys) => { console.log(val*keys);})
// 1 1x1
// 4 2x2
// 9 3x3
// 16 4x4
~~~

### 遍历应用

+ 数组去重

  ```javascript
  let arr = [1,2,3,4,3,2,1,5,5,6];
  let uniq = [...Set(arr)];
  console.log(uniq);//[1,2,3,4,5,6]
  ```

+ 使用数组**map**和**filter**方法

  ~~~javascript
  let nSet = new Set([1, 2, 3, 4]);
  let nMap = new Set([...nSet].map(x => x * 3));
  console.log([...nMap]); //[ 3, 6, 9, 12 ]
  
  let nFilter = new Set([...nSet].filter(x => x%2 == 0));
  console.log([...nFilter]); //[ 2, 4 ]
  
  ~~~

+ 实现并集，交集，差集

  ~~~javascript
  let aSet = new Set([1,2]);
  let bSet = new Set([1,3,4]);
  
  //并集
  let newArr1 = new Set([...aSet,...bSet]);
  console.log([...newArr1]); //[ 1, 2, 3, 4 ]
  
  //交集
  let newArr2 = new Set([...aSet].filter( x => bSet.has(x)));
  console.log([...newArr2]); //[ 1 ]
  
  //差集
  let newArr3 = new Set([...bSet].filter(x => !aSet.has(x)));
  console.log([...newArr3]); //[ 3,4]
  ~~~

+ 改变原来的Set结构。

  + 利用原Set结构映射出新的Set结构赋值给原来的Set结构。
  + 使用Array.from()方法。





## ES6 WeakSet

+ 绝大部分特性同Set，但是WeakSet只能接受**对象**作为参数，不能接受其他类型的值。
+ WeakSet方法
  + <code>WeakSet.prototype.add(value)</code>:添加成员
  + <code>WeakSet.prototype.delete(value)</code>：删除成员
  + <code>WeakSet.prototype.has(value)</code>:是否含有指定成员。
+ WeakSet不能遍历。