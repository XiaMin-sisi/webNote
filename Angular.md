## 一、AngularJS介绍

?	MVX模式——数据、表现分离
?	作用：减轻程序员的负担
?	扩展了html的功能：颠覆性、可扩展
?	M:	model	 模型 -数据
?	V:	View 	视图-表现层
?	C:	Controller	 控制器-业务逻辑

## 二、指令

### 	作用

?				扩展了html的功能，可以是E: element元素即标签  C:class 类   A:attribute 属性  M：注释

### angular中常用的指令：

?            以下是属性指令，写在标签内的指令

#### 	ng-app=""

?			指定了Angular的作用范围，放在html标签中就是全局范围的作用域

#### ng-model="变量名"：

?			双向绑定 使用某个变量、改变某个变量。 通过该标签的输入可以影响变量的值 其他地方改变变量的值也会影响该值在标签中的（一般写在input 输入框中 那么此时该变量的值就是输入框的内容）

#### ng-bind="变量名":

?			单向绑定。使用某个变量，即该变量会显示在这个标签中。可以做一些简单的运算，而且每次变量更新会把该标签内的所有内容清除。所以推荐使用表达式代替 bind

#### {{}}表达式：

?			{{变量的一些操作}} 普通字符{{变量的一些操作}}。在angular自己的属性里不需要使用表达式，在html的属性中使用变量就需要用表达式{{}}

#### ng-init="a=0;b=0;":

?			初始化Angular的变量，写在父元素的标签上或者自己标签上也行

#### ng-cloak:

?			在angular表达式没有加载出来的情况下，不显示标签的该内容

#### ng-repeat: 

?			循环、重复  。遍历数组、json。用 in 循环=》循环的是一个标签和其子标签

value in json  默认是循环value。(key，value）in json 两个变量的话，第一个是key 第二个是value，数组的话key就是下标索引

数组里有重复的值就会出错:因为angular会给每一个值取一个变量名，数组没有key，value就是key，就是重复定义了。

解决方法：$index =》是系统给的变量 代表循环到第几次了。value in arr track by $index 。依靠下标来追踪循环
ng-repeat和ng-click在一起会出现一些问题，直接用表达式会失效，用一个函数过渡就可以了。
循环中的系统变量：

 				$index: val=n 第n次循环	
		 		$first: val=true 第一次循环时，其他时候都等于 false 	
		  	   $last: val=true 最后一次循环时，其他时候都是 false
		  	   $middle:val=true 不是第一次和最后一次循环时，其他时候都是 false
			 	$even:val=true 数组下标是偶数时，也就是说第奇数次循环时
		 	    $odd:和$even相反

#### ng-repeat-start/end：

?			ng-repeat-start和ng-repeat-end循环的是几个兄弟标签

代码示例：

```html
<div ng-repeat-start="val in [1,2,3]">1</div>
<div>2</div>
<div ng-repeat-end>1</div>
```

#### ng-controller：

?	控制器 逻辑代码的编辑,桥梁。$scope的作用范围，下面会详细介绍

#### ng-src:

指定src地址

#### ng-href:

指定链接地址

#### ng-class:

指定元素的class属性，两种写法   =》指令中使用angular的变量需要使用表达式 {{ 变量名 }}

?		1、一个数组，数组里是class的名字
?		2、一个json,   key是class名字，value是布尔值，true代表添加该类（其他的属性也可以这种方式，或者说当你涉及判断一个值是否需要存在的时候就可以用一个对象）

#### ng-style:

一个json，json的各个属性对应着css属性=》属性名带有- 比如 font-style 那么key值需要带上'' 如果有指令中使用angular的变量需要使用表达式 {{ 变量名 }}

#### ng-attr-属性名：

标签有很多属性，比如上面的 href 、title 、src。angular不会每个都专门写一个指令，这个就是通用的

示例代码

```
ng-attr-href 
ng-attr-title 
```

#### ng-show="条件":

条件为真时元素显示，否则隐藏元素

#### ng-hide="条件":

条件为真时隐藏元素，否则显示元素 （如果一个标签内同时出现ng-show 和 ng-hide 执行的行为以hide为准）

#### ng-if="条件":

条件为真时添加元素，否则删除元素

#### ng-switch on="变量"：

选择结构

```html
<div ng-init="sw=24" ng-switch on="sw">
			<h1 ng-switch-when="22">1</h1>
			<h1 ng-switch-when="23">2</h1>
			<h1 ng-switch-default >3</h1>
</div>
```

#### 表单验证中的属性指令:

代码示例：

```html
<form name="myform" ng-init="fr=153224">
<input type="email" name="myemail" ng-model="fr"  required ng-minlength="5" ng-maxlength="8" ng-pattern="/^[\d]+$/"/>
<p>{{myform.myemali.$valid }}</p>
<p>{{myform.myemali.$invalid}}</p>
<p>{{myform.myemali.$pristine}}</p>
<p>{{myform.myemali.$dirty}}</p>
<p>{{myform.myemail.$error}}</p>
	</form>
```

form表单验证中的属性指令：
		required:输入框不能为空，否则$error会出现报错信息
		ng-minlength/ ng-maxlength:输入框字符长度最小/大的限制，不符合则$error会出现报错信息
		ng-pattern：正则表达式的验证，输入框的值不符合表达式则$error会出现报错信息
form表单验证中的系统变量：
		$valid/$invalid：输入框中的是否符号规定
		$pristine/$dirty：输入框中的值是否为初始值
上面四个变量都对应着四个类，.ng-valid/.ng-invalid/... 你自己可以编辑这几个类控制css样式，当符合条件时就	会在输入框中添加该类
$error：输入框中的错误信息，空值时就是没有错

#### 三目运算：

和原生的js一样使用

......
(其他指令参考angular手册)

---

### angular自定义指令

#### 作用

自定义标签 自定义组件 =>代码重用

#### 定义

```javascript
let mod1=angular.module("a1",[])
		mod1.directive("mydir",function(){
		let json={
				restrict:"C",
				template:"<ng-transclude></ng-transclude><div>mydirective</div>",
				replace:false,//一般不写这个属性，只有注释的时候才写
				transclude:true
			}
				return json;
		});
```

#### 使用

```
restrict:约束 指定指令的激活类型 ：
E: element元素即标签  C:class 类   A:attribute 属性  M：注释 =》可以组合使用
什么类型的激活条件就怎么用=》具体请看代码
```

## 三、controller：控制器

### 作用

 逻辑代码的编辑,桥梁。=》依赖注入的体现

### 控制器的使用

1、得到angular的核心module：	

```javascript
var mod1=angular.module("ng-appName",[]);
```

2、定义：得到一个controller：一个module里可以用很多的controller

```javascript
mod1.controller("controllerName",function($scope){ //$scope是angular的作用域，angular所有的数据都存在 $scope中
			$scope.a=12;
			})
```

压缩过程中依赖会被简写 比如$scope 可能会被压缩成 $s 这样angular就不能识别依赖
解决方法：
mod1.controller("controllerName",["依赖1"，"依赖2"，function(形参1，形参2){}])	；

不管形参写什么，所对应的依赖都是数组前面几个依赖(按顺序对应),因为字符是不会被压缩的，只有变量，才会被压缩。
3、在所需要用到变量a的元素的父级引用controller ng-controller="controllerName"

### angular自带的依赖：

#### $scope:作用域

angular所有的东西（变量、函数）都在这个依赖中。

 AngularJS和JavaScript一般不互通 ，通过$scope这个对象，可以实现js与angular的互通
 示例：把 js的alert()函数给angular用

```javascript
	$scope.alert=function(msg){alert(msg);}
```

##### $scop的子服务：

$watch、$apply()

##### $watch():

对变量的监控作用

```javascript
$scope.$watch('变量名'，function(){
			//变量值发生改变时 需要做的处理
			},true)
第三个参数：决定是否为深度监控，比如数组、对象改变其某一个属性值。这需要深度监控才能监控到
```

##### $apply()

在angular之外某个变量发生改变时，$watch()是监控不到的，使用 $apply()就是手动告诉angular某个值发生了变化。没有参数。

#### $interval:定时器

```javascript
var timer=$scope.$inetrval(function(){},time);
$interval.cancle(timer);//关闭定时器
```

####  $timeout:延时器

```javascript
var timer=$scope.$timeout(function(){},time);
$timeout.cancle(timer);//关闭延时器
```

#### $inter:表达式的服务

#### $http:ajax

```javascript
1、var mod1=angular.module("ng-appName",[]);
		2、mod1.controller("controllerName",function($scope,$http){ 
		//get()	
		//第一种方法,get/post 返回的是一个promise,数据在res的data上
			$http.get('fileName',{param:{传递给后台的数据，responseType：json,其他参数}).then(functiion(res){
			console.log(res.data);
			},functiion(){});
			})
		//第二种数据在res上
			$http.get('fileName',{传递的参数}).success(function(res){
				console.log(res);
			}).error(functiom(){});
		//post的问题，angularjs采用的参数传递方式是json 而传统的传输方式是 a=2&b=3。一部分浏览器不支持json的传输格式
			解决：
				1、单个配置：
				

		//jsonp	
			$http.jsonp("请求的地址",{params：{
			传递给后台的数据
			cb:'JSON_BACK'           =》回调函数，必须写成这样
			}}).success(function(){}).error(function(){})
```

---

#### 其他依赖：

其他angular预定义的依赖请参考手册

### Provider 提供者

服务的提供者：对服务进行某些配置

#### 服务提供者的命名规律

```javascript
服务名称+Provider 比如
$http的提供者 $httpProvider 可以配置post请求的数据传输格式
$interpolate的提供者$interpolateProvider 可以配置表达式的两端符号是什么
```

#### 配置服务

```javascript
var mod1=angular.module("ng-appName",[]);
		mod1.config(function(服务提供者1，服务提供者2){
			//ToDo 参考Ajax中 $httpProvider 配置post请求的数据传输格式
			});
```

---

### 自定义服务

#### 创建依赖：

```javascript
方法一：factory
			app.factoty("依赖名字"，function(){
			return something;
			});
			工厂返回什么依赖就是什么，工厂可以返回一些值也可以返回函数
方法二：provider=>推荐使用 因为可以动态配置，即可以使用config函数通过服务提供者进行服务的配置
			app.provider("依赖名字"，functiom(){
			return{
				myname:"xiamin",
				setname:function(newName){this.mynam=newName;},
				$get:function(){return this.myname;}//=》服务被调用的时候，就只调用这个函数，上面的函数是配置的时候用的
			};
			})
			和工厂差不多 ，就是需要把返回的东西放在 $get中
方法三：service 
			app.service("",function(){
			//不需要return什么 这个函数里定义了什么 直接就可以用 包括函数
			let name=""xiamin";
			});
方法四：constant 常量=>不可修饰不是不能改变其值
			app.constant("依赖名字"，"值");
方法五：value 变量
			app.value("依赖名字"，"值");
```

#### 依赖的修改

```javascript
依赖的修改（装饰）：decorator 会修改原来的依赖
		app.decorator("依赖名"，function($delegate){
		//$delegate代理原来的依赖，对依赖进行修改
		$delegate.name="sisi";
		//返回修改完的依赖（代理）
		return $delegate;
		})
依赖被多个控制器引用 只会被创建一次=》依赖在多个控制器中是共享的
```

#### 控制器数据的共享

##### 父子控制器

```javascript
子控制器会复制父控制器的$scope的属性。仅仅是复制，二者对某个属性进行修改不会影响对方
		消息机制：
			$scope.$emit("名字","数据"); =》向上发送
			$scope.$broadcast("名字","数据");=》向下广播
			$scope.$on("名字","数据");=》接收上面二者发送的数据
			示例：
				$scope.$on("aa1",function(event,data){
				console.log(event,data);
				//把父级发送过来的数据保存在自己的作用域中
				this[event.name]=data;
				console.log(this.aa1);
				}); 
```

##### 无关控制器

自定义的依赖（服务）实现数据共享=》推荐使用provider进行服务的定义，需求不同可以通过配置更改 

---

## filter过滤器

作用：输出之前对数据进行某种处理
语法：data|过滤器名称

### 过滤器的使用

```javascript
表达式中使用angular自带的过滤器：
	currency：是一个对钱进行处理的过滤器  99.3|currency =》$99.30
	date：是一个带参数的对日期进行处理的过滤器{{times|date:"yyyy-MM-dd-hh-mm-ss"}}=>2020-04-	 24-03-33-15  (里面y代表年份 - 原样输出)

js中使用angular自带的过滤器过滤器：引入依赖 $filter
	$filter("过滤器的名称")（”需要处理的数据“，”参数“）；
```

### 自定义过滤器

```javascript
mod1.filter("myfilter",function(){
			return function(input){
				//TODO 对传进的东西进行操作
				input=input+"-myfilter";
				//返回处理后的数据
				return input;
				}
			          });
```

---

## module:模块

###    定义一个模块：

请看代码

###     使用一个模块：

具体请看代码

?	使用一个模块后，就可以使用该模块里面的 controller filter directive ...

---

## router：路由

分离视图 、控制器。每一个视图文件就有一个控制器文件 。主文件只需要引用就可以

### 使用路由

```javascript
1、引入route.js
2、引入route 的模块
		let mod1=angular.module("main",["ng-Route"]);
3、配置模块：
		mod1.config(function($routeProvider){
4、配置Route：	
		$routeProvider.when()
		})
...请看具体代码文件
```

[route的使用](file:///C:/11/t1.txt)

