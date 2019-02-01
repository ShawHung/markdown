# 19-01-25JQuery学习内容

## :book:jquery自定义事件

+ 用`on`操作符来绑定事件，用`trigger/triggerHandler`来触发
+ 事件命名空间：通过`.`操作符为事件取别名，如`click.a`，会触发`click`，`chick.a事件`。如果用`trigger`来触发还会触发父元素同名事件（事件冒泡）。`triggerHandler`则会阻止默认行为和事件冒泡。



## :book:Jquery事件委托

+ 普通事件绑定如`click`是在页面加载完成后绑定所有匹配到的元素。不会匹配新增元素，所以此时要用到事件委托

+ `delegate`，通过委托页面加载时就存在的元素来给元素动态绑定事件。不过此方法在高版本的Jquery中已经废弃，推荐使用on()方法来绑定

  ~~~javascript
   <script>
      $(function () {
        $("button").click(function () {
          $("ul").append("<li>新增li</li>");
        })
     // 原方法（新增li不会输出）
        $("ul>li").click(function(){
          console.log($(this).text());
        })
      //通过delegate委托
        $(document).delegate("li","click",function(){
          console.log($(this).text());
        })
  
        //通过on绑定
        $(document).on("click","li",function () {
          console.log($(this).text());
        })
     })
  
  
    </script>
  
  
  <ul>
    <li>我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
  </ul>
  <button>添加一个li</button>
  ~~~



