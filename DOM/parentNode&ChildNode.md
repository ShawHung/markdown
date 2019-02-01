# parentNode&ChildNode

## :book:parentNode接口

如果当前节点是父节点，就会继承`ParentNode`接口。由于只有元素节点（element）、文档节点（document）和文档片段节点（documentFragment）拥有子节点，因此只有这三类节点会继承`ParentNode`接口。



### :books:方法和属性

+ `children`:返回HTMLCollection实例成员是所有的元素子节点，只读属性。
+ `firstElementChild,lastElementChild`:返回当前节点第一个元素子节点或者最后一个元素子节点。不存在返回null
+ `childElementCount`:返回一个整数，表示当前节点所有元素子节点的数目。
+ `append(),prepend()`:在最后一个元素子节点后面添加子节点（可以是元素节点和文本节点），在最前面一个元素子节点后面添加子节点（可以是元素节点和文本节点），没有返回值





## :book:childNode接口

一个节点有父节点，就会继承childNode接口方法和属性



### :books:方法和属性

+ `remove()`：从父节点移除当前节点
+ `before()，after()`:在当前节点前面/后面插入同级节点，可以是元素节点或是文本节点。
+ `replaceWith()`:接受文本节点或者元素节点但用来替换当前节点