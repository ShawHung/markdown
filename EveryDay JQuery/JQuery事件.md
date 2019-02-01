# JQuery事件

## Jquery事件绑定

+ 通过eventName(fn)的形式绑定事件
+ 通过on(eventName,fn)绑定事件
+ 事件可以绑定多个

+ 通过bind(eventName,fn)来绑定



## Jquery事件解绑

+ off()方法：如果不传参，移除所有绑定事件，传一个参，移除指定事件，传两个参，移除指定参数的绑定事件
+ unbind()方法：同off()



## Jquery阻止事件冒泡和默认行为

+ 直接在相应元素内return false
+ 使用event.stopPropagation()方法



## Jquery事件自动触发

+ trigger()方法：不会阻止冒泡和默认行为（有一个例外是a标签不会触发默认行为，需要在其中加一个子标签来触发）
+ triggerHandler()方法：会阻止事件冒泡和默认行为



## Jquery自定义事件

+ 通过on()方法来绑定事件
+ 通过trigger()/triggerHandler()方法来触发事件。



## Jquery事件命名空间

+ 通过on()方法来绑定事件（事件名为自定义（在多人协作任务中加上后缀））
+ 通过trigger()/triggerHandler()方法来触发事件。（相处发水就传递哪个事件名）
+ 通过trigger()方法触发子元素命名空间的事件，会触发父元素带有相同命名空间的元素。





