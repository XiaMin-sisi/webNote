# 问题

1.行内元素能不能设置 宽、高、内边距 、外边距？？？

宽高:无效

padding:上下左右都用有，但是上下的内边距会浮动起来。仅仅是边距浮动。

margin:左右有用，上下没有作用。

2.元素浮动是相对于块级元素？ 给span设置 float=right ，浮动是相对于 li 的,span浮动到了li的最右侧

```html
*{margin: 0;padding: 0;text-decoration: none;}
div{width: 160px;height: 600px;background-color: rgba(0,0,0,0.3);}
li{list-style: none;padding: 15px;background-color: #BA1711;}span{float: right;}
a{background-color: #00FFFF;}
<div>
    <ul>
        <li>
            <a href="#">
                javascript <span> X </span>
            </a>
        </li>
    </ul>
</div>
```

确实是相对于块级祖先元素来说的浮动。但是这只是特殊的，因为只有块级元素里面才能放其他元素，a标签作为一个行内元素，里面也还能添加其他元素。

3.margin、padding的百分比设置是相对于谁

都是相对于父元素来说，而且是相对于父元素的 **宽度**

4.行内元素、行内块元素作为父元素时。有多个子元素，给其中一个子元素设置外边距，效果如何。

# HTML

#### span和div

span和div都没有具语义，只是一个盒子而已。不同的是 div 是一个块级元素，独占一行。span 是一个行内元素，可以好几个元素一行排列

#### img

```html
<img src="图片路径" alt="替换文本"  title="鼠标悬停标题">
```

#### a

```html
<a href="" target="_blank"></a> 打开新的窗口
<a href="" target="_self"></a>  覆盖原窗口，默认就是这种打开链接方式
<!-- 
使用链接访问本地文件非html标签
浏览器可以解析的就会直接打开比如 文本文件、图片，
打不开的就会下载比如：.exe、.rar、.zip 
-->
<a href="1.txt">查看文本文件1.txt</a>
<a href="test.exe">下载文件 test.exe</a>

<!-- 锚点链接=》跳转到响应的 id 的元素 -->  
<a href="#div1"></a>
<div id="div1"></div>
锚点元素默认会出现在屏幕的顶部,如果想要控制锚点元素与顶部的距离,可以设置代替元素锚点.
1、新增一个无关元素在真正的需要锚点的元素前面
2、隐藏无关元素、设置高度、设置顶部边距为负值以抵消
3、给无关元素设置id
<div className={styles.maodian} id={item.id}>工具元素</div>
<div >真正要锚点的元素</div>
.maodian{
    visibility: hidden;
    height: 80px;
    margin-top: -80px;
  }

```

#### ul 、ol 、li

**ul** 、**ol** 的直接子元素只能是 **li**,**li**的子元素可以是任意的

####  radio、checkbox

```javascript
<!-- 单选框 radio 的 name属性相同的为一组，一组之中只能有一个被选中 -->
<input type="radio" name="sex" value="1"/>
<input type="radio" name="sex" value="2"/>
<input type="radio" name="sex" value="3"/>
    
<!-- 复选框 checkbox的name属性相同的为一组，但是一组中可以 选中若干个 即结果集是一个数组 -->
<input type="checkbox" name="hobbit" value="1">
<input type="checkbox" name="hobbit" value="2">
<input type="checkbox" name="hobbit" value="3">
```

#### label

```html
<!--
label 标签用于帮助获取表单元素获取焦点 
对于 text 输入框来说就是输入框获取焦点
对于 radio、checkbox 单选框、复选框来说就是选中该项
-->
<!-- label的 for 属性 与表单元素的 id 相对应 -->
<label for="man">男</label>
<label for="wman">女</label>
<label for="allnot">保密</label>
<input type="checkbox" name="hobbit" value="1" id="man">
<input type="checkbox" name="hobbit" value="2" id="wman">
<input type="checkbox" name="hobbit" value="3" id="allnot">
```



# CSS

### 文本装饰

#### text-decoration-line

语法：**text-decoration-line**：none | [ underline || overline ||  line-through || blink ]

 取值：

- none： 指定文字无装饰 ，取消某些自带装饰元素的装饰，比如 a标签的下划线
- underline： 指定文字的装饰是下划线 
- overline： 指定文字的装饰是上划线 
- line-through： 指定文字的装饰是贯穿线 
- blink： 指定文字的装饰是闪烁。 

#### text-decoration-color

语法：**text-decoration-color**：color

指定装饰的颜色

#### text-decoration-style

语法：**text-decoration-style**：solid | double | dotted | dashed |  wavy

 取值：

- solid： 实线 
- double： 双线 
- dotted： 点状线条 
- dashed： 虚线 
- wavy：波浪线

### 文本属性

#### text-indent：文本缩进

语法： 

text-indent：“ <length>[each-line] [hanging]”

取值：

- length： 用长度值 px 指定文本的缩进。可以为负值。  用百分比指定文本的缩进。可以为负值。还可以使用 **em** 作为单位，表示缩进几个字
- each-line： 定义缩进作用在块容器的第一行或者内部的每个强制换行的首行，软换行不受影响。（CSS3） 
- hanging： 反向所有被缩进作用的行。（CSS3） 

#### text-transform: 大小写转换

语法：**text-transform**：none | capitalize | uppercase | lowercase |  full-width

取值：

- none： 无转换 
- capitalize： 将每个单词的第一个字母转换成大写 
- uppercase： 将每个单词转换成大写 
- lowercase： 将每个单词转换成小写 
- full-width： 将所有字符转换成fullwidth形式。如果字符没有相应的fullwidth形式，将保留原样。这个值通常用于排版拉丁字符和数字等表意符号。（CSS3） 

### 复合(关系)选择器

#### 后代选择器

语法：选择器1 选择器2 {}

语义：选择器1 的后代元素 中再使用选择器2，注意是 后代，不一定是子元素

示例： div p {} 选择的就是 div 元素里的 p 标签

#### 子元素选择器

语法：选择器1 > 选择器2>... {}

语义：选择器1 的元素 的子元素中再使用选择器2,第二个选择器只能从第一个选择器的直接子元素中选择

示例： div p {} 选择的就是 div 元素里的 直接子元素且元素为p 标签

#### 并集选择器

语法：选择器1,选择器2 ,...{}

语义：符合其中任意一个选择器的元素都会被选择到。就是 选择器1的元素 和 选择器2的元素

示例： div,p {} 选择的就是 div 元素 和 p 标签

#### 后面兄弟选择器

语法：选择器 1~ 选择器2{}

语义：选择器1的同级元素中 符合 选择器2的元素且在选择器1后面的，如果选择全部同级元素 就使用通配符 *

示例：div ~ p{} 选择的是 div 元素同级、且在div后面的的 p 元素

#### 下一个兄弟选择器：

语法：选择器 1 +  选择器2{}

语义：选择器1的同级元素中的紧邻自己的下一个元素，且必须满足选择器2的条件，如果没有选择器2就写 *

示例：div  + * 	表示无条件选择紧邻 div 元素的下一个元素

​			div + span  	表示选择紧邻 div 元素的下一个元素，如果这个元素是 span 标签的话

----

### 属性选择器

##### 存在某个属性

语法： 选择器1[属性名]{}

语义：选择器1 中 带有该属性的元素

示例：*[name]{}

​			span{name}

##### 属性值相等

语法： 选择器1[属性名=“value”]{}

语义：选择器1 中 带有该属性且属性值为 value的元素

示例：*[name=“夏敏”]{}

​			span{name=“思思”}

##### 包含某个属性值

语法： 选择器1[属性名~=“value”]{}

语义：选择器1 中 带有该属性且属性值中含有 一个值为 value 元素的

示例：*[class~=“c1”]{}

​			span{name~=“思思”}

##### 属性值开头

语法： 选择器1[属性名^=“value”]{}

语义：选择器1 中 带有该属性且属性值以 value 开头的元素

##### 属性值结尾

语法： 选择器1[属性名$=“value”]{}

语义：选择器1 中 带有该属性且属性值以 value 结尾的元素

##### 属性值包含字符串

语法： 选择器1[属性名*=“value”]{}

语义：选择器1 中 带有该属性且属性值包含有为 value 字符串的元素



### 伪类选择器

##### 超链接伪类

+ :link {} ：链接未被点击时的状态
+ :visited {} ：链接被点击后的状态
+ :hover {} ：鼠标悬停在链接上时的状态，不光可以用于链接，其他元素也可以
+ :active {}：鼠标按下还没有弹起的状态，不光可以用于连接其他元素亦可以

注意：如果你要给超链接设置四种状态，你就必须按照一定顺序来编写。

​			a:hover 必须位于 a:link 和 a:visited 之后，a:active 必须位于 a:hover 之后

##### input焦点伪类

:focus：选择获取到焦点的元素，一般只有表单元素才会获取焦点

##### 过滤、排除某些元素

语法：**E:not(s)** { sRules }

语义：E是一个选择器，S也是一个选择器，最终的结果是，E-S 的结果集

##### 父亲的长子

语法：选择器1:first-child{}

语义：选中 选择器1 的父元素的第一个子元素

😂 最后的结果也必须是符合第一个选择器的，比如 span:first-child{}表示：

如果span是某个元素的第一个子元素才会被选择。并不是说，只要有span标签就去找span的长兄，还不如叫，我是父亲的长子吗，是的话，选择我。

##### 父亲指定类型的长子

语法：选择器1 tagname**:first-of-type{}** 

语义：选择与自己标签名相同的第一个兄弟元素，我只要是最大的 男孩，即使我有姐姐，我也会被选中。

##### 父亲的庶子

:last-child{}

😂用法和 :first-child{},一样，不过选的是最后一个元素而已

##### 父亲指定类型的庶子

语法：选择器1 tagname**:first-of-type{}** 

语义：选择与自己类型相同的最后元素，我只要是最小的 男孩，即使我有妹妹，我也会被选中。

##### 独生子元素

语法：选择器1:only-child{}

语义：选择器1 选出的元素 且没有兄弟元素

😂但是吧只能用来选择自己：我是独生子吗？

##### 第 N 个兄弟元素

语法：选择器:nth-child(n) { }，可以写 n ,也可以写具体的数字

语义：选取兄弟元素 从 n=0 1 2 3 ...开始选取。写具体数字的话，就是代表 第几个兄弟元素

用法：我们可以 写成带 n 的式子，来过滤一些兄弟元素

​			如 ：2n 就会选择 是偶数个的兄弟元素 即第 2 4 6 8 10...个兄弟

​					 2n+1 就是选择 是奇数个的 兄弟元素 即第 1 3 5 7 9...个兄弟

​					 5-n 就是选择前4个兄弟元素

​			        写成具体的数字：nth-child(3) { }选择第三个兄弟元素

😂 最后的结果也必须是符合第一个选择器的，比如说  span:nth-child(n) { n },只能选择到 类型为span的标签

##### 倒数第 N 个兄弟元素

语法：选择器**:nth-last-child(n)**

语义：选择该元素的倒数 第 0 1 2 3 ...个兄弟元素

用法和:nth-child(n)大致，:nth-child(n)不能选取最后一个兄弟，:nth-last-child(1)可以

##### 空元素

语法：**E:empty** {  }

语义：**匹配没有任何子元素（包括text节点）的元素E。**

##### 选中的radio、check

语法：**E:checked** { sRules }

语义：**匹配用户界面上处于选中状态的元素E。(用于input  type为radio与checkbox时)** 

##### 可用状态的元素

语法：**E:enabled** { sRules }

语义：**匹配用户界面上处于可用状态的元素E。** 表单元素才有这个属性

##### 禁用状态

语法：**E:disabled { sRules }**

语义：**匹配用户界面上处于可用状态的元素E。** 表单元素才有这个属性

### 元素的显示模式

##### 显示模式的分类

1. **块级元素**： div、p 、h1~h6、ul、ol、li、table

   + 独占一行

   + 高度、宽度都可以设置

   + 宽度默认是父级的 100%（独占一行，宽度当然是 100%）

   + 本身是一个容器，里面可以添加其他元素，包括块级元素

     **注**：文字类块级元素（p 、h1~h6）只能放行内元素和文字

2. **行内元素**： span、a  ...等等

   + 相邻行内元素会在同一行，除非放不下了才会换行

   + 行内元素设置不了 宽、高,宽高都是靠内容撑

   + 行内元素只能放文本或者其他行内元素

     **特殊的**：a 标签作为行内元素，但是里面不能再放一个 a 标签。

     ​				 但是 a 标签里面可以放块级元素 

3. **行内块元素**：img  、input  、td

   😂因为这类元素既有块级元素的特点又有行内元素的特点，我们叫它行内块元素

   + 相邻元素可以在同一行，虽然两者之间会有距离=》行内元素的特点
   + 默认宽度就是本身内容的宽度 =》行内元素的特点
   + 可以设置本身的宽高和边距 =》块级元素的特点

##### 显示模式的转换

* 转块级元素： display:block;
* 转行内元素：display: inline;

* 转行内块元素： display :inline-block;

----

### 背景

背景颜色和背景图片可以同时设置，背景图片会把背景颜色覆盖，某些特定时候，背景图片会比元素小，就可以既看得到背景图片，有看得到背景颜色

#### 背景颜色

​	**background-color**：color

----

#### 背景图片

​	**background-image**:url

----

##### 	背景图片平铺

当所用图片比元素更小时，默认会平铺背景图以沾满整个元素

**background-repeat**：repeat 默认值

​	取值：

- repeat-x： 背景图像在横向上平铺 
- repeat-y： 背景图像在纵向上平铺 
- repeat： 背景图像在横向和纵向平铺 
- no-repeat： 背景图像不平铺 
- round： 当背景图像不能以整数次平铺时，会根据情况缩放图像。（CSS3） 
- space： 当背景图像不能以整数次平铺时，会用空白间隙填充在图像周围。（CSS3）

----

##### 图片位置和精灵图

不管背景图片比元素大还是小，都可以设置。背景图片过大，为了把主要内容显示出来，可以让背景居中显示。

background-position：x  y       默认值为 0% 0%，效果等同于left top

1. *方位名词取值*： 
   
   - center： 背景图像横向或纵向居中。 
   - left： 背景图像从元素左边开始出现。 
   - right： 背景图像从元素右边开始出现。 
   - top： 背景图像从元素顶部开始出现。 
   - bottom： 背景图像从元素底部开始出现。 
2. *百分比取值*：和精确数值的参数一样使用，不过使用的是元素长宽的百分比

3. *精确数值取值*：left 和 top 有严格的顺序关系，第一个一定是左边距，第二个是上边距

   20px 30px =>left top =>代表左边距20px 和 上边距30px

4. *混合使用*：

   第一种有顺序之分：left 30px 、center 60px、20px center

   还可以这样混合，这种可以不分顺序 ：left 30px bottom 20px=》表示距离左边 30px 距离底部 20px
   
   控制背景图片的位置，就可以控制**精灵图**显示的部分是哪里

##### 固定背景图片

语法：**background-attachment**：fixed | scroll |local

 取值：

- fixed： 背景图像相对于视口（viewport）固定。 
- scroll： 背景图像相对于元素固定，也就是说当元素内容滚动时背景图像不会跟着滚动，因为背景图像总是要跟着元素本身。但会随元素的祖先元素或窗体一起滚动。
- local： 背景图像相对于元素内容固定，也就是说当元素随元素滚动时背景图像也会跟着滚动，因为背景图像总是要跟着内容。（CSS3） 

**注**： 简单说，如果该元素 设置了 overflow: scroll; 那么你设置背景图片的 background-attachment: scroll 背景图片是不会跟着滚动的 ，必须设置  background-attachment: local

----

##### 背景颜色的范围

语法：**background-clip**：默认值 border-box

- border-box： 从border区域（含border）开始向外裁剪背景。从边框开始绘制背景，如果边框自己设置了背景色，会覆盖元素的背景。
- padding-box： 从padding区域（含padding）开始向外裁剪背景。不绘制边框 
- content-box： 从content区域开始向外裁剪背景。 不绘制padding 及边框
- text： 从前景内容的形状（比如文字）作为裁剪区域向外裁剪，如此即可实现使用背景作为填充色之类的遮罩效果。[遮罩效果](http://demo.doyoe.com/css3/background-clip/mask-text2.htm) See with Webkit ，只给里面的文字加背景（相当于给文字设置颜色，这样就可以设置字体的透明度了）

----

##### 背景图片的大小

语法：**background-size**：百分比 |具体值 |auto|cover

取值：

- 精确值： 用长度值指定背景图像大小。不允许负值。  需要两个参数分别代表宽 高。如果只写一个默认只设置宽度，高度将使用真实的高度。
- 百分比： 用百分比指定背景图像大小。不允许负值。 百分比是相对于元素来说的 需要两个参数分别代表宽高。如果只写一个默认只设置宽度，高度将使用真实的高度。
- auto： 背景图像的真实大小。 =》默认值
- cover： 将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器。 等比例缩放时，要覆盖整个元素，并不可能宽、高同时都和元素一样，其中一个达到后，也会继续跟着缩放，直到完全覆盖。
- contain： 将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包含在容器内。等比例缩放背景图片时，只要宽高任意一个和元素的相等，则停止缩放。

----

### CSS三大特性

##### 层叠性

前面的覆盖后面的

##### 继承性

哪些样式会被继承： 文字相关的样式比如:text-、 line- 、font- 开头的样式,以及颜色 color

##### 优先级

+ 选择器相同则执行层叠性

+ 选择器不同则看选择器的权重

  继承、* < 元素选择器< class、伪类选择器 < id选择器 <行内样式 <!important

总结：如果使用的是复合选择器，只要 某一方，有更高级的，那么这一方的优先级更高，如果所用的选择器 类型都是相同的级别，谁多谁优先。示例

​		class+class>class

​		class+ class<id

​		class+ class+id>id+class   => 两边同时减去一个 id class => class>0😂天才

### 盒子模型

#### 边框

语法：border： width| style|color

width取值：

- 精确值： 用长度值来定义边框的厚度。不允许负值 。单位是像素
- medium： 定义默认厚度的边框。计算值为3px 
- thin： 定义比默认厚度细的边框。计算值为1px 
- thick： 定义比默认厚度粗的边框。计算值为5px

style的取值：

- none： 无轮廓。当定义了该值时，[border-color](border-color.htm)将被忽略，[border-width](border-width.htm)计算值为`0`，除非边框轮廓应用了[border-image](border-image.htm)。 
- hidden： 隐藏边框。 
- **dotted**： 点状轮廓。 
- **dashed**： 虚线轮廓。 
- **solid**： 实线轮廓 
- double： 双线轮廓。两条单线与其间隔的和等于指定的[border-width](border-width.htm)值 
- groove： 3D凹槽轮廓。 
- ridge： 3D凸槽轮廓。 
- inset： D凹边轮廓。 
- outset： 3D凸边轮廓。 

---

##### 相邻边框合并

语法：**border-collapse: collapse;**

语义：两个元素相邻的边框不会重叠在一起，而导致边框变宽。

----

##### 圆角边框

语法：**border-radius:**精确值 |百分比

1. 如果你想做一个圆形边框：先使元素的宽和高相等，在设置 border-radius:宽高的一半
2. 如果你想要一个圆角矩形：你就设置border-radius:矩形高度的一半
3. 如果你想要四个角不一样的圆角：你就设置4个参数给border-radius，从左上角开始顺时针设置

----

##### 盒子阴影

语法：**box-shadow**=none 默认值

1. none： 无阴影 
2. 有六个参数

- length①： 第 1 个长度值定义元素的阴影水平偏移值。正值，阴影出现在元素右侧；负值，则阴影出现在元素左侧 。就是距离 左边的距离 left 
- length②： 第 2 个长度值定义元素的阴影垂直偏移值。正值，阴影出现在元素底部；负值，则阴影出现在元素顶部 。就是距离顶部的距离 top
- length③： 第 3 个长度值定义元素的阴影模糊值半径（如果提供了）。该值越大阴影边缘越模糊，若该值为`0`，阴影边缘不出现模糊。不允许负值 。就是控制阴影的模糊程度，越大越模糊。
- length④： 第 4 个长度值定义元素的阴影外延值（如果提供了）。正值，阴影将向四面扩展；负值，则阴影向里收缩 。盒子外部阴影的大小，负数当然就是里面一部分没阴影
- color⑤： 定义元素阴影的颜色。如果该值未定义，阴影颜色将默认取当前最近的文本颜色 
- inset⑥： 定义元素的阴影类型为内阴影。该值为空时，则元素的阴影类型为外阴影 。默认外阴影

####  padding

如果元素设置**width**属性，再设置 **padding**，会导致元素的宽高变化，会加上 padding

但是，如果你没有给那个元素设置**width**属性，**padding**属性就不会改变盒子的宽高，比如块级元素，默认宽度等于父级的宽度，你再设置 **padding**，宽度也还是等于父级的宽。

**注意**：一直的误区，padding没有auto的属性值，margin才能设置auto

----

#### 在盒子里居中

##### 块级元素居中

使用**marrgin**，子元素设置  **margin: 0 auto**;或者 **margin：auto 0**， **margin：auto**

**前提**是你必须设置子元素的宽度，因为你不手动设置宽度，默认和父元素一样宽，不就是沾满了盒子，还居中个屁啊。为什么父元素宽度不用设，因为就算你不设置，块级元素默认宽度等于父级的宽度，最后不行所有父级都没宽度，不就和 **网页body**的宽度一样。

同理如果你想设置**垂直方向居中**，必须把子元素和父元素的高度都设置好

##### 行内、行内块元素

使用text-align: center;设置父元素 **text-align: center;**

----

#### 父子外边距合并问题

```html
#div1{
			background-color: #00FFFF;
			text-align: center;
			width: 800px;height: 200px;
		}
#div2{
            margin-top: 100px;
            width: 100px;height: 50px;
            background-color: #008000;	
	}
<div id="div1">
	<div id="div2"></div>	
</div>

```

<img src="C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1592037222962.png" alt="1592037222962" style="zoom:50%;" />

此时子元素的外边距，就会变成父元素的外边距。

解决办法：

1. 给父元素设置边宽或者内边距
2. 父元素设置溢出隐藏
3. 给子元素设置为浮动

### 设置颜色的透明度

设置颜色的同时，设置颜色的透明度，和 opacity 不同，opcity只能设置元素的透明度。

示例：RGBA(255,255,255,0.3) =》白色，透明度为0.3

----

### 浮动

语法: float =left|right |none

任何元素都能加浮动属性，设置了这个属性的元素都具有**行内块元素**的特点。

浮动的理解：浮动是元素飘起来了，比没有浮动的盒子会更高一点，所以如果一个盒子浮动了，后面有一个没有浮动的盒子，后面的盒子会被浮动的盒子压住，导致两个盒子重合。如下图，蓝色的盒子是一个浮动的盒子，粉红色的盒子不浮动，所以被蓝色的盒子压住了。

![1592061461814](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1592061461814.png)

***为了避免这种情况，浮动的盒子一般都被不浮动的盒子包裹着。*****用标准流搭建大框架，浮动元素准确布局**。

##### 文字环绕图片

正如上面图显示的，浮动虽然有不好的影响，但是也可以利用这一点，实现一个这样的效果： 一张图片在段落中间，文字环绕这种图片，因为和定位元素不同，float虽然会压着后面的元素，但是很讲道理，不会压着你的文字

##### 父盒子需要高度吗？

就像上面说的，浮动就是飘起来了，飘起来了自然就不能撑起父元素的高度。那么父元素的高度就是 0 px.

如何解决？=》请看下一个知识点-》清除浮动 

##### 清除浮动

1.额外标签法

```html
<!-- 在父元素的 最后面添加一个空标签 这个标签是额外的，什么内容都不需要，但是这个标签必须是块级元素
	 只要设置样式清除浮动  clear: both 浮动就不会影响父元素外面的元素了，相当于这个额外的标签，
	 把负面影响一个人扛了下来。
-->
<div>
    <div style="float: left;"></div>
    <div style="float: left;"></div>
    <div style="clear: both;"></div>
</div>

```

2.父级设置属性 ：overflow=hidden | auto |scroll

3 :after为伪素法：给父元素添加一个伪元素，通过css属性的方式添加一个伪元素

属性内容如下：

```css
.clearfix:after{
    content:"";				/*设置内容为空*/
    height:0;				/*高度为0*/
    line-height:0;			/*行高为0*/
    display:block;			/*将文本转为块级元素*/
    visibility:hidden;		/*将元素隐藏*/
    clear:both;				/*清除浮动*/
}
.clearfix{
    zoom:1;					/*为了兼容IE*/
}
类名或者id都行，只要是 通过 :after 添加了这些属性就可以,其实也就是相当于第一种方法，只是 通过css添加元素罢了。
```

4.双伪元素法 ：不仅仅通过 **:after**在盒子后面添加一个伪元素清除浮动，还在通过 **:before **最前面再添加一个伪元素

```css
.clearfix:before,.clearfix:after{
   content:"";
   display:table;
}
.clearfix:after{
  clear:both;
}
.clearfix{
  *zoom:1;
}
```

----

### 导航栏的写法

导航栏不要直接用 a 标签写，要用。li 标签包裹每一个 a 标签。这样做的原因是，如果太多链接对堆砌在一起，容易让搜索引擎 降权 ，影响网站排名

----

### 定位

position：static|relative|absolute| fixed| sticky

五种定位：静态 static、相对 relative、绝对 absolute、固定 fixed、粘性 sticky

##### static

静态定位 static 就是默认的定位，其实就是没有定位

##### relative

相对定位又叫做 自恋定位，因为他所有的定位都是相对于 自己本身  来说的。top left right bottom

*relative 不会脱离标准流*

##### absolute

绝对定位又叫做 拼爹定位，因为他的定位是相对于 一个*最近的且有定位的祖先元素*来说的。如果没有符合要求的祖先元素，就以 body 为准。一般我们都使用 **子绝父相 ** 的原则 。top left right bottom。

*absolute 会脱离标准流*

##### fixed

fixed 叫做固定定位，具有fixed属性的元素是相对于浏览器的*可视化窗口来说的。*不会随着滚动条的滚动而滚动。不会占用元素位置，*会脱离标准流*。

#####  sticky

粘性定位被认为是 固定定位和相对定位的混合。相对于浏览器的可视化窗口来设置边距，会占用原来的位置，即 不脱标。

效果就是，比如设置 top =10 px，在随着鼠标滚动而滚动的时候，当元素距离可视化窗口顶部 10px 时，变成固定定位，不再随着鼠标的滚动而滚动。

##### 定位的left和margin

比如：left   和 margin-left 两个同时设置，左边距是会相加的。

##### 固定（定位）在版心右边

利用 left   和  margin-left 两个会相加这一特性，如果我们想要一个 固定定位的盒子紧贴版心的右侧，我们就可以设置 left=50%,此时left=网页的一半。此时盒子就在可视窗口的中间右侧，再设置 margin-left=版心宽度的一半，此时固定的盒子就是紧贴版心的右侧。

##### 绝对定位的盒子居中

使用 margin= auto 不能实现绝对定位的盒子在父级中居中，假如我们需要设置一个绝对定位的盒子水平居中，先设置 left=50%,再向左移一个自身宽度的一半，margin-left= **-**自身宽度的一半。

***为什么不直接设置准确值？？直接设置当你改变窗体大小的时候就不一样了***

##### 定位对显示模式的影响

1. 行内元素使用定位后，就可以直接设置 宽 高了
2. 块级元素使用定位后，如果没有设置宽高，宽高默认是里面的内容

##### 叠放次序 **z-index**

当定位的盒子重叠时，我们需要指定哪个盒子的优先级高。

**z-index**=数值**

数值越大，越在上面，越不容易被覆盖。

### 显示与隐藏

##### display

隐藏：display=none   显示：display=block

特点：隐藏后，元素不会占着原来的位置

##### **visibility**

- visible： 设置对象可视 
- hidden： 设置对象隐藏 
- collapse： 主要用来隐藏表格的行或列。隐藏的行或列能够被其他内容使用。对于表格外的其他对象，其作用等同于hidden

特点：隐藏后的元素会占着原来位置

### 精灵图和字体图标

#### 精灵图

##### **为什么要使用精灵图？**

精灵图一般用于设置背景图片，把很多小图片放在一张大图片上，可以减少服务器的请求，提高网页的加载速度。

##### **精灵图的原理：**

通过 background-position 来控制显示精灵图的哪一部分，一般先精确量出 你所想要使用的部分大小，再设置 精灵图的偏移量。

##### **精灵图的弊端：**

图片的总的来说还是很大，而且精灵图一旦制作完成，就不能修改样式，除非 让UI设计师重新设计。因此一些能够使用字体图标完成的图标，我们一般都选择使用字体库完成，一些复杂的背景才考虑使用精灵图。

#### 字体库

##### **字体图标的优点**

字体图标 其实就是长得像图标的文字，体积小，而且可以通过代码修改样式，使用简单。

##### **常用的字体图标网站**

[国外的一个字体图标网站](https://icomoon.io/) 图标很丰富，但是太慢了，毕竟是国外的服务器。

[阿里巴巴矢量图标库](https://www.iconfont.cn/)  说起这个我就气，以前一直把这个当作下载 透明图片用了，没想到人家是字体。虽然也可以直接下载图片用。

##### **使用字体图标**

阿里巴巴矢量图标库，提供了三种使用的方式

Unicode、 fontclass 、symbol

1. Unicode 引用

下载好字体图标文件后，会得到 一个文件夹，里面有5 个字体图标文件 .ttf .eot .woff .woff2 .svg ,因为浏览器支持的字体文件不同，所以这几个字体文件都需要放进项目中。还有一个 html文件，打开看看示例。

```css
/* url要改成 字体文件的存放位置 */
@font-face {
		  font-family: 'iconfont';
		  src: url('fonts/iconfont.eot');
		  src: url('fonts/iconfont.eot?#iefix') format('embedded-opentype'),
		      url('fonts/iconfont.woff2') format('woff2'),
		      url('fonts/iconfont.woff') format('woff'),
		      url('fonts/iconfont.ttf') format('truetype'),
		      url('fonts/iconfont.svg#iconfont') format('svg');
		}
/*  这是定义字体的样式，引用字体的 span 中需要写上这个类，里面只有  font-family 是必须的，指定了文字的字体，这个字体必须是上面写@font-face的那个font-family,其他样式，如 颜色、大小，另自行定义。*/		.iconfont {
		  font-family: "iconfont" !important;
		  font-style: normal;
		  -webkit-font-smoothing: antialiased;
		  -moz-osx-font-smoothing: grayscale;
		}

<!--
&#xe504;是字体对应的unicode编码，打开下载的文件夹，里面有一个 html文件，里面有字体示例及字体对应的编码  -->
<span class="iconfont">&#xe504;</span>

```

2. fontclass引用:把文件夹中的五个字体文件和 iconfonts.css 文件放入项目中

```csss
1、引入字体的类样式文件 iconfonts.css （注意 5个字体文件和 iconfonts.css  应该在同一个文件夹下）
<link rel="stylesheet" href="./fonts/iconfont.css">

2、在元素中使用 类 添加对应的字体 iconfont 是指定字体的class，必须要有，后面的类名对应哪个字体，打开示例有 字体示例及对应的类名
<span class="iconfont icon-bird "></span>
```

3. symbol引用：这种引用方式，支持多色字体，上面两种引入方式只支持纯色字体。

 第一步：引入项目下面生成的 symbol 代码：

```html
<script src="./iconfont.js"></script>
```

 第二步：加入通用 CSS 代码（引入一次就行）：

```html
<style>
.icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
```

 第三步：挑选相应图标并获取类名，应用于页面：

```html
<svg class="icon" aria-hidden="true">
  <use xlink:href="#icon-xxx"></use>
</svg>
```

##### 添加新的字体进入文件

如果我们已经下载好了网站生成的字体文件，邮箱添加新的字体图标。那我们就可以看到 下好文件夹中 有一个 json文件，显然这个文件 记录了我们字体文件中添加了哪些字体图标。但是我也不知道有什么用。

#### 三角形

```html
.sanjiao{/* 本质是一个没有身体只有边框的div 最后的三角形也就是 其中一条边 */
		width: 0;
		height: 0;
		/* 边框大小决定三角形的大小，让4个边框的颜色都是透明的 */
		border: solid 50px transparent;
		/* 重新设置让想要方向的边框显示出来 */
		border-top-color: pink;
		}

<div class="sanjiao"></div>

```

----

### 用户界面样式

#### 鼠标样式

**cursor**：| context-menu | help | pointer | progress | wait | cell | crosshair | text |  vertical-text | alias | copy | move | no-drop | not-allowed | e-resize |  n-resize | ne-resize | nw-resize | s-resize | se-resize | sw-resize | w-resize |  ew-resize | ns-resize | nesw-resize | nwse-resize | col-resize | row-resize |  all-scroll | zoom-in | zoom-out | grab | grabbing

😂太多了只有你想不到，没有她没做到。什么小手啊，转圈圈得等待，禁止，边缘拉宽的箭头...

#### 取消表单外轮廓

pink老师说外轮廓不好看，我就的还行。外轮廓就是表单元素获取焦点后会有一个蓝色的边框。

outline:none

#### 取消文本域的放大

文本域默认可以被用户伸缩放大，但是这样会影响页面布局，一般都禁止这个操作。

resize：none

#### 图片与文字的对齐方式

想要实现一个div中 图片和文字都垂直居中，就需要使用这个属性，光使用  line-height: height;方式已经不起作用了，连文字都不垂直居中。我们还需要给图片设置 vertical-align: middle;

不仅仅针对于图片与文字的垂直居中，其他行内元素 、行内块元素都可以这样设置。当然块级元素可以转换成行内或者行内块元素。

```html
.cd{
			width: 200px;
			height: 60px;
			line-height: 60px;
			background-color: pink;
			cursor: wait;
		}
		img{
			vertical-align: middle;
		}
<div class="cd"> 
	<img src="img/kefu_03.png"/>对齐对齐
</div>
```

<img src="C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1592195831138.png" alt="1592195831138" style="zoom:50%;" />

默认对齐方式为 基线对齐，所以当div不指定宽度时，底部会有一个空隙，我们需要指定 对齐方式为底线，就不会有空隙了。

vertical-align的取值：

baseline：  基线对齐；

sub：  下标显示；

super：  上标显示；

top：   顶端对齐；

text-top：  文本的顶端对齐；

middle：  中部对齐；  *//没有研究透的属性*

bottom：  底端对齐；

text-bottom：  文本的底端对齐；

##### 图解-基线、底线、中线

![1592200929650](C:\Users\xiamin\AppData\Roaming\Typora\typora-user-images\1592200929650.png)

----

#### 溢出文本 ... 代替

##### 单行文本溢出

```css
/* 强制文字一行显示 */
white-space: nowrap;
/* 溢出隐藏 */
overflow: hidden;
/* 后面显示 ... */
text-overflow: ellipsis;
```

##### 多行文本溢出

兼容性太差了，一般webkit浏览器才支持。所以，这个效果让后台去做吧。

```css
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
	/*控制显示的行数 */
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
```

-----

# h5新标签

#### 视频标签 video

##### 基本使用：

src就是视频文件的路径，可以直接写在标签中，但是浏览器支持的文件格式不一样，你可能需要准备几个不同格式的视频文件，那么你就可以在 标签内部 添加 source 标签，代表文件的路径，如果第一个文件格式不支持，就会查看下一种格式。不过，mp4格式大多数主流浏览器都支持。

```html
<video width="320" height="240" src="./vdeo/hp.mp4">
	  <source src="./vdeo/hp.mp4" type="video/mp4" />
	  <source src="./vdeo/hp.ogg" type="video/ogg" />
	  <source src="./vdeo/hp.webm" type="video/webm" />
</video>
```

##### 常用属性：

- [ ] | **controls** | **true \| false** | **如果是 true，则向用户显示控件，比如播放按钮。**            |
  | ------------ | ----------------- | ------------------------------------------------------------ |
  | end          | *numeric value*   | 定义播放器在视频流中的何处停止播放。默认地，声音会播放到结尾。 |
  | height       | *pixels*          | 设置视频播放器的高度。                                       |
  | loopend      | *numeric value*   | 定义在视频流中循环播放停止的位置，默认是 end 属性的值。      |
  | loopstart    | *numeric value*   | 定义在视频流中循环播放的开始位置。默认是 start 属性的值      |
  | playcount    | *numeric value*   | 定义视频片段播放多少次。默认是 1。                           |
  | loop         | true\|false       | 定义是否循环播放                                             |
  | poster       | *url*             | 在视频播放之前所显示的图片的 URL。                           |
  | src          | *url*             | 要播放的视频的 URL。                                         |
  | start        | *numeric value*   | 定义播放器在音频流中开始播放的位置。默认地，声音在开头进行播放。 |
  | autoplay     | true \| false     | 如果是 true，则视频在就绪后马上播放。                        |
  | preload      | true \|false      | 是否预加载                                                   |
  | muted        | true \| false     | 是否静音                                                     |

谷歌浏览器禁用了自动播放选项，但是配合静音播放可以实现自动播放。

##### video相关的方法：

- Media.error; //null:正常
- Media.error.code; //1.用户终止 2.网络错误 3.解码错误 4.URL无效

***//网络状态 ***

- Media.currentSrc; //返回当前资源的URL
- Media.src = value; //返回或设置当前资源的URL
- Media.canPlayType(type); //是否能播放某种格式的资源
- Media.networkState; //0.此元素未初始化 1.正常但没有使用网络 2.正在下载数据 3.没有找到资源
- Media.load(); //重新加载src指定的资源
- Media.buffered; //返回已缓冲区域，TimeRanges
- Media.preload; //none:不预载 metadata:预载资源信息 auto:

**准备状态 **

- Media.readyState;//1:HAVE_NOTHING 2:HAVE_METADATA 3.HAVE_CURRENT_DATA 4.HAVE_FUTURE_DATA 5.HAVE_ENOUGH_DATA
- Media.seeking; //是否正在seeking

**回放状态 **

- Media.currentTime = value; //当前播放的位置，赋值可改变位置
- Media.startTime; //一般为0，如果为流媒体或者不从0开始的资源，则不为0
- Media.duration; //当前资源长度 流返回无限
- Media.paused; //是否暂停
- Media.defaultPlaybackRate = value;//默认的回放速度，可以设置
- Media.playbackRate = value;//当前播放速度，设置后马上改变
- Media.played; //返回已经播放的区域，TimeRanges，关于此对象见下文
- Media.seekable; //返回可以seek的区域 TimeRanges
- Media.ended; //是否结束
- Media.autoPlay; //是否自动播放
- Media.loop; //是否循环播放
- Media.play(); //播放
- Media.pause(); //暂停

**视频控制 **

- Media.controls;//是否有默认控制条

- Media.volume = value; //音量

- Media.muted = value; //静音

   **TimeRanges(区域)对象  **

- TimeRanges.length; //区域段数

- TimeRanges.start(index) //第index段区域的开始位置

- TimeRanges.end(index) //第index段区域的结束位置

##### 常用的事件：

eventTester = function(e){
    Media.addEventListener(e,function(){
      console.log((newDate()).getTime(),e);
    });
  }

  eventTester("loadstart");  //客户端开始请求数据
  eventTester("progress");  //客户端正在请求数据
  eventTester("suspend");   //延迟下载
  eventTester("abort");    //客户端主动终止下载（不是因为错误引起）
  eventTester("error");    //请求数据时遇到错误
  eventTester("stalled");   //网速失速
  eventTester("play");    //play()和autoplay开始播放时触发
  eventTester("pause");    //pause()触发
  eventTester("loadedmetadata"); //成功获取资源长度
  eventTester("loadeddata"); //
  eventTester("waiting");   //等待数据，并非错误 
  eventTester("playing");   //开始回放
  eventTester("canplay");   //可以播放，但中途可能因为加载而暂停
  eventTester("canplaythrough"); //可以播放，歌曲全部加载完毕
  eventTester("seeking");   //寻找中
  eventTester("seeked");   //寻找完毕
  eventTester("timeupdate"); //播放时间改变
  eventTester("ended");    //播放结束 
  eventTester("ratechange"); //播放速率改变
  eventTester("durationchange"); //资源长度改变  eventTester("volumechange");  //音量改变

#### 音频标签 audio

##### 基本使用

可以直接把路径写在标签上，考虑兼容问题可以准备多个格式的音频文件，写在 source标签中

```html
<audio id="a1">
			<source src="songs/Young%20And%20Beautiful.mp3" type="audio/mp3" />
			<source src="song.ogg" type="audio/ogg" />
			<embed height="100" width="100" src="songs/Young%20And%20Beautiful.mp3" />
</audio>
```

##### 常用属性

| [autoplay](https://www.w3school.com.cn/tags/att_audio_autoplay.asp) | autoplay | 如果出现该属性，则音频在就绪后马上播放。                     |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| [controls](https://www.w3school.com.cn/tags/att_audio_controls.asp) | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| [loop](https://www.w3school.com.cn/tags/att_audio_loop.asp)  | loop     | 如果出现该属性，则每当音频结束时重新开始播放。               |
| [muted](https://www.w3school.com.cn/tags/att_audio_muted.asp) | muted    | 规定视频输出应该被静音。                                     |
| [preload](https://www.w3school.com.cn/tags/att_audio_preload.asp) | preload  | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| [src](https://www.w3school.com.cn/tags/att_audio_src.asp)    | *url*    | 要播放的音频的 URL。                                         |

##### 方法和事件

video和audio都属于多媒体元素，事件和方法都一样有。

----

#### 输入框 input

##### 新增类型

h5给input新增了很多类型，很方便我们进行校验用户的输入是否符合规范

```text
button   		定义可点击的按钮（大多与 JavaScript 使用来启动脚本）
checkbox 	 	定义复选框。
color   		定义拾色器。
date   			定义日期字段（带有 calendar 控件）
datetime 		定义日期字段（带有 calendar 和 time 控件）
datetime-local  定义日期字段（带有 calendar 和 time 控件）
month   		定义日期字段的月（带有 calendar 控件）
week    		定义日期字段的周（带有 calendar 控件）
time    		定义日期字段的时、分、秒（带有 time 控件）
email   		定义用于 e-mail 地址的文本字段
file    		定义输入字段和 "浏览..." 按钮，供文件上传
hidden  		定义隐藏输入字段
image  			定义图像作为提交按钮
number  		定义带有 spinner 控件的数字字段
password  		定义密码字段。字段中的字符会被遮蔽。
radio  			定义单选按钮。
range  			定义带有 slider 控件的数字字段。
reset  			定义重置按钮。重置按钮会将所有表单字段重置为初始值。
search 			定义用于搜索的文本字段。
submit 			定义提交按钮。提交按钮向服务器发送数据。
tel  			定义用于电话号码的文本字段。
text  			默认。定义单行输入字段，用户可在其中输入文本。默认是 20 个字符。
url  			定义用于 URL 的文本字段。
```

##### 新增属性

**1.** **placeholder**

placeholder 属性提供可描述输入字段预期值的提示信息（hint）。该提示会在输入字段为空时显示，并会在字段获得焦点时消失。

placeholder 属性适用于以下的 <input> 类型：text, search, url, telephone, email 以及 password。

与value的区别就是用户输入字的时候，value需要删除默认的字，如下面的"请输入关键词"，而placeholder 不需要，像背景，并且颜色也浅一点

```
1  <input type="search" name="" id="" value="请输入关键词"><br><br>
2  <input type="search" name="" id="" placeholder="请输入关键词">
```

**2.autofocus**

当载入页面时，光标焦点会自动定在文本框内，默认是没有光标焦点的，需要鼠标点击才会有

```
自动获取光标焦点<input type="text" name="" id="" autofocus>
```

![img](https://img2018.cnblogs.com/blog/1543474/201907/1543474-20190705171317110-1881055021.png)

 **3.multiple**

multiple 属性规定输入字段可选择多个值。如果使用该属性，则字段可接受多个值。

multiple 属性使用欧冠与以下 <input> 类型：email 和 file。

文件上传可以一次上传多个文件，默认是只能一次选择上传一个

```
多文件上传<input type="file" name="" id="" multiple>
```

![img](https://img2018.cnblogs.com/blog/1543474/201907/1543474-20190705171431623-536168486.png)

 **4.autocomplete（了解**）

属性规定输入字段是否应该启用自动完成功能。

元素必须有 name 属性，且成功提交过表单，才会自动补全

注释：autocomplete 属性适用于 <form>，以及下面的 <input>  类型：text, search, url, telephone, email, password, datepickers, range 以及  color。

**5.accesskey**

使用快捷键让元素获得焦点。注释：以下元素支持 accesskey 属性：<a>,  <area>, <button>, <input>, <label>,  <legend> 以及 <textarea>。

几乎所有浏览器均 accesskey 属性，除了 Opera

```
快捷键 是 Alt + accesskey。mac中是 CTRL + Alt + accesskey
<a href="http://www.w3school.com.cn/" accesskey="w">W3School</a><br />
<a href="http://www.google.com/" accesskey="g">Google</a>
```

**6.required**

规定该输入框不能为空

------

# css3新特性

#### 伪对象选择器

通过css代码创建一个 html标签
●before和after创建一个元素 ,但是属于**行内元素**
●新创建的这个元素在文档树中是找不到的,所以我们称为伪元素
●语法: element::before {}
●before和after必须有content属性
●before在父元素内容的前面创建元素, after 在父元素内容的后面插入元素
●伪元素选择器和标签选择器一样,权重为1

```css
这是使用 伪元素清除浮动的代码，里面的代码 只有 content 是必须的，content就是伪元素里面的内容，即使是空也需要写上去，伪对象就是只能做大儿子或者小儿子元素，说到底就是一个元素，该怎么操作就怎么操作。
.clearfix:after{
    content:"";				/*设置内容为空*/
    height:0;				/*高度为0*/
    line-height:0;			/*行高为0*/
    display:block;			/*将文本转为块级元素*/
    visibility:hidden;		/*将元素隐藏*/
    clear:both;				/*清除浮动*/
}
.clearfix{
    zoom:1;					/*为了兼容IE*/
}
类名或者id都行，只要是 通过 :after 添加了这些属性就可以,其实也就是相当于第一种方法，只是 通过css添加元素罢了。
```

#### 盒子模型

语法：**box-sizing**：content-box | border-box

以前我们给一个 块级元素设置了width 又设置了 boder 和 padding时，此时盒子的宽度会等于三者之和。如果我们想盒子的宽度就等于 width，那我们可以设置**box-sizing**： border-box，前提是 padding +boder < width

 取值：

- content-box： 

  padding和border不被包含在定义的width和height之内。对象的实际宽度等于设置的width值和border、padding之和，即 (  Element width = width + border + padding ) 

  此属性表现为标准模式下的盒模型。 

- border-box： 

  padding和border被包含在定义的width和height之内。对象的实际宽度就等于设置的width值，即使定义有border和padding也不会改变对象的实际宽度，即  ( Element width = width ) 

  此属性表现为怪异模式下的盒模型。 

#### filter 过滤器

语法

**filter**: none | blur() | brightness() | contrast() | drop-shadow() | grayscale() | hue-rotate() | invert() | opacity() | saturate() | sepia() | url();

要使用的滤镜效果。多个滤镜之间用空格隔开

##### 图片模糊处理函数

天！梦寐以求的效果终于学到了，终于等到你，还好我没放弃！

语法：filter：blur(10px) 括号里的数值越大，越模糊，用这个就能取出一张图片的主题色，qq音乐的的背景就是这样的。

##### 其他函数

| none                                               | 默认值，没有效果。                                           |
| -------------------------------------------------- | ------------------------------------------------------------ |
| blur(*px*)                                         | 给图像设置高斯模糊。"radius"一值设定高斯函数的标准差，或者是屏幕上以多少像素融在一起， 所以值越大越模糊；  如果没有设定值，则默认是0；这个参数可设置css长度值，但不接受百分比值。 |
| brightness(*%*)                                    | 给图片应用一种线性乘法，使其看起来更亮或更暗。如果值是0%，图像会全黑。值是100%，则图像无变化。其他的值对应线性乘数效果。值超过100%也是可以的，图像会比原来更亮。如果没有设定值，默认是1。 |
| contrast(*%*)                                      | 调整图像的对比度。值是0%的话，图像会全黑。值是100%，图像不变。值可以超过100%，意味着会运用更低的对比。若没有设置值，默认是1。 |
| drop-shadow(*h-shadow v-shadow blur spread color*) | 给图像设置一个阴影效果。阴影是合成在图像下面，可以有模糊度的，可以以特定颜色画出的遮罩图的偏移版本。 函数接受<shadow>(在CSS3背景中定义)类型的值，除了"inset"关键字是不允许的。该函数与已有的box-shadow  box-shadow属性很相似；不同之处在于，通过滤镜，一些浏览器为了更好的性能会提供硬件加速。`参数如下：``  **** **** (必须) 这是设置阴影偏移量的两个 值. **** 设定水平方向距离. 负值会使阴影出现在元素左边. ****设定垂直距离.负值会使阴影出现在元素上方。查看****可能的单位. **如果两个值都是0**, 则阴影出现在元素正后面 (如果设置了 and/or ，会有模糊效果). **** (可选) 这是第三个code>值. 值越大，越模糊，则阴影会变得更大更淡.不允许负值 若未设定，默认是0 (则阴影的边界很锐利). **** (可选) 这是第四个 值. 正值会使阴影扩张和变大，负值会是阴影缩小.若未设定，默认是0 (阴影会与元素一样大小). 注意: Webkit, 以及一些其他浏览器 不支持第四个长度，如果加了也不会渲染。  **** (可选) 查看 该值可能的关键字和标记。若未设定，颜色值基于浏览器。在Gecko (Firefox), Presto (Opera)和Trident (Internet Explorer)中， 会应用color**color**属性的值。另外, 如果颜色值省略，WebKit中阴影是透明的。  ` |
| grayscale(*%*)                                     | 将图像转换为灰度图像。值定义转换的比例。值为100%则完全转为灰度图像，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0； |
| hue-rotate(*deg*)                                  | 给图像应用色相旋转。"angle"一值设定图像会被调整的色环角度值。值为0deg，则图像无变化。若值未设置，默认值是0deg。该值虽然没有最大值，超过360deg的值相当于又绕一圈。 |
| invert(*%*)                                        | 反转输入图像。值定义转换的比例。100%的价值是完全反转。值为0%则图像无变化。值在0%和100%之间，则是效果的线性乘子。 若值未设置，值默认是0。 |
| opacity(*%*)                                       | 转化图像的透明程度。值定义转换的比例。值为0%则是完全透明，值为100%则图像无变化。值在0%和100%之间，则是效果的线性乘子，也相当于图像样本乘以数量。 若值未设置，值默认是1。该函数与已有的opacity属性很相似，不同之处在于通过filter，一些浏览器为了提升性能会提供硬件加速。 |
| saturate(*%*)                                      | 转换图像饱和度。值定义转换的比例。值为0%则是完全不饱和，值为100%则图像无变化。其他值，则是效果的线性乘子。超过100%的值是允许的，则有更高的饱和度。 若值未设置，值默认是1。 |
| sepia(*%*)                                         | 将图像转换为深褐色。值定义转换的比例。值为100%则完全是深褐色的，值为0%图像无变化。值在0%到100%之间，则是效果的线性乘子。若未设置，值默认是0； |
| url()                                              | URL函数接受一个XML文件，该文件设置了 一个SVG滤镜，且可以包含一个锚点来指定一个具体的滤镜元素。 例如： `filter: url(svg-url#element-id)` |
| initial                                            | 设置属性为默认值，可参阅： [CSS initial 关键字](https://www.runoob.com/cssref/css-initial.html) |
| inherit                                            | 从父元素继承该属性，可参阅：[CSS inherit 关键字](https://www.runoob.com/cssref/css-inherit.html) |

-----

#### 计算盒子大小

calc()函数

**用于动态计算长度值。**

- 需要注意的是，运算符前后都需要保留一个空格，例如：`width:  calc(100% - 10px)`；  
- 任何长度值都可以使用calc()函数进行计算；  
- calc()函数支持 "+", "-", "*", "/" 运算；  
- calc()函数使用标准的数学运算优先级规则； 

----

#### 过渡效果

语法：transition:< transition-property >< transition-duration >< transition-timing-function >< transition-delay >

| **transition-property**        | 指定CSS属性的name 如果所有属性都需要可以写 all，多个属性分开写，逗号隔开 |
| ------------------------------ | ------------------------------------------------------------ |
| **transition-duration**        | **transition效果需要指定多少秒或毫秒才能完成**               |
| **transition-timing-function** | **指定transition效果的转速曲线**  可以省略，默认 ease逐渐慢下来，还可以有设置为linear 匀速 |
| **transition-delay**           | **定义transition效果延迟时间** 默认0s,立即开始               |

##### 哪些属性支持过渡效果

宽、高、透明度、**transform**、

----

#### 网站SEO

SEO- 利用[搜索引擎](https://baike.baidu.com/item/搜索引擎/104812)的规则提高[网站](https://baike.baidu.com/item/网站/155722)在有关搜索引擎内的[自然排名](https://baike.baidu.com/item/自然排名/2092669)。目的是让其在行业内占据领先地位，获得[品牌](https://baike.baidu.com/item/品牌/235720)收益。很大程度上是网站经营者的一种商业行为，将自己或自己公司的排名前移。 

怎么优化？三大标签很关键 title  、description、keywords

##### **title**:

建议 网站名称+ 网站描述  30字左右

##### **description**

简要说明我们网站主要是做什么的。我们提倡, description作为网站的总体业务和主题概括,多采用“我们...”.“我们提供..”、 "xxx网作为..”、“电话 : 0..之类语句。
例如:

```html
<meta name="description" content="京东JD.COM-专业的综合网上购物商城销售家电、数码通讯、电脑、
家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务,为您提供愉悦的网上购物
体验!" />
```

##### keywords:

四到六个关键词

```html
<meta name="keywords" content="京东JD.COM-专业的综合网上购物商城销售家电、数码通讯、电脑、
家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务,为您提供愉悦的网上购物
体验!" />
```

##### logo

1. logo里面首先放-个h1标签,目的是为了提权,告诉搜索引擎,这个地方很重要。
2. h1 里面再放一一个链接,可以返回首页的,把logo的背景图片给链接即可。
3. 为了搜索引擎收录我们,我们链接里面要放文字(网站名称) ,但是文字不要显示出来。
    ●方法1 : text-indent移到盒子外面( text -indent: -9999px) , 然后overflow:hidden , 淘宝的做法。
    ●方法2 :直接给font-size:0;就看不到文字了,京东的做法。
4. 最后给链接-个title属性,这样鼠标放到logo上就可以看到提示文字了。

#### 2D转换——transform

转换可以实现的效果： 移动 旋转 缩放 等效果

##### 二维移动

语法：**transform**：**translate(100px,100px)** | **translateX(100px)** | **translateY(100px)**

+ 定义2D转换中的移动,沿着X和Y轴移动元素
+ translate最大的优点:不会影响到其他元素的位置
+ translate中的百分比单位是相对于**自身元素**的translate:(50%,50%);像其他的 top left 的百分比都是父亲的
+ 对行内标签没有效果

##### 二维旋转

语法：**transform**：**rotate(90deg)** 顺时针旋转 90°，逆时针用负值表示

##### 缩放

语法：**transform**：**scale(x,y)**  | **scaleX()**  | **scaleY()** 

参数：x 和 y 代表宽度和高度的放大缩小的倍数，如果两个缩放的倍数一样可以只写一个。

优点还是不会挤压其他元素，只会覆盖。

##### 设置转换的中心点

默认是围绕元素的中心点进行转换，我们也可以自己设置转换的中心点。注意，不单单是旋转的中心点。但是吧，对于移动来说，中心点在哪都一样。

语法：**transform-origin: x y** ，默认值 50% 50%

取值：

- 百分比： 用百分比指定坐标值。可以为负值。 百分比相对于自身
- 像素值： 用长度值指定坐标值。可以为负值。 
- left： 指定原点的横坐标为left 
- center： 指定原点的横 / 纵坐标为center 
- right： 指定原点的横坐标为right 
- top： 指定原点的纵坐标为top 
- bottom： 指定原点的纵坐标为bottom 

参数个数：

- 该属性提供2个参数值。  
- 如果提供两个，第一个用于横坐标，第二个用于纵坐标。  
- 如果只提供一个，该值将用于横坐标；纵坐标将默认为50%。 

##### 转换顺序

其他的顺序不重要，但是 **移动** 一定得先做！！！

#### 动画

动画的基本使用

##### 定义动画

Keyframes--动画序列定义动画

```css
@keyframes move{
    from{
        开始样式
    }
    to{
        完成时样式
    }
}
或者
@keyframes move{
    0%{
        开始样式
    }
    100%{
        完成样式
    }
}
多个过程的动画
@keyframes move{
    /* 百分比不仅仅代表一个过程，两者之间的差值还代表该过程占用总时间的百分之几 */
    0%{}
    25%{}
    75%{}
    100%{}
}
```

+ 0% |  from是动画的开始, 100% | to 是动画的完成。这样的规则就是动画序列。如果一开始的状态就是元素本身的状态，就可以不写 0%.
+ 在@keyframes中规定某项CSS样式,就能创建由当前样式逐渐改为新样式的动画效果。
+ 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变任意的样式任意多的次数。
+ 请用百分比来规定变化发生的时间,或用关键词"from"和"to" ,等同于0%和100%。

##### 调用动画

```html
div{
    /* 调用动画的名称 */
    animation-name: move;
    /* 动画持续时间 */
    animation-duration: 3s;
}
```

多个动画需要使用 动画的连写  **animation**： 属性用空格隔开，动画用 逗号隔开  

##### 动画属性

- animation-name： 检索或设置对象所应用的动画名称 

- animation-duration： 检索或设置对象动画的持续时间  默认 0S

- animation-timing-function： 检索或设置对象动画的过渡类型  默认 即越来越慢

- animation-delay： 检索或设置对象动画延迟的时间  默认 0S

- animation-iteration-count： 检索或设置对象动画的循环次数  **infinite** 代表无限循环

- animation-direction： 检索或设置对象动画在循环中是否反向运动 

- animation-fill-mode： 检索或设置对象动画时间结束之后的状态 ，默认值 **backwards**--返回元素的起始状态，并不是0%的状态，就是元素本身的状态。 **forwords** --结束后保持 100%状态

- animation-play-state：  检索或设置对象动画的状态。默认是 **runing**，所以动画是自动执行,**paused**就是暂停状态，w3c正考虑是否将该属性移除，因为动画的状态可以通过其它的方式实现，比如重设样式  


#####  运动曲线

![](C:\Users\xiamin\Desktop\运动曲现.png)

注意一下最后一个 **steps(num)** 表示这个过程用 几步来完成，每一步之间没有过渡效果，蛮有意思的

#### 3D转换

##### 三维坐标系

x轴:水平向右注意: x右边是正值,左边是负值
y轴:垂直向下注意: y下面是正值，上面是负值
z轴:垂直屏幕注意:往外面是正值,往里面是负值

##### 3D移动

语法：**transform**：**translate3d(100px,100px,100px)** | **translateX(100px)** | **translateY(100px)** |**translateZ(100px)**

三个一起写的时候不能省略某一个，没有就写 0. 记住覆盖问题，translateX 、translateY 都是同一个属性，会覆盖的，不能分开写。

**translateZ(100px)**:改变的是元素在z轴上的距离。

##### 透视 perspective

在2D平面产生近大远小视觉立体,但是只是效果二维的
 ● 如果想要在网页产生3D效果需要透视(理解成3D物体投影在2D平面内)。
 ● 模拟人类的视觉位置,可认为安排-只眼睛去看
 ● **透视我们也称为视距:视距就是人的眼睛到屏幕的距离**
 ● 距离视觉点越近的在电脑平面成像越大,越远成像越小
 ● 透视的单位是像素

**透视写在被观察元素的父盒子上面的**

语法： perspective:200px

**perspective**：**改变的是观察者的视距，就是眼睛到屏幕的距离**

##### 3D旋转

语法：

transform:rotateX(45deg) :	沿着x轴正方向旋转45度
transform:rotateY(45deg) :	沿着y轴正方向旋转45deg
transform:rotateZ(45deg) : 	沿着Z轴正方向旋转45deg  😂不就是2D旋转的效果么
transform:rotate3d(x,y,z,deg) :	沿着自定义轴旋转deg为角度(了解即可) （x,y,z）形成的是一个矢量方向，就是把 坐标原点和那个点连起来的那条线。

**左手准则**：伸出你的左手，四指握紧，大拇指指向旋转轴的正方向，其余四指的弯曲的方向就是旋转的方向

##### 3D呈现

控制子元素是否开启三维立体环境。

transform-style:flat | preserve-3d
transform-style: flat	子元素不开启3d立体空间默认的
transform-style: preserve-3d;	子元素开启立体空间

代码写给父级,但是影响的是子盒子这个属性很重要,后面必用

---

#### 浏览器的私有前缀

浏览器私有前缀是为了兼容老版本的写法,比较新版本的浏览器无须添加。
1.私有前缀
	●	-moz- :代表firefox浏览器私有属性
	●	-ms- :代表ie浏览器私有属性
	●	-webkit- :代表safari、chrome 私有属性
	●	-0- :代表Opera私有属性

2、写法

```css
-moz-border-radius: 10px;
-webkit-border-radius: 10px;
-0-border-radius: 10px;
border-radius: 10px;
```

# 移动端布局

### 视口

视口( viewport )就是浏览器页面内容的屏幕区域。视口可以分为布局视口、视觉视口和理想视口

1. 布局视口   layout viewport,等比例缩放网页大小适应移动端
   + 一般移动设备的浏览器都默认设置 了一个布局视口,用于解决早期的PC端页面在手机上显示的问题。
   + iOS, Android基本都将这个视口分辨率设置为980px ,所以PC上的网页大多都能在手机上呈现,不
     过元素看上去很小, -般默认可以通过手动缩放网页。

2. 视觉视口   visual viewport，保持网页原来的大小
   + 字面意思,它是用户正在看到的网站的区域。注意:是网站的区域。
   + 我们可以通过缩放去操作视觉视口,但不会影响布局视口,布局视口仍保持原来的宽度。
3. 理想视口   ideal viewport
   + 为 了使网站在移动端有最理想的浏览和阅读宽度而设定理想视口,对设备来讲,是最理想的视口尺寸
   + 需要手动添写meta视口标签通知浏览器操作
   + **meta视口标签**的主要目的 :布局视口的宽度应该与理想视口的宽度-致,简单理解就是设备有多宽,我
     们布局的视口就多宽

#### meta视口标签

```css
<meta name="viewport" content= "width=device -width, user- sqalable=no,initial-scale=1.0, maximum-scale=1.0, minimum-scale=1. 0">
```

+ width:宽度设置的是viewport宽度,可以设置device-width特殊值
+ initial-scale:初始缩放比,大于0的数字
+ maximum-scale：最大缩放比,大于0的数字
+ minimum-scale：最小缩放比，大于0的数字
+ user-scalable：用户是否可以缩放, yes或no ( 1或0 )

### 多倍图

#### 物理像素&物理像素比

+ 物理像素点指的是屏 幕显示的最小颗粒,是物理真实存在的。这是厂商在出厂时就设置好了,比如苹果6\7\8是750* 1334
+ 我们开发时候的1px不是一定等于1个物理像素
+ pc端 1个px等于1个物理像素的,但是移动端就不尽相
+ 一个px的能显示的物理像素点的个数,称为物理像素比或屏幕像素比
+ PC端和早前的手机屏幕/普通手机屏幕: 1CSS像素= 1物理像素的
+ Retina (视网膜屏幕)是一种显示技术,可以将把更多的物理像素点压缩至一块屏幕里,从而达到更高的分辨率,并提高屏幕显示的细腻程度。

#### 处理图片失真

在视网膜屏幕中，网页会被类似放大，比如iphone8是2倍的进行放大，字体是矢量的，放大不会失真。但是图片放大会失真，所以如果我们需要一个50px大小的图片，我们应该把 100px大小的图片设置为 50px ,放在网页中，在手机端被放大两倍，也不会失真。 同样的背景图片也会面临相同的问题，我们也应该需要实际大小的两倍的图片，再缩放为实际大小。

#### 二倍精灵图的做法

+ 在firework里面把精灵图等比例缩放为原来的一半
+ 之后根据大小测量坐标
+ 注意代码里面background-size也要写 :精灵图原来宽度的一半

### 移动端的选择

#### 单独制作移动端的页面 (主流)

+ 流式布局( 百分比布局)
+ flex弹性布局(强烈推荐)
+ less + rem+媒体查询布局
+ 混合布局

#### 使用响应式布局

+ 媒体查询
+ 媒体查询

### 移动端技术解决方案

#### 兼容

移动端的兼容主要是兼容web-kit内核的浏览器

#### CSS初始化

移动端CSS初始化推荐使用normalize.css/
●Normalize.css :保护了有价值的默认值
●Normalize.css :修复了浏览器的bug
●Normalize.css :是模块化的
●Normalize.css :拥有详细的文档
官网地址: http://necolas.github.io/normalize.css/

#### 特殊样式

```css
/*CSS3盒子模型*/
box-sizing: border -box;
-webkit -box- si zing: border- -box;
/*点击高亮我们需要清除清除设 置为transparent完成透明*/
-webkit- tap-highlight- -color: transparent;
/*在移动端浏览器默认的外观在ios.上加。上这个属性才能给按钮和输入框自定义样式*/
-webki t- appearance: none;
/★禁用长按页面时的弹出菜单*/
img,a { -webkit- touch-callout: none; }
```

### 流式布局

流式布局也叫做百分比布局，通过百分比来规定元素的宽高（这个我熟），以适应屏幕大小的不同，同时可以设置宽高的最大、最小值。

最大宽高：**max-width/height**

最小宽高：**min-width/height**

### 图片格式

1、DPG图片压缩技术京东自主研发推出DPG图片压缩技术，经测试该技术，可直接节省用户近50%的浏览流量，极大的提升了用户的网页打开速度。能够兼容jpeg，实现全平台、全部浏览器的兼容支持，经过内部和外部上万张图片的人眼浏览测试后发现，压缩后的图片和webp的清晰度对比没有差距。

2、webp图片格式
谷歌开发的一种旨在加快图片加载速度的图片格式。图片压缩体积大约只有JPEG的2/3，并能节省大量的服务器宽带资源和数据空间

### flex布局

●操作方便,布局**极为简单**,移动端应用很广泛
●PC端浏览器支持情况较差
●IE 11或更低版本,支持或仅部分支持

#### 布局原理

flex是flexible Box的缩写, 意为"弹性布局" ,用来为盒状模型提供最大的灵活性,任何一个容器都可以指定为flex布局。

+ 当我们为父盒子设为 flex布局以后,元素的float、clear 和vertical align属性将失效。
+ 伸缩布局=弹性布局=伸缩盒布局=弹性盒布局年flex布局

+ 就是通过给父盒子添加flex属性,来控制子盒子的位置和排列方式

#### 父元素属性

+ flex-direction :设置主轴的方向：主轴和侧轴是会变化的,就看flex-direction设置谁为主轴,剩下的就是侧轴。而我们的子元素是跟着主轴来排列的。单个子元素按顺序从排列，即会改变子元素的顺序，比如从右到左排列顺序会变成 4 3 2  1
  + row   默认值，从左到右
  + row-reverse  从右到左
  + column   从上到下
  + column-reverse   从下到上
+ justify-content :设置 **主轴** 上的子元素排列方式，子元素整体排列，顺序不会变，比如从右到左排列顺序还是 1 2 3 4
  + flex-start默认值从头部开始如果主轴是x轴，则从左到右
  + flex-end从尾部开始排列
  + center在主轴居中对齐(如果主轴是x轴则水平居中)
  + space-around平分剩余空间
  + space-between先两边贴边再平分剩余空间(重要)
+ flex-wrap :设置子元素是否换行（如果放不下，会缩小子元素的大小），直到所有的子元素都可以放在主轴
  + nowrap 默认值，不换行
  + wrap：换行
+ align-items :设置 **侧轴** 上的子元素排列方式(单行)
  + flex-start默认值从上到下
  + flex-end从下到上 
  + center挤在一起居中(垂直居中)
  + stretch拉伸
+ align-content :设置 **侧轴** 上的子元素的排列方式（多行=》换行就会出现多行）
  + flex-start		默认值在侧轴的头部开始排列
  + flex-end		在侧轴的尾部开始排列
  + center		在侧轴中间显示
  + space -around		子项在侧轴平分剩余空间
  + space-between		子项在侧轴先分布在两头,再平分剩余空间
  + stretch 		设置子项元素高度平分父元素高度
+ flex-flow :复合属性,相当于同时设置了flex-direction和flex-wrap

#### flex布局子项常见属性

●flex 	子项目占剩余空间的份数（它会把兄弟元素里找到所有的 flex 计算比例），还可以写百分比，表示站父亲的百分之几
●align-self   	控制子项自己在侧轴的排列方式
●order 	属性定义子项的排列顺序(前后顺序) 默认都是0 ，越小越靠前，一样大的话看书写顺序。

### 背景颜色渐变

#### 线性渐变

+ background: linear-gradient (起始方向，颜色1，颜色2，...) ;
  + background: -webkit-linear-gradient(left, red ，blue) ;（移动端需要带浏览器私有前缀，默认方向 top  自上向下渐变）
  + background: -webkit-linear-gradient(left top, red ，blue) ;（左上角到右下脚）
  + 还可以用角度控制渐变方向

### less+rem+媒体查询布局

#### rem

rem是一个单位，rem (root em)是一个相对单位 ,类似于em , em是相对于元素字体的大小。不同的是rem的基准是相对于html元素的字体大小。比如,根元索( html )设置font- size= 12px;非根元素设置width:2rem;则换成px表示就是24px。可以理解为就是一个单位，用来控制元素的大小，作为一个长度标准，只要修改html的字体大小就可以控制 rem的大小，进而控制元素的大小。

#### 媒体查询

媒体查询( Media Query )是CSS3新语法。

+ 使用@media查询,可以针对不同的媒体类型定义不同的样式
+ @media 可以针对不同的屏幕尺寸设置不同的样式
+ 当你重置浏览器大小的过程中,页面也会根据浏览器的宽度和高度重新渲染页面
+ 目前针对很多苹果手机、Android手机 ,平板等设备都用得到多媒体查询

语法：**@media**：媒体类型 and 查询条件 and 查询条件{选择器+css样式编写}

语义：在该媒体类型下，并且查询条件符合的时候，某些标签的样式是怎样的。

##### 媒体类型 Media Types

| 媒体类型   | 版本           | 兼容性              | 描述                                             |
| ---------- | -------------- | ------------------- | ------------------------------------------------ |
| aural      | CSS2不推荐使用 | Opera               | 用于语音和音乐合成器                             |
| braille    | CSS2           | Opera               | 用于触觉反馈设备                                 |
| handheld   | CSS2           | Chrome,Safari,Opera | 用于小型或手持设备                               |
| print      | CSS2           | 所有浏览器          | 用于打印机                                       |
| projection | CSS2           | Opera               | 用于投影图像，如幻灯片                           |
| screen     | CSS2           | 所有浏览器          | 用于计算机显示器                                 |
| tty        | CSS2           | Opera               | 用于使用固定间距字符格的设备。如电传打字机和终端 |
| tv         | CSS2           | Opera               | 用于电视类设备                                   |
| embossed   | CSS2           | Opera               | 用于凸点字符（盲文）印刷设备                     |
| speech     | CSS2           | Opera               | 用于语音类型                                     |
| all        | CSS2           | 所有浏览器          | 用于所有媒体设备类型                             |

##### 查询条件

就是css属性，比如：max-width=300px;

##### 利用媒体资源引用不同的css文件

```css
<link rel=" stylesheet" href=" style320. css" media="screen and (min-width:320px)">
<link rel="stylesheet" href="sty1e640.css" media="screen and ( min-width: 640px)">
```

#### less

CSS是一门非程序式语言,没有变量、函数、SCOPE (作用域)等概念。

+ CSS 需要书写大量看似没有逻辑的代码, CSS冗余度是比较高的。不方便维护及扩展,不利于复用。
+ CSS 没有很好的计算能力
+ 非前端开发工程师来讲,往往会因为缺少CSS编写经验而很难写出组织良好且易于维护的CSS代码项目。

less就是来弥补css的弊端。Less ( Leaner Style Sheets的缩写)是一门CSS扩展语言,也称为CSS预处理器。做为CSS的一种形式的扩展,它并没有减少CSS的功能,而是在现有的CSS语法上,为CSS加入程序式语言的特性。它在CSS的语法基础之上,引入了**变量,** **Mixin(混入)** , **运算**以及**函数**等功能,大大简化了CSS的编写并且降低了CSS的维护成本,就像它的名称所说的那样, Less可以让我们用更少的代码做更多的事情。
Less中文网址: http://lesscss.cn/
常见的CSS预处理器: Sass、Less、 Stylus

安装less之前需要安装node.js

##### less变量

语法：@变量名:值;
变量命名规范

+ 必须有 @为前缀.
+ 不能包含特殊字符
+ 不能以数字开头
+ 大小写敏感

示例：

```less
@color=pink;
body{
backcolor:@color;
}
```

##### less编译

less语法，浏览器不能识别，只能转换成css文件才能识别；

vscode有一个插件 easy less,安装好后，当我们编写并保存一个less文件，会自动帮我们编译成一个同名的css文件。

而使用webpack打包的时候，webpack会自动帮我们打包成css文件。

##### less嵌套

这是less一种比较好的写法，比较直观，不会出现大量重复代码。

```less
body{
    color:red;
    div{//后代选择器的语法
        color:green;
        &:hover{background:black; //伪类选择器的语法
        }
    }
}
```

##### less运算

```less
/* 加减乘除 甚至带括号的运算都可以*/
div{
    width:200px + 20;
}
```

+ 乘号(*)和除号(/ )的写法
+ 运算符中间左右有个空格隔开1px+ 5
+ 对于两个不同的单位的值之间的运算,运算结果的值取第一个值的单位
+ 如果两个值之间只有一个值有单位,则运算结果就取该单位

##### rem适配方案

1.让一些不能等比自适应的元素,达到当设备尺寸发生改变的时候,等比例适配当前设备。
2.使用媒体查询根据不同设备按比例设置html的字体大小，然后页面元素使用rem做尺寸单位,当htmI字体大小变化元尺寸也会发生变化,从而达到等比缩放的适配。

**适配方案的选择**

1. less + media + rem 
   + 通过媒体查询设置不同屏幕宽度，body的宽度、rem(html的字体)不同
   + 所有的元素宽高都使用 rem作为单位，即可实现随着屏幕的改变，元素等比例缩放。
2. flexible.js + rem
   + 原理一样，只是通过js,把 rem 设置成了body的十分之一，即把屏幕分成十等分。不需要自己在css中设置不同宽度不同的 rem,只是还需要自己设置最大宽度、及最大宽度下的rem值，即最大宽度 除以十

##### cssrem插件

这款插件可以实现将像素值转换为 rem,省略了自己书写计算式子，默认 rem=16px,需要自己更改成 最大宽度的rem值。

