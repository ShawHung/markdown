# state&setState

## state

## setState

使用注意项：

+ 不能直接更新状态而是使用setState()

  ~~~javascript
  //不能这样做
  this.state.count = 12
  
  //应该这样
  this.setState({count:12})
  ~~~

+ setState()可能是异步的（调用setState并不会马上修改state），所以想在setState后马上进行后续运算不能做到

  ~~~javascript
  this.setState({
      this.state.count++//不能完成运算
  })
  ~~~

+ 上述虽然不能通过接受对象来完成但是可以通过接受一个函数来完成

  ~~~
  this.setState((prev)=>{
      return {count:prev.count++}
  })
  ~~~

+  在你调用setState()时，React会将状态合并更新