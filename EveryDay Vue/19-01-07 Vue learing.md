# 1月9号学习内容

## Vue生命周期函数

1.**beforeCreate()：**此时data和methods还未初始化，根据官方文档，在数据观测和事件之前被配置



2.**created():**在实例创建完立即被调用，在这个阶段，时间已经完成数据观测，属性和方法的运算，事件回调。



3.**beforeMount():**在挂载之前被调用



4.**mounted():**挂载完成，此时用户可见。



-----------------------------

挂载完成后，组件正式运行

1.**beforeUpdate():**当数据发生改变，此时调用页面数据还未更新，但是data数据保持最新。



2.**update():**页面重新渲染后调用



------------------

运行结束后，实例销毁。

1.**beforeDestroy():**实力尚未正式销毁，data和methods等仍然可用。



2.**destroyed():**正式销毁。