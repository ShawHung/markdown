# JavaScript消息队列与事件循环

## :bookmark:进程和线程

+ **进程**是cpu分配资源的最小单位（比如分配内存）
+ *线程*是cpu可调度的最小单位
+ 一个**进程**内可有一个或多个*线程*
+ **进程**之间相互独立
+ 一个或多个*线程*在**进程**内协作完成任务
+ *单线程*和*多线程*是指在一个**进程**内

----------------------------------------------------
## :bookmark:浏览器

 + 浏览器是多进程的
 + 浏览器进程包括
   + **浏览器主线程：**负责浏览器页面显示，页面管理，其他进程的创建与销毁，网络资源的管理等
   + **GPU进程：**最多只存在一个，用于3D绘制
   + **插件进程：**第三方插件打开时创建，不同插件为独立进程
   + **renderer进程（浏览器内核）：**默认每个tab页包含一个，负责页面渲染，脚本执行，事件处理

-----------------------------------------------------
## :bookmark:浏览器内核（渲染进程）

### 渲染进程是多线程的

+ **GUI渲染线程：**负责渲染页面
+ **js引擎线程：**负责处理脚本
+ **事件触发线程：**处理事件
+ **定时器触发线程：**setInterval,setTimeout
+ **异步http请求线程：**XMLHttpRequest

-----------------------------------------------------

## :bookmark:主线程与Renderer进程通信过程

+ 主线程接受用户请求，获取页面内容并通过接口将任务传递给渲染进程
+ Renderer进程接收到消息交由渲染线程后开始渲染页面，其中可能需要Browser进程获取资源和需要GPU进程来帮助渲染。如果此时JS操作DOM可能导致回流并重绘，最后将结果交给主进程
+ 主进程接收结果并绘制

-----------------------------------------------------
## :bookmark:事件循环与消息队列

+ JS分为同步任务和异步任务

+ 同步任务都在主线程上执行，形成一个`执行栈`

+ 主线程之外，**事件触发线程**管理着一个`任务队列`，只要异步任务有了运行结果，就在`任务队列`之中放置一个事件。

+ 一旦`执行栈`中的所有同步任务执行完毕（此时JS引擎空闲），系统就会读取`任务队列`，将可运行的异步任务添加到可执行栈中，开始执行。

  ![img](https://user-gold-cdn.xitu.io/2018/1/21/1611938b898ed9ef?imageslim)