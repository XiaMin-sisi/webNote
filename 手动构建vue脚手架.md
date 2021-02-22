### 渲染入口组件

通过渲染的方式把入口组件代替原来Vue控制的区域，html入口文件中只有一个Vue容器，最终被入口组件代替。

#### 入口html页面

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<div id="div1">
			
			<!-- 啥都不要，全在vue文件中写 -->
			
		</div>
	</body>
</html>

```

#### 入口组件模板

一个vue文件，其实就是一个组件模板而已。后面再介绍其组成部分

```html
<template>
	<div>
		<button  @click="changesum">改变名字</button>
	</div>
</template>

<script>

</script>

<style>
	
</style>

```

#### 入口js文件

在这里通过js把准备好的入口组件渲染到入口html中，代替Vue所控制的区域。

```javascript
import Vue from 'vue'	//引入vue
import App from './app.vue' 	//引入组件

new Vue({
	el:"#div1",
	//给实例注册组件
	components:{
		App
	},
	//代替#div1的组件标签
	template:"<App/>"
});
//当然这里也可以使用 render 方式进行渲染
```

### vue文件的结构

vue文件其实就是一个组件模板，前面我们学习组件，组件模板也有自己的属性、方法。

#### template

标签  template  中就是该组件的模板，和前面学习的组件模板一样，只有一个根元素。

```html
<template>
	<div>
		<button  @click="changesum">改变名字</button>
	</div>
</template>
```

#### script

标签 script 中写的就是该组件的属性和方法。该标签暴露出的数据，组件自己当然可以直接访问，其他组件若是需要获取data数据，需要导入 import 得到暴露出的数据，但是如果是父组件需要获取，推荐使用 ref 引用得到。

```html
<script>
	export default {//向外暴露出一个对象 Es6语法
		data:function(){//组件的data是一个方法
			return {
				name:"xiamin",
				sum:5
			};
		},
		methods:{
			changesum(){
				this.sum++;
					},
				}
	}
</script>

```

#### style

style中的就是组件的样式。

```html
<style>
    #div1{
        bgcolor:red;
    }
</style>
```

#### 作用范围

```html
/*如果想设置的样式只对当前的组件模板起作用需要设置样式的作用范围*/
<style scoped>
   
</style>
```

#### 样式支持

```html
/*普通的 style标签只支持普通的样式，如果想要启用scss或less，需要为 style 元素，设置lang属性*/
<style lang="scss">
   
</style>
```

### 安装vue-router

模块化工程使用路由和直接引用路由js文件有区别，先获取再安装，才能使用路由。

#### 下载vue-router

```cmd
npm i vue-router -S
```

#### 导入vue-router

```javascript
import VueRouter from 'vue-router'
```

#### 安装vue-router

```javascript
Vue.use(VueRouter);
```

其他的使用和直接引用js文件时是一样的。

### 分离路由

路由的创建有很多，全部写在入口js文件中显得很乱，把路由创建写在其他js文件中，显得清晰。

1、创建一个js文件，向外暴露已经创建好的路由对象

```javascript
//导入 vue-router
import VueRouter from 'vue-router'
//导入组件
import login from '../components/login.vue'
import regist from '../components/regist.vue'
//创建路由对象
var router=new VueRouter({
	routes:[
		{path:'/',redirect:'/login'},
		{path:"/login",component:login},
		{path:'/regist',component:regist}
	]
});
//导出路由对象
export {router};
```

2、入口文件获取暴露出的路由对象，并注册到自己的控制区域。

```javascript
//导入模块
import Vue from 'vue'
import VueRouter from 'vue-router'

//安装模块
Vue.use(VueRouter)

//获取路由对象
import {router} from './src/js/router.js'

new Vue({
	el:"#div1",
	//给实例注册组件
	components:{
		App
	},
	//代替#div1的组件标签
	template:"<App/>",
	router//注册路由
});
```

### mintUI

mint-ui是一套**组件库**，用vue封装的一套组件，适用于Vue项目。不同于bootstrap，bootstrap提供了配套的样式、配套的html代码，是一组代码片段。理论上任何项目都可以使用bootstrap。

**mintUI**组件分为三种，**js组件、css组件、表单组件**，css组件就是vue组件，js组件就是方法吧

#### 使用 mintUI

##### 下载安装mintUI

```cmd
#Vue 1.x
npm install mint-ui@1 -S
#Vue 2.0
npm install mint-ui -S
```

##### 导入、注册mintUI的组件

导入组件可以分为全部导入和按需导入，全部导入方便使用，但是会加大项目的负担，按需导入比较灵活。

1. 全部导入

```javascript
//1.1、导入全部mintui css components组件
	import MintUi from 'mint-ui'
//1.2、注册MintUi，就相当于把全部组件注册一遍，就可以全部使用了
	Vue.use(MintUi);
```

2. 按需导入

```javascript
//2.1、按需导入css components组件
//需要一个插件babel-plugin-component
//npm install babel-plugin-component -D
//根目录新建 .babelrc文件，将文件内容改成
/*
{
  "presets": [
    ["es2015", { "modules": false }]
  ],
  "plugins": [["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }
  ]]]
}
*/
//组件名称参考文档 http://elemefe.github.io/mint-ui/#/
import{ Button, Header } from 'mint-ui'
//2.2、注册导入得到的组件
	//Vue.component(name, Header);name可以自己定义也可以使用 mintui定义好的name
	Vue.component(Header.name, Header);
	Vue.component(Button.name, Button);

//js组件只能按需导入，js组件其实就是方法呗

```

##### 导入mintUI样式

不论是全部、按需导入，都需要用到MintUi样式

```javascript
import 'mint-ui/lib/style.css'
```

##### 使用组件

**mintUI**组件分为三种，js组件、css组件、表单组件。详情参考：http://mint-ui.github.io/docs/#/en2/button  

中文：http://mint-ui.github.io/docs/#/zh-cn2/button

1. 使用css组件

   不管是全部导入还是按需导入，只需要写入标签名就可以使用。组件的样式可以自行设置，参考手册进行修改。也可以查看中文的手册 https://cloud.tencent.com/developer/doc/1273

   ```html
   示例：通过 type 属性改变按钮的颜色
   <mt-button type="primary">提交</mt-button>
   ```

2. 使用 js 组件 

   js组件就是一个别人暴露出来的方法呗，那不就简单了

   ```javascript
   //1.导入该方法
   import {Toast} from 'mint-ui'
   //使用该方法
   Toast('提示信息');
   //通过参数 设置该方法的效果
   Toast({
     message: '提示',
     position: 'bottom',
     duration: 5000
   });
   ```

### mui

MUI不同于Mint-Ul,MUI只是开发出来的一套好用的代码片段，里面提供了配套的样式、配套的HTML代码段，类似于Bootstrap;而Mint-Ul，是真正的组件库，是使用Vue技术封装出来的成套的组件，可以无缝的和VUE项目进行集成开发;因此，从体验上来说，Mint-UI体验更好，因为这是别人帮我们开发好的现成的Vue组件;从体验上来说，MUI和Bootstrap类似;理论上，任何项目都可以使用Mui或boctstrap，但是，MInt-ui只适用于Vue项目;

#### 使用mui

##### 下载mui

mui不支持npm下载，只能去官网下载再手动添加到项目中，推荐在 src 目录下新建lib文件夹，里面存放手动添加的类库。把mui的dist文件夹放在项目中即可。（我已经下好放在css库中了）

##### 使用mui

1. 引入样式

   mui不是组件库，只是写好的代码片段，和css样式，样式一般通过 类名控制，所以先要把样式引进

   ```javascript
   //导入 mui样式
   import './src/lib/dist/css/mui.min.css'
   
   ```
   
2. 写入代码片段

   代码片段可以通过下载mui的包中 examples/hello-mui/examples 中的代码示例获取，或者examples/hello-mui/index.html 导航查看代码效果并复制该代码片段。

   ```html
   /*以下代码为 按钮代码，是通过类名进行样式控制的*/
   <div class="mui-btn mui-btn-primary">
   	蓝色
   </div>
   ```

   





----

### 入口文件的作用域

入口文件导入的css样式，全部的组件文件都可以用吗？ 

是的，导入的css样式，其他组件可以直接使用

入口文件导入的vue组件,其他的组件文件可以调用吗？

当然不能，mint-ui导入组件，其他组件可以直接使用，是因为把导出的组件注册到全局的 Vue中了，在vue的控制范围内就可以使用注册好的组件啊。

```javascript
//导入组件
import btn from './src/components/btn.vue'
//注册为全局的组件
Vue.component("btn",btn)
```

入口文件导入的 js ,其他的组件文件中可以使用吗？

当然不可以

入口文件导入的模块 其实就是 js 

当然不可以

**总结：**入口文件main.js没有什么特殊的，也就是普通的js文件，也就是说，它和别的js文件之间的数据交互，也需要符合规则，先把数据 暴露  ，被人才能导入数据。特殊的是，入口文件引入了 全局 Vue,把组件注册 在全局 Vue中，只要其他组件在 Vue的控制范围内就能使用 全局Vue 中注册的组件。