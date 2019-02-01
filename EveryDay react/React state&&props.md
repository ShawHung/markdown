# props&state总结

## :book:state

state主要用于组件保存，控制，修改自己的可变状态，在组建内部初始化，可以被组件自身修改而无法被外部访问和修改。state中的状态可以通过this.setState方法来更新，该方法会导致组件的重新渲染。



## :book:props

props是通过组件外部传入来修改组件状态，组件内部无法对其控制和修改。除非主动更新状态



## :book:无状态组件和函数式组件

+ 未设置state的组件时无状态组件，尽量少写无状态组件来降低维护代码的复杂度。

+ 函数式组件书写方式

  ~~~javascript
  const Hello = (props) =>{
      const hello = (event) =>console.log("hello")
      return <div onClick={hello}>hello</div>
  }
  ~~~

  使用该函数式组件的方法和类继承Component相同
