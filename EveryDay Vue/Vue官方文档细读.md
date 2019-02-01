# Vue官方文档精读



## Vue计算属性

**设计目的：**虽然Vue支持模版内的表达式，但是模板内过多的逻辑会让模板变得难以维护。所以对于复杂逻辑，应该使用**计算属性**。

~~~javascript
 <div id="app">
    <P>{{msg}}</P>
    <P>{{reverseMsg}}</P>
  </div>


  <script>
    var vm = new Vue({
      el: '#app',
      data: {
        msg: "hello",
        name:"xiao"
      },
      computed: {
        reverseMsg:function(){
          return this.msg.split("").reverse().join("")
        }
      },
      methods: {
        reverseMsg:function(){
          console.log("方法")
          return this.msg.split("").reverse().join("")
        }
      },

    })
  </script>
~~~



**方法和计算属性的区别：**方法在渲染时会重新执行函数，而**计算属性基于依赖进行缓存**，只有相关依赖发生改变才会重新求值。如果不希望有缓存，可以用方法替代。

**区别：**

+ 修改与计算属性无关的数据，不会重新计算（缓存机制）。适用于多个数据影响一个数据。

![Fz2oND.jpg](https://s2.ax1x.com/2019/01/15/Fz2oND.jpg)

+ 修改与方法无关的数据，都会触发方法，所以会有性能上的问题。如果不希望有缓存就使用方法。

  ![FzRSUS.jpg](https://s2.ax1x.com/2019/01/15/FzRSUS.jpg)

**计算属性与侦听属性的区别：**

+ 侦听属性适合用于操作开销比较大的或者异步操作场景。

+ 跟watch一样具有缓存机制，改变无关的值不会重新调用。