中文官网：https://doc.react-china.org

proxy

# 代码任务

## 11.20 

1. state 的修改是怎么修改的，如果state里面的属性也是一个对象，那么修改该对象的其中一个属性会不会影响其他属性。
2. 事件的传递真有那么复杂嘛在类中定义除了 state 属性之外的属性，是否能正常属性。



# 问题

1.为什么类中的函数，访问不到 this

```javascript
class Square extends React.Component {
	constructor(arg) {
	    super(arg);
		this.state = {
		      value: null,
		    };
  };
  showX(){
    ()=>{
      console.log(this) /*undifine*/
    }
  }
 //事实证明确实是访问不到，只有react的生命周期函数中才可以获取到 this ，我们可以在标签里，写一个箭头函数，在箭头函数中执行普通的成员函数
   getthis(){
    this.setState({value:"X"});
    console.log("hello");
  }
  render() {
    return (
      <button className="square"  onClick={
        () => {
        getthis(that);
        }
        }>
        {this.state.value}
      </button>
    
 //另一种方法更简单，在构造函数中，绑定成员函数的 this 指向。在类里面，只有构造函数和生命周期函数可以获取到 this
 constructor(props) {
    super(props);
    this.state = {value: true};
    // 为了在回调中使用 `this`，这个绑定是必不可少的    
    this.handleClick = this.handleClick.bind(this); 
 }
  handleClick() {    
      this.setState({value:"X"});  
  }
 //还有一种办法就是 把成员函数设置成 箭头函数
getthis2=()=>{
    this.setState({value:"X"});
  }
render() {
    return (
      <button className="square"  onClick={this.getthis2}>
        {this.state.value}
      </button>
    );

```

2.为什么通过手动改变浏览器的路径可以切换路由，但是把 Link 和 Route 分开写，点击 Link 改变了路径却没有切换路由。

# 创建React项目

一、可以直接引用 js 文件使用。

二、使用脚手架安装React项目

```javascript
--安装全局脚手架
npm install-g create-react-app
--创建项目
npx create-react-app projectName
--或者
create-react-app projectName
```

# JSX语法

## 创建 js 对象

即创建 html 元素对象。每一个元素对象有且只有一个根元素。

```react
let el=<h1>hello</h1>
//如果元素节点比较多，为了方便代码的读写 可以用括号括起来
let el=(
    <div>
        <h1>hello</h1>
        <h2>你好</h2>
    </div>
);
```

###   Fragment标签

如果在外面添加一层无关的 div 进行包裹 jsx 对象会有影响，可以使用标签 Fragment 进行包裹，渲染到界面后这个标签会消失。

#### 引入组件 Fragment

```javascript
import React,{Component,Fragment } from 'react'
```

#### 使用 Fragment

```jsx
return  (
            <Fragment>
               <div><input /> <button> 增加服务 </button></div>
               <ul>
                   <li>头部按摩</li>
                   <li>精油推背</li>
               </ul> 
            </Fragment>
        )
```



## 插值表达式

react的插值表达式是单括号。在 react 的插值表达式中，也可以使用简单的逻辑。比如 三元运算符。复杂的逻辑则不行。

```react
let time=new Date().tostring;
let clock=<h1>现在时间是：{time}</h1>
```

## 类名

JSX元素对象中添加类名 不能写 class。因为样式 class  和 js 的关键字 Class 重复了。我们用 className 给元素添加样式类名。

```react
let clock=<h1 className="clockstyle">现在时间是：{time}</h1>
```

多个类名 用空格隔开

```react
let clock=<h1 className="clockstyle1 clockstyle2">现在时间是：{time}</h1>
//如果是变量形式的类名 需要做一些处理  比如 {class1+" "+class2}
//也可以先放进数组中，再通过 join() 函数进行转换成字符串形式，中间用 空格连接
```

## 行内样式

jsx对象也可以像普通 html 代码一样，通过 style 添加行内样式。只不过在 jsx 中，style 接受的是一个对象，不是一个字符串。

```react
//正确写法
let clock=<h1 style={{height:200px}}>现在时间是：{time}</h1>
//错误写法
let clock=<h1 style="height:200px">现在时间是：{time}</h1> 
//直接定义一个对象，进行赋值
let styobj={
    color:"red",
    backgroundImg:"url(./img/p1.png)", //对象形式的写法中，属性不可以使用连字符，需要使用驼峰命名书写属性名。
    "margin-top":"20px"//或者使用双引号引起属性名
}
let clock=<h1 style={styobj}>现在时间是：{time}</h1>
```

# 组件的创建

1. **创建一个组件**

2. **组件引用自己本身元素属性的值** 。**props   元素上的属性值数组**  这是一个只读属性。通过props父组件可以给子组件传递数据。即**在子组件上添加自定义属性**。

3. **组件的私有属性写在构造函数的 state  上**。这里面的数据和页面是单向绑定的关系。

4.  **组件名称必须以大写字母开头**。

   React 会将以小写字母开头的组件视为原生 DOM 标签。例如，`` 代表 HTML 的 div 标签，而 `` 则代表一个组件，并且需在作用域内使用 `Welcome`

## 函数组件

```react
//函数组件 props 需要写在形参上，没有state属性;
function Welcome(props) {
  return(<h1>Hello, {props.fathername}</h1>);
}
//调用就是
<Welcome fathername={"hello"}></Welcome>
//或者
<Welcome fathername={"hello"}/>


//一般简单的组件可以写成 函数组件，如果组件有事件的话，建议写成类组件，因为在函数中写函数的话不是很方便。
```

## 类组件

```react
class Square extends React.Component {
  render() {//这个函数就是渲染函数
    return (
      /*
      这里面是html代码片段，代码片段里的插值表达式使用 {}
      */
    );
  }
}

//类组件  props 和 state 已经封装在 this中了
class Square extends React.Component {
   //构造函数里一定要调用 super(props)
   //和一般的类一样，可以拥有自己的自定义属性，在构造函数中进行定义。
   constructor(props) {
	    super(props);
		this.state={value:null}
	}; 
   render() {
    return (
      <button className="square" >
        {this.props.value} /* props 是组件元素上的属性数组 */
      </button>
    );
   }
}
```

# 组件的组合

即在某一个组件中引用其他组件。这就会形成父子组件。

1. **引用其他组件，来创建组件=》父子组件**
2. **通过给子组件添加自定义属性，达到传参的目的**

```javascript
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}

class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i}/>; //父组件通过属性传递参数给子组件。
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}//引用子组件
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
      </div>
    );
  }
}
```

# props校验

父子组件传值时，如果数据太多，很可能就会出现传递错误的情况。而传递错误 、甚至不进行传递，是不会报错的。这样的错误我们一般很难发现。所以我们可以使用 提供的一个功能进行 props 校验。

### prop-types

##### 导入 prop-types

```js
import PropTypes from 'prop-types'
```

#####  使用prop-types进行校验

 需要注意的是子组件的最下面（不是类里边)

+ 验证属性的 类型
+ 验证属性的 必填
+ 规定属性的默认值

```js
MyComponent.propTypes = {
  // 你可以将属性声明为 JS 原生类型，默认情况下
  // 这些属性都是可选的。
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // 任何可被渲染的元素（包括数字、字符串、元素或数组）
  // (或 Fragment) 也包含这些类型。
  optionalNode: PropTypes.node,

  // 一个 React 元素。
  optionalElement: PropTypes.element,

  // 一个 React 元素类型（即，MyComponent）。
  optionalElementType: PropTypes.elementType,

  // 你也可以声明 prop 为类的实例，这里使用
  // JS 的 instanceof 操作符。
  optionalMessage: PropTypes.instanceOf(Message),

  // 你可以让你的 prop 只能是特定的值，指定它为
  // 枚举类型。
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // 一个对象可以是几种类型中的任意一个类型
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),

  // 可以指定一个数组由某一类型的元素组成
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // 可以指定一个对象由某一类型的值组成
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),

  // 可以指定一个对象由特定的类型值组成
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),

  // An object with warnings on extra properties
  optionalObjectWithStrictShape: PropTypes.exact({
    name: PropTypes.string,
    quantity: PropTypes.number
  }),

  // 你可以在任何 PropTypes 属性后面加上 `isRequired` ，确保
  // 这个 prop 没有被提供时，会打印警告信息。
  requiredFunc: PropTypes.func.isRequired,

  // 任意类型的必需数据
  requiredAny: PropTypes.any.isRequired,

  // 你可以指定一个自定义验证器。它在验证失败时应返回一个 Error 对象。
  // 请不要使用 `console.warn` 或抛出异常，因为这在 `onOfType` 中不会起作用。
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },

  // 你也可以提供一个自定义的 `arrayOf` 或 `objectOf` 验证器。
  // 它应该在验证失败时返回一个 Error 对象。
  // 验证器将验证数组或对象中的每个值。验证器的前两个参数
  // 第一个是数组或对象本身
  // 第二个是他们当前的键。
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};

//设置属性的默认值
XiaojiejieItem.defaultProps = {
    avname:'松岛枫' //规定组件的属性 avname 默认值是 松岛枫
}
```

# state

state 就是组件的私有属性。在构造函数中进行初始化。更新 state 可以达到更新视图的效果。

```react
constructor(props){
    super(props);
    this.state={
      name:"夏敏",
      age:22,
      mess:{id:"001",identity:"student"}
    };
  };
```

## 更新state

更新 state  的值不能通过赋值的形式来改变，需要使用特定的函数进行更新。

```react
//单个属性更新
this.setState({name:"思思"});
//多个属性一起更新
this.setState({
        name:"思思",
        age:23
      });
//对象形式的属性，如果只改变其中一个属性，那么这个对象的其他属性就没有了。
this.setState({mess:{
    id:"002"
}});
console.log(this.state.mess)//{id:"002"},没有其他属性了。
```

## 巨大的坑

虽然直接操作 state里面的数据，并不会报错。但是 **不允许直接操作 state** 里面的数据。 

```	javascript
//比如 state 中有一个 数组 arr[]  你需要使用上一个 arrp[] 来更新新的 arr[]
//错误的做法
	this.state.arr.push(2)  //往 arr[] 中添加一个数 2 。这样达不到更新视图的效果
	//你可能会想到，把这个改变后的数据再赋值给 arr[]
	this.setstate({arr:this.state.arr}) //这样的作法虽然使得视图更新，且不报错。但是 不允许
//正确的做法
	let arr2=[...this.state.arr];//一语惊醒梦中人 let arr2= this.state.arr;不是同一个地址吗
	arr2.push(2);
	this.setstate({arr:arr2})
```



# 子元素向父元素传递数据

父元素向子元素传递数据使用 自定义属性进行传递，子元素通过 props 进行获取。

子元素向父元素传递数据也是类似。父元素向子元素传递一个 函数。子函数获取之后进行执行。函数里面对父元素的数据进行更改，就达到了向父元素传递数据的效果。

# 渲染组件

ReactDOM.render(内容,目标对象) 是渲染方法，所有的 js,html 都可通过它进行渲染绘制，他有两个参数，内容和渲染目标 js 对象。

**内容**就是要在渲染目标中显示的东西，可以是一个 React 组件，也可以是一段HTML或TEXT文本。

**渲染目标JS对象**，就是一个DIV或TABEL,或TD 等HTML的节点对象。

```react
//首先要引入 react-dom
import ReactDom from 'react-dom'
//创建组件
let time=new Date().tostring;
let clock=<h1>现在时间是：{time}</h1>
//渲染到 index.html的 root 元素中.默认是在 public 的 index.html
ReactDom.render(<clock></clock>,document.getElementById("root"));

```

# ref

ref 即为引用，和 vue 中的 ref 很相似。即 引用元素本身，如果是引用的 **html元素** 则可以用来操作 dom 。也可以用来获取元素身上的属性。引用之后得到的就是一个**原生的 Dom 对象**，就可以使用 **Dom 对象的原生方法**去操作 Dom 。如果引用的是一个 组件，那么得到的是一个 组件实例，可以调用实例的数据和方法。需要注意的是，函数组件没有实例，所以不能引用函数组件。

示例：

### 第一个方法

在需要引用的元素上写上 ref  属性。 把 元素本身 赋值 给 this 。通过 this 获取到该元素的引用

```react
<input 
    id="jspang" 
    className="input" 
    value={this.state.inputValue} 
    onChange={this.inputChange.bind(this)}
//关键代码——----------start
//把 input 元素本身 赋值给 this.input那么在组件中就可以通过 this.input 进行数据获取和 dom 操作
    ref={(input)=>{this.input=input}} 
 //关键代码------------end
/>

//获取数据
inputChange(){
    this.setState({
        //通过原生的Dom对象方法获取 input 的value值，就不需要使用 e.target.value 
        inputValue:this.input.value 
    })
}
```

### 第二种方法

Refs 是使用 `React.createRef()` 创建的，并通过 `ref` 属性附加到 React 元素。在构造组件时，通常将 Refs 分配给实例属性，以便可以在整个组件中引用它们。

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();  //创建 refs
  }
  render() {
    return <div ref={this.myRef} />;  //将 div 作为引用 赋值给 this.myRef.current
  }
}
```

#### 访问 Refs

当 ref 被传递给 `render` 中的元素时，对该节点的引用可以在 ref 的 `current` 属性中被访问。

```js
const node = this.myRef.current;
```

以上示例都是 引用 原生的 Dom 元素，引用 类组件是一样的，只是能用的东西不一样。

# 已渲染组件的不可变性

##  重新渲染

更新 UI 唯一的方式是创建一个全新的元素，并将其传入 [`ReactDOM.render()`](https://react.docschina.org/docs/react-dom.html#render) 重新渲染

## 更新 state 的属性值

更新 UI 唯二的方式就是更新 **state** 的值。不管这个 state 的值是否会影响页面的数据，都会导致组件的重新渲染。

但是不能直接进行赋值，需要使用函数   **`setState()`** 。构造函数是唯一一个直接给 state 赋值的地方。

```javascript
this.setState({comment: 'Hello'});//并不是说重新给 state 赋值一个新对象，只是修改其对应的属性值
```

**注意的是：state  `props` 的更新时异步的所以你不要依赖他们的值来更新下一个状态。**

例如，更新全名可能会出错（全名 = 姓 + 名 ）

```js
// Wrong
this.setstate({
    name:"Xiamin"
});
this.setstate({fullName:this.state.firstName+this.state.name});//此时 name 未更新完成
```

要解决这个问题，可以让 `setState()` 可以有两个参数。第二个参数就是更新完状态的回调函数。此时状态已经更新完毕了。

```react
this.setstate({name:"xiamin"},()=>{
    this.setstate({fullName:this.state.firstName+this.state.name})
});
```

## 父元素重新渲染

父元素的重新渲染会导致子元素的重新渲染。只要父元素重新渲染，不管 props 是否发生变化，子元素都会跟着重新渲染。如果不想要无效的渲染，可以在生命周期函数  shouldComponentUpdate(nextProps,nextState) 中阻止重新渲染。

# 生命周期函数

只有在生命周期函数中才能获取到 **this** 指向组件。其他成员函数并不能获取到指向组件的 this 。但是使用箭头函数来构建普通成员函数就可以获取到 this 。

react 组件的生命周期分为三个阶段 :**挂载阶段 更新阶段   卸载阶段**

## 挂载阶段

### 1.1.constructor()

constructor()中完成了React数据的初始化，只执行一次。它接受两个参数：props和context，当想在函数内部使用这两个参数时，需使用super()传入这两个参数。
注意：只要使用了constructor()就必须写super(),否则会导致this指向错误。

### 1.2componentWillMount()

**已弃用 ** 

componentWillMount()一般用的比较少，它更多的是在服务端渲染时使用。它代表的过程是组件**已经经历了constructor()初始化数据**后，但是还未渲染DOM时。在这里更新 state 不会引起组件的重渲染。因为此时组件还没有开始第一次渲染。  该周期只执行一次，即组件挂载前，重新渲染的时候不会回到这个生命周期。但是有一说一，组件的实例之间是互不干扰的。即每调用一次组件都需要经历一次挂载。如下：组件 com 挂载了三次

```react
<div>
	<com></com>
	<com></com>
	<com></com>
</div>    
```

### 1.3 render()

render函数会插入jsx生成的dom结构，react会生成一份虚拟dom树。就是渲染到页面上。

### 1.4componentDidMount()

组件**第一次渲染完成** 即 挂载完成，此时dom节点已经生成，可以在这里调用ajax请求，返回数据setState后组件会重新渲染.一般都在这里进行数据请求。

## 更新过程

### state 更新

#### 1、shouldComponentUpdate(nextProps,nextState)

1. 主要用于性能优化(部分更新)

2. 唯一用于控制组件重新渲染的生命周期，由于在react中，setState以后，state发生变化，组件会进入重新渲染的流程，在这里**return false**可以阻止组件的更新，**后面几个生命周期都不会执行** 。 return true 流程则正常执行。即 **false 一定不会重新渲染， true 不一定会重新渲染（但是 state 都发生改变了，正常流程应该需要重新渲染了）**

3. **因为react父组件的重新渲染会导致其所有子组件的重新渲染**，这个时候其实我们是不需要所有子组件都跟着重新渲染的，因此需要在子组件的该生命周期中做判断

4. 示例：子组件只接收了来自父组件的 name 属性，所以只有当 props.name 发生改变数才重新渲染

   ```js
   shouldComponentUpdate(nextProps,nextState)
   {
       if(this.props.name===nextProps.name)
           return false; //name 值没有发生改变，不重新渲染
       else
           return true //name 发生改变，所以重新进行渲染
   }
   ```

####    2、componentWillUpdate (nextProps,nextState)

​	shouldComponentUpdate返回true以后，组件进入重新渲染的流程，进入componentWillUpdate,这里同样可以拿到nextProps和nextState。

####     3、render()

​	render函数会插入jsx生成的dom结构，react会生成一份虚拟dom树，在每一次组件更新时，在此react会通过其diff算法比较更新前后的新旧DOM树，比较以后，找到最小的有差异的DOM节点，并重新渲染。

**render()里不能更新 state**，否则会陷入死循环。

#### 4、componentDidUpdate(prevProps,prevState)

​	组件更新完毕后，react只会在第一次初始化成功会进入componentDidmount,之后每次重新渲染后都会进入这个生命周期，这里可以拿到prevProps和prevState，即更新前的props和state。

### Props 更新

#### 1、 componentWillReceiveProps (nextProps)

0. **只要父组件重新渲染了，就会执行这个函数，不管 props 有没有发生变化**

1. 在接受父组件改变后的props需要重新渲染组件时用到的比较多（第一次挂载到 Dom 不会执行）
2. 接受一个参数nextProps；新的 props
3. 通过对比nextProps和this.props，将nextProps的state为当前组件的state，从而重新渲染组件。可是我直接初始化时，把 props的 某个值作为 state 的某个值不是一样的效果吗？
4. 这边也可以看出，就算componentWillReceiveProps()中执行了this.setState，更新了state，但在render前，如shouldComponentUpdate，componentWillUpdate 周期中，this.state依然指向更新前的state，不然nextState及当前组件的this.state的对比就一直是true了。

#### 2、shouldComponentUpdate(nextProps,nextState)

#### 3、componentWillUpdate (nextProps,nextState)

#### 4、render()

#### 5、componentDidUpdate(prevProps,prevState)

## 卸载

### componentWillUnmount ()

当组件从 dom树中被移除时发生。

```react
//当 isshow 从 true 状态变为 false 状态，此时就会发生这一事件
{this.state.isshow?<Child></Child>:null}
```

在此处完成组件的卸载和数据的销毁。

1. clear你在组建中所有的setTimeout,setInterval

2. 移除所有组建中的监听 removeEventListener

3. 有时候我们会碰到这个warning

   ```javascript
   Can only update a mounted or mounting component. This usually      means you called setState() on an unmounted component. This is a   no-op. Please check the code for the undefined component.
   ```

    因为你在组件中的ajax请求返回setState,而你组件销毁的时候，请求还未完成 。

## React新增的生命周期

### 3.1. getDerivedStateFromProps(nextProps, prevState)

代替componentWillReceiveProps()。
老版本中的componentWillReceiveProps()方法判断前后两个 props 是否相同，如果不同再将新的 props 更新到相应的 state 上去。这样做一来会破坏 state 数据的单一数据源，导致组件状态变得不可预测，另一方面也会增加组件的重绘次数。应该声明为  static **类的静态成员函数**。

```javascript
// before
componentWillReceiveProps(nextProps) {
  if (nextProps.isLogin !== this.props.isLogin) {
    this.setState({ 
      isLogin: nextProps.isLogin,   
    });
  }
  if (nextProps.isLogin) {
    this.handleClose();
  }
}

// after
static getDerivedStateFromProps(nextProps, prevState) {
    //这里拿不到 this.props。只能去比较之前的 state 值 。因为这里拿不到 this 。这个方法应该被声明为静态方法  staic
    //也就是说这里也不能改变 state 值，只能放到下一个生命周期 componentDidUpdate 中更新
  if (nextProps.isLogin !== prevState.isLogin) {
    return {
      isLogin: nextProps.isLogin,
    };
  }
  return null;
}

componentDidUpdate(prevProps, prevState) {
  if (!prevState.isLogin && this.props.isLogin) {
    this.handleClose();
  }
}
```

这两者最大的不同就是:
 在 componentWillReceiveProps 中，我们一般会做以下两件事，一是根据 props 来更新 state，二是触发一些回调，如动画或页面跳转等。

1. 在老版本的 React 中，这两件事我们都需要在 componentWillReceiveProps 中去做。
2. 而在新版本中，官方将更新 state 与触发回调重新分配到了 getDerivedStateFromProps 与 componentDidUpdate 中，使得组件整体的更新逻辑更为清晰。**而且在 getDerivedStateFromProps 中还禁止了组件去访问 this.props，强制让开发者去比较 nextProps 与 prevState** 中的值，以确保当开发者用到 getDerivedStateFromProps 这个生命周期函数时，就是在根据当前的 props 来更新组件的 state，而不是去做其他一些让组件自身状态变得更加不可预测的事情。

### 3.2. getSnapshotBeforeUpdate(prevProps, prevState)

代替componentWillUpdate。 常见的 componentWillUpdate 的用例是在组件更新前，读取当前某个 DOM 元素的状态，并在 componentDidUpdate 中进行相应的处理。
 这两者的区别在于：

1. 在 React 开启异步渲染模式后，在 render 阶段读取到的 DOM 元素状态并不总是和 commit 阶段相同，这就导致在
    componentDidUpdate 中使用 componentWillUpdate 中读取到的 DOM 元素状态是不安全的，因为这时的值很有可能已经失效了。
2. getSnapshotBeforeUpdate 会在最终的 render 之前被调用，也就是说在 getSnapshotBeforeUpdate 中读取到的 DOM 元素状态是可以保证与 componentDidUpdate 中一致的。
    此生命周期返回的任何值都将作为参数传递给componentDidUpdate（）。

# 事件处理

事件处理中， 事件对象 e  ，需要进行传递吗？ 参数如何传递？

调用的时候，事件对象 e 不需要传递，但是如果函数本身还有其他参数，就需要通过下面两种方法进行传递事件对象。

## 参数传递

事件里面 需要写一个 事件对象，而不是字符串。所以不能带 括号传递参数

```javascript
<button className="square"  onClick={this.getthis2}>
        {this.state.value}
</button>
```

### 通过箭头函数

在事件中写一个箭头函数，箭头函数中调用 函数，并进行传参。 此时事件对象  e 需要显式传递 

```javascript
getthis2=(e)=>{
    this.setState({value:"X"});
    console.log(e);
}
<button className="square"  onClick={
        (e)=>{this.getthis2(e);}
        }>
        {this.state.value}
</button>
```

### 通过 bind方式

通过bind方式为函数绑定参数，此种方式 事件对象 e 是隐式传递。

**注意： e 需要放在最后一个参数**

```javascript
this.getthis=this.getthis.bind(this,"hello");//绑定参数

getthis(mess,e){
    this.setState({value:"X"});
    console.log(mess);
    console.log(e);
}

<button className="square"  onClick={
        this.getthis
        }>
        {this.state.value}
</button>

//上面这种方式可能看起来不方便，因为全都是在构造函数中绑定的参数，但是其实也可以直接在 事件中绑定。
//如下：
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

## 事件名称的写法

react 中事件的名称和原生事件名称写法不一样。react 使用小驼峰写法，即 第一个单词首字母小写，后面单词首字母大写。

```react
<button onClick={}></button>
```

## 默认事件-事件冒泡

原生 js  的阻止默认、冒泡事件，可以通过 return false 。但是在 react 中只能通过事件对象进行阻止默认事件，

```react
e.preventDefault();
```



# 条件渲染

react的条件渲染，和其他框架不一样，react 没有指令一说，只能通过 javascript 对组件进行控制。显然，通过 if

进行判断就是 react 的条件渲染。

就两种方向：控制返回的组件  控制渲染的组件 。全靠自己写js去判断控制。

## 判断渲染某个组件

通过判断，控制渲染的对象是哪个。

```javascript
function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
function Greeting(props) {
   const isLoggedIn = props.isLoggedIn;
   if (isLoggedIn) {    return <UserGreeting />;  }  
   return <GuestGreeting />;
}
```

## 控制返回的对象

通过判断条件，控制返回对象的是什么。返回 null 就是返回一个空组件。

```javascript
function LogoutButton(props) {
   if(res)
       return(
        <button onClick={props.onClick}>
          Login
        </button>
       );
    else
      return (
        <button onClick={props.onClick}>
          Logout
        </button>
      );
}
	
```

## &&运算符

之所以能这样做，是因为在 JavaScript 中，`true && expression` 总是会返回 `expression`, 而 `false && expression` 总是会返回 `false`。

因此，如果条件是 `true`，`&&` 右侧的元素就会被渲染，如果是 `false`，React 会忽略并跳过它

```javascript
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {
      unreadMessages.length >0&&<h2> You have unread.messages.</h2>      
	  }    
    </div>
  );
}
```

## 三目运算符

就很简单啊

```javascript
{
    2>0?<h1>我是真的情况下显示的组件h1</h1> : <h1>我是假的情况下显示的组件h1</h1>
}
```



# 列表渲染

同样的，列表渲染同样是通过 js  生成一个 组件数组。再把这个组件数组渲染出来。

用到的函数是数组的 map 函数。它可以遍历数组，并返回一个我们想要生成的新数组。

## 生成组件数组

```javascript
//回顾map()
//arr.map()重构数组，返回一个数组
var arr=[1,2,3]
let res2=arr.map(function(val,index,arr){//默认一个参数的话就是 数组的值
    console.log(val);
    return val+index;
});
//res2 是arr中 值与下标和的数组 1  3  5

//------------------------------------------------------

const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>  <li>{number}</li>);
/*
 <li>1</li>
 <li>2</li>
 ...
*/
```

## 渲染组件数组

```javascript
ReactDOM.render(
  <ul>{listItems}</ul>,  
  document.getElementById('root')
);
```

## key值

和其他框架一样。列表渲染的时候，都希望你给每个元素提供一个 key  值，以便区分渲染出来的单个元素。后续如果你更新数组，就会根据 key 值来判断哪些元素是不需要进行更新的，以避免元素的重复渲染，提高渲染效率

```javascript
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map(
  (number)=><li key={number.toString()}>{number}</li>
);
```

需要注意的是：key 属性不会出现在组件的元素中。

# 表单控件

在react中，表单控件 input textarea select 可以把 value 属性绑定在 state 的值中。此时，表单控件就是 **受控控件**。

## input

```javascript
<input type="text" placeholder="选填" value={this.state.reason}/>
```

此时，如果没有给表单控件 input 。添加一个 **onchange()** 函数，用户输入则不会成功。

```javascript
whenchange=(inputindex,e)=>{
        if(inputindex===0)
        {
            this.setState({reason:e.target.value});
        }
        else
        this.setState({measure:e.target.value});
    }
<input type="text" placeholder="选填" value={this.state.reason} onChange={(e)=>{this.whenchange(0,e)}}/>
```

## textarea 标签

HTML 的 textara 标签 

```
<textarea>
  你好， 这是在 text area 里的文本
</textarea>
```

react 中的textarea 标签

 `` 使用 `value` 属性代替。这样，可以使得使用 `` 的表单和使用单行 input 的表单非常类似： 

```javascript
<textarea value={this.state.value} onChange={this.handleChange} />
```

## select 标签

HTML 中的 select 标签,通过给子元素 设置 selected 来判断哪一项被选择

```HTML
<select>
  <option value="grapefruit">葡萄柚</option>
  <option value="lime">酸橙</option>
  <option selected value="coconut">椰子</option>
  <option value="mango">芒果</option>
</select>
```

react 中依旧使用 value 来决定某一项值被选中

```javascript
<form onSubmit={this.handleSubmit}>
        <label>
          选择你喜欢的风味:
          <select value={lime} onChange={this.handleChange}>            <option value="grapefruit">葡萄柚</option>
            <option value="lime">酸橙</option>
            <option value="coconut">椰子</option>
            <option value="mango">芒果</option>
          </select>
        </label>
        <input type="submit" value="提交" />
      </form>
```

# React动画

css3的关键帧当然也能实现动画效果，但是无法实现元素的移除之类效果。

### 安装react-transition-group

react  官方 推出的一个 动画库

```cmd
npm install react-transition-group --save
```

### 使用

和 Vue 中的动画使用很类似。具体可以学习官方的 API 文档。暂时先不细学。



# 插槽

React的插槽和VUE相比相对复杂一些。原理就是父组件可以给子组件传递 props 。子组件的插槽预留的位置就是 props 的某一个 dom、组件、文本对象。父组件给子组件传递的 dom 、jsx  在props的 children 数组中。

```react
//子组件预留插槽位置。
//可以直接使用 {this.props.children[0]}通过插槽的索引值预留位置。插槽对象也可以有 props ，所以也可以使用一个自定义的变量预留位置，再对整个 children 进行判断再给这个对象进行赋值。
render(){
        console.log(this.props.children[0].props.position);//获取某个插槽的属性
        return(
            <div>
                this is head: <br></br>
                {this.props.children[0]}
                this is body: <br></br>
                {this.props.children[1]}
                this is footer: <br></br>
                {this.props.children[2]}
            </div>
        );
}

//父组件传递插槽  每一个根就是一个插槽，好像是按顺序存入数组。可以给每一个插槽添加自定义属性。会传入插槽的 props 中。所以子组件也可以通过 插槽的自定义属性值来区分不同的插槽，而不是单纯的通过索引值来添加插槽。
<ChildrenCom>
    <div position="head">这是父组件传过来的插槽---头部</div>
    <div>这是父组件传过来的插槽---主体</div>
    <div>这是父组件传过来的插槽---尾部</div>
</ChildrenCom>
```

# 路由

要始终清楚的认识到 路由切换的不是页面 是组件，**控制某块区域组件的切换**。并不是切换页面。

## 安装路由

```node
npm install react-router-dom --save
```

## 导入路由模块

```react
//react 路由分为 hash 模式 和 history 模式
//1、 hash 模式需要的路由模块 # hash值的变化不会导致页面请求
import {HashRouter as Router,Link,Route} from 'react-router-dom'
//2、 history 需要用到的路由模块 / 和后端配合使用，即使是 / 后面的路径发生改变也不会发送请求
import {BrowserRouter as Router,Link,Route} from 'react-router-dom'
```

## 使用路由

感觉 react 的路由很不方便和 vue 相比。路由链接 Link 和路由模块 Route 都必须写在同一个 根 Router 下。

如果路由组件 还有 子路由，就必须自己再写一个 Router ,否则就会被父组件的 Router 包括，改变的就是父组件的路由地址。

```react
//basename 即 基本路径 、默认根路径。会自动加到 Link 、Route 的路由路径上
//Router 不会转化成 html 元素。渲染到页面中就消失了。Router 中可以写入除了路由外的其他元素，可以正常显示。
<Router basename="student/"> 
    <div>
        {/*路由链接 Link 默认被渲染成一个 a 标签。 to 属性对应着 route 的 path*/}
        <Link to="/">首页</Link> <br/>
        {/* 默认地址的切换是一个追加操作， replace 代表的是替换，会把前一个路由地址在历史记录中删除，就是不能再回退到前一个页面 */}
        <Link to="/self" replace >个人中心</Link><br/>
        <Link to="/study">学习中心</Link><br/>
        
    </div>
    <br/>
    其他东西 
    <br/>
    {/* Route 标签 path 对应着当前路径，显示相应的组件。compoent 必须是一个组件 */}
    {/* 
    exact 表示精确，普通的匹配规则是 包含匹配 ，只要包含某个路径就会显示对应的组件。 
    利用这一特性我们可以实现同一个路径显示多个路由组件的效果，但实际上只需要写多个相同路径，
    不同组件的Route，就可以实现相同路径显示多个不同组件的效果。
    */}
    
    {/* 
    Route  标签好像也不会被渲染在页面上
    Router 标签不会被渲染在页面上
    */}
    <Route path="/" exact component={Home}></Route>
    <Route path="/self"  component={Self}></Route>
    <Route path="/study" component={Study}></Route>
</Router>
```

### 路由组件特有的属性

路由组件的 props 自带 三个属性

#### match

这个属性里面包含路由规则、组件对应的路由地址、动态路由传递的参数等等

#### history

这个属性包含着一些属性和方法，包括 当前路由的操作是什么，提供了一些路由历史记录的操作，比如回退、前进路由历史。

#### location

地址的一些属性，当前url 地址，search 即 地址上传递的参数等

### to 属性

Link 链接的 to 属性代表了跳转的地址。可以接受一个字符串，代表跳转的地址。除了可以改变地址，还可以带 参数  、哈希值、状态。所以 to 属性也可以接收一个对象。**这个对象会随着跳转，添加在对应组件的 props.location 中**

```react
let tomess={
    pathname:"/self", //跳转的地址
    search:"?name=xiamin&age=22", //地址带的参数
    hash:"#student", //哈希值
    state:{mess:"hello router"} //状态
}
<Link to={tomess}>个人中心</Link><br/>
// Link标签会进行拼接 /student/self?name=xiamin&age=22#student
```

### 动态路由

在 Link 跳转的路径中可以给组件传递参数。

```react
<Link to="/study/20173033103">学习中心</Link><br/>
//需要注意的是 如果使用了 动态路由  路径不传递任何值，这样是匹配不到 路由的。 比如下面这样
<Link to="/study">学习中心</Link><br/>
//所以如果想要可以不传 也可以传值的匹配路由，可以使用 对象形式的 to 属性
```

在组件中获取路径中的参数

```react
//这样获取到的数据就是  id=20173033103 
<Route path="/study/:id" component={Study}></Route>
```

**这个参数在组件的 props.match.params中保存**

## 重定向路由

重定向，故名思意会改变页面的路径。跳转到其他的组件。和 **Link** 的区别就是会**自动跳转**。两种方式可以实现页面的重定向 一种就是 使用重定向组件 Redirect  一种是使用 js方法进行路由的管理

### 引入路由模块

```react
import {HashRouter as Router,Link,Route,Redirect} from 'react-router-dom'
```

### 使用重定向路由

```react
//这个组件就是用来重定向的。没有自己的内容，只是切换了地址。从而切换了路由，显示其他组件
let Islogin =(props)=>{
  if(props.location.state.status==="success")
  return <Redirect to="/home"></Redirect>
  else
  return <Redirect to="/error"></Redirect>
}
```

## history 重定向

路由组件的 props 中都有一个 history 。里面记录着 组件的路由操作：push  pop replace 之类。还有一些路由操作函数 push go  goBack goForward replace

### push

push 一个路由地址（就是添加一个界面放入最顶部）

```react
//第一个参数是路由地址 第二个参数是传给组件的 state 可以省略
this.props.history.push("/home",{name:"xiamin"})
```

### replace

移除自己路由地址，跳转到其他路由地址。（不能回退到自己了）

```react
//第一个参数是路由地址 第二个参数是传给组件的 state 可以省略 
this.props.history.replace("/home",{name:"xiamin"})
```

### go

正数表示向前进几个路由；负数表示后退几个

```react	
this.props.history.go(2);
```

###  goBack

回退（后退）一个路由 goBack()；

```react
this.props.history.goBack();
```

### goForward

前进一个路由

```react
this.props.history. goForward();
```



## Switch

Switch这个组件的作用就是用来限制路由选择的，上面我们说了，react 选择路由会有缺陷，会一次选择到多个路由。 比如 /a  会选择到  /    和  /a 。一般我们用 exact 表示精确选择。用 switch 把 Router 包裹起来。路由选择只会选择一个，但是是按顺序先后进行选择。

```react
<Switch>
    <Route path="/" exact component={()=>{return <h1>去登陆</h1>}}></Route>
    <Route path="/islogin" exact component={Islogin}></Route>
    <Route path="/error" exact component={Error}></Route>
    <Route path="/home" exact component={Home}></Route>
    <Route path="/self"  component={Self}></Route>
    <Route path="/study/:id" component={Study}></Route>
</Switch>
```

# Redux

解决React 数据管理（状态管理)，用于中大型，数据比较庞大，组件之间数据交互多的情况下使用。如果你不知道是否需要使用Redux，那么你就不需要用它!

+ 解决组件的数据通信。
+ 解决数据和交互较多的应用

Redux 只是一种状态管理的解决方案，完成这个解决方案还是靠如下：

+ Store:数据仓库，储存数据的地方
+ State:State 是一个对象，数据仓库所有的数据都放在**同一个  state** 里面
+ Action: 一个动作，动作就是用来改变数据的方法。
+ DisPath: 触发动作的方法
+ Reducer: 是一个方法，获取动作从而改变数据，生成一个**新的 state** 进而改变页面
+ subscribe: 是一个方法，用于监听仓库的变化，变化的话你可以重新渲染。

## 安装 redux

```react
npm i redux --save
```

## 引入Redux

```react
import {createStore} from 'redux'
```

## 创建仓库

```react
//仓库 Store 的创建 需要一个 Reducer 。就是一个自定义的方法。用来获取 action ，返回新的状态
reducer=function(state={num:0},action){
    //最好不要直接修改 state ，先进行一次深度拷贝，再把 state 进行返回是最好的
    let newState={...state}
        if(action.type==="add")
        newState.num++;
        else
        newState.num--;
        return newState;//最好是返回一个新的对象,这里结构后生成一个新对象进行返回
}
//创建仓库
const Store=createStore(reducer);
```

## 触发 action

通过  dispatch()  触发 action 进行状态的更新。

```react	
//函数的参数是一个对象， action 的触发就是通过 判断对象的某些属性进行区分，执行哪个 action 
add=function(){
    Store.dispatch({type:"add",id:20173033});  //参数就是 action
}
sub=function(){
    Store.dispatch({type:"sub",name:"xiamin"});
}
```

小技巧： action 的 type 如果是字符串的话，写错了也不会报错，只是在 reduce 函数中找不到相应的处理方法，会执行默认的处理方法。如果把 type 的值变成一个变量值，写错了就会报错没有这个变量。所以建议，把 type 的值独立成一个 js 文件，导出单独的变量。 使用 dispatch 的页面 和 reducer 的页面都是引用这个 type js 文件。

## 获取仓库的数据

仓库的数据 存在 一个对象中。所有的组件数据，都放在这一个对象里面。各个组件可以获取这个对象。

getState()

```react
let Counter=function(){
    let state=Store.getState();
    return (
        <div>
            <button onClick={add}>+</button>state.num<button onClick={sub}>-</button>
        </div>
    );
}
```

## 监听数据的变化

数据发生改变后，视图不会自动刷新，我们需要对仓库进行一个监听，当监听到数据发生改变时，我可以选择性的进行渲染操作。

```react 
Store.subscribe(()=>{//监听到 仓库发生变化时执行的函数
    //可以重新渲染
    //可以获取仓库数据进行判断。选择要做什么操作。
})
```

## 浏览器插件 redux-tools-dev

安装插件之后，就能看到仓库里的 数据，但是创建仓库的时候，需要多加一个参数，否则浏览器使用插件时候会是一片空白。

```js
const Store=createStore(
    Reducer,
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);

```

## 项目开发编写

1. 建议在项目开发时可以单独建立一个文件夹进行状态管理。 

+ Reducer 的创建单独写一个 js 文件，暴露出去让 store  文件 创建 仓库。这个文件中只进行 actiond的处理

+ store 的创建单独写一个文件夹，主要把仓库 store 暴露出去让其他组件可以进行引用。
+ action 的 type 也全都放在一个 js 文件里，用变量的形式存储，这样填错了 type 会报错。
+ 建议再写一个 创建 action 对象的函数 文件。如果不使用中间件，这个函数可以有一个参数，用于返回一个 action 对象的数据部分。  要是使用中间件，这个函数可以返回一个 函数，再这个函数中可以进行其他操作，包括异步获取数据进行 action的获取。具体看下面 中间件的使用。

2. 分离  UI  和 逻辑代码

+ 使用了状态管理之后，我们可以把组件的 UI 和 逻辑  进行分离。 其实就是写两个组件，逻辑组件和UI 组件，逻辑组件引用 UI 组件，即 逻辑组件是父组件，负责获取仓库的数据，编写逻辑方法，并且 通过 props 把数据和方法传递给 UI 子组件。
+ 无状态组件，即 函数组件 ，没有 state 。只有 props 。既然我们刚刚说的 UI 组件只依靠 逻辑父组件 的传值，那就没有必要 state 。写成 函数组件 要比写成类组件提升很多的性能。

## redux 中间件

### redux-thunk安装

**redux-thunk**  是一款 **redux** 的中间件。注意这不是 react 的中间件。

```cmd
npm install --save redux-thunk
```

#### 导入相关组件

```cmd
import {createStore,applyMiddleware,compose} from 'redux'
import thunk from "redux-thunk";
```

#### 配置

```js
//本来直接把 thunk 放入 创建仓库的第二个参数就可以的，但是因为我们还要兼容 redux-tools-dev 就会多点配置
//不兼容 插件
const store = createStore(
    reducer,
    applyMiddleware(thunk)
) 
//使用 compose 增强函数 。作用类似于 链式函数，执行一个函数后立即执行下一个函数。因为 createStore()第二个参数只能接受一个函数，但是我们需要把 插件的函数和中间件的函数都放进去。
//兼容插件
import { createStore , applyMiddleware ,compose } from 'redux'  
import reducer from './reducer'    
import thunk from 'redux-thunk'

const composeEnhancers =   window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose

const enhancer = composeEnhancers(applyMiddleware(thunk))

const store = createStore( reducer, enhancer) // 创建数据存储仓库
export default store   //暴露出去
```

#### 使用

以前我们 获取异步数据之后，需要先把数据放进 action 中，再通过  dispatch 传递给 仓库。也就是说 dispatch

中只能传递一个对象形式的 action 。那我们就只能把异步请求数据的逻辑放在组件的生命周期中。

使用中间件后，我们可以在 dispatch 中传入一个函数。

```js
//在 创建 actioin 的 js 文件中
//这是一个使用了 中间件后，创建 action 的函数，返回的是一个函数。
//返回的函数中的参数  dispatch 是 store.dispatch(function(this){}) 自动传递的
export const getTodoList = () =>{
    return (dispatch)=>{
        axios.get('https://www.easy-mock.com/mock/5cfcce489dc7c36bd6da2c99/xiaojiejie/getList').then((res)=>{
            const data = res.data
            const action = getListAction(data)//这里才是创建一个action对象。{type:,data}
            dispatch(action)

        })
    }
}

//在组件中调用 dispatch
componentDidMount(){
    const action = getTodoList() //返回的就不是一个对象了，是一个函数
    store.dispatch(action)//自动把 dispath 也就是自己当作参数传入
}

```

###  Redux-saga安装

#### 安装

```cmd
npm install --save redux-saga
```

#### 配置

##### 创建仓库的配置

此中间件 dispath()函数接收的还是一个 对象形式的 action ，逻辑代码会写在一个单独的 js 文件。  

```js
import { createStore , applyMiddleware ,compose } from 'redux'  //  引入createStore方法
import reducer from './reducer'
import mySagas from './sagas' //引入 sagas.js 文件，逻辑代码都写在这个文件中
//------关键代码----start----------- 
import createSagaMiddleware from 'redux-saga' 
const sagaMiddleware = createSagaMiddleware();
//------关键代码----end-----------

const composeEnhancers =   window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ?
    window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose
//------关键代码----start-----------
const enhancer = composeEnhancers(applyMiddleware(sagaMiddleware))
//------关键代码----end-----------

const store = createStore( reducer, enhancer) // 创建数据存储仓库

sagaMiddleware.run(mySagas)//运行逻辑文件

export default store   //暴露出去
```

##### 逻辑文件的编写

 `redux-saga`希望你把业务逻辑单独写一个文件，这里我们在`/src/store/`文件夹下建立一个`sagas.js`文件。 

这个文件需要使用 generator 函数，所有的函数都写成 generator 函数。

```js
import { -takeEvery  } from 'redux-saga/effects'
import {-GET_MY_LIST} from './actionTypes'
import igetListAction}  from './actionCreators'
import axios  from 'axios'
//generator
function*·mySaga(){
 yield takeEvery(GET_MY_LIST, getList  )}
function* getList(){
const res = yield axios.get( 'https://www.easy-mock.com/mock/5cfcce489dc7c36bd6da2cconst·action·= getListAction(res.data);
                            
yield put(action)//这里就不需要使用 dispath     
})

```



# react-redux

这是一个 redux 的插件，省略监听、获取仓库数据步骤。但是多了一个连接步骤（将仓库和组件连接起来，即将数据 和 改变数据的方法 给组件）

## 安装 react-redux

```react
npm i react-redux --save
```

## 导入模块

```react
import React from 'react'
import {createStore} from 'redux'
import {Provider,connect} from "react-redux" 
```

## 创建仓库

```react	
let reducer=function(state={name:"minmin"},action){
    console.log("reducer");
    if(action.type==="add")
    state.name=state.name+"xia";
    else
    state.name=state.name+"ni";;
    return {...state};
}

let Store=createStore(reducer);  

```

## 连接组件

连接组件  传递仓库数据 传递改变数据的方法 。这两个的实现需要通过两个自定义函数，因为

```react
//组件获取仓库数据
class Counter extends React.Component{
    constructor(props){
        super(props)
    }
    render(){
        //通过把数据传给 props 达到数据传递的效果，不需要通过 方法获取 State
        this.name=this.props.name;
        this.change=this.props.change;
        return(
            <div>
                {this.name} <br/>
                <button onClick={this.change}>改变名字</button>
            </div>
        );
    }
}
//创建仓库
let reducer=function(state={name:"minmin"},action){
    console.log("reducer");
    if(action.type==="add")
    state.name=state.name+"xia";
    else
    state.name=state.name+"ni";;
    return {...state};
}

let Store=createStore(reducer);

//传递数据 就是把 仓库的数据 传递给组件的 props
function getvalue(state){// state 可以认为是 仓库的 state ,下面调用时会自动传递参数。 
    return {
        name:state.name
        ...
        key:state.key
    }
} 
//传递方法 把触发方法 传递给组件的 props 使组件可以操作仓库的 state 进行改变
function changeState(dispatch){
    return {
        change:()=>{dispatch({type:"add"})},
        ...
        functionName:()=>{dispath({})}
    }
}
//将这两个方法传给组件的props，组件进行使用就能操控 仓库数据了。这一步将组件封装成了一个新组件 App
let App=connect(getvalue,changeState)(Counter);

```

## Provider组件

自动监听。使用组件 包裹 刚刚生成的新组件，就能实现自动监听数据的变化自动重新渲染。

```react
//属性 store 代表了监听哪个仓库的数据
<Provider store={Store}>
    <App></App>
</Provider>
```

# HOOKS

 `React Hooks`就是用函数的形式代替原来的继承类的形式，并且使用预函数的形式管理`state`，有Hooks可以不再使用类的形式定义组件了。这时候你的认知也要发生变化了，原来把组件分为有状态组件和无状态组件，有状态组件用类的形式声明，无状态组件用函数的形式声明。那现在所有的组件都可以用函数来声明了 

## usestate()

在HOOKS中使用 usestate() 进行状态声明。这个函数接收一个参数，作为某一个状态的初始值。返回值是一个数组，第一个值是状态的名称，我们也可以理解为 key 。第二个值是一个函数，用来改变当前状态的值。

```js
import React, { useState } from 'react';
function Example(){
    //定义一个 初始状态为 0 的状态。我们解构赋值时声明状态的名字叫做 count ，改变状态 count 的方法叫做 setCount()
    //setCount(newCount) 接收一个参数作为新的状态值。进而修改相对应的状态
    const [ count , setCount ] = useState(0);//声明状态
    return (
        <div>
        	//使用状态
            <p>You clicked {count} times</p>
			//改变状态
            <button onClick={()=>{setCount(count+1)}}>click me</button>
        </div>
    )
}
export default Example;
```

**需要注意的是，状态的声明不能出现在 判断语句中，我们可以理解为 状态的声明不能动态的进行。**

错误示例：

```js
import React, { useState } from 'react';

let showSex = true
function Example2(){
    const [ age , setAge ] = useState(18)
    if(showSex){
        const [ sex , setSex ] = useState('男') //报错
        showSex=false
    }

    const [ work , setWork ] = useState('前端程序员')
    return (
        <div>
            <p>JSPang 今年:{age}岁</p>
            <p>性别:{sex}</p>
            <p>工作是:{work}</p>

        </div>
    )
}
export default Example2;
```

##  useEffect()

useEffect(callback) 是一个函数，可以写两个参数，第一个参数是一个函数f1，函数f1的返回值也可以是一个函数f2。我理解成，f1是状态改变完成之后执行的函数，而f2是状态即将发生改变，但是还没改变时执行的函数。第二个参数是一个数组，数组里面写组件对应的状态名称。代表 effect 函数的执行是依赖于哪些状态的改变而执行的。如果不写第二个参数，那么所有状态的改变都会触发 effect 函数的执行。如果数组写成 [] 空数组，代表 effect 函数的执行，不依赖于任何状态，只在组件第一次渲染时执行 f1,组件销毁时执行 f2。

useEffect() 是 hooks 用来代替类组件的生命周期函数的，组件第一次渲染，以及之后的每一次状态更新都会自动触发。 执行回调函数。可以用 Effect 代替 类组件三种生命周期。 组件第一次挂载 、组件数据更新（props、state）、组件卸载--- `componentDidMount`，`componentDidUpdate` 和 `componentWillUnmoun` 

```js
//下面这种写法就是组件的 componentDidMount 和 componentWillUnmoun  两个生命周期
useEffect(()=>{
        console.log("--------组件重新渲染-----");
    return ()=>{
        console.log("-------组件卸载，清除负面效果-----");
    }
},[])
```

##  useContext

类似于 Context  ，方便父子组件，或者说 **祖先组件** 和 **后代组件** 之间的数据传递。

### 创建、声明、获取上下文

```js
import React, { useState , createContext,useContext} from 'react';

const CountContext = createContext()//创建上下文

function Example4(){
    const [ count , setCount ] = useState(0);

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={()=>{setCount(count+1)}}>click me</button>
            {/* 声明上下文的作用范围*/}
            <CountContext.Provider value={count}>
                {/* 在这个范围内的组件都可以使用上下文*/}
				<Counter></Counter>
            </CountContext.Provider>

        </div>
    )
}
function Counter(){
    const count = useContext(CountContext)  //获取上下文
    return (<h2>{count}</h2>)
}

export default Example4;
```

## useReducer

简单的说，reducer 并不只是 redux 独有的，reducer 就是一个函数。接受两个参数，一个状态值，一个action，返回一个状态。

```js
import React, {useReducer} from 'react';
//下面这个函数就是 reducer 
let counter=function (state,action){
        if (action.type==="add")
            return  state+action.value;
        else
            return  state-action.value;
    }
//使用 reducer，返回的是一个数据，第一个值就是返回的状态，第二个字就是 dispath(),触发状态的函数
//useReducer() 第一个参数就是一个 reducer ，第二个值是 默认状态值。
let [num,dispath]=useReducer(counter,0);

//使用reducer的状态值
 my age is {num}
//触发 action 改变状态
<button onClick={()=>{dispath({type:"add",value:1})}} >年纪 + </button>
<button onClick={()=>{dispath({type:"sub",value:2})}} >年纪 - </button>
```

## context +reducer

context +reducer 配合使用可以实现类似于 redux 的效果。

### 创建共享数据组件

```js
//我们可以把 context 写成一个单独的组件，配合路由使用，就可以在上下文组件中插入其他组件
import React, { createContext,useReducer } from 'react';

export const ColorContext = createContext({})

export const UPDATE_COLOR = "UPDATE_COLOR"
//要想改变共享数据，就需要把共享数据变成 reducer 返回的状态，再把 dispath 函数也共享出去
const reducer= (state,action)=>{
    switch(action.type){
        case UPDATE_COLOR:
            return action.color
        default:
            return state
    }
}

export const Color = props=>{
    const [color,dispatch]=useReducer(reducer,'blue')
    return (
        //把状态值 和 dispath 函数进行共享。 
        <ColorContext.Provider value={{color,dispatch}}>
            {props.children}
        </ColorContext.Provider>
    )
}

```

### 使用共享数据

```js
//导入上下文组件   再将需要使用数据的组件进行包裹
<Color>
  <Text></Text>   
</Color>

//再 Text 组件中使用数据

import React , { useContext } from 'react';
import { ColorContext } from './color';
function Text(){
    const {color,dispath} = useContext(ColorContext)
    return (<div style={{color:color}}>字体颜色为{color}</div>)

}
export default Text
```

##  useMemo

简单来说，只要组件发生了重新渲染，组件中定义的变量、函数都会重新定义。你可以理解为会把所有的语句重新执行一遍。

```react
function(){
    let a=0;
    let fun=()=>{
        
    }
    const [b,setB]=useState(0);
    
    return (
		<button onClick={()=>{
                a=1;
                setB(1);
            }}>改变状态</button>
    )
}
```

点击按钮之后，函数重新渲染。a=0   b=1  函数 fun 重新定义一遍。这样会很耗费资源。

**如果这些变量和函数与改变的状态没有关系，那就没有必要重新渲染。**

**在类组件的时候，我们就发现了，只要父组件的状态发生了变化，不管是否影响到子组件，子组件都会重新渲染一遍。如果只是普通的UI就算了，要是子组件需要重新向后台发送请求之类，性能消耗就会很大。在类组件中，我们会在生命周期函数中阻止没有必要的重新渲染，那么在Hooks中，我们怎么阻止没有必要的代码执行呢？**

 **useMemo 可以帮助我们实现这一功能，useMemo() 是一个函数，接受两个参数，第一个就是是否要执行的函数，第二个参数就是一个变量，只有这个变量发生； 指定的函数或者代码片段（你可以把代码片段封装成一个函数）才会执行。**

```js
function ChildComponent({name,children}){
    function changeXiaohong(name){
        console.log('她来了，她来了。小红向我们走来了')
        return name+',小红向我们走来了'
    }
	//只有 name 发生变化的时候  changeXiaohong（） 才会执行
    const actionXiaohong = useMemo(()=>changeXiaohong(name),[name]) 
    return (
        <>
            <div>{actionXiaohong}</div>
            <div>{children}</div>
        </>
    )
}
```

## useCallBack()

useMemo() 缓存的是一个函数，而useCallBack()缓存的是一个变量值。

##  useRef

和 React 中的 Ref 差不多，就是引用一个 dom 元素 或者 引用一个组件。

```js
import React, { useRef ,useState,useEffect } from 'react';

function Example8(){
    const inputEl = useRef(null)
    const onButtonClick=()=>{ 
        inputEl.current.value="Hello ,useRef"
        console.log(inputEl)
    }
    const [text, setText] = useState('jspang')
    return (
        <>
            {/*保存input的ref到inputEl */}
            <input ref={inputEl} type="text"/>
            <button onClick = {onButtonClick}>在input上展示文字</button>
            <br/>
            <br/>
            <input value={text} onChange={(e)=>{setText(e.target.value)}} />

        </>
    )
}

export default Example8
```

# Ant Design

这是一套企业级的UI框架。 听说现在 4.X css可以自动按需加载，不需要安装配置插件了

 `antd` 是基于 Ant Design 设计体系的 React UI 组件库，主要用于研发企业级中后台产品。 

https://mobile.ant.design/components    移动端组件

https://ant.design/components   web端组件





# 懒加载

# 全局属性 context

 Context 设计目的是为了共享那些对于一个组件树而言是“全局”的数据 。

### 创建context

```javascript
//contex 不是全局属性的集合，而是单个全局属性。
const ThemeContext = React.createContext('light');
```

### 使用 contex 

使用 context  向下传递数据，其实就是指明 这个数据的使用范围，包含根元素就是全局范围。

```javascript
const ThemeContext = React.createContext('light');
class App extends React.Component {
  render() {
// 使用一个 Provider 来将当前的 theme 传递给以下的组件树。    
// 无论多深，任何组件都能读取这个值。   
// 在这个例子中，我们将 “dark” 作为当前的值传递下去。  toolbar及其子元素都将可以获得 
      return (
      <ThemeContext.Provider value="dark">        
          <Toolbar />
      </ThemeContext.Provider>
    );
  }
}
```

# proxy 跨域

1. 使用中间件 http-proxy-middleware 安装

```javascript
npm i http-proxy-middleware
```

2. 配置中间件

   在 src  下建立文件夹 setupProxy.js，内容如下

   ```javascript
   const {createProxyMiddleware} = require("http-proxy-middleware");
   module.exports = function(app){
       app.use(
           createProxyMiddleware("/api",{//这就是用来替换地址的名称
               target:"https://saastest.ilabservice.cloud/", //这是你需要代理的地址
               changeOrigin:true,
               pathRewrite:{
                   "^/api":"" //以 /api 开头的请求都会被代理到上面的服务器地址。
               }
           })
       )
   };
   
   //	 本来要访问的地址是
   //   https://saastest.ilabservice.cloud/platform/web/api/v3/unsecure/bizType
   //	 代理之后访问的地址变成  /api/platform/web/api/v3/unsecure/bizType
   //	 不需要在其他页面中中引入此文件的东西，因为上面已经使用  app 全局安装过了此代理
   ```

   

# axios

一个 ajax 的封装库。

### 安装

```cmd
npm install axios --save
```

### 引用

```js
import axios from 'axios'
```

### 使用

```js
 axios.get( "https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata").then((res)=>{
            console.log(res)
        });
```

# easy mock

一个可以造数据，创造接口的网站。



