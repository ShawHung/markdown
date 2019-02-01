# 关于this指向

**:grey_question:是否是函数调用**

```javascript
var name = "window";
var a = {
    var name = "inner";
    f:function(){
        console.log(this.name);//window
    }
}
f();//window//相当于window.f();this指向window
```

**:grey_question:是否是作为对象方法调用**

```javascript
var name = "window";
var a = {
    var name = "inner";
    f:function(){
        console.log(this.name);
    }
}
a.f();//inner  作为a对象方法调用，绑定a对象
```

**:grey_question:是否有显示绑定（call,apply,bind,new,包括上述第一条window）**

```javascript
var name = "window";
var a = {
    var name = "inner";
    f:function(){
        console.log(this.name);//window
    }
}
var fn = a.f;
fn.call(a);//inner
fn.call(window);//window
//call与apply区别，call传参数列表，apply传参数数组
//bind绑定不会立即调用,需要手动调用
fn.bind(a)();



//new绑定(指向创建对象)
function personInfo(name,age){
    this.name = name;
    this.age = age;
  
}
var person1 = new personInfo("xiaohuang",21);
person1.age;//21

//new原理(详见面向对象)
var person1 = new personInfo("xiaohuang",21);
new personInfo{
    var obj = {};
    obj.__proto__ = personInfo.prototype;
    var result = personInfo.call(obj,"xiaohuang",21);
    return typeof result === "obj"?obj:result;
}
//可见使用call改变了this指向
```

**:grey_question:箭头函数的this**

**箭头函数没有自己的this值，指向定义时所在作用域的this值**