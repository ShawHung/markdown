# 1月6日上午学习内容

## JQuery部分

+ js对象都有属性，属性节点只有DOM对象具有
+ js元素对象拥有一个<code>attributes</code>属性，返回一个类似数组的属性对象。其他类型的<code>attributes</code>属性返回<code>null</code>。
+ 属性节点的<code>name</code>和<code>value</code>值返回属性名和属性值，等同于<code>nodeName,nodeValue</code>。
+ 属性节点方法
  + <code>getAttribute():</code>返回当前结点的指定属性值。
  + <code>getAttributeNames():</code>返回一个数组，数组成员是当前元素所有属性的名字。跟<code>attributes</code>的区别是<code>attributes</code>返回一个类数组。
  + <code>setAttribute():</code>用于为当前元素节点新增属性。如果同名属性已存在，则相当于编辑已存在的属性。该方法没有返回值（接受两个参数，第一个参数是当前结点的制定属性，第二个参数是属性值）。
  + <code>hasAttribute():</code>返回一个布尔值，表示当前元素节点是否包含指定属性。
  + <code>removeAttribute():</code>移除指定属性。该方法没有返回值。
+ <code>prop()</code>方法和<code>removeProp()</code>方法:和attr方法作用类似，接收参数也相同，prop()方法适合用于判断true和false的场景，如“selected,checked,disabled”等
