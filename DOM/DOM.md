# DOM详解

## :book:DOM概述

### :books:DOM

`DOM`（Document Object Model,对象文档模型）它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作



### :books:节点

> DOM的最小单位，DOM树由不同节点组成

**节点类型：**

 `Document`：整个文档树的顶层节点

`DocumentType`：doctype标签（比如<!DOCTYPE html>）

`Element`：网页的各种HTML标签（比如<body>、<a>等）

`Attribute`：网页元素的属性（比如class="right"）

`Text`：标签之间或标签包含的文本

`Comment`：注释

`DocumentFragment`：文档的片段



### :books:节点关系

+ 父级节点：`parentNode`
+ 子节点：`childNodes`
+ 同级结点：`sibling`



## :book:Node接口

> 所有DOM对象都继承Node接口，拥有一些共同的属性和方法。

### :books:Node接口属性

+ `nodeType`:返回一个整数值，表示节点类型

+ `nodeName`:返回节点的属性名

  + 文档节点（document）：`#document`
  + 元素节点（element）：大写的标签名
  + 属性节点（attr）：属性的名称
  + 文本节点（text）：`#text`
  + 文档片断节点（DocumentFragment）：`#document-fragment`
  + 文档类型节点（DocumentType）：文档的类型
  + 注释节点（Comment）：`#comment`

+ `NodeValue`:属性可读写，返回一个字符串，表示当前节点的文本值。只有属性节点（`attr`）,注释节点（`comment`）,文本节点（`text`）三种类型节点可以返回`nodeValue`属性值。其他节点返回`null`

+ `textContent`:返回当前节点和它所有后代节点的文本值

+ `baseURI`:返回一个字符串，表示当前网页的绝对路径。浏览器根据这个属性，计算网页上的相对路径的 URL。该属性为只读。无法读取到URI则返回null

+ `ownerDocument`:返回当前节点所在的顶层文档对象，即`document`对象。

+ `nextSibling`:返回紧跟在当前节点后面的第一个同级节点。如果当前节点后面没有同级节点，则返回`null`。

+ `previousSibling`：返回当前节点前面的、距离最近的一个同级节点。如果当前节点前面没有同级节点，则返回`null`

+ `parentNode`：返回当前节点的父节点。对于一个节点来说，它的父节点只可能是三种类型：元素节点（element）、文档节点（document）和文档片段节点（documentfragment）

  **文档节点（document）和文档片段节点（documentfragment）的父节点都是`null`。另外，对于那些生成后还没插入 DOM 树的节点，父节点也是`null`。**

+ `parentElement`:返回当前节点的父元素节点。如果当前节点没有父节点，或者父节点类型不是元素节点，则返回`null`。

  `parentElement`属性返回当前节点的父元素节点。如果当前节点没有父节点，或者父节点类型不是元素节点，则返回`null`。

  **相当于`parentNode`排除了文档节点和文档片段节点，只保留元素节点**

+ `firstChild,lastChild`:`firstChild`返回当前节点的第一个子节点，`latstChild`返回当前节点的最后一个子节点。两者没有找到相应节点则返回`null`。

  **`firstChild,lastChild`返回的除了元素节点，还可能是文本节点或注释节点。**

+ `childNodes`:返回一个类似数组的对象（`NodeList`集合动态集合），成员包括当前节点的所有子节点。没有任何子节点返回空集合。返回值包括**文本节点**和**注释节点**

+ `isConnected`:返回一个布尔值，表示当前节点是否在文档之中。



### :books:Node接口方法

+ `appendChild`():接受一个节点对象作为参数，将其作为**最后一个子节点**，插入当前节点。该方法的返回值就是插入文档的子节点。若节点已经存在，则将其移动到新的位置

+ `hasChildNodes()`:返回一个布尔值，表示当前节点是否有子节点。

  + 判断一个节点有没有子节点，有许多种方法，下面是其中的三种。
    + `node.hasChildNodes()`
    + `node.firstChild !== null`
    + `node.childNodes && node.childNodes.length > 0`

+ `cloneNode`():用于克隆一个节点。它接受一个布尔值作为参数，表示是否同时克隆子节点。它的返回值是一个克隆出来的新节点。

  + 注意点：
    + 克隆节点会拷贝该节点的所有属性，但是会丧失`addEventListener`方法和`on-`属性（即`node.onclick = fn`）
    + 该方法返回的节点不在文档之中，即没有任何父节点，必须使用诸如`Node.appendChild`这样的方法添加到文档之中。
    + 克隆一个节点之后，DOM 有可能出现两个有相同`id`属性（即`id="xxx"`）的网页元素，这时应该修改其中一个元素的`id`属性。如果原节点有`name`属性，可能也需要修改。

+ `insertBefore()`:用于将某个节点插入父节点内部的指定位置。返回值是插入的新节点

  + 参数分别是：

    + 第一个参数表示要插入的节点
    + 第二个参数表示要在那个结点之前插入的那个节点，若第二个参数为null,则变成最后一个子节点。

  + 可以配合`nextSibling`属性插入到结点之后

    ~~~javascript
    parent.insertBefore(s1, s2.nextSibling);//插入s2结点之后
    ~~~

+ `removeNode()`:接受一个子节点作为参数，用于从当前节点移除该子节点。返回值是移除的子节点。

+ `replaceNode()`:方法用于将一个新的节点，替换当前节点的某一个子节点。返回值是被替换掉的节点

+ `contains()`:返回一个布尔值，表示节点是否满足以下三个条件

  + 参数节点为当前节点。
  + 参数节点为当前节点的子节点。
  + 参数节点为当前节点的后代节点。

+ `isEqualNode()`:返回一个布尔值，用于检查两个节点是否相等。所谓相等的节点，指的是两个节点的类型相同、属性相同、子节点相同。

+ `isSameNode()`:返回一个布尔值，表示两个节点是否为同一个节点。

+ `normalize()`:用于清理当前节点内部的所有文本节点（text）。它会去除空的文本节点，并且将毗邻的文本节点合并成一个，也就是说不存在空的文本节点，以及毗邻的文本节点。

+ `getRootNode()`:返回当前节点所在文档的根节点`document`，与`ownerDocument`属性的作用相同。