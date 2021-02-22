### 入口函数的区别

1. 代码示例

```javascript
//原生JS：
window.onload=function(){
  //加载完dom元素和图片之后再进行执行JS代码   
 };
//jQuery：
$(document).ready(function(e){
	//加载完dom元素后就立即执行js代码，此时图片还未加载完		
})；
jQuery(document).ready(function(e){
	//加载完dom元素后就立即执行js代码，此时图片还未加载完		
})；
$(function(){
    //加载完dom元素和图片之后再进行执行JS代码
});
jQuery(function(){
    //加载完dom元素和图片之后再进行执行JS代码
});
```

2. 原生JS如果编写多个入口函数后面的会覆盖前面的Jquery则不会覆盖，先执行前面的再执行后面的

---

### $符号的冲突问题

$符号可能在其他JS框架中被使用，这时候$就会产生冲突，其中一个库中的$被覆盖。
解决方法：
1、jQuery中$可以用jQuery代替，并且使用函数jQuery.noConflict();释放$的使用权。

2、自定义简化符号：var xia=jQuery.noConflict();就可以用xia代替$

---

### jquery的核心函数

$()或者jQuery()就代表调用jQuery的核心函数

#### 用法

##### 接收一个函数

***接收一个函数，并立即执行这个函数***

```javascript
//接收一个函数，并立即执行这个函数
$(function(){
    alert("hello world !");			
})
```

##### 接收字符串

1. 接收一个**字符选择器**，返回一个被选择的**jQuery对象**

2. 接收一个**字符串代码片段**，返回一个**jQuery对象**，对象中包含了一个DOM元素

3. 接收一个**DOM元素**，会包装成一个**jQuery对象**返回给我们

---

### jQuery对象

1. jQuery对象是一个伪数组
2. 伪数组：有0到length-1的属性 并且有length属性

#### jquery的静态方法

##### jQuery.each()

遍历数组或者伪数组：返回值是原数组

```javascript
jQuery.each(warr，function(index,value){
    //warr:伪数组  function：回调函数 index:索引  value：值        
})
```

##### jQuery.map()

jQuery的map()的返回值默认是空数组 回调函数的返回值就是map()的返回值,和 es6 里面的一样

```javascript
jQuery.map(warr,function(value,index){
	     console.log(index+":"+value);
	     return 2;
});
```

##### jQuery.trim()

去除空格  注：去除字符串两端的空格

##### jQuery.isArray()

判断是不是数组

##### jQuery.iswindow()

判断是不是 window对象

##### jQuery. isFunction()

判断是不是方法

---

### JQuery选择器

css**所有的选择器**，包括伪类选择器，jquery都能使用。还有自己**独有的伪类选择器**

##### :empty 

没有文本或者子元素的元素  eg：**$("div:empty");** 找到div 且没有子元素或文本的

##### :parent

有文本或者子元素的元素     eg：**$("div:parent");** 找到div 且有子元素或文本的

##### :contains

包含某个文本内容的元素 eg：**$("div:contains('hello')");** 找到div 且包含文本 hello 的div (注意是包含而不是等于)

##### :has

包含某个子元素的元素 eg：**$("div:has('span')");** 找到div 且包含子元素\<span>\</span>的div (注意是包含而不是只有)

##### :not

排除某些元素，即不包含某些选项。   **$("div:not(:empty)")**  选取有文本或者子元素的元素的div

---------------------------------------------------------------------------------------------------

### 过滤、查找、串联

jquery除了提供很多强力的选择器外还提供了许多强大的 过滤、查找、串联函数帮助我们选择需要的元素

#### 过滤

##### eq(n)

选择jquery中的第 n-1 个元素

##### first()

选择jquery中的第 1 个元素

##### last()

选择jquery中的最后 1 个元素

##### hasClass("className") 

判断含有某个类的元素，不包含的就被排除

```javascript
var res=$("div").hasClass("cd");
//只能用来判断，配合过滤函数使用，不能直接用来选择元素
```

##### filter(expr|obj|ele|fn)

筛选元素，从jQuery对象集合中选定某些符合标准的元素,可以包括（选择器）表达式、jQuery对象、元素、测试函数fn(index)。**多个表达式之间用逗号分隔**

```javascript
//函数过滤器的演示，函数会自动遍历所有元素，返回 true 则保留 反之排除  。函数的参数是遍历过程中元素的索引值。
$(".c1").filter(function(index){
    if($(this).text()=="1111")
        return true;
    else
        return false;
}).text("filter");
```

##### not(expr|ele|fn)	

从jQuery对象集合中排除某些符合标准的元素,括号里可以是一个选择器字符串、一个DOM元素、一个用来检查集合中每个元素的函数fn(index)。**this是当前的元素。**

```javascript
//和 filter 相反，符合条件则排除，不符合就保留
$(".c1").not(function(index){
    if($(this).text()=="filter")
        return true;
    else
        return false;
}).css("background","pink");
```

##### slice(start, [end])	

从jQuery对象集合中截取一部分，start和end是集合的索引，其中不包括end的索引项。如果不设置end则从start的索引截取到最后。

##### is(expr|obj|ele|fn)

**判断j**Query对象中是否有符合条件的dom对象，有则返回true，否则返回false。参数可以是选择器表达式、jQuery对象、dom元素、一个测试函数fn(index)。同样只能用来判断，不能直接选择元素。

#### 查找	

##### children([expr])

取得一个包含匹配的元素集合中每一个元素的**直接子元素**的元素集合。可通过可选的表达式来过滤所匹配的子元素

##### find(expr)

取得一个包含匹配的元素集合中每一个元素的所有**后代元素**的集合。可以通过可选的表达式来过滤所匹配的子元素

##### closest(expr|object|element)

向上匹配祖先元素，包含本身，而且只返回**最先匹配**到的符合要求的**一个**元素，可通过可选的表达式来过滤所匹配

##### parent([expr])

只返回父元素，不包含祖先元素，可通过可选的表达式来过滤所匹配的元素

##### parents([expr])

parents()不包含本身，直接从父元素开始匹配**所有祖先元素**，可通过可选的表达式来过滤所匹配的元素

##### parentsUntil([expr|element],[filter])

向上匹配祖先元素，**直到匹配到某个符合要求的祖先元素**，**把自己和该祖先元素之间的祖先元素返回**，不包括自己和该祖先元素在内，第一个过滤器匹配目标祖先元素，第二个过滤所匹配到的祖先元素。

##### offsetParent()

返回第一个定位的祖先元素

##### next([expr])

取得一个包含匹配的元素中每一个元素**紧邻的后面同辈元素**的元素集合，可通过可选的表达式来过滤所匹配的元素

##### nextAll([expr])

查找当前元素之后**所有的同辈元素**，可通过可选的表达式来过滤所匹配的元素

##### nextUntil([expr|element],[filter])

查找当前元素之后所有的同辈元素**直到匹配的指定元素**，**返回自身与该同辈元素之间的兄弟元素，取开集**。第一个过滤器匹配目标兄弟元素，第二个过滤所匹配到的兄弟元素。

##### prev()

向前查找兄弟元素  **prev([expr])、prevAll([expr])、prevUntil([expr|element],[filter]).** 

##### siblings([expr])

取得一个包含匹配的元素集合中每一个元素的所有唯一**同辈元素的集合**。可以用可选的表达式进行筛选。

#### 串联

##### add(expr|ele|html|obj,[con])

在原先的jQuery对象中再加入一个jquery对象或元素.第一个参数 是jQuery 对象、一个或多个元素、HTML 片段 .后一个参数可选，表示上下文，即 从哪里开始匹配 第一个参数的元素

##### addBack()

添加调用上一步操作的的jQuery对象至操作之后的jQuery中.

```javascript
//把调用siblings()的jquery对象$("#big2")也添加在了最后的选中元素中
$("#big2").siblings().addBack().css("width","600px");
```

##### end()

返回到最后一个"破坏性"操作之前的jquery对象。即将匹配的元素列表变为前一次的状态。

----

### 属性、属性节点

#### 属性

1. 什么是属性
   对象保存的变量就是属性

2. 如何操作属性
   object.属性名称     或者    object['属性名称']

#### 属性节点

##### 什么是属性节点

编写HTML代码时 在HTML标签中添加的属性就是属性节点,\<span name="span1">\</span>
属性节点保存在DOM元素的**attribute**属性中

##### **如何操作属性节点**

d.attr("name") :获取属性该属性节点的值

d.attr("name","value")：设置   /  添加 该属性节点

d.removeAttr(" name1 name2 ...")可同时删除多个DOM元素的多个属性节点  中间用空格隔开

d.prop("name")：和 attr()一样

d.prop("name","value"):和 attr()一样


d.removeprop(" name1 name2 ...")

**attr和prop的区别**： 
prop不仅能够操作属性节点还能操作属性推荐：属性节点值是 true/false时使用prop()

#### 属性和属性节点的区别

所有对象都有属性。只有DOM对象才有属性节点

---

### 类操作相关方法

##### dom.addClass("classname1 classname2 ")

添加类,可同时添加多个类用中间用空格隔开

##### dom.removaClass("classname1 classname2 ")

删除类 ，可同时删除多个类 类名用空格隔开

##### dom.toggleClass("classname1 classname2")

切换类,有就删除 没则添加，可同时切换多个类 类名用空格隔开

---

### 文本值相关方法

#####  dom.html()

dom.html("代码片段"); 设置html代码。没参数代表获取dom里面的代码片段 代码片段：代码+文本

##### dom.text()

dom.text("文本内容");设置文本。dom.text();得到文本

##### dom.val()

dom.val("value值");设置value值 如 input 的value值。dom.val();得到value值 

---

### css样式相关方法

#### 设置样式

1. 逐个属性设置:dom.css("name","value");

2. 链式设置：dom.css("name1","value1").css("name2","value2").css("name3","value3")...;不建议超过三个属性连着写

3. 批量设置(推荐写法)：

   ```javascript
   dom.css({
       name1:"value1",        
       name2:"value2"
    });
   ```

#### 获取样式

dom.css("name");

-----

### 位置的操作

##### 相对于窗口的边距

**dom.offset()**

获取：dom.offset().left     dom.offset().top
设置：dom.offset({left:10, top:10});

和原生 js 不同，原生只能获取，不能设置。

##### 相对于定位元素的边距

**dom.position()**

获取：dom.position().left         dom.position().top   

注：position()不能设置 **只能获取**  直接用dom.css()就可以设置

##### 滚动条的偏移量

scrollTop()、scrollLeft()  有参设置 无参获取
特殊的：获取整个网页滚动条的偏移量浏览器兼容：IE 用body 其他用html 
兼容：
获取：$("body").scrollTop()+$("html").scrollTop();
设置：$("body，html")scrollTop(300);

------------------------------------------------------------------------------------------------------------------------------------------------
### 事件绑定

1. eventName(fn)   推荐使用这种，编码效率高，有提示，不可以绑定自定义事件

```javascript
	$("button").click(function(){});
```

2. on(eventName,fn)  可以绑定自定义事件和系统事件

```javascript
	$("button").on("click",function(){});
```

同一个事件定义两次不会被覆盖

---

### 事件解绑、冒泡、默认事件

####  事件解绑 off()

无参数：$("button").off()   移除所有绑定的事件
一个参数：$("button").off("click")   移除所有指定类型的事件
两个参数：$("button").off("click",fname)   移除指定类型的事件的指定函数

#### 事件冒泡

事件冒泡：事件由子元素逐级传递给父元素

##### 阻止冒泡

1. return false;
2. event.stopPropagation()  

#### 默认行为

默认行为:很多元素都有默认事件 比如单机鼠标右键弹出菜单、点击链接会跳转

##### 阻止默认行为

1. return false;

2. event.preventDefault()   

----

### 事件自动触发

1. **trigger(eventName)** 

   $("button").trigger("click") ；此方法会事件冒泡、会触发默认行为

2. **triggerHandler(eventName)** 

   $("button").triggeHandler("click") ；此方法不会事件冒泡、且阻止默认行为

-----

### 自定义事件

#### 特点

1. 自定义事件只能通过on(eventName,fn)来绑定
2. 自定义事件只能用事件自动触发来触发事件

#### 绑定及触发

jQuery事件命名空间：（多人协同制作的时候让大家使用自己的定义事件）
绑定：on(eventName.namespace,fn)        namespace是命名空间，自定义名字
触发件:  $("button").trigger("click.namespace") ;
注意：

利用trigger触发子元素带命名空间事件，会触发父元素带相同命名空间的事件
利用trigger触发子元素不带命名空间的事件，那么子元素所有相同类型的事件和父元素所有相同类型的事件都会被触发

-----

### 事件的委托

事件的委托：将事情交给别人做，别人再把事情结果告诉你
使用场景：给某个加载时还不存在的元素添加事件 ，让入口函数执行之前就存在的元素去监听程序动态生成的元素的某些事件
注：只能是子元素委托事件给父元素监听
$("父元素").delegate("子元素","click",function(){});

----

常用事件
mouseover();鼠标进入事件
mouseout();鼠标离开事件      这两个方法都会触发父元素的事件

**mouseenter();**
**mouseleave();这两个方法不会触发父元素**

**hover(ftn);移入移出同一个方法**
**hover(ftn,ftn);第一个参数是移入的方法 第二个参数是鼠标移出的方法**

其他事件参考手册

---

### 显示与隐藏动画

#### show(time,fn)

实质是设置display="block";具有动画效果的显示 。动画是右上角到左上角 

参数 time 是动画显示时间 fn是动画结束后执行的函数 fn可省略

#### hid(time,fn)

实质是设置display="none";具有动画效果的隐藏  。动画是右上角到左上角 

参数 time 是动画显示时间 fn是动画结束后执行的函数 fn可省略

#### toggle(time,fn)

切换 顾名思义 当是隐藏时切换成显示 显示时切换成隐藏。动画是右上角到左上角 

#### slideDown(time,fn)

实质是设置display="block"。动画是向下展开 

#### slideUp(time,fn)

实质是设置display="none";动画是向上收起 参数同上

#### slidetoggle(time,fn);

切换 顾名思义 当是隐藏时切换成显示 显示时切换成隐藏。

#### fadeIn(time,fn)

淡入，透明度0到1

#### fadeout(time,fn)

淡出，透明度1到0

#### fadetoggle(time,fn)

淡入淡出 切换

#### fadeto(n)

淡入到多少 就是调整透明度 n=0到1  

----

### 动画的停止

#### stop()

1. dom.stop(false,false) , dom.stop(false);  **停止某个元素正在进行的事件** **继续执行后续的事件**

2. dom.stop(true);dom.stop(true,false)     **停止当前和后续动画**

3. dom.stop(false,true);        **立即完成当前事件，继续后续动画**

4. dom.stop(true,true);          **立即完成当前事件，停止后续动画**

#### 动画队列

某个元素的多个动画效果，**不会同时执行**，先执行先出现的效果，执行完毕后才会执行后面的效果。如果想插队，就得stop前面的动画正因为有动画队列，如果你想要执行顺序执行几个不同的动画效果，不需要嵌套事件 如：slideDown(1000,functiom(){ fadein()  });
链式动画：dom.slideDown().fadeIn();

----

### 自定义动画

多个属性的动画是同时执行的 
animate({属性值},time,ftn);  {属性值}->{width:500,height:500}  属性：值
animate({属性值},time,"动画节奏",ftn); 动画节奏 ：分为匀速 linear和缓动swing  默认缓动  基本运动也可以加这个参数

#### 属性的变化

确切的值：{width:500,height:500}

对象累加属性：{width:"+=500"} 属性=属性+500
对象关键字属性：{width:"hide";height:"toggle"} 其他关键字百度

延时函数：delay(time);

#### 动画设置

fx.off=false 动画效果的开关，默认打开 false

fx.interval=13;设置动画的帧数 默认13

---

### 文档操作（节点操作）

#### 创建元素

var obj=$("代码片段");

jquery核心函数会把代码片段里的元素返回成一个jQuery对象，jQuery对象包含了该元素对象

#### 添加节点

##### 内部插入

?	parent.append(child);添加到指定元素的内部的最后面
?	parent.prepend(child);添加到指定元素的内部的最前面

##### 外部插入：	

?	dom.after(dom1);将dom1添加到dom外部且紧跟dom后面
?	dom.before(dom1);将dom1添加到dom外部且紧跟dom前面

?	dom1.inserAfter(dom);将dom1添加到dom外部且紧跟dom后面
?	dom1.inserBefore(dom);将dom1添加到dom外部且紧跟dom后面

##### 删除节点：

?	dom.empty();删除dom的子元素及文本内容 dom本身并不会删除
?	dom.remove();删除dom及子元素
?	detach();删除dom及子元素

##### 替换节点：

?	dom.replaceWith(dom1);用dom1替换所有dom
?	dom1.replaceAll(dom);用dom1替换所有dom

#### 复制节点：

##### 浅复制

dom.clone(false);复制dom这个元素及文本  不会复制元素身上绑定的事件

##### 深复制

dom.clone(true);复制dom这个元素及文本   会复制元素身上绑定的事件

---

### jQuery原理

#### jQuery结构

jQuery的本质是一个闭包：
   （function(window,undefined)
	 {
	 }）(window)

#### 闭包

一个立即执行的函数	/	定义在一个函数内部的函数

#### jQuery为什么要使用闭包？

避免多个框架之间的冲突，比如变量、函数重名。把变量放在闭包中，就是把变量放在函数中，作用域只在该函数内部

#### jQuery如何向外部暴露数据

把需要暴露的数据变成全局的  window.XXX=XXX       jQuery只是往外部暴露了一个对象 jQuery，这个对象包含了jQuery所有的方法和变量

#### jQuery为什么要给自己传递一个window参数

为了后期压缩代码

提升查找的效率

---

### Ajax

$.Ajax() 这个函数就是jquery对ajax的封装，支持 promise 写法。

```javascript
//读取json数组文件，返回一个数组，里面是对象的集合
				$.ajax({
					url:"test.json",
					success:function(data)
					{
					console.log(data);
					},
					dataType:"json"
				});
//读取一个json对象文件，返回一个json对象，里面还有很多对象
				$.ajax({
					url:"a2.txt",
					success:function(data)
					{
					console.log(data);
					},
					dataType:"json"
				});
//读取一个不标准的json文本，返回的是纯文本，对文本操作转换成对象或数组
				$.ajax({
					url:"test3.json",
					success:function(data)
					{
					console.log(data);
					var obj=eval("("+data+")");
					console.log(obj);
					},
					dataType:"text"
				});
//读取一个XML文件，返回的是一个文档对象，就像HTML的document一样
				$.ajax({
					url:"x1.xml",
					success:function(data)
					{
					console.log(data);
					console.log(data.querySelector("yifu > title").innerHTML);
					},
					dataType:"xml"
				});
```

