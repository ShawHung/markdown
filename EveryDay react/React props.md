# React props

**:book:React提供props属性是组件可配置，通过外部传入新的props来重新渲染子组件，它是一个对象，包含了对组件的配置**

~~~javascript
class PropsLikeButton extends Component{
  constructor(){
    super()
    this.state = {liked:false}
  }

  handler(){
    this.setState(
      {liked:!this.state.liked}
    )
  }

  render(){
    const likeText = this.props.likeText||"点赞"
    const dislikeText = this.props.dislikeText||"取消"
    return(
      <button
      onClick={this.handler.bind(this)}>
        {this.state.liked?likeText:dislikeText}👍
      </button>
    )
  }
}
~~~

上述代码通过<code>this.props</code>获取到组件内部属性likeText和dislikeText，使其变为可配置。

**:heavy_check_mark:在使用组件时通过传入属性来配置likeText和dislikeText**

~~~javascript
render(){
    return (
    	<div>
        	<PropsLikeButton likeText = "good" dislikeText="bad"/>
        </div>
    )
}
~~~





## 默认配置defaultProps

可以使用defaultProps代替上例的“||”操作符来设置默认配置

上例可修改为

~~~javascript
class PropsLikeButton extends Component{
  static defaultProps{
  	likeText:"点赞"
    dislikeText:"取消"
  }
  constructor(){
    super()
    this.state = {liked:false}
  }

  handler(){
    this.setState(
      {liked:!this.state.liked}
    )
  }

  render(){
    const likeText = this.props.likeText
    const dislikeText = this.props.dislikeText
    return(
      <button
      onClick={this.handler.bind(this)}>
        {this.state.liked?likeText:dislikeText}👍
      </button>
    )
  }
}
~~~



**props不可变**

props一旦传入就不可改变，但是可以通过主动重新渲染的方式传入新的props

~~~javascript
class PropsLikeButton extends Component{
  
  constructor(){
    super()
    this.state = {
          likeText:"点赞"
          dislikeText:"取消"
      }
  }

  handler(){
    this.setState(
        {
            likeText:"Good"
            dislikeText:"Bad"
        }
    )
  }

  render(){
    	<div>
            <PropsLikeButton 
      			likeText = {this.state.likeText}		
      			dislikeText = {this.state.dislikeText}
      		/>
             
            <div>
              <button onClick={this.handler.bind(this)}>
                    修改props
              </button>
            </div>
        </div>	
      	
    )
  }
}
~~~

