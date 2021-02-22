### 变量的定义

1. let:定义变量，没有预解析，不存在变量提升，不能重复定义变量
2. const：定义常量，声明的时候就必须得赋值。后续不能改变值（此特性对于对象属性的操作不适用，如数组的push()方法添加数组的数据，对象有一个函数freeze(）使对象不能改变）
3. 使用以上两种方法定义的变量作用域增加了块级作用域  {}
注意：var 定义的变量属于window而let和const不是

---
### 解构赋值

**非常有用特别是在做数据交换的东西**

```javascript
	  //把数组、json中的值赋值给变量
	  let [a,b,c]=[12,56,65]	
	  let json={name:"xiamin",age:21};
	  let {name,age}=json;
	 //当你先定义好变量，再解构赋值json给该变量
      let a,b;
      ({a,b}={a:"xiamin",b:"18"};)
	//当你写{}时,可能会被当作块级作用域语法，此时如果你不想{}当作块级作用域可以用小括号包围该语句 
```

---

### 字符串模板

字符串连接：不用考虑双引号、单引号、随意换行

```javascript
//格式：`string1${string2}string3`
let name="xiamin";
let hello=`你好我是${name},请多多关照`;
```

---

### 字符串查找

```javascript
string.includes("str");判断字符串中是否含有某个字符串，返回bool值
string.startsWith("str")；判断某个字符串是否已某个字符串开头
string.endsWith("str")；判断某个字符串是否已某个字符串结尾，可以用来判断文件名的后缀
string.repeat(n);重复某个字符串多少次
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 函数

##### 	默认参数

1. function fname(par1=默认值，par2=默认值){}

2. 函数的参数默认是已经定义的，函数内部不能用 let const重复定义

##### ... 运算符

扩展（展开）/  重置(剩余)运算符(如果是剩余运算，则必须放到最后) **...** ，**...** 可以把一个数组展开成一个个的变量

1. 把传入的几个参数封装成一个数组

```java
function ftname(...a){}
ftname(6,5,8,4,);
```

2. 把传入的这个数组拆分成一个个变量传入函数

```java
function ftname(a,b,c){}
arr=[1,2,3]
ftname(...arr);
```

3. 数组的赋值 arr1=arr2;数组是引用类型，arr2改变时arr1也会变。

```javascript
arr2=[1,2,3]  
arr1=[...arr2]
```

##### 箭头函数 =>

简化函数的定义

格式：let ftname=(par1,par2)=>{语句}；

1. 如果用了箭头函数，在函数内部调用用了其他函数，其他函数内部的this不是 “谁调用就是谁，而是看箭头函数的this 是谁，那么其内部的其他this就是谁”

2. 
   箭头函数的 **this** 指向**定义**它时，所处上下文的对象的this指向。即ES6箭头函数里this的指向就是上下文里对象this指向。只有**函数**才有this指向，所以一般只需要看箭头函数在哪个函数中被定义，且是离箭头函数最近的父函数的 **this** 指向。偶尔没有上下文对象，this就指向window。
   
3. 箭头函数里面arguments函数,可以用...代替

4. 箭头函数不能当构造函数

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 数组

#### ES5新增数组操作

##### foreach()

```javascript
//遍历数组
arr.foreach(
 function(val,index,arr){}, //第一个参数回调函数
 this//第二个参数，this指向的对象，一般不用这个参数
);
```

##### arr.map()

用法和foreach一样，不同的是map可以在回调函数中return 某个值，返回值将组成一个数组，最后将数组返回

```java
//arr.map()重构数组，返回一个数组
var arr=[1,2,3]
let res2=arr.map(function(val,index,arr){
    console.log(val);
    return val+index;
});
//res2 是arr中 值与下标和的数组 1  3  5
```

##### arr.filter()

过滤。用法和foreach()一样，不同的是循环的时候可以进行判断，是否符合条件，符合条件返回true，则会返回到一个新数组中，不符合条件返回false，不会出现在新数组中。最后返回新数组。

```java
let res3=arr.filter(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
					/* else
					return false; */ //可以省略return false
				});
```

##### arr.some()

用法和foreach一样，不同的是判断数组是否存在**某个**元素符合某个条件，最后返回bool值

```javascript
//只要有一个符合条件就 return true
let res4=arr.some(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
	});
```

##### arr.every()

用法和foreach一样，不同的是判断数组是否**所有**元素都符合某个条件，最后返回一个bool值

```javascript
//符合条件 return true ，不符合 return false。只要有一个 false 就是 false
let res5=arr.every(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
					/* else
					return false; */ //可以省略return false
				});
```

##### arr.reduce()

用法和foreach一样，不同的是，可以返回一个数值，多了一个参数 pre ,pre就是上一次返回的值。只有最后一次的返回值能被接收到。

```javascript
var sum=arr.reduce(function(prev,val,index,arr){//prev是上一次操作返回的结果
			return prev+val*val;//举例，求数组元素的平方和
			})
```

##### arr.reduceRight()

arr.reduce()一样的作用，但是计算从右边（数组的尾部）开始。

#### ES6新增数组操作

##### 	Array.from()

把一个伪数组转化成一个数组

```javascript
//标准伪数组转换成真数组
let warr=document.querySelectorAll("div");
let arr2=[Array.from(warr)];
//let arr2=[...warr]; 拓展运算符... 也可以实现标准伪数组转换成真数组

//不标准的伪数组，但是必须要有length属性
let warr2={
    0:2,
    1:4,
    2:6,
    length:2//长度写2 那么转换后的数组长度只有2
};
Array.from(warr2);
```

##### Array.of()

把一组值转化成一个数组，类似 ...的功能。Array.of()基本上可以用来替代Array()或newArray()，并且不存在由于参数不同而导致的重载，而且他们的行为非常统一。 

```javascript
//推荐使用这种方法代替 Array()或newArray()
var arr=Array.of(2,6,8,4,7);
```

##### arr.find()

返回第一个符合条件的元素

```javascript
//碰到第一个符合条件的值，则停止继续寻找
let res7=arr.find(function(val,index,arr){
					if(val>5)
					return true;
				});
```

##### arr.findindex()

返回第一个符合条件的元素的下标  return true 则停止循环,并返回该元素的下标

```javascript
let res8=arr.findIndex(function(val,index,arr){
					if(val>5)
					return true;
				});
```

##### arr.fill(val,start,end)

填充数组,就是用某个值替换数组的某些值，但是**不能改变数组原来的长度**。

```javascript
//第一个参数 val 就是用来填充的值， start 是数组的开始填充的索引，end就是填充结束的索引。包括start,不包括end
arr.fill("41",3,5);//用41 填充数组的第[3]到[5]不包括[5]
```

##### arr.includes(val)

判断数组中是否包含某个元素，和some()差不多，但是更简单不需要回调函数中先判断，弊端就是不能对值操作后进行判断，只能判断元素本身是否存在。

```javascript
let res9=arr.includes(9);//判断数组长是否存在 9
```

arr.indexOf(val)

返回数组中该值的下标，只能返回第一个。不存在该值，返回-1

``` javascript
let res10=arr.indexOf(5);//返回数组中，值为 5 的元素下标
```

####  ES2017新增数组循环

for (let ... of ...)循环，对象，数组都可以使用这种循环。

对象和数组多了几种属性：
		arr.values()
		arr.keys()：数组的下标形成的数组
		arr.entries()：是数组元素值和下标形成的数组，所组成的数组 即 [[val,key],[val,key],[val,key]]

```javascript
//默认循环的就是 数组/对象的 values()
for (let val of arr) {
    console.log(val);
}
//keys()循环数组的下标
for (let index of arr.keys()) {
    console.log(index);
}
//entries()数组值和下标组成的数组 arr.entries()=[[index,val],[index,val],...]
for (let arr1 of arr.entries()) {
    console.log(arr1[0],arr1[1]);
}
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 对象

#### 对象的简洁语法

```javascript
let name=xiamin;
let age=18;
let show=function(){};

let json={
    name,	//等价于 name:name
    age,	//等价于 age:age
    show	//等价于 show:function(){},最好不要用箭头函数,箭头函数在外部定义，this永远指window
}
```

#### 新增对象的函数

#####  Object.is()

判断两个对象是否相等,长得一样就相等,以下两种情况 和 == 判断的情况不一致。根据需要选择使用

```javascript
NaN==NaN   false	Object.is(NaN,NaN) true
+0==-0     true		Object.is(-0,+0)  false
```

##### Object.assign(obj，obj1,obj2,...)

1. 合并对象的属性,将合并后的目标对象返回，如果属性有重合的，后面的会覆盖前面的，obj是目标对象，会被改变值，后面本身的不会改变。
2. 值复制对象（包括数组）：let newarr=Object.assign([],oldarr);

```javascript
//1、利用返回值，获取合并后的对象
let js5=Object.assign({},js2,js3,js4);//前面写一个空对象，否则js2,会被改变
//2、直接把容器放在目标对象位置
Object.assign(js5,js2,js3,js4);
```

#### ES2017对象新增的属性

Object.values(obj)：对象的值数组
Object.keys(obj)：对象的key数组
Object.entries(obj)：键值对数组所组成的数组 即 [[val,key],[val,key],[val,key]]

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Promise

#### 作用

解决异步回调问题，为异步编程提供了一种解决方案

#### 状态

1. 一共有三种状态，分别为pending（进行中）、fulfilled（已成功）和rejected（已失败）。
2. 只有异步操作可以决定当前处于的状态，并且任何其他操作无法改变这个状态；
3. 一旦状态改变，就不会在变。状态改变的过程只可能是：从pending变为fulfilled和从pending变为rejected。如果状态发生上述变化后，此时状态就不会在改变了，这时就称为resolved（已定型）

#### 使用步骤

1.创建一个promise对象

```javascript
let promise=new Promise(function(resolve,reject){
   		if(条件)
   		{resolve(message);}	//pending变为fulfilled成功时返回的信息，可以不返回信息但是必须执行这个函数状态才会改变
   		else
   		{reject(message)；}	//pending变为rejected时返回的信息，可以不返回信息但是必须执行这个函数状态才会改变
   		});
//只有执行了 resolve() reject()函数，状态才会改变
```

2、通过then方法，分别指定pending变为fulfilled状态和pending变为rejected状态的回调函数。（如果没有发生这两个变化 then里的函数不会执行）

 ```javascript
promise.then(function(success){
    //to do  something
},function(fail){
    //to do  something 
});
//两个回调函数,成功时（resolved状态）执行的函数，和失败时（rejected）执行的函数。回调函数的参数是promise创建时所定义的执行时的resole/reject函数返回的信息。第二个回调函数一般不写，写在catch()中

//promise.catch(),返回一个Promise，并且处理拒绝的情况。它的行为与调用Promise.prototype.then(undefined, onRejected)相同。
//推荐使用catch方法，不要在then方法中定义rejected状态的回调函数；这是因为使用catch还可以捕获在then方法执行中存在的错误。
promise.then(function(data) { 
    // success to do something
}).catch(function(err) {
    // error to do something
});

//Promise.finally(),返回一个Promsie。是指，在上一轮 promise 运行结束后，无论fulfilled还是 rejected，都会执行指定的回调函数。该方法适合，无论结果如何都要进行的操作，例如清除数据。
Promise.finally(functin(){
       //执行代码
});
 ```

#### Promise.resolve(value)

快速生成一个成功状态的promise对象,参数 value 主要有以下几种情况：

1. 一个Promise实例：原封不动的返回该实例

```javascript
var original = Promise.resolve('我在第二行');
var cast = Promise.resolve(original);
cast.then(function(value) {
    console.log('value: ' + value);
});
console.log('original === cast ? ' + (original === cast));
// "original === cast ? true"
// "value: 我在第二行"
```

2. 一个thenable对象：是指含有then方法的对象跟随这个thenable对象的，采用它的最终状态

 ```javascript
let thenable = {
    then: function(resolve, reject) {
        resolve(42);
    }
}
let p = Promise.resolve(thenable);
p.then(function(value) {
    console.log(value);
})
// 42
 ```

3. 普通数据：[String|Array|Object|Number]：直接将传入参数当最终结果并返回一个新的Promise

```javascript
let p = Promsie.resolve(123);
p.then(function(num) {
    console.log(num);
})
  // 123
```

4. 无参数：直接返回一个resolved状态的Promise对象

```javascript
let p = Promsie.resovle();
p.then(function() {
    // do something here...
})
```

#### Promise.reject()：

快速生成一个失败状态的promise对象：let promise=Promise.reject("message");

#### Promise.all(iterable)

iterable 必须是一个可迭代对象，如 Array 或 String。把promise对象打包扔到一个迭代器里，最后返回一个promise对象，但是必须所有promise的状态都是成功状态。才是成功状态如果有多个promise对象状态是失败，返回的错误信息是第一个失败的promise结果。

#### Promise. race(iterable)

把promise对象打包扔到一个迭代器里，最后返回一个promise对象，但是只要有一个promise的状态是成功状态。就是成功状态

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 模块

ES6统一服务端和客户端的模块规范

#### 模块化

我理解为类似Java的Java包，一个类一个文件，类之间相互访问需要导包

#### 定义模块

导出模块数据: 使用关键字  export 导出模块数据

1. 单个导出数据： 

   定义的时候就导出：export  定义变量、函数、类的语句

```javascript
export let qq=123456;
export class student {
    constructor(name,age) {
        this.name=name;
        this.age=age;
    }
    showname(){
        console.log(this.name);
    }
}
```

?	先定义再导出：export 已经定义好的变量名、函数名、类名

```javascript
let qq=154564;
export qq;
```

2. 批量导出：

```java
//export {变量名，函数名，类名}
let  x=12;
let y=5;
let a=2;
let b=9;
export {x,y,a,b};
```

3. 导出时取别名： export  {变量名 as 别名，函数名 as 别名，类名 as 别名};取了别名的数据，对方如果需要引用就必须通过别名导入

```javascript
let tel=1872083;
export {tel as pnum};
```

4. 导出默认数据：每一个模块只能导出一个默认数据，如果需要多个默认数据，考虑将所有设置为默认数据的数据放在一个json中。export default 变量名    也可以是匿名的

```javascript
let teacher="sisi";
let age=18;
let json={
	teacher,
	age
};
//不匿名导出数据
export default json;
//匿名导出数据
export default{
teacher,
age
}
```

#### 使用模块

1. 引入主模块文件：（相当于其他高级语言的主函数 所有执行的语句都写在这个js文件中 其他模块相当于需要用到的类包）

<script src="模块文件路径" type="module"></script>
2. 在模块中导入其他模块的数据： 

   + 加载所需要的数据： import {变量名，函数名，类名} from '其他模块的所在位置'	

     注意：即使两个模块文件在同一文件夹下路径也需要 ./文件名

   + import '其他模块的所在位置' 相当于引用文件（不知道什么意思）

   + 加载所有目标文件暴露出的数据： import * as 别名 from './model2.js'

   + 导入默认的数据：导入其他文件默认导出的数据，若其他文件没有设置导出默认数据则不能使用
import 任意名称 from '其他模块的所在位置'
	
	+ 动态引入模块：import()。默认情况下import语法不可以写入 if 之类不确定的语句中，即import只支持静态引入，编译时就需要引入需要的模块文件。 但是import()采用promise规范：即import()返回一个promise对象
		?			          import("./model2.js").then(function(res){//res是一个对象，包含所有目标文件导出的数据
   	?			          console.log(res);
   	?			           });
   	
   + 取别名：import {变量名 as 别名，函数名 as 别名，类名 as 别名} from '其他模块的所在位置'。取了别名后就必须通过别名使用数据，原本的名称不再适用
   
   + import 模块的位置可以是相对路径也可以是绝对路径
   
   + import 语句有提升效果 即会自动放到顶部先执行
----------------------------------------------------------------------------------------------------------------------------------------------------------------

### 类

#### 类的定义

```javascript
	class  ClassName{
		//构造函数
		constructor(name) {
			this.name = name;
		}
		//成员函数
		functionName(){}
		functionName(){}
		}
```

#### 对象的声明

```javascript
	let ObjectName=new ClassName("xiamin");//使用类的构造函数
```

#### 类的存取函数

get和set：对属性进行存取、设置时**自动触发**的两个函数， 如若只设置一个get函数没有设置set函数，那么这个属性就是只读属性，无法赋值。总的说，设置了的话两个都得设置，要不就都不进行设置。

```javascript
class student {
				constructor(name) {
						this.name = name;
					}
					set name(val){
						console.log(`正在设置name的值为：${val}`);
						name=val;//真正的赋值就是这一步
					}
					get name(){
						console.log(`正在试图获取name的值`);
						return name;//得到的就是你 return 的东西 
					}
					[aa]() {
						console.log(this.name);
					}
			}
//获取值 / 不需要手动调用这两个，自动触发。只需要通过 obj.attribute 就行
```

#### 静态方法

类的方法，通过类名调用的方法，就像之前的原型属性。
	定义： static functionName(){}
	调用：ClassName.functionName();

#### 类的继承:

关键词 extends

```JavaScript
class person{
    constructor(name) {
        this.name=name;
    }
    showmessage(){
        console.log(`姓名：${this.name}`);
    }
    eat(){
        console.log(this.name+"在吃饭了。。。");
    }

}
class student extends person{
    constructor(name,num) {
        super(name);//父类的参数，调用父类的构造函数赋值
        this.num=num;//自己的参数自己赋值
    }
    //重写父类的函数，不需要重写的就不用写出来，直接可以用。
    showmessage(){
        super.showmessage();//继承父类的函数（可以不继承）
        console.log("学号:"+this.num);//添加自己的代码
    }
}
```
注意:
 1、属性名（对象的函数、属性名）可以使用表达式（变量）来定义，用 [ ] 括起来

 ```javascript
let abc="name";
let Obj={
[abc]:"xiaominmin"
};
console.log(Obj.name);
//xiaominmin 
 ```

 2、类的定义语句没有预解析功能，必须先定义再使用

-------------------------------------------------------------------------------------------------------------------------------------------------------
### symbol

一种新的数据类型，symbol是一个单独的数据类型、基本类型

##### 定义

```javascript
let sym1=Symbol("somethig");//不用new
```

##### 唯一性

symbol()返回值是一个唯一值（老师说可以用来定义一些唯一或者是私有的一些东西）

```javascript
let symb=Symbol("age");
//作用域不同，相同的代码得到的 symbol对象是不一样的
for(let i=0;i<1;i++)
{
    let symb2=Symbol("age");	
    console.log(symb==symb2);//false
}
//即使相同的作用域相同的代码得到的 symbol对象也是不一样的
let symb3=Symbol("age");
console.log(symb==symb3);//false

//只有通过 = 赋值的 symblo对象是相等的
```

#### symbol做属性名

如果symbol作为一个对象的属性名（key），用for in 循环显示不了symbol所在的属性及属性名。只可以直接用obj[symbol]输出属性值（所以说这就像私有属性）

```javascript
//因为symbol的唯一性，只有得到一开始定义的symbol才能访问。除非你暴露对象的同时把symbol对象也暴露出去，否则别人就只能访问你对象中其他的属性
let symb=Symbol("age");
let json={
    name:"xiamin",
    [symb]:"22",
    tel:123456,
			}		
//for 循环检查不到symbol做属性名的属性
    for (let key in json) {
        console.log(key+" "+json[key]);
    }
```

### iterator

#### 概念

 iterator是一 种**接口**机制， 为各种不同的数据结构提供统-的访问机制

#### 作用

1. 数据结构，提供-一个统一的、 简便的访问接口;

2. 使得数据结构的成员能够按某种次序排列

3. ES6创造了一“种新的遍历命 令for...of循环，Iterator接口 主要供for... of消费。就是说只要把接口部署到某个数据上就能使用 for  of 循环

####  工作原理

1. 创建一个指针对象(遍历器对象)，指向数据结构的起始位置。第一次调用next方法，指针自动指向数据结构的第一 个成员  

2. 接下来不断调用next方法，指针会一 直往后移动，直到指向最后一个成员

3. 每调用next方法返回的是一 个包含value done的对象，{value: 当前成员的值, done: 布尔值}

4. value表示当前成员的值，done对应的布尔值表示当前的数据的结构是否遍历结束。
   当遍历结束的时候返回的value值是undefined, done 值为true,表示已经遍历结束。

####  原生具有iterator的数据

数组、字符串 、argument、set容器、map容器

### generator

解决异步函数深度嵌套，作用和promise差不多。本质是一个特殊的函数，生成的是一个 iterator对象，value值就是  yield 后一句的东西。可以是一个表达式、语句的执行结果。

#### 定义generator

```javascript
var gen=show();
function * show(){//不同的是 名字前面有一个星号
    n语句 yield  语句
	n语句 yield  语句
	n语句 yield  语句 
}
```

函数里的yield控制代码块执行，yield会把前面没执行的代码全部执行，以及yield后面第一句代码执行
而yield的执行是由函数next()控制执行，每执行一次next()就会按顺序执行下一个yield代码块。

#### next()

next()不止可以让暂停的函数执行下一步，还可以指定当前执行这一步的返回值。即 value。很有用，异步操作的结果是不能直接 return 的，因为 return 永远会比异步操作更快，而且只能在回调里拿到 异步的结果，在回调中更不可能 return 数据。所以只能在 回调中 执行 next(data) 既能在确保异步执行完成后执行下一个异步操作，又能把异步操作的结果给返回出去。有的异步操作会依赖于上一步异步操作的结果。比如先要 异步获取 一个的异步地址，再异步请求这个地址获取需要的数据。详情参考 generato.html 模拟后台处理数据。

#### 代码的执行

##### 自动执行

```javascript
//1、定义一个全局变量 得到generator对象  var gen=show();
//2、在需要等待的语句或函数后面加上一句   gen.next();
//3、按同步顺序编写generator函数 用yield 分割需要异步的代码块
//4、开始执行generator函数 的执行		gen.next();
var gen=show();//第一步			
function showname(reso){
    setTimeout(()=>{
        console.log("夏敏");
        gen.next();//第二步
    },4000);
}
function showage(){
    setTimeout(()=>{
        console.log("22");
        gen.next();//第二步
    },3000);
}
function showtel(){
    setTimeout(()=>{
        console.log("1872083");
    },1000);
}
function * show(){//第三步
    console.log("异步编程开始");
    yield showname();
    console.log("异步编程继续");
    yield showage();
    console.log("异步编程再继续");
    yield showtel();
}
gen.next();//第四步
```

##### 手动调用

obj.next();返回一个json,{value:value,done:false}，第一个值value是执行第一个yield语句的返回值（不需要return yield后面的是什么就返回什么）。value可以是一个promis对象、数字、字符串等。 第二个值done是代表函数是否运行完毕，即后面是否还有yield语句

```javascript
function * show2(){
    yield new Promise((reso)=>{
        setTimeout(()=>{
            console.log("夏敏");
            reso();
        },4000);	
    });
    yield new Promise((reso)=>{
        setTimeout(()=>{
            console.log("21");
            reso();
        },2000);	
    });
    yield new Promise((reso)=>{
        setTimeout(()=>{
            console.log("1872083");
            reso();
        },1000);	
    });
}
let g2=show2();
//手动执行 next()
g2.next().value.then(()=>{
    return g2.next().value;
}).then(()=>{g2.next();});
```

---

### async和await

#### 定义

async function functionName(){
?		 await 异步语句块
?		 await 异步语句块
?		 await 异步语句块
?		 ... .... 
?		}
?	具体使用请看文件 10_ansync和await

#### 与generator相比

不用手动调用 next() 方法去执行下一个异步操作， await等待当前异步完成后会自己调用下一个异步操作。好像只能和promise相结合使用。就是说其实是通过判断 是否执行了 resolve() 来判断是否执行下一个 await等待的异步操作。那么generator 的 next() 可以指定返回值。那么 async  怎么指定返回值？ 通过promise的resolve() 、reject()指定返回值。虽然说只能和promise结合使用，但是书写的方式更像同步代码，不需要调用 promise的then()方法。

#### 示例

```javascript
 async function show() {
     let name=await new Promise((res, rej) => {//返回一个Promise对象
         setTimeout(() => {
             console.log("你好");
             res("xiamin");//指定返回的数据
         }, 3000);
     });
     await new Promise((res, rej) => {//返回一个Promise对象
         setTimeout(() => {
             console.log(name);//使用上一步返回的数据
             res();
         }, 1000);

     });
 }
show();//调用 asycn函数
```

#### 特点

1. 语义化强
2.  里面的await只能在async函数中使用
3.  await后面的语句返回值可以是promise对象、数字、字符串等
4. async函数返回的是一个Promsie对象
5. await语句后的Promise对象变成reject状态时，那么整个async函数会中断，后面的程序不会继续执行，所以我们一般只执行 resolve()函数，即使出错了也执行 resolve()。通过参数判断 到底异步请求成功没有。或者使用第六条所说的。
6. 基于上面的async的特点，我们会用到异常捕获机制，学过java的都知道，java中有异常捕获try...catch...

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Set 和WeakSet

set：类似与数组，不同与数组，不能有重复值,没有下标

#### 定义set

new set([val,val,val]) Set函数可以接受一个数组（或类似数组的对象）作为参数，用来初始化，不能是对象，并且支持定义的时候直接赋值，但是可以用add函数添加对象进去

```javascript
let set=new Set();
let set1=new Set([1,2,"hello",2]);//定义时初始化
```

#### set的操作

1. 添加值：set.add(val);

2. 删除：set.delete(val);

3. 判断set中是否有某个值： set.has(val);

4. 清空set：set.clear();

5. set的大小：set.size();

6. set的循环遍历： 可以用 for ... of ...

7. 作用：数组去重     arr=[...new set(arr)]；

8. set转数组，转数组之后可以用数组的一些方法处理数据 arr=[...set];

9. set的交、并、差集

   ```java
   let set2=new Set([1,2,3,5,9]);
   let set3=new Set([2,4,5,6,7]);
   //并集
   let set4=new Set([...set2,...set3]);
   console.log(set4);
   //交集
   let set5=new Set([...set2].filter((val)=>{
       if(set3.has(val))
           return true;
   }));
   console.log(set5);
   //差集 u1-u2=>从u1中去掉两者相同的部分
   let set6=new Set([...set2].filter((val)=>{
       if(!set3.has(val))
          return true;
   }));
   ```

#### WeakSet

weakSet的元素可以是对象，不支持定义的的时候直接赋值

```javascript
let weakObj = new WeakSet({a:1111})
console.log(weakObj)  // 这样直接赋值会报错
//正确的用法：
let weakObj = new WeakSet()
let obj = {a:123}
weakObj.add(obj)
console.log(weakObj) 
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Map和WeakMap

#### Map

Map类似于json,又有不一样，比如：key可以是任何值，不一定是字符串

##### 定义Map

let map=new Map();

##### Map操作

1. 添加值：Map.set(key,vaule);key可以是任何值，不一定是字符串
2. 获取值：Map.get(key);
3. 删除值：Map.delete(key);
4. 清空set：Map.clear();
5. 判断Map中是否有某个值： Map.has(key);
6. 循环 for ... of ...  / forEach

#### WeakMap

WeakMap和Map差不多，不过key只能对象

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 数字变化、Math新增

#### 新增进制

二进制：let a=0b0101;
八进制：let a=0o1247;
十六进制：let a=0x78Ab

#### 方法的变化

**很多关于数字的函数都放在Number身上**，这些方法原本都是在对象身上，这样做的好处是比如：
Number.isNaN();是否是NaN
Number.isFinite();是否是数字
Number.isInteger();是否是整数
......
Number.parseInt();字符串转整数
.....
安全整数：-(2^53-1) 到 （2^53-1）
Number.isSafeInteger();判断是否为安全整数
Number.MAX_SAFE_INTEGER   最大安全整数
Number.MIN_SAFE_INTEGER	  最小安全整数

#### Math

Math.trunce() =>保留整数
Math.sign()=>判断一个数是整数 （返回1）、负数（返回-1）或0（返回0）

------------------------------------------------------------------------------------------------------------------------

### Es2018

#### 命名捕获

在正则表达式中子表达式可以把匹配的字符串赋值给一个变量
语法：(?<变量名>表达式)
使用变量:

1.通过match()得到一个对象groups。str.match(re).groups
2.刚刚所定义的变量都在groups的属性中

```javascript
let str="2017-03-20";
//尽管是2018新增的 2020火狐依然不支持这种写法的正则
let re=/(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
let obj=str.match(re).groups;
console.log(obj.year,obj.month,obj.day);
```

#### 反向引用命名捕获 ：

在表达式中反向引用：\k<变量名> 和以前的反向引用 \1 \2 差不多,就是引用的时候可以给子表达式取名字
在replace()第二个参数中引用：$<变量名> 和以前的反向引用 $1 $2差不多

#### 正则的新参数：

s ：参数s代表正则表达式是dotAll模式，该模式下 元字符 .  可以代表任意字符包括 \n \t 之类字符

#### 标签函数

定义： functiion fname(){}

调用：fname \` 参数 \`

-----------------------------------------------------------------------------------------------------------------------------------------------

### proxy

代理（是设计模式的一种 代理模式）
作用：拦截、预警、扩展功能、统计、增强对象等等 比如get()、set() 就是类似于 类里面的存取函数，会自动调用
语法：let obj=new Proxy(被代理的对象，对代理对象的操作handel );

##### handel常见的一些处理方法	

handel{
		apply(){},//拦截函数的方法
		construct(){},
		defineProperty(){},
		deleteProperty(){},
		get(){},//获取对象属性值时自动触发的函数
		getOwnPropertyDescriptor(){},
		getPrototypeOf(){},
		has(){},//设置对象中某些属性是否隐藏
		isExtensible(){},
		ownKeys(){},
		preventExtensions(){},
		set(){},//设置对象属性值时自动触发的函数
		setPrototypeOf(){}//设置原型属性值时自动触发的函数
		}

具体使用参考 16_proxy和reflect.html

### Reflect

反射 
Reflect.apply(function,this的指向,[arg1,arg2]) 类似于 call()

具体使用参考 16_proxy和reflect.html