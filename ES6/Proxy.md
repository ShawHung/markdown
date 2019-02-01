# ES6 Proxy

**:book:用于修改某些默认行为**



### 创建Proxy对象

+ 使用<code>Proxy</code>函数创建Proxy对象。

~~~javascript
var proxy = new Proxy(target,handler);
//target代表拦截目标对象
//handler是一个用于定义拦截行为的对象
~~~

+ 必须操作Proxy实例对象才能使Proxy产生作用，而不是对目标对象进行操作
+ 若handler为空对象，就是直接读取原对象。
+ 可以将Proxy对象设置成对象属性，就可以在对象上调用。

### Proxy实例对象方法

+ <code>get()</code>方法用于拦截某个属性的读取
