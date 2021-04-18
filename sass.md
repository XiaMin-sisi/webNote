# 文件后缀名

Sass 有两种语法格式，两种语法格式对应两种不同的后缀名 sass scss

## .scss

首先是 SCSS (Sassy CSS),这种格式仅在 CSS3  语法的基础上进行拓展，所有 CSS3 语法在 SCSS 中都是通用的，同时加入 Sass 的特色功能。此外，SCSS 也支持大多数 CSS  hacks 写法以及浏览器前缀写法 (vendor-specific syntax)，以及早期的 IE 滤镜写法。这种格式以 **`.scss`** **作为拓展名**。

## .sass

另一种也是最早的 Sass 语法格式，被称为缩进格式 (Indented Sass) 通常简称 "Sass"，是一种简化格式。它使用  “缩进” 代替 “花括号” 表示属性属于某个选择器，用 “换行” 代替 “分号” 分隔属性，很多人认为这样做比 SCSS  更容易阅读，书写也更快速。缩进格式也可以使用 Sass 的全部功能，只是与 SCSS 相比个别地方采取了不同的表达方式，具体请查看 [the indented syntax reference](http://sass-lang.com/docs/yardoc/file.INDENTED_SYNTAX.html)。这种格式以 **`.sass` 作为拓展名。**

# 样式嵌套

**将一套 CSS 样式嵌套进另一套样式中，内层的样式将它外层的选择器作为父选择器**

```scss
.box {
    width:200px;  
    height: 300px;
    background-color:pink;
    
    .smallBox {
        width: 10%;
        height: 10%;
        background-color: green;
        }
}
```

# 父选择器 `&`

**& 代表父元素，或者理解为元素本身,甚至这个符号就是等于父元素的选择器名称**

**`&` 必须作为选择器的第一个字符**

```scss
.box {
    &>span{
        color: orange;
    }
    
    &-child{
        margin: 5%;
        width: 80%;
        height: 15%;
        background-color: cyan;
    }
}

//编译后-------------------------------------------------------------

.box>span{
    color: orange;
}

.box-chid{
     margin: 5%;
     width: 80%;
     height: 15%;
     background-color: cyan;
}
```

# 属性嵌套

**不仅仅样式可以嵌套，有些复合属性，在sass中也是允许嵌套**

```scss
.box {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

# SassScript

**在 CSS 属性的基础上 Sass 提供了一些名为 SassScript 的新功能。 SassScript 可作用于任何属性，允许属性使用变量、算数运算等额外功能。**

**通过 interpolation，SassScript 甚至可以生成选择器或属性名，这一点对编写 mixin 有很大帮助。**

## 变量

### 定义使用变量

**变量以美元符号开头，赋值方法与 CSS 属性的写法一样     **

```scss
$width:300px;
.box {
    width:$width;
    height: 300px;
}
```

### 变量定义 `!default`

可以在变量的结尾添加 `!default` 给一个未通过 `!default` 声明赋值的变量赋值，此时，如果变量已经被赋值，不会再被重新赋值，但是如果变量还没有被赋值，则会被赋予新的值。

```scss
$content: "First content";
$content: "Second content?" !default;
$new_content: "First time reference" !default;

#main {
  content: $content;
  new-content: $new_content;
}
```

编译为

```css
#main {
  content: "First content";
  new-content: "First time reference"; }
```

变量是 null 空值时将视为未被 `!default` 赋值。

### 变量作用域

**变量支持块级作用域。和 js 变量的作用域一样。 局部变量可以通过  !global 转变成全局变量**

```scss
$width:300px;
.box{
	$width:200px;
    width:$width;//width:200px
    height: 300px;
}
```

### 数据类型

SassScript 支持 6 种主要的数据类型：

- 数字	`1, 2, 13, 10px`
- 字符串
  - 有引号字符串 `"foo", 'bar'`
  - 无引号字符串，`baz`
- 颜色，`blue, #04a3f9, rgba(255,0,0,0.5)`
- 布尔型，`true, false`
- 空值，`null`
- 数组 (list)，用空格或逗号作分隔符，`1.5em 1em 0 2em, Helvetica, Arial, sans-serif`
- maps, 相当于 JavaScript 的 object，`(key1: value1, key2: value2)`

SassScript 也支持其他 CSS 属性值，比如 Unicode 字符集，或 `!important` 声明。然而Sass 不会特殊对待这些属性值，一律视为无引号字符串

## 运算

所有数据类型均支持相等运算 `==` 或 `!=`，此外，每种数据类型也有其各自支持的运算方式。

### 插值表达式 #{}

在字符串中使用变量，类似于 ${变量}

```scss
$p:before {
  content: "I ate #{5 + 10} pies!";
}
```

### 数字运算

SassScript 支持数字的加减乘除、取整等运算 (`+, -, *, /, %`)，如果必要会在不同单位间转换值。

#### 除法运算

以下三种情况 `/` 将被视为除法运算符号：

- 如果值，或值的一部分，是变量或者函数的返回值
- 如果值被圆括号包裹
- 如果值是算数表达式的一部分

```scss
p {
  font: 10px/8px;             // Plain CSS, no division
  $width: 1000px;
  width: $width/2;            // 变量
  width: round(1.5)/2;        // 函数返回值
  height: (500px/2);          // 圆括号
  margin-left: 5px + 8px/2px; // 算数表达式的一部分
}
```

如果需要使用变量，同时又要确保 `/` 不做除法运算而是完整地编译到 CSS 文件中，只需要用 `#{}` 插值语句将变量包裹。

```scss
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height;// 12px/30px
  };
```

### 颜色运算

颜色值的运算是分段计算进行的，也就是分别计算红色，绿色，以及蓝色的值.

```scss
p {
  color: #010203 + #040506;//#050709
}
```

### 字符串运算

`+` 可用于连接字符串，（字符串最好写成有引号的，否则有可能会被认为是带单位的数字运算）

```scss
p {
  cursor: e + -resize;//cursor: e-resize;
}
```

如果有引号字符串（位于 `+` 左侧）连接无引号字符串，运算结果是有引号的，相反，无引号字符串（位于 `+` 左侧）连接有引号字符串，运算结果则没有引号。

### 布尔运算

SassScript 支持布尔型的 `and` `or` 以及 `not` 运算。

### 数组运算

数组不支持任何运算方式，只能使用 [list functions](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#list-functions) 控制。

### 函数

SassScript 定义了多种函数，有些甚至可以通过普通的 CSS 语句调用：

# @-Rules 与指令

Sass 支持所有的 CSS3 @-Rules，以及 Sass 特有的 “指令”（directives）。这一节会详细解释，更多资料请查看 [控制指令 (control directives)](https://www.sass.hk/docs/#8) 与 [混合指令 (mixin directives)](https://www.sass.hk/docs/#9) 两个部分。

## @import

Sass 拓展了 `@import` 的功能，允许其导入 SCSS 或 Sass 文件。被导入的文件将合并编译到同一个 CSS 文件中，另外，被导入的文件中所包含的变量或者混合指令 (mixin) 都可以在导入的文件中使用

**不可以在混合指令 (mixin) 或控制指令 (control directives) 中嵌套 `@import`**

## 分音 (Partials)

如果需要导入 SCSS 或者 Sass 文件，但又不希望将其编译为 CSS，只需要在文件名前添加下划线，这样会告诉 Sass 不要编译这些文件，但导入语句中却不需要添加下划线。

例如，将文件命名为 `_colors.scss`，便不会编译 `_colours.css` 文件。

```scss
@import "colors";
```

上面的例子，导入的其实是 `_colors.scss` 文件

###  @extend

顾名思义 继承，继承一个选择器中的所有样式。

```scss
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```

### @if

```scss
p {
  @if 1 + 1 == 2 { border: 1px solid; }
  @if 5 < 3 { border: 2px dotted; }
  @if null  { border: 3px double; }
}
```

### @for

```scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
```

编译为

```css
.item-1 {
  width: 2em; }
.item-2 {
  width: 4em; }
.item-3 {
  width: 6em; }
```

### @each

`@each` 指令的格式是 `$var in <list>`, `$var` 可以是任何变量名，比如 `$length` 或者 `$name`，而 `<list>` 是一连串的值，也就是值列表。

`@each` 将变量 `$var` 作用于值列表中的每一个项目，然后输出结果，例如：

```scss
@each $animal in puma, sea-slug, egret, salamander {
  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}
```

### @while

`@while` 指令重复输出格式直到表达式返回结果为 `false`。这样可以实现比 `@for` 更复杂的循环，只是很少会用到。例如：

```scss
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}
.item-6 {
  width: 12em; }

.item-4 {
  width: 8em; }

.item-2 {
  width: 4em; }
```

# 混合

### 定义混合指令`@mixin`

混合指令的用法是在 `@mixin` 后添加名称与样式，比如名为 `large-text` 的混合通过下面的代码定义：

```scss
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}
```

### 引用混合样式 `@include`

使用 `@include` 指令引用混合样式，格式是在其后添加混合名称，以及需要的参数（可选）：

```scss
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```

### 参数 (Arguments)

参数用于给混合指令中的样式设定变量，并且赋值使用。在定义混合指令的时候，按照变量的格式，通过逗号分隔，将参数写进圆括号里。引用指令时，按照参数的顺序，再将所赋的值对应写进括号：

```scss
@mixin sexy-border($color, $width:1px) { //可以给参数设置默认值
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue, 1in); }
p { @include sexy-border($color: blue); }//可以使用关键词进行赋值
```

### 向混合样式中导入内容 (Passing Content Blocks to a Mixin)

在引用混合样式的时候，可以先将一段代码导入到混合指令中，然后再输出混合样式，额外导入的部分将出现在 `@content` 标志的地方：

```scss
@mixin apply-to-ie6-only {
  * html {
    @content;
  }
}
@include apply-to-ie6-only {
  #logo {
    background-image: url(/logo.gif);
  }
}
```

编译为

```css
* html #logo {
  background-image: url(/logo.gif);
}
```

##  函数指令 (Function Directives)

Sass 支持自定义函数，并能在任何属性值或 Sass script 中使用：

```scss
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }
```

编译为

```css
#sidebar {
  width: 240px; }
```

与 mixin 相同，也可以传递若干个全局变量给函数作为参数。一个函数可以含有多条语句，需要调用 `@return` 输出结果

# sass函数

## 字符串函数

| 函数                                    | 描述 & 实例                                                  |
| --------------------------------------- | ------------------------------------------------------------ |
| quote(*string*)                         | 给字符串添加引号。      **实例:** quote(runoob) 结果: "runoob" |
| str-index(*string*, *substring*)        | 返回 substring 子字符串第一次在 string 中出现的位置。如果没有匹配到子字符串，则返回 null。   `str-index(abcd, a)  => 1 str-index(abcd, ab) => 1 str-index(abcd, X)  => null str-index(abcd, c)  => 3` |
| str-insert(*string*, *insert*, *index*) | 在字符串 string 中  index 位置插入 insert。      **实例:** str-insert("Hello world!", " runoob", 6) 结果: "Hello     runoob world!" |
| str-length(*string*)                    | 返回字符串的长度。      **实例:** str-length("runoob") 结果: 6 |
| str-slice(*string*, *start*, *end*)     | 从 string 中截取子字符串，通过  start-at 和 end-at 设置始末位置，未指定结束索引值则默认截取到字符串末尾。   `str-slice("abcd", 2, 3)   => "bc" str-slice("abcd", 2)      => "bcd" str-slice("abcd", -3, -2) => "bc" str-slice("abcd", 2, -2)  => "bc"` |
| to-lower-case(*string*)                 | 将字符串转成小写      **实例:** to-lower-case("RUNOOB") 结果: "runoob" |
| to-upper-case(*string*)                 | 将字符串转成大写      **实例:** to-upper-case("runoob") 结果: "RUNOOB" |
| unique-id()                             | 返回一个无引号的随机字符串作为 id。不过也只能保证在单次的 Sass 编译中确保这个 id 的唯一性。      **实例:** unique-id() Result:     uad053b1c |
| unquote(*string*)                       | 移除字符串的引号          **实例:** unquote("runoob") 结果: runoob |

------

## 数字函数

| abs(*number*)              | 返回一个数值的绝对值。      **实例:** abs(15) 结果: 15 abs(-15) 结果: 15 |
| -------------------------- | ------------------------------------------------------------ |
| 函数                       | 描述 & 实例                                                  |
| ceil(*number*)             | 向上取整      **实例:** ceil(15.20) 结果: 16                 |
| comparable(*num1*, *num2*) | 返回一个布尔值，判断 *num1* 与 *num2* 是否可以进行比较      **实例:** comparable(15px, 10px) 结果: true comparable(20mm, 1cm) 结果:     true comparable(35px, 2em) 结果: false |
| floor(*number*)            | 向下取整      **实例:**  floor(15.80) 结果: 15               |
| max(*number...*)           | 返回最大值      **实例:** max(5, 7, 9, 0, -3, -7) 结果: 9    |
| min(*number...*)           | 返回最小值      **实例:** min(5, 7, 9, 0, -3, -7) 结果: -3   |
| percentage(*number*)       | 将数字转化为百分比的表达形式。          **实例:** percentage(1.2) 结果: 120 |
| random()                   | 返回 0-1 区间内的小数，      **实例:** random() 结果: 0.45673 |
| random(*number*)           | 返回 1 至 number 之间的整数，包括 1 和 limit。      **实例:** random(6) 结果: 4 |
| round(*number*)            | 返回最接近该数的一个整数，四舍五入。      **实例:** round(15.20) 结果: 15 round(15.80) 结果: 16 |

------

## Sass 列表(List)函数

| append(*list*, *value*, [*separator*])           | 将单个值 *value* 添加到列表尾部。*separator* 是分隔符，默认会自动侦测，或者指定为逗号或空格。       **实例: **append((a b c), d) 结果: a b c d append((a b c), (d), comma)     结果: a, b, c, d |
| ------------------------------------------------ | ------------------------------------------------------------ |
| index(*list*, *value*)                           | 返回元素 *value* 在列表中的索引位置。      **实例:** index(a b c, b) 结果: 2 index(a b c, f) 结果: null |
| is-bracketed(*list*)                             | 判断列表中是否有中括号      **实例:** is-bracketed([a b c]) 结果: true  is-bracketed(a b c) 结果:     false |
| join(*list1*, *list2*, [*separator, bracketed*]) | 合并两列表，将列表 *list2* 添加到列表 *list1* 的末尾。*separator*    是分隔符，默认会自动侦测，或者指定为逗号或空格。 *bracketed* 默认会自动侦测是否有中括号，可以设置为 true 或 false。          **实例:** join(a b c, d e f) 结果: a b c d e f join((a b c), (d e f),     comma) 结果: a, b, c, d, e, f join(a b c, d e f, $bracketed: true) 结果:     [a b c d e f] |
| length(*list*)                                   | 返回列表的长度      **实例:** length(a b c) 结果: 3          |
| list-separator(*list*)                           | 返回一列表的分隔符类型。可以是空格或逗号。      **实例:** list-separator(a b c) 结果: "space" list-separator(a, b, c)     结果: "comma" |
| nth(*list*, *n*)                                 | 获取第 *n* 项的值。      **实例:** nth(a b c, 3) 结果: c     |
| set-nth(*list*, *n*, *value*)                    | 设置列表第 *n* 项的值为 *value*。          **实例:** set-nth(a b c, 2, x) 结果: a x c |
| zip(*lists*)                                     | 将多个列表按照以相同索引值为一组，重新组成一个新的多维度列表。      **实例:** zip(1px 2px 3px, solid dashed dotted, red green blue) 结果: 1px     solid red, 2px dashed green, 3px dotted blue |

## Sass Map(映射)函数

| map-get(*map*, *key*)        | 返回 Map 中 *key* 所对应的 value(值)。如没有对应的 key，则返回 null 值。      **实例:** $font-sizes: ("small": 12px, "normal": 18px, "large": 24px) map-get($font-sizes,     "small") 结果: 12px |
| ---------------------------- | ------------------------------------------------------------ |
| map-has-key(*map*, *key*)    | 判断 *map* 是否有对应的 *key*，存在返回 true，否则返回 false。  **实例:** $font-sizes: ("small": 12px, "normal": 18px, "large": 24px) map-has-key($font-sizes,     "big") 结果: false |
| map-keys(*map*)              | 返回 *map* 中所有的 key 组成的队列。  **实例:**     $font-sizes: ("small": 12px, "normal": 18px, "large": 24px) map-keys($font-sizes) 结果:     "small", "normal, "large" |
| map-merge(*map1*, *map2*)    | 合并两个 map 形成一个新的 map 类型，即将 *map2* 添加到 *map1*的尾部      **实例:** $font-sizes: ("small": 12px, "normal": 18px, "large": 24px)     $font-sizes2: ("x-large": 30px, "xx-large": 36px) map-merge($font-sizes,     $font-sizes2) 结果: "small": 12px, "normal": 18px, "large": 24px,     "x-large": 30px, "xx-large": 36px |
| map-remove(*map*, *keys...*) | 移除 *map* 中的 keys，多个 key 使用逗号隔开。  **实例:** $font-sizes: ("small": 12px, "normal": 18px, "large": 24px) map-remove($font-sizes,     "small") 结果: ("normal": 18px, "large": 24px) map-remove($font-sizes,     "small", "large") 结果: ("normal": 18px) |
| map-values(*map*)            | 返回 *map* 中所有的 value 并生成一个队列。  **实例:** $font-sizes: ("small": 12px, "normal": 18px, "large": 24px) map-values($font-sizes) 结果:     12px, 18px, 24px |

## Sass 选择器函数

| is-superselector(*super*, *sub*)                        | 比较两个选择器匹配的范围，即判断 *super* 选择器是否包含了    *sub* 选择器所匹配的范围，是的话返回 true，否则返回 false。      **实例:** is-superselector("div", "div.myInput") 结果: true is-superselector("div.myInput",     "div") 结果: false is-superselector("div",     "div") 结果: true |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| selector-append(*selectors*)                            | 将第二个 (也可以有多个) 添加到第一个选择器的后面。    selector.      **实例:** selector-append("div", ".myInput") 结果: div.myInput selector-append(".warning",     "__a") 结果: .warning__a |
| selector-extend(*selector*, *extendee*, *extender*)     |                                                              |
| selector-nest(*selectors*)                              | 返回一个新的选择器，该选择器通过提供的列表选择器生成一个嵌套的列表。      **实例:** selector-nest("ul", "li") 结果: ul li selector-nest(".warning",     "alert", "div") 结果: .warning div, alert div |
| selector-parse(*selector*)                              | 将字符串的选择符 *selector* 转换成选择器队列。       **实例: **selector-parse("h1 .myInput .warning") 结果: ('h1' '.myInput'     '.warning') |
| selector-replace(*selector*, *original*, *replacement*) | 给定一个选择器，用replacement 替换 original 后返回一个新的选择器队列。      **实例:** selector-replace("p.warning", "p", "div") 结果: div.warning |
| selector-unify(*selector1*, *selector2*)                | 将两组选择器合成一个复合选择器。如两个选择器无法合成，则返回 null 值。      **实例:** selector-unify("myInput", ".disabled") 结果: myInput.disabled     selector-unify("p", "h1") 结果: null |
| simple-selectors(*selectors*)                           | 将合成选择器拆为单个选择器。          **实例:** simple-selectors("div.myInput") 结果: div, .myInput     simple-selectors("div.myInput:before") 结果: div, .myInput,     :before |

## Sass Introspection 函数

| call(*function*, *arguments*...)         | 函数的动态调用，即调用函数 function 参数为 arguments，并返回结果。 |
| ---------------------------------------- | ------------------------------------------------------------ |
| content-exists()                         | 查看当前的混入是否传递 @content 块。                         |
| feature-exists(*feature*)                | 检查当前的 Sass 实现是否支持该特性。       **实例:** feature-exists("at-error"); 结果: true |
| function-exists(*functionname*)          | 检测指定的函数是否存在      **实例:** function-exists("nonsense") 结果: false |
| get-function(*functionname*, css: false) | 返回指定函数。如果 css 为 true，则返回纯 CSS 函数。          |
| global-variable-exists(*variablename*)   | 检测某个全局变量是否定义。      **实例:** variable-exists(a) 结果: true |
| inspect(*value*)                         | 返回一个字符串的表示形式，value 是一个 sass 表达式。         |
| mixin-exists(*mixinname*)                | 检测指定混入 (mixinname) 是否存在。      **实例:** mixin-exists("important-text") 结果: true |
| type-of(*value*)                         | 返回值类型。返回值可以是 number, string, color, list,     map, bool, null, function, arglist。      **实例:** type-of(15px) 结果: number type-of(#ff0000) 结果: color |
| unit(*number*)                           | 返回传入数字的单位（或复合单位）。      **实例:** unit(15px) 结果: px |
| unitless(*number*)                       | 返回一个布尔值，判断传入的数字是否带有单位。          **实例:** unitless(15px) 结果: false unitless(15) 结果: true |
| variable-exists(*variablename*)          | 判断变量是否在当前的作用域下。          **实例:** variable-exists(b) 结果: true |

## Sass 颜色函数

| rgb(*red*, *green*, *blue*)                     | 创建一个 Red-Green-Blue (RGB) 色。其中 R 是 "red" 表示红色，而 G 是 "green" 绿色，B 是 "blue" 蓝色。      **实例:** rgb(0, 0, 255); |
| ----------------------------------------------- | ------------------------------------------------------------ |
| rgba(*red*, *green*, *blue*, *alpha*)           | 根据红、绿、蓝和透明度值创建一个颜色。      **实例:** rgba(0, 0, 255, 0.3); |
| hsl(*hue*, *saturation*, *lightness*)           | 通过色相（hue）、饱和度(saturation)和亮度（lightness）的值创建一个颜色。      **实例:** hsl(120, 100%, 50%); // 绿色 hsl(120, 100%,     75%); // 浅绿色 hsl(120, 100%, 25%); // dark green hsl(120, 60%,     70%); // 柔和的绿色 |
| hsla(*hue*, *saturation*, *lightness*, *alpha*) | 通过色相（hue）、饱和度(saturation)、亮度（lightness）和透明（alpha）的值创建一个颜色。      **实例:** hsl(120, 100%, 50%, 0.3); // 绿色带有透明度     hsl(120, 100%, 75%, 0.3); // 浅绿色带有透明度 |
| grayscale(*color*)                              | 将一个颜色变成灰色，相当于 desaturate( color,100%)。      **实例:** grayscale(#7fffd4); 结果: #c6c6c6 |
| complement(*color*)                             | 返回一个补充色，相当于adjust-hue($color,180deg)。      **实例:** complement(#7fffd4); 结果: #ff7faa |
| invert(*color*, *weight*)                       | 返回一个反相色，红、绿、蓝色值倒过来，而透明度不变。      **实例:** invert(white); 结果: black |