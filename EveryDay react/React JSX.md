# JSX语法

## 基础语法

+ ReactDOM.render(JSX,CONTAINER,CALLBACK):将JSX渲染到页面上。
  + 三个参数是：JSX：虚拟元素
  + CONTAINER:容器
  + CALLBACK：回调函数，页面渲染完成后执行操作

+ 不要把JSX直接渲染到body中，应该渲染到自己创建的框架中。
  + 一个组件里面至少有一个render()方法，这个方法返回一个JSX元素，返回多个元素不合法。

    ~~~javascript
    ...
    //不合法
    render(){
        <div>1</div>
        <div>2</div>
    }
    
    //应该这么写
    
    render(){
        <div>
            <div>1</div>
       		<div>2</div>
        </div>
    }
    ~~~

  + 表达式插入，用{}大括号可以在JSX语法中插入表达式，包括变量、表达式计算、函数执行等等。

    ~~~javascript
    ...
    render(){
        <p>{1+2}</p>
    }
    
    render(){
        <p>{function(){
            return "hello world"
        }()}</p>
    }
    ~~~

  + 条件返回

  + 元素变量

    + JSX元素可以赋值给变量，作为函数参数传递或者作为函数返回值

+ React元素在创建后无法被改变，React只会更新发生改变的部分



## 事件监听

+ 使用<code>on*</code>采用驼峰式命名来添加事件，而且只能用在普通HTML标签上。
+ **event对象：**
  + 和普通event对象相似，不过经由React封装，对外提供统一的API和属性，就不存在兼容性问题。
  + 不能使用<code>return false</code>来创建组织默认行为，应该使用e.preventDefault()等
  + 关于this，对于传入的事件不是经由对象调用事件处理函数，而是直接调用，所以要获取得到当前实例，需要手动绑定this.