# 介绍

 dva 首先是一个基于 [redux](https://github.com/reduxjs/redux)[ ](https://github.com/reduxjs/redux) 和 [redux-saga](https://github.com/redux-saga/redux-saga)[ ](https://github.com/redux-saga/redux-saga) 的数据流方案，然后为了简化开发体验，dva 还额外内置了 [react-router](https://github.com/ReactTraining/react-router)[ ](https://github.com/ReactTraining/react-router) 和 [fetch](https://github.com/github/fetch)[ ](https://github.com/github/fetch)，所以也可以理解为一个轻量级的应用框架。 

## 特性

- **易学易用**，仅有 6 个 api，对 redux 用户尤其友好，[配合 umi 使用](https://umijs.org/guide/with-dva.html)后更是降低为 0 API
- **elm 概念**，通过 reducers, effects 和 subscriptions 组织 model
- **插件机制**，比如 [dva-loading](https://github.com/dvajs/dva/tree/master/packages/dva-loading)可以自动处理 loading 状态，不用一遍遍地写 showLoading 和 hideLoading
- **支持 HMR**，基于 [babel-plugin-dva-hmr](https://github.com/dvajs/babel-plugin-dva-hmr)实现 components、routes 和 models 的 HMR

## withRouter

众所周知，只有路由组件 props 上才会有 路由的一些方法和属性。那么非路由组件，怎么才能拿到这些路由方法，进行路由跳转呢。 使用 withRouter() 就可以使组件获取到路由。这也叫做 写入路由。

## 切换路由方式

dva 的默认路由方式是 哈希路由，看起来不美观。可以切换为文件路由。

1. 下载 history 依赖

   ```bash
    npm i history --save
   ```

2. 修改入口文件

   ```js
   import {createBroserHistory as creatHistory } from 'history'
   const app = dva()
   
   //修改成如下
   
   const app = dva({
   	history:creatHistory();
   });
   ```

## models

文件结构如下。

```js
//一般一个组件的所有异步请求的函数都写在 service 下的某一个文件中，需要使用再引入即可。
import {getUserName} from  '../services/user.js'
------------------------------------------------------------------------
export default {
 	namespace:"user",, //命名空间
  //------------------------------------------------------------
	state:{//数据
		name:"xiamin"
	},
 //-----------------------------------------------------------   
    //dva 的 reducer 有更特殊的写法，本身是一个对象，包含很多函数。
    //不需要在函数中自己判断 action 再去执行相应的代码
    //而是调用者通过 action.type == namespace/functionName 自己去寻找要执行的reducer中的函数
    reducers: { //处理动作 =》修改 state 
        changename(state, action) {
            let newstate={...state};
            newstate.name=action.name;
            return newstate;
        },
        update(state, action) {
            return { ...state, ...action.payload };
        }
     },
 //-------------------------------------------------------------
    //当需要异步数据来更新 state 时，由 effect 执行异步获取的逻辑，获取到数据后，再由 effect触发 reducer, 把数据传递给 reducer 中的某个处理函数进行数据更新。
    //effect 也是一个对象，对象中有很多函数，组件也是通过触发reducer的方法触发相应的 effect函数。
    //需要注意的时 effect 里面的函数都是 generator 函数。
    //函数的第一个参数就是组件传递过来的action,可以不用结构的方式进行获取参数
    //函数的第二个参数是一个函数对象，这个参数应该是 connect 自动传值。常用的函数有 call put select 等等函数。
    //put(action)用来触发 reducer。此时的 type 不需要加上命名空间
    //call 用来执行异步代码。第一个参数就是异步请求函数（不能写参数），后面可以写很多个参数，作为异步函数的参数。
    //select 用来获取 state 的数据。接收一个函数作为参数，函数的默认参数就是 state。返回值就是 select 的返回值。
 	effects: {
	  *changeNameSync({ payload }, { call, put ,select}){
          
          let name= yield select((state)=>{state.name});
          
		  let name= yield call(getUserName,20173033103,18);
          
		  yield put({type:"changename",name:name.data.message[0].open_type})
	  }
	},
    
//-----------------------------------------------------------------   
    //这是一个函数对象，里面的函数会在组件（不知道是不是只用路由组件）第一次渲染的时候自动触发
    //函数有两个参数，第一个 dispath().第二个参数 history 就是一些路由操作。
    //我们可以在这个函数中做一些初始化的数据请求。当然如果是异步请求数据当然是触发 effect。同步获取数据进行更新就可以直接触发 reducer
    subscriptions: {
	  whenUser({ dispatch, history }) {
		  if(history.location.pathname=='/user')
		  console.log("----------1111history1111--------");
	  },
	  whenUser2({ dispatch, history }) {
	  		  if(history.location.pathname=='/user')
	  		  console.log("----------2222history2222--------");
	  },
	},
 
};

```

## connect

把 数据--models 和 组件 连接起来的一个 ApI。 

### 使用数据

需要先在路口文件注册需要用到的 models

 ```js
app.model(require('./models/user').default);
 ```

再组件中使用 connect () 进行数据连接

```js
//参数 state 并不是某个文件的 state ,而是所有注册过的 models state 的集合
// state一个对象，对象里是各个 models 文件的 state，key值是命名空间
// { namespace1:{...state} , namespace1:{...state} ,...}   
let myprops=(state)=>{
    return{
        state.user
        //返回的值就是会传入 组件 props 中的数据。这里返回的就是命名空间user下的 state 数据。
    }
}
//接收一个函数 fn1参数 需要自定义.   
//返回值 fn2 也是一个函数 所以可以链式调用 。fn 的参数是组件。意味着 fn1返回的数据和组件连接起来了
	connect(myprops) (组件名)

//-------------------------------------------------------------------------
import React from 'react';
import { connect } from 'dva';

let User=(Userprops)=>{
	return(
	<div>我是 user page---{Userprops.user.name}</div>
	)
}

//export default User;
let myUserProps=(state)=>{
	console.log(state)
	return{
		...state
	}
}
export default connect(myUserProps)(User)


```

### 修改数据

使用  connect() 进行过数据连接的组件，props 即使不传递也会有一个 dispath() 函数，很明显，我们要通过这个来触发 动作，修改数据。

```js
// dva 中的 dispath() 函数的 action 有规定的写法 
dispath({
    
})
```

## mock

模拟接口请求数据。

**建立接口文件**

在 mock目录下新建一个 user.js

```js
export default {
	//请求方式 请求url地址
	'Get /getuserApi/user':(req,res)=>{
		//req 请求数据
		//res 响应数据
		res.send({name:"夏敏敏"}) //返回的数据
	}
}
```

**注册接口**

在 .roadhogrc.mock.js 文件下注册接口

```js
export default {
    //把刚刚建立的接口注册到全局 也可以通过 import，require 可以动态引入，用到再引入
	...require('./mock/user') 
};
```

**请求接口**

```js
export const getName=(id,age)=>{
	
	return requests("getuserApi/user");
}
```

**触发请求**

```js
//就是上面的呗，通过 effect 去进行异步请求接口。
//部分代码如下
effects: {
	  *changeNameSync({ payload }, { call, put }){
		  let name=yield call(getName,20173033103,18);
		  console.log(name);
		  yield put({type:"changename",name:name.data.name})
		  
	  }
	}
```



 