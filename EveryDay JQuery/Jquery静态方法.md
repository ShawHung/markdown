# Jquery Day3

## JQuery静态方法

### :book:each方法，map方法

+ 可以遍历数组和伪数组

+ 不同点：

  + map可对遍历项进行操作并返回一个新数组
  + 仅遍历操作each返回遍历数组，map返回空数组

  ```javascript
  var arr = [1,2,3];
  var obj = {0:1,1:2，2:3}
  
  var res = $.each(arr,function(index,value){
      console.log(index+":"+value);
  });//0:1,1:2，2:3
  console.log(res);//[1,2,3]
  $.each(obj,function(index,value){
      console.log(index+":"+value);
  });//0:1,1:2，2:3
  
  
   var res1 = $.map(arr,function(value,index){
      console.log(index+":"+value);
  });//0:1,1:2，2:3
  console.log(res1);//[]
  $.map(obj,function(value,index){
      console.log(index+":"+value);
  });//0:1,1:2，2:3
  
   var res2 = $.map(arr,function(value,index){
      console.log(index+":"+value);
       return index + value; 
  });
  console.log(res2);//[1,3,5]
  ```

## Jquery内容选择器

+ **[:contains(text)]**：匹配包含给定文本的元素

  ```javascript
  
  <div>John Resig</div>//选中
  <div>George Martin</div>
  <div>Malcom John Sinclair</div>//选中
  
  $("div:contains('John')")
  ```

+ **[:empty]**：匹配所有不包含子元素或者文本的空元素

  ```javascript
  <table>
    <tr>
      <td>Value 1</td>
  	<td></td>//选中
    </tr>
    <tr>
      <td>Value 2</td>
  	<td></td>//选中
   </tr>
  </table>
  
  $("td:empty");
  ```

+ **[:has(selector)]**：匹配含有选择器所匹配的元素的元素

  ```javascript
  <div><p>Hello</p></div>
  <div>Hello again!</div>
  
  $("div:has(p)").addClass("test");//[ <div class="test"><p>Hello</p></div> ]
  ```

+ **[:parent]**：匹配含有子元素或者文本的元素

  ```javascript
  <table>
    <tr>
      <td>Value 1</td>
  	<td></td>//选中
    </tr>
    <tr>
      <td>Value 2</td>
  	<td></td>//选中
   </tr>
  </table>
  
  $("td:parent");//[ <td>Value 1</td>, <td>Value 2</td> ]
  ```
