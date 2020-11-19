# React开发

## **配置react开发环境**

npm install -g create-react-app

npx create-react-app my-app  创建一个react APP 有多种方式

cd my-app	进入项目内

npm start		启动项目

### **结构目录**

<img src=".\image\9d233c6920d84696952b760001586308.jpg" alt="img" style="zoom: 67%;" />

public是静态文件路径

images存放图片

css存放css样式

src里面页面

components自定义子组件

APP.js入口

## **子组件开发基本骨架**

```react
import React from 'react';  导入react模块 
class Home extends React.Component{  创建Home组件    
	constructor(props){   接收调用时传递过来的实参        
        super(props);        
        this.state = { 
        	
    	}    
    }    
    渲染的页面卸载render方法里    
    render() {        
        return ()    
    } 
} 
导出模块 
export default Home 

如果不想在组件外围嵌套一个标签展示出来  也可以直接用一个空标签

import React, { Fragment } from "react"; 
return(    
    <Fragment >  
    return时使用Fragment作为外层不会展示在dom中    
    </Fragment > 
) 
```

## **属性绑定**

类名class换成className设置

classnames模块动态添加class属性

```react
import classNames form "classnames" 
<div className={this.state.color}></div> 
<div className={classNames('a', {'b': true, 'c': false})}></div> 
```

for要改成 htmlFor

```react
<label htmlFor="name">姓名</label> <input id="name"/> 
```

style写法 对象格式写 也可以在state里面定义一个style对象存放属性

```react
<div style={{color: "red"}}></div>
```

**引入图片 当做引入模块一样引入**

import引入

```react
import logo from "../assets/images/1.jpg" 
<img src={logo}/> 
```

require引入

```react
<img src={require(../assets/images/1.jpg)}/> 
```

远程引入

```react
<img src="图片链接"/> 
```

两个方法都是引入的同一张图片

## **props**

所有 React 组件都必须像纯函数一样保护它们的 props 不被更改

props里面的值是组件使用时传递过来的，每个组件的props不同

组件嵌套子组件

组件内嵌套的内容在props中的children中

```
调用Home组件并且在Home组件内写内容那么这些内容存在props.children里面 
<Home>     
这是什么   
</Home> 
```

```react
<div id="root"></div>
    <script type="text/babel">
        // var name = "张三";
        // const element = <h1>{name}</h1>;
        // function uname() {
        //     return <h2>nihao</h2>
        // }
        // function Home (props) {
        //     return <div>hello, {props.uname}</div>
        // }
        function formatDate(date) {
            return date.toLocaleDateString();
        }
        function Avatar (props) {
            return (
                <img className="Avatar" src={props.user.avatarUrl} alt=									{props.user.name}/>
            )
        }
        function UserInfo (props) {
            return (
                <div className="UserInfo">
                    <Avatar user={props.user}/>
                    <div className="UserInfo-name">
                        {props.user.name}
                    </div>
                </div>
            )
        }
        function Comment (props) {
            return (
                <div className="Comment">
                    <UserInfo user={props.author}/>
                    <div className="Comment-text">
                        {props.text}
                    </div>
                    <div className="Comment-date">
                        {formatDate(props.date)}
                    </div>
                </div>
            )
        }
        const comment = {
            date: new Date(),
            text: "react",
            author: {
                name: "hei",
                avatarUrl: ""
            }
        }
        ReactDOM.render(
            <div>
                <h2>nihao</h2>
                <Comment author={comment.author} text={comment.text} date={comment.date}/>
            </div>,
            document.querySelector("#root")
        );
    </script>
```

## **class组件开发**

1. 创建一个同名的 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)，并且继承于 React.Component。
2. 添加一个空的 render() 方法。
3. 将函数体移动到 render() 方法之中。
4. 在 render() 方法中使用 this.props 替换 props。
5. 删除剩余的空函数声明
6. state是类局部的数据
7. props是调用组件是传递过来的数据

```react
class Home extends React.Component{  创建Home组件    
	constructor(props){   接收调用时传递过来的实参        
		super(props);        
		state局部数据        
		this.state = { 
            
		}    
	}    
	渲染的页面卸载render方法里    
	render() { 
        
	} 
} 
```

## **state**

​	1、state局部数据

​	2、不要直接修改 通过setState更新数据

​	3、state数据可能是异步更新

​	 	在事件处理函数内部的 setState是异步的 

​	4、setState可以接收一个函数

​	5、数据是浅合并 会替换更改的数据 保留未更改的数据

```react
this.sate.数据名= 新数据  这是错误的写法 
//应该通过setState() 设置 
this.setState({数据名: 新数据}) 更新数据正确的写法  
箭头函数写法 
this.setState((state, props) => ({  
    counter: state.counter + props.increment 
})); 
普通函数写法 
this.setState(function(state, props) {    
    return 
    {        
        counter: state.counter + props.increment    
    } 
}) 
```

**state props 的数据是从上向下流动的**

## **react事件**

​	1、react事件的命名采用小驼峰(camelCase)

​	2、使用jsx语法时需要传入一个函数作为事件处理函数，而不是一个字符串

​	3、在组件里面定义事件处理函数

​	4、在这里，e是一个合成事件

### **循环数据**

​	1、直接使用{ 数组 } react会内部遍历数组 渲染到页面中

​	2、普通数据也可以遍历数组添加标签包裹数据

​	3、也可以直接遍历过滤this.state里面的数组

​	4、遍历数据渲染需要添加key  

不到万不得已不要使用索引作为key会导致性能变差，

尽量自定义，例如放在一个数组里面然后遍历数组添加  key只是在兄弟节点之间是唯一的

```react
list: ['11111', '22222', '33333'], 
list1: [<h2 key="1">我是一个h2</h2>, <h3 key="2">我是一个h3</h3>], 
list2: [     
    {title: '新闻1111'},     
    {title: '新闻2222'},     
    {title: '新闻3333'},     
    {title: '新闻4444'}, ] 
var listResult = this.state.list.map((result, key) => {     
    return <li key={key}> { value } </li> 
}) listResult的内容是  [<li>11111</li>, <li>22222</li>, <li>33333</li>] 
这个代码就会遍历list里面的数据  
通过map循环添加标签  
返回一个标签数组 {     
    this.state.list3.map((value, key) => {         
        return <li key={key}> { value.title } </li>     
    }) 
} 
```

### **事件方法**

注意复杂的this指向问题

若要在定义的方法里面调用例如 state里面的数据则要改变函数内部的this指向

​	1、bind() 方法改变函数内部的this指向且不调用函数

​	2、在constructor里面定义

```react
this.函数名 = this.函数名.bind(this)
```

3、函数名等于一个箭头函数 推荐方法

运用的是箭头函数内部this不可变性 (不可变性不是指箭头函数内部的 this永

远指向一致，而是指其内部的 this永远指向箭头函数被定义时外部最近的 this

如果需要向函数传递参数那么就要用bind

```react
// 事件方法 
import React from 'react' 
class EventMethod extends React.Component{   
    constructor(props) {     
        super(props);     
        this.state = {       
            msg: "123456"     
        }   
    }   
    run () {     
        alert("我被点击了")   
    }   
    getData () {     
        console.log(this)  
        这里面的this是不存在的     
        alert(this.state.msg)   
    }   
    render () {     
        return (       
            <div className="EventMethod">         
                <button onClick={this.run}>点击</button>         
                <br/>         
                <br/>         
                <button onClick={this.getData.bind(this)}>获取数据</button>       
            </div>     
        )   
    } } 
export default EventMethod 
```

### **事件**

事件对象，键盘事件、表单事件、ref获取dom节点、react实现类似vue双向数据绑定

​	1、事件对象 event与原生JavaScript DOM里面的event事件一样

​	2、ref获取dom节点   不要过度使用

**不能在函数组件上使用 ref 属性**

1、在constructor里面使用React.createRef()创建

```react
constructor(props) {    
    super(props);    
    this.myRef = React.createRef(); myRef 是自定义名字 
} 
```

2、this.节点的名字.current (ref里面的值)

```react
<input ref={this.myRef}/> 获取节点   
let val = this.textInput.current.value 获取input里面的值 
```

react实现vue双向数据绑定  MVVM设计

model改变影响view view改变反过来影响model

```react
inputChange = (event) => {    
    this.setSate({        
        username: event.target.value    
    }) } 
<input value={this.state.username} onChange={this.inputChange}/> 
input里面的内容发生改变下面这个数据也会发生改变 {this.state.username} 
当input内容发生改变时就会触发onChange事件然后调用inputChange函数 
inputChange函数将input输入的值重新复制给this.state.username就实现了双向数据绑定 
```

### **表单事件**

在使用value绑定this.state数据的时候必须监听onChange数据 实现MVVM设计

defaultValue 只获取值  只实现MV model 影响 view 

input   select   这两个表单控件都是监听onChange改变

checkbox 多选控件改变check属性

```react
hobby: [
    {'title': "睡觉",checked: true},
    {'title': "吃饭",checked: false},
    {'title': "打豆豆",checked: false},
]  
handelHobby(key) {     
    var hobby = this.state.hobby;     
    hobby[key].checked = !hobby[key].checked     
    this.setState({       
        hobby: hobby     
    })   
} 
爱好： 
{    
    this.state.hobby.map((value, key) => {        
        return (            
            <span key={key}>                
                <input type="checkbox" checked={ value.checked } onChange={ this.handelHobby.bind(this, key) } /> 
                {value.title}            
            </span>        
        )    
    }) 
} 
```

## **父子组件传值 (状态提升)**

props可以在调用时通过自定义属性传递，可以是值也可以是变量或方法(通过大括号引起来) props的值是不能改变的

```react
<Header run={this.run} /> 
传递run方法 
    <Header msg={this.state.msg} /> 
        传递state里面的msg值 
	<Header news={this}/> 
    将整个父组件传递给子组件 
```


父组件获取子组件的数据

class组件能用定义一个函数然后再子组件调用传递this就可以获取整个组件

**父组件给子组件传值 都是定义在子组件里**

defaultProps：父子组件传值中，如果父组件调用子组件的时候不给子组件传值

则可以在子组件中使用defaultProps定义的默认值

```react
现在有一个Header组件 在Header组件外面 
Header.defaultProps = {    
    定义默认值 
} 
```

propTypes：验证父组件传值的类型

```react
先引入prop-types 
import PropTypes from "prop-types" 
组件.propTypes = {    
    name: PropTypes.string    
    name是字符串类型的 
} 
```

## **react声明周期函数**

#### **组件加载时触发的函数**

constructor  

componentWillMount 

#### 组件将要挂载

render 

componentDidMount (DOM操作) 组件挂载完成

#### **组件更新时触发的生命周期函数**

shouldComponentUpdate  是否要更新数据返回true 或 false 

```react
shouldComponentUpdate () {    
    return true 返回true就更新 false不更新 
} 
```

componentWillUpdate

#### 组件将要更新数据时触发

render

componentDidUpdate 组件更新完成

#### **在父组件里面改变props传值的时候触发**

componentReceiveProps

#### **组件销毁的时候触发的**

componentWillUnmount 

react解析HTML标签

```react
解析前 
    <div className="p_content" dangerouslySetInnerHTML={{__html:this.state.list.content}}> 
        解析之后 
<p> 
        娃娃菜富含维生素和硒，叶绿素含量较高，具有丰富的营养价值。 娃娃菜还含有丰富的纤维素及微量元素，也有助于预防结肠癌。 娃娃菜吃起来口感脆嫩清甜。我们吃娃娃菜喜欢到饭店里吃蒜蓉粉丝娃娃菜， 妈妈喜欢做娃娃菜炖豆腐，有一股自然的清香，女儿很喜欢吃姥姥做的，说是好吃又减肥。111 
</p> 
```

## **context**

context是react提供的一个用于跨组件传值的方法

```react
import React, {createContext} from 'react' 
把createContext调用后产生的方法解构出来 
const {   
    Provider,   
    Consumer: CounterConsumer   CounterConsumer是自己定义的名字 
} = createContext(); 
通过Provider可以进行传值   
值和方法都可以传递 
    <Provider value={{ count: 10 }}> </Provider> 
        通过Consumer包含组件里面必须是函数 
            <Consumer>    
            (value) => { 
            	value 是 {count: 10}        
               	return <p>{value.count}</p>   
        	} 
            </Consumer> 
```

## **HOOK**

让无状态组件可以使用状态

使用react HOOK中的useState来进行实现 React.useState

React.useState() 要给一个初始值

返回的是一个数组 第一个值是当前的状态值 

第二个是用于更改状态的函数类似于setState

```react
import React from "react" 
function App () {    
    let [val, setVal] = React.useState(0);    
    useEffect类似于componentDidMount  componentDidUpdate    
    React.useEffect(() => {        
        console.log("更新了")    
    })    
    val 是值     
    setVal可以改变val值 一个函数    
  	<button onClick=(() => {setValue(val + 1)})>点击val加1</button> 
} 
```

声明对象形式的状态

```react
let [val, setVal] = React.useState({ val1: 10 }) 这个解构出来的val就是一个对象形式的数据了 
```

建议使用多次声明的形式写

## **高阶组件**

可以用来拦截组件渲染

```react
import React from 'react' 
const WithCopyright = (YouComponent) => {   
    return class WithCopyright extends React.Component {     
        render () {       
            return (         
                <>           
                <h1>这是高阶组件</h1>           
                <YouComponent {...this.props} />   这个是传递App组件                    
                App组件传递的props属性值传递下去，子组件中直接访问是访问不到                    
                需要传递         
                </>       
            )     
        }   
    } 
} 
export default WithCopyright 
导入WithCopyright组件 
import WithCopyright from './WithCopyright' 
function App(props) {   
    return (     
        <Fragment>       
            <props.name/>     
        </Fragment>   ) 
} 
export default WithCopyright(App)  传递App组件作为参数 
```

