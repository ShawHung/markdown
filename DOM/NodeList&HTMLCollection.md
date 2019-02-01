# NodeList&HTMLCollection

## :book:NodeList

**是一个类数组对象，成员是节点对象，如NodeList，querySelectorAll()方法返回的就是NodeList集合**



### :books:length属性

**用途：**

返回NodeList实例包含的节点数量。



### :books:forEach()方法

**用途：**

用于遍历NodeList数组成员。用法和数组forEach()方法相同



### :books:item()方法

**用途：**

接受一个整数作为参数，返回该位置上的成员。

如果参数值大于实际长度，或者索引不合法（比如负数），`item`方法返回`null`。如果省略参数，`item`方法会报错



### :books:keys(),values()，entries()方法

**用途：**

分别返回键名，键值，和键值对。适用于ES6for...of循环



## :book:HTMLCollection

是一个节点对象的集合，只能包含元素节点（element），不能包含其他类型的节点。它的返回值是一个类似数组的对象，但是与`NodeList`接口不同，`HTMLCollection`没有`forEach`方法，只能使用`for`循环遍历。



### :books:length属性

**用途：**

返回HTMLCollection实例包含的节点数量。



### :books:item()方法

**用途：**

同`NodeList`的item()方法



### :books:namedItem()方法

**用途：**

`namedItem`方法的参数是一个字符串，表示`id`属性或`name`属性的值，返回对应的元素节点。如果没有对应的节点，则返回`null`。