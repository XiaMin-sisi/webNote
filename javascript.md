###  函数的两种写法

##### 变量形式

```javascript
//定义
var show=function(){
     alert("hello");
     };
//调用
show();
```

##### 普通形式

```javascript
//定义 
function show(){
     alert("hello");
 };
//调用
show();
```



----------------------------------------------------------
### 数组

#### 数组的几种实现方法

1. var a=new Array();JavaScript数组不需要指定大小，是可以动态增长的  （new 可以省略）
2. var a=new Array(6);6是数组初始大小，也可以动态增长的
3. var a=new Array(1,2,3,4,5,6)；用一组值初始化数组，可以动态增长的
4. var a=[1,2,3,4,5,6]；可以动态增长的
5. 推荐使用es6 新语法Array.of()代替Array()

注：在JavaScript中数组元素的类型可以不一样

#### 数组的操作

##### a.push(val)

从尾部进栈,在数组的后面添加一个数据

##### a.pop()

从尾部出栈，将数组最后面的一个元素删除。

##### a.shift()

从头部出队，将数组的第一个元素删除

##### a.unshift(val)

从头部入队，在数组的最前面添加一个数据

##### a.sort()

对数组进行排序 。sort()是从小到大的顺序把数组进行排序，即数组本身变了，但是sort（）只能对字符串进行排序 。 对数字进行排序可以自己编写回调函数如下：

```javascript
let arr=Array.of(1,16,33,7,5);
//return a-b;是从小到大排序， return b-a; 是从大到小排序。结合reverse()也可以实现大到小排序
arr.sort((a,b)=>a-b);
console.log(arr);//Array(5) [ 1, 5, 7, 16, 33 ]
```

##### a.reverse() 

可以把数组反序（结合排序函数可以从大到小排序）

##### a.concat(a1,a2,a3...);

数组的连接  var b=a.concat(a1，a2);  b为数组a和a1、a2连接起来后的数组，a数组和a1、a2数组本身并不变

```javascript
let arr=Array.of(1,2);
let arr1=Array.of(16);
let arr2=Array.of(33);
let arr0=arr.concat(arr1,arr2);//arr本身不会改变
console.log(arr);//Array [ 1, 2 ]
console.log(arr0);//Array(4) [ 1, 2, 16, 33 ]
```

##### a.slice(startindex,endindex)

数组的截取.（开始位置，结束的位置）不包括结束位置

```javascript
let arr=Array.of(1,2,3,4,5);
//截取arr[0]开始到arr[3]
let arr1=arr.slice(0,3);
console.log(arr1);//Array(3) [ 1, 2, 3 ] 不包括 arr[3]
console.log(arr);//Array(5) [ 1, 2, 3, 4, 5 ] 本身不会改变
```

#####   a.splice(start,num,val,val)

对数组进行替换、插入、删除操作。start:开始的索引位置 num:数据的个数  val:可以是一个数组，表示替换的值

```javascript
let arr=Array.of(1,2,3,4,5);
//arr[0]开始的两个元素替为 6 。val只写了一个，所以数组长度会减一
arr.splice(0,2,6);
console.log(arr);//Array(4) [ 6, 3, 4, 5 ]
//从arr[2]开始插入两个元素 8 9 （替换数组中不存在的就是插入咯）
arr.splice(2,0,8,9);
console.log(arr);//Array(6) [ 6, 3, 8, 9, 4, 5 ]
//从arr[2]开始删除两个元素（替换不给 val就是删除咯）
arr.splice(2,2);
console.log(arr);//Array(4) [ 6, 3, 4, 5 ]
```



------------------------------------------------------------------------------
### 对象

#### 对象的几种定义方法

1. var a=new object()   //var a=object() 
2. var a={name:夏敏,sex:男} 这种方法又叫做Json，字面量形式
3. 构造函数方法 

```javascript
function student（a,b）{this.name=a;this.age=b;}    
var a= new student("夏敏",22)
```

#### 操作对象

1. 添加新属性：a.age=5;
2. 访问某一属性：
   + a.age
   + a["age"]

3. 删除某一属性：delete a.name;

#### 对象的原型属性

prototype。任何函数都有一个默认属性--原型属性 prototype,**对象只能调用创造它本身的函数所拥有的原型属性里面的方法和变量**。一般把函数设为原型，这样更省内存，构造函数写属性。某个对象可以改变这个属性值但是其他对象的这个属性值不变, 例外：如果某个原型属性是数组，那其中一个对象用 push方式增加数组时，其他对象的原型属性也会改变（引用），所以如果想要把原型属性变成自己的属性只有通过赋值才行

```javascript
   //构造函数写各自的属性
       function student(name,age){
           this.name=name;
           this.age=age;
       }
       //原型添加共有的方法、属性
       student.prototype.sayhello=function(){//
           alert("hello");
       }
       student.prototype.type="student";
       var sisi=new student("sisi",18);
       var xiamin=new student("xiamin",18);
       //对象可以使用 原型上的方法 、属性
       sisi.sayhello();
       //对象改变原型中的属性，只是改变自己的属性、方法
       sisi.type="xxs";
       console.log(sisi.type);//xxs
       console.log(xiamin.type);//student
       console.log(student.prototype.type);//student
```

#### 类的静态属性

实例对象不能调用类的静态属性，类的静态属性只能通过类名调用。

```javascript
//直接添加在构造函数上的 属性 就是 静态属性
student.sayhello=function(){
console.log("hello");
}
//调用
student.sayhello();
```

**实例对象可以调用类的原型属性，但是不能调用类的静态方法。**

#### 类的继承

1. call的用法：  函数.call(this,函数参数，函数参数)，调用别人的函数，并且可以改变原函数的this  ->继承函数
2. A.prototype=B.prototype    ->继承原型属性（适用于混合构造法），（引用）
   解决引用的方法：一个一个赋值： for（ var x in A.prototype）{B.prototype.x=A.prototype.x;}
3. 引用：在js中，存在一类机制，比如，将一个数组直接等号赋值给另一个数组，为了节约内存，其实是把第二个数组的地址指向同一个节点的地址，即两个数组指向同一个空间，改变其中一个两个都会变。继承原型属性时就是引用 

```javascript
function student(name,age){
           this.name=name;
           this.age=age;
       }
       student.prototype.sayhello=function(){
           alert("hello");
       }
       //构造函数继承
       function xxs(name,age){
        student.call(this,name,age);
       }
       //原型属性继承（非引用）
       for (var key in student.prototype) {
           xxs.prototype[key]=student.prototype[key];
       }

      var minmin=new xxs("minmin",5);
      console.log(minmin.name)
      minmin.sayhello();
```

#### JS里的三种对象类型

1. 非静态对象（本地对象）：object  function String。。。。。（实例化后才能有）
2. 静态对象（内置对象）：Global 、Math（不能new出来用，即不能实例化，可以直接用）
3. 宿主对象：Dom BOM  （由浏览器提供的对象 ，即js的运行环境对象）

---

### for in 循环

特殊的for循环遍历对象的全部属性：
for（ var x in a）{  } 
a可以是有很多属性的对象，也可以是一个数组
a是对象时 x 表示 a 的属性名并不是属性值 ，a[x]才能取出属性值 a.x会被认为a里面有一个x的属性名
a时数组时 x 表示 a 的下标  a[x]取出数组里的值

---------------------------------------------------------------------------------
### window

浏览器的全局对象：window。页面自定义的全局变量都是 window的成员变量，可以省略 window. 进行调用

document：是一个页面对象，代表一个HTML页面，也是window的一个成员变量

location：代表当前文档的url

status：在网页左下角出现的小字  status=“memory”

--------------------------------------------------------------------------------
### 数据类型

#### 基本数据类型

string number function bolean object undefined

#### 获取数据的类型

```javascript
 console.log(typeof minmin);//object
```

#### 类型转换

##### parseInt(string)

字符串转整型：从左到右依次扫描，直到碰到非数字，如果字符串不能转换成数字则返回 Nan

##### parseFloat(string)

字符串转浮点型从左到右依次扫描，直到碰到非数字，如果字符串不能转换成数字则返回 Nan

##### isNaN()

判断是否为NaN

##### toLowerCase()

大写转小写：string.toLowerCase()

##### toUpperCase()

小写转大写：string.toUpperCase()

#### 字符串操作

字符串查找：string.search(s1);如果string含有s1返回，s1在string里的位置序号，否则返回-1，
切分字符串： var arr=string.split(s1); 通过字符串s1来切分string，s1通常为空格，返回的是一个字符串数组

#### ==、===

双等号：== 先把类型转换成相同类型再比较
全等号： === 不转换类型直接比较，即类型不一样就直接不一样了

#### 命名规范

匈牙利命名法：
1.类型前缀：数组 a     布尔值 b     浮点数 f
                   函数 fn     整数 i         对象 o 
                   正则表达式 re      字符串 s     变体变量 v
2.首字母大写

#### JS里的真真假假

真：true、非零数字、非空字符串、非空对象
假：false 、0、“”、空对象、未定义

---------------------------------------------------------------------------------------------------------
### 函数的可变参

arguments 是js的一个内置对象 任何一个函数都有一个arguments对象
arguments是一个伪数组，里面是函数的实参（就是实际调用时传过来参数，包括形参但不限于形参）
伪数组：和数组的差别，自带length属性 记录伪数组的长度

在函数不确定参数的情况下，可以不写形参。即使写了形参，实参也可以比形参多。这两种情况都可以用函数的arguments数组获取实参的个数和值。

---

#### 获取元素样式属性值

#### 获取行间样式属性值

样式属性值即 style 中的各个属性的值。通过dom元素的style 属性即可进行获取和设置。但是仅仅只能获取和设置行内的样式值。写在其他样式文件、或者style标签的样式值无法获取和设置。设置一般没有问题，因为行内元素的样式优先级最高。

```javascript
 dom.style.width="50px";
```

#### 获取非行间样式属性值

IE：currenstyle
非IE：getcomputedstyle（element，任意）.属性

```javascript
//ie
var width=document.querySelector("div").currentStyle.width;
//非ie
var width=getComputedStyle(document.querySelector("div")).width;
//解决兼容性：
function getStyle(element, attr) {
    if(element.currentStyle) 
        return element.currentStyle[attr];
    
    else 
        return getComputedStyle(element, false)[attr];
}
```

-----------------------------------------------------------------------------------
### 定时器、延时器

setInterval(function,time)隔多少时间执行一次，间隔型
setTimeout(function,time)隔多长时间执行，只执行一次，延时型
关闭定时器/延时器： 

clearInterval(定时器对象)；
 clearTimeout(延时器器对象)；

----------------------------------------------------------
### Dom

#### 元素的子节点

| 属性名            | 作用               | 其他                     |
| ----------------- | ------------------ | ------------------------ |
| childNodes        | 获取所有子节点     | 不推荐使用，包含文本节点 |
| children          | 获取所有子节点     | 推荐使用，不包含文本节点 |
| firstChild        | 获取首个子节点     | 推荐使用，包含文本节点   |
| lastChild         | 获取最后一个子节点 | 推荐使用，包含文本节点   |
| firstElementchild | 获取首个子节点     | 不包含文本节点           |
| lastElementchild  | 获取最后一个子节点 | 不包含文本节点           |

#### 元素的父节点

 parentNode ：直接父元素 w3c标准

 parentElement  ：直接父元素 ie标准

 offsetParent：获取祖先节点就是body

#### 元素的兄弟节点

previousSibling：前一个兄弟元素，会匹配字符，包括换行和空格

previousElementSibling：前一个兄弟元素，只匹配元素节点

 nextSibling：后一个兄弟元素，会匹配字符，包括换行和空格

nextElementSibling： 后一个兄弟元素，只匹配元素节点

#### 创建元素

var e1=document.createElement("li")；//只能写标签名，再通过其他函数添加东西进该标签。不能像jquery一样写完整的标签代码。

不推荐这种方法创建添加的元素，如果只是想向页面中插入一个元素，还不如使用inteinnerHtml。

#### 添加元素

eparent.appendChild(e1) 	添加到父节点的尾部；
eparent.insertbefore(e1,e2)	表示在e2前面添加节点e1，e2也应该是eparent的子节点

注意：若e1原来就在网页上，那么操作就是，先把e1从原来的地方移出，再添加到新的父节点下面；利用这一特点可以用来对元素进行排序

其实用inteinnerHtml也是可以实现的，innerHtml 方法需要把所有代码补齐,并且会修改原有的代码结构，上面的是Dom方法

#### 删除元素

eparent.removeChild（e1）：删除子元素

remove()：删除自身

#### 文档碎片：

 document.createDocumentFragment();
提升性能，但是用处不大

--------------------------------------------------------------------------
### 表格

简便操作： tBodies  tHead   tfoot  rows  cells 利用这些表格的属性就不需要进行复杂的js定位了，tHead   tfoot在一个表格里，只存在一个，tBodies是一个数组

----------------------------------------------------------------------------------
### 透明度

alpha（opacity：30）；alpha：0.3；前IE后火狐

-------------------------------------------------------------------------------------------
### 各种 height top

#### clientHeight

包括内容区域、padding。不包括border、 滚动条、margin的元素的高度。对于inline的元素这个属性一直是0，单位px，只读元素 。对于body就是页面的可视区域

#### offsetHeight

包括内容区域、padding、border、水平滚动条（只是滚动条的高度而已，并不是滚动条隐藏的内容高度），但不包括margin的元素的高度。对于inline的元素这个属性一直是0，单位px，只读元素。

#### scrollHeight

在有滚动条时，如果因为滚动而隐藏了部分内容。scrollHeight 就会是 可见区域 + 隐藏区域 的高度。只读元素 

#### offsetTop

 当前元素顶部距离最近父元素顶部的距离,和有没有滚动条没有关系。单位px，只读元素 

#### scrollTop

documentElement.scrollTop:滚动条距离元素顶部的距离，即被上面被隐藏部分的高度，可读可设置

#### top

相对于**最近的定位父元素**的上边的距离。 可读可设置。

#### 叠加边距

获取元素相对于 body 的左边距 上边距，即使该元素不是定位元素。

```javascript
function getPoint(obj) { //获取某元素相对于body的边距，而不是简单的marring-left
var t = obj.offsetTop; //获取该元素对应父容器的上边距
var l = obj.offsetLeft; //对应父容器的上边距
//判断是否有父容器，如果存在则累加其边距
while (obj = obj.offsetParent) {//等效 obj = obj.offsetParent;while (obj != undefined)
t += obj.offsetTop; //叠加父容器的上边距
l += obj.offsetLeft; //叠加父容器的左边距
}
return x={left:l,top:t};
} 
```



-----

### 属性节点

属性节点 即  元素的属性  不存在于 style中，style也是一个属性节点，style里面的属性叫做样式属性。 而 id class  name value ...就是属性节点。

#### 获取属性节点

 setAttribute("属性","值") 

#### 设置属性节点

 getAttribute("属性") 

#### 移除属性节点

removeAttribute("属性") 

----

### 多物体运动框架

多物体运动中，所有的东西都不能公用，要变成自身的属性，定时器也可以成为自己的属性。尽量少使用 offset  。看看自己写的框架，还挺不错，都看不懂了。

```javascript
/* 任意值运动 */
function move(obj, atil, sstyle) {
	clearInterval(obj.time);
	obj.time = setInterval(function() {
		var iwidth = obj.currentStyle ? parseInt(obj.currentStyle[sstyle]) : parseInt(getComputedStyle(obj, true)[sstyle]);
		var speed = ((atil - iwidth) / 5);
		speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
		if (sstyle == "opacity") {
			iwidth = obj.currentStyle ? (obj.currentStyle[sstyle]) : (getComputedStyle(obj, true)[sstyle]);
			speed = ((atil - iwidth * 100) / 10);
			speed = Math.round(speed);

			if (iwidth * 100 == atil) {
				clearInterval(obj.time);

			} else {
				obj.style[sstyle] = iwidth - 0 + speed / 100;
				obj.style["filter"] = "alpha(opacity=" + (iwidth - 0 + speed / 100) + ")";
			}
			if (speed == 0) {
				obj.style[sstyle] = atil / 100;
			}
		} else {
			if (iwidth == atil) {
				clearInterval(obj.time);

			} else {

				obj.style[sstyle] = iwidth + speed + "px";
			}
		}

	}, 30)
}

/* 链式移动 */
function linkMove(obj, atil, sstyle, functionEnd) {
	clearInterval(obj.time);
	obj.time = setInterval(function() {
		var iwidth = obj.currentStyle ? parseInt(obj.currentStyle[sstyle]) : parseInt(getComputedStyle(obj, true)[sstyle]);
		var speed = ((atil - iwidth) / 5);
		speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
		if (sstyle == "opacity") {
			iwidth = obj.currentStyle ? (obj.currentStyle[sstyle]) : (getComputedStyle(obj, true)[sstyle]);
			speed = ((atil - iwidth * 100) / 10);
			speed = Math.round(speed);

			if (iwidth * 100 == atil) {
				clearInterval(obj.time);
				if (functionEnd) functionEnd();
			} else {
				obj.style[sstyle] = iwidth - 0 + speed / 100;
				obj.style["filter"] = "alpha(opacity=" + (iwidth - 0 + speed / 100) + ")";
			}
			if (speed == 0) {
				obj.style[sstyle] = atil / 100;
			}
		} else {
			if (iwidth == atil) {
				clearInterval(obj.time);
				if (functionEnd) functionEnd();

			} else {

				obj.style[sstyle] = iwidth + speed + "px";
			}
		}

	}, 30)
}

/* 完美运动 */
function perfectMove(obj, jsonStyle) {
	clearInterval(obj.time);
	obj.time = setInterval(function() {
	var bpand = true;/* 判断是否所有运动都达到预期 */
		for (var x in jsonStyle) {
			var sstyle = x;
			var atil = jsonStyle[x];
			var iwidth = obj.currentStyle ? parseInt(obj.currentStyle[sstyle]) : parseInt(getComputedStyle(obj, true)[sstyle]);
			if (sstyle == "opacity") {
				iwidth = obj.currentStyle ? (obj.currentStyle[sstyle]) : (getComputedStyle(obj, true)[sstyle]);
				if (iwidth * 100 != atil) bpand = false;
			} else {
				if (iwidth != atil) bpand = false;
			}
		}
		for (var x in jsonStyle) {
			sstyle = x;
			atil = jsonStyle[x];
			iwidth = obj.currentStyle ? parseInt(obj.currentStyle[sstyle]) : parseInt(getComputedStyle(obj, true)[sstyle]);
			var speed = ((atil - iwidth) / 5);
			speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);

			if (sstyle == "opacity") {
				iwidth = obj.currentStyle ? (obj.currentStyle[sstyle]) : (getComputedStyle(obj, true)[sstyle]);
				speed = ((atil - iwidth * 100) / 10);
				speed = Math.round(speed);
				if (bpand) {
					clearInterval(obj.time);
				} 
				else {
					obj.style[sstyle] = iwidth - 0 + speed / 100;
					obj.style["filter"] = "alpha(opacity=" + (iwidth - 0 + speed / 100) + ")";
				}
				if (speed == 0) {
					obj.style[sstyle] = atil / 100;
				}
			} 
			else {
				if (bpand) {
					clearInterval(obj.time);
				} else {
					obj.style[sstyle] = iwidth + speed + "px";
				}
			}

		}

	}, 30);

}

```



-------------------------------------------------------------------------------

### 事件

#### 常用事件

| onaborton       | 图像加载被中断                 |
| --------------- | ------------------------------ |
| **onscroll**    | **滚动条滚动的时候**           |
| onblur          | 元素失去焦点                   |
| **onchange**    | **用户改变域的内容**           |
| **onclick**     | **鼠标点击某个对象**           |
| **ondblclick**  | **鼠标双击某个对象**           |
| onerror         | 当加载文档或图像时发生某个错误 |
| **onfocus**     | **元素获得焦点**               |
| **onkeydown**   | **某个键盘的键被按下**         |
| **onkeypress**  | **某个键盘的键被按下或按住**   |
| **onkeyup**     | **某个键盘的键被松开**         |
| **onload**      | **某个页面或图像被完成加载**   |
| **onmousedown** | **某个鼠标按键被按下**         |
| **onmousemove** | **鼠标被移动**                 |
| **onmouseout**  | **鼠标从某元素移开**           |
| **onmouseover** | **鼠标被移到某元素之上**       |
| **onmouseup**   | **某个鼠标按键被松开**         |
| onreset         | 重置按钮被点击                 |
| onresize        | 窗口或框架被调整尺寸           |
| onselect        | 文本被选定                     |
| onsubmit        | 提交按钮被点击                 |
| onunload        | 用户退出页面                   |

####  event对象

##### 获取event对象

火狐：事件函数的第一个参数就是event对象  即 arguments[0]（现在火狐也支持 全局属性 event）

非火狐：event  作为全局属性，直接使用

兼容写法： var evt = window.event || arguments[0]; 

##### event对象获取事件信息

用来获取事件的详细信息，如： 鼠标点击的位置的坐标clientX、clientY，键盘的按键

```javascript
event.clientX //鼠标点击的x坐标
event.keyCode //按下的鼠标键码
//ctrlKey、shiftKey、altKey:判断ctrl、shift、alt是否被按下。
event.ctrlkey==true?按下了ctrl : 没有按下ctrl
```

#### 事件冒泡

事件会通过层级关系，向上传递。通常会取消事件冒泡。
取消事件冒泡

```javascript
var oEvent=window.event || arguments[0]; 
oEven. cancelBubble=true;//IE
//或者
oEven.stopPropagation();//W3c
```

#### 默认行为

浏览器自带的事件,如：鼠标右键菜单，按下键盘某个键，点击链接。
阻止默认事件:

```javascript
event.preventDefault();//w3c
//或者
return false;//IE
```

#### 事件绑定

同一个事件可以绑定很多个触发的函数。

```javascript
document.querySelector("div").onclick=function(){
            console.log("hello");
       };
//普通写法 前一个会被覆盖
document.querySelector("div").onclick=function(){
    console.log("xiamin");
};
```

attachEvent（事件名，函数）；
兼容性问题：
IE： attachEvent（事件名，函数）； attachEvent("onclick",function(){});
非IE：addEventListener（事件名，函数，false）第三个参数可以省略addEventListener("click",function(){});
自定义函数解决兼容性问题：

```javascript
function bindEvent(obj,e,fun){
if(obj.attachEvent){
obj.attachEvent("on"+e,fun);
}
else{
 obj.addEventListener(e,fun，false)
}
}
```

```javascript
document.querySelector("div").addEventListener("click",function(){
            console.log("hello");
        })

document.querySelector("div").addEventListener("click",function(){
    console.log("xiamin");
})
//两个都会被执行
```

#### 解除绑定

detachEvent（事件名，函数）；removeEventListener（事件名，函数，false）;兼容问题和上面一样解决。

只能解除有 函数名的 绑定吧

```javascript
function ftn1(){
            console.log("hello");
        }
document.querySelector("div").addEventListener("click",ftn1)
document.querySelector("div").addEventListener("click",function(){
    console.log("xiamin");
})
//只有第一个 用函数名的绑定可以解除
document.querySelector("div").removeEventListener("click",ftn1);
```

----------------------------------------------------------------------------
### Ajax

无刷新数据读取

基础应用：
动态数据：请求JS（或json）文件
局部刷新：请求并显示部分网页文件

请求并显示静态TXT文件： 字符集编码
缓存、阻止缓存：url不同则没有缓存，如在 url？t=time  则url每次都不一样，但是真实地址是一样的

#### 使用Ajax的步骤：

##### 1、创建Ajax对象

```javascript
var oAjxt=new XMLHttpRequest();  //非IE6
var oAjxt=new ActiveXobject("Microsoft.XMLHTTP");//IE6
//解决兼容性问题：
if（window.XMLHttpRequest）
{
var oAjxt=new XMLHttpRequest();
}
else
{
var oAjxt=new ActiveXobject("Microsoft.XMLHTTP");
}
```

##### 2、连接到服务器

```javascript
//同步：事情一件一件依次进行
//异步：事情一起进行
//oAjax.open(方法，文件名，是否异步传输)
oAjax.open("get","a.txt?t="new Date().getTime(),true);
```

##### 3、发送请求

```javascript
oAjax.send();
```

##### 4、接收返回值

```javascript
/*  oAjax.readyState 浏览器和服务器进行到那一步了 */
oAjax.onreadystatechange=function(){
    if(oAjax.readyState==4){  //完成
        if(oAjax.status==200){     //状态码200代表成功

        }
    }
}
/*  一般只写oAjax.readyState=4的情况
0  未初始化，还没有调用open（）
1  载入，已经调用sent()方法，正在发送请求
2  方法已完成，已经收到全部响应内容
3  正在解析响应内容
4  响应内容已经解析完成，可以在客户端调用了
*/
```

#### eval(string）

将一个字符串转换成JS可以识别的语句；虽然   **JSON.parse();    JSON.stringify(); ** 也可以起到这样的作用，但是这两个函数只能转换标准的 json 字符串 即 key 用 引号括起来。

比如将一个 字符串形式的 json  、数组 装换成一个对象。请求数据时经常用到。但是注意格式

```javascript
var obj=eval("("+data+")");
//不能直接 eval(data);因为 json数据最外层会有 {}，会被当成块级作用域。用小括号括起来消除块级作用域。
```

---

### 面向对象

将面向过程的程序改成面向对象
原则：不能函数套函数，但是可以有全局变量
整个过程 -> 构造函数
变量  ->  属性

函数  ->  方法

---

### BOM基础

#### document.write("")

document.write("");如果放在事件里，write会先清空document里的东西，再写东西

#### window.open()

打开窗口： window.open("about:blank","_blank");第一个参数打开的是空白页面，第二个参数，_blank:另开一个新窗口，_self：覆盖当前页面。第三个参数：窗口的属性值，每个属性值之间用逗号分隔

#### window.close()

关闭窗口：window.close();IE 和火狐 不能用脚本关闭非脚本打开的窗口

#### 常用属性

##### window.navigator.userAgent   

浏览器的类型及版本号

##### window.location   

页面的地址，可赋值以改变页面 

#### 系统对话框

警告框：alert（”内容“）；没有返回值
选择框：confirm("提问的内容")，返回 Boolean;

输入框:prompt（）；返回输入的字符串或null

---

### cookie基础与应用

cookie：页面用来保存信息：如：自动登录、记住用户名

#### 特性

1. 同一个网站中所有的页面公用一套cookie(同一个域名)
2. 数量、大小有限（4k-10k）
3. 有过期时间

#### 使用

document.cookie

```javascript
//键值对的形式：设置cookie
document.cookie="password=123456";
//设置日期：
//document.cookie="password=123456;expires=time"; time是一个日期，如2019-04-5
var odate=new Date(); 
odate.setDate(odate.getDate()+x);//x是保质期x天
document.cookie="password=123456;expires="+odate；
//取出cookie：
var  acookie=document.cookie.split(";");   //用分号把字符串分开，变成一个数组。
for(var i=0;i<acookie.length;i++){
    var arr2=acookie[i].split("=");              //再次用等号把字符分开
    if(arr2[0]==key)
        return arr2[1];
}

//删除cookie：设置 某个键的过期时间为 -1  。系统自动删除
```

具体请参考 自定义js文件  **cookie/js/cookie.js**

---

### 正则表达式

#### 字符串函数

str.match(str) 所有匹配项返回
str.search(str) 返回第一个匹配项的位置
str.replace(re,str)） 将匹配到的re 换成 str

#### 正则表达式

正则表达式：规则、模式强大的字符串匹配工具

##### 两种写法

1. Js风格：var re =new  RegExp('a','i');          RegExp('表达式','参数')

2. per风格：var re=/a/i              /表达式/参数

##### 参数

+ i 忽略大小写（ignore）

+ g :全局匹配   

+ m:多行匹配

+ s: 安全模式 元字符  .   可以代表	\t \n \r \v \f

##### 表达式

表达式分为两种子表达式  [] 、()，子表达式由元字符和量词组成

+ []:一个[]代表一个字符
  + \[abc]:多选一abc中任意一个都可以
    
  + \[0-9] 或者 [a-z]:规定取值范围
    
  + \[^abc]:取反 匹配不在方括号之内的字符
  
+ ():子表达式一个()代表着一个或多个字符，并且子表达式里的匹配的东西可以被反向引用（不是引用这个式子而是这个式子匹配到的字符）
  
  + \n代表引用第个n子表达式匹配到的值  \1 引用第一个子表达式的值，不光可以在正则表达式自身引用子表达式的值。
  
    ```javascript
    //匹配aabb形式 再转换=>bbaa
    //1、先匹配到aabb形式的字符串
    var re2=/(.)\1(.)\2/;
    ```
  
  + 在用replace()函数时替换的字符也可以引用，引用形式 $n 引用第n个子表达式的值
  
    ```javascript
    //2、再引用子表达式进行替换
    var str1=str.replace(re2,"$2$2$1$1");
    ```
  
  + (abc|bcd|ef|a)：多选一，几个字符串中任选一个

##### 元字符

是拥有特殊含义的字符。一个元字符代表一个字符

+ \w:	英文、数字、下划线任意一个   
+ \W:除了英文、数字、下划线
+ \d:	数字
+ \D：除了数字
+ \s:	空格字符（包括 \t \n \r \v \f  ）
+ \S：除了空格
+ \b：匹配单词边界 eg /\bc/匹配一个c 这个c还得是字符边界
+ \uxxxx：查找以十六进制数 xxxx 规定的 Unicode 字符。（16进制的unicode编码翻译出来的意思进行匹配，

​     就是找出英文意思是 爱 的单词 就是 love，） 

+ .：任意字符但是不包括 	\t \n \r \v \f (在Es2019中加参数 s 就可以了)
+ \t \n \r \v \f    tab/换行/

##### 量词

+ n+：至少一个某个字符     /x+/ 匹配至少一个x的

+ n*：任意个某个字符

+ n？：1或者0个某个字符

+ n{x}：x个

+ x {n,m}：最少n个 最多m

+ x{n,}：量词 最少n个 最多无限

+ ^n：以什么开头

+ n$：以什么结尾

+ (?=n)：匹配任何其后紧接指定字符串 n 的字符串

  ```javascript
  //正向预查 或者叫正向断言 要取得某个表达式需要通过其后紧跟字符进行判断，但是表达式不取后面该字符
  //取一个string，string后面紧跟@qq.com
  var re4=/\d+(?=@qq.com)/g;
  console.log(("1532241857@qq.com1564654@").match(re4));
  ```

+ (?!n)：匹配任何其后没有 紧接指定字符串 n 的字符串。

----------------

### 闭包

闭包：函数嵌套函数，子函数可以使用父函数的局部变量。**子函数就是闭包，闭包包含了引用外部函数的变量**。

##### 闭包产生的条件 

+ 函数嵌套
+ 内部函数使用外部函数定义的变量 （我们编写的程序本身就是一个闭包 ，onload函数中定义全局变量，各个函数都能使用）

+ 执行外部函数 

##### 常用情况

将内部函数作为返回值暴露出去,或者把多个函数封装在一个对象中暴露出去，供别人调用，**外部函数调用结束后，内存并没有被释放，作用域一直存在**。所以延长了局部变量的生命周期。并且通过闭包外部（这里的外部指的是 外部函数的外部）还可以操作函数内部（这里的内部是指外部函数的内部）的数据，只要在暴露出去的内部函数中编写代码就行。

```javascript
function ft1(){
    var a=1;
    function ft2(){
        a++;
        console.log(a);
    }
    return ft2;//把 内部函数暴露出去
}
//得到内部函数
//调用了一次外部函数，所以产生了一个闭包。外部函数调用结束后，内存并没有被释放。我理解为，ft2是函数的一部分，ft2被保存下来，是引用保存，内存地址当然不能释放。
var fn=ft1();
fn();//3
fn();//4

```

##### 作用

1. 延长了局部变量的生命周期。**外部函数调用结束后，内存并没有被释放，作用域一直存在**
2. 外部操作函数的局部变量。**函数外部通过返回的内部函数，就可以控制外部函数的变量**

##### 生命周期

如下述代码

```javascript
function ft1(){
//变量定义的代码提升，在这里函数就已经被定义了。 生命开始
    var a=1;
    function ft2(){
        a++;
        console.log(a);
    }
    return ft2;
}
var fn=ft1();
fn();//3
fn();//4
//只要 fn 不改变值  闭包就不会被回收，直到程序结束。fn重新开拓了内存，闭包就会被当作垃圾回收内存。为了不会造成内存泄漏，浪费内存，使用完就释放对象。
fn=null;
//内存溢出  ：程序运行的内存超过了设备的总内存，程序奔溃。
//内存泄漏  ：使用完的内存没有及时释放，致使程序可利用的内存减小，容易造成内存溢出
```

##### 应用

定义JS模块

* 具有特定功能的js文件
* 将所有的数据和功能都封装在一个 函数内部(私有的)
* 只向外暴露一一个 包信n个方法的对象或函数
* 模块的使用者，只需要通过模块暴露的对象调用方法来实现对应的功能

### 立即执行的函数

字面意思。就是函数定义好后就立即执行。

```javascript
(function(){
    //to do  something
})()
//或者
(function(){
    //to do  something
}())

```

