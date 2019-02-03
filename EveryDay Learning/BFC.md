# BFC

## :books:BFC是什么



> BFC(Block Formatting Context)快格式化上下文：是可视化渲染网页的一部分，只有Block-level-box参与。规定了块如何布局。该区域与外部毫不相干。
>
> 除了BFC,还有普通文档流(文档流分为定位流，普通流和浮动流)，IFC,GFC(Grid),FFC(flex)等

**BFC = Block-level-box+Formatting Context**



### 视觉格式化模型

（visual formatting model）视觉格式化模型规定了盒（Box）的生成。主要包括行盒，块盒，匿名盒。

盒的类型由`display`属性决定。

#### 块盒

+ `display`属性为block,list-item,table时，他是块级元素block-level。
+ 竖直排列，呈现为块状。
+ 块级格式化上下文



#### 行内盒（inline-block）

+ `display``:inline,inline-block,inline-table,`称为行内块元素。
+ 视觉上将行内元素排成多行。
+ 行内格式化上下文（inline formatting context）



#### 匿名盒（anonymous box）

+ 无法被选择器选中，分为匿名块盒和匿名行内盒。属性值为`inherit`

  ~~~html
  <div>
      hello<!--匿名-->
  	<p>
          HELLO
      </p>
      Hello<!--匿名-->
  </div>
  ~~~



### 定位方案（文档流）

#### 普通流

+ `position:relative,static`或者`float:none`
+ 在块级格式化上下文中垂直排列
+ 在行内格式化上下文中水平排列
+ 参考position：relative(相对定位)，static(静态定位)



#### 浮动流

+ 盒称为浮动盒
+ 处于当前行的开头或结尾
+ 导致常规流环绕在其周围，需清楚浮动。



#### 绝对定位

+ `position:absolute`
+ 相对于最近的设置了定位的父元素，否则相对于body定位。





### 如何生成BFC

+ 根元素或其他包含他的元素
+ 浮动（`float left/right`）
+ 绝对定位（`position:absolute`）
+ 行类块元素（`display:inline-block`）
+ 表格单元格 (`display:table-cell`)
+ overflow值不为visiable
+ 弹性盒（flex boxes `displat:flex,display:inline-flex`）



### BFC范围

> 包括该上下文所有的子元素，但是不包含创建了新的BFC的子元素的内部元素



### BFC规则

+ 内部的Box会在垂直方向上一个接一个的放置
+ 垂直方向上的距离由margin决定。（完整的说法是：属于同一个BFC的两个相邻Box的margin会发生重叠（塌陷），与方向无关。）
+ 每个元素的左外边距与包含块的左边界相接触（从左向右），即使浮动元素也是如此。（这说明BFC中子元素不会超出他的包含块，而position为absolute的元素可以超出他的包含块边界）
+ BFC的区域不会与float的元素区域重叠
+ 计算BFC的高度时，浮动子元素也参与计算
+ BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然

  看到以上的几条约束，想想我们学习css时的几条规则

+ Block元素会扩展到与父元素同宽，所以block元素会垂直排列
+ 垂直方向上的两个相邻DIV的margin会重叠，而水平方向不会(此规则并不完全正确)
+ 浮动元素会尽量接近往左上方（或右上方）
+ 为父元素设置overflow：hidden或浮动父元素，则会包含浮动元素



### BFC应用

**解决margin重叠**

~~~html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>BFC margin塌陷</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    *{
      margin: 0;
      padding: 0;
    }
    div#box>p{
      width: 300px;
      height: 100px;
      background-color: #ff0000;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div id="box">
      <p>我设置了margin:10px</p>
      <p>我设置了margin:10px</p>
  </div>
</body>
</html>
~~~

此时属于同一个BFC的元素发生margin重叠。解决方式（根据BFC范围规则给子元素创建一个BFC即可）

[![kG0OW8.md.png](https://s2.ax1x.com/2019/02/03/kG0OW8.md.png)](https://imgchr.com/i/kG0OW8)

[![kGBCoq.md.png](https://s2.ax1x.com/2019/02/03/kGBCoq.md.png)](https://imgchr.com/i/kGBCoq)

~~~html
 
.wrapper{
	overflow:hidden;
}
<div id="box">
    <div class="wrapper">
        <p>我设置了margin:10px</p>
    </div>      
      <p>我设置了margin:10px</p>
  </div>
~~~

[![kGBL7R.md.jpg](https://s2.ax1x.com/2019/02/03/kGBL7R.md.jpg)](https://imgchr.com/i/kGBL7R)

**对于左右布局也可以通过添加BFC来解决margin重叠问题**



**清除浮动**

根据BFC规则，会计算浮动子元素的规则，可通过设置设置父元素BFC来清除浮动（浮动元素脱离文档流，造成父元素高度塌陷）

~~~html
.parent{
	border:2px solid #fffddd;
	overflow:hidden;
}
.son{
	heigh:100px;
	width:100px;
	background-color:#fff000;
	float:left;
}
<div class="parent">
   <div class="son">
       
    </div> 
    <div class="son">
        
    </div>
</div>
~~~



**自适应布局**

根据BFC规则：

> BFC的区域不会与float的元素区域重叠
>
> 内部的Box会在垂直方向上一个接一个的放置

可以通过创建BFC实现自适应布局

~~~HTML
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>自适应布局</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    html,
    body {
      height: 100%;
      width: 100%;
    }
    .wrapper{
      height: 100%;
      width: 100%;
      overflow: hidden;
    }
    .left {
      width: 200px;
      height: 100%;
      float: left;
      background-color: #ff6f4a;
    }

    .right {
      width: 200px;
      height: 100%;
     
      float: right;
      background-color: #350ac3;
    }

    .main {
      height: 100%;
      overflow: hidden;
      background-color: #30e9e4;
    }
  </style>
</head>

<body>
  <div class="wrapper">
    <div class="left"></div>
    <div class="right"></div>
     <div class="main"></div>
  </div>





</body>

</html>
~~~

[![kGWOMt.md.gif](https://s2.ax1x.com/2019/02/03/kGWOMt.md.gif)](https://imgchr.com/i/kGWOMt)