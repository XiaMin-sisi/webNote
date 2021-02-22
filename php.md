### 变量

#### 命名规则

$ 开头 。字母、数字、下划线组成。且不能数字跟在 $后面

#### 定义、赋值、修改、删除

```php
$age;//先定义
$age=18;//再赋值

$name='xiamin';//定义的同时进行赋值

echo $age.'  '.$name;//输出变量 变量与字符串之间用 . 进行连接
echo '<hr/>';
$age=20;//变量的修改
echo $age;
echo '<br/>';
unset($age);//=>删除变量，在内存中释放变量
```

#### 输出变量

```php
//echo 输出字符串、数值型变量，字符串变量与普通字符串之间用 . 连接
$name="xiamin";
echo '我的名字是'.$name;
//其他类型变量输出 var_dump(变量名)，比如bool 数组 对象 方法
var_dump($re)
```

#### 可变变量

变量的值作为另一个变量的名字

```php
$a='b';
$b='c';
echo $$a; // c
```

#### 预定义变量

php有很多预定义好的变量，超全局变量,全是数组,通过key值索引的数组。

```php
$GLOBALS 		//引用全局作用域中可用的全部变量
$_SERVER 		//服务器和执行环境信息
$_GET 			//HTTP GET 变量
$_POST			//HTTP POST 变量
$_FILES 		//HTTP 文件上传变量
$_REQUEST 		//HTTP Request 变量
$_SESSION 		//Session 变量
$_ENV 			//环境变量
$_COOKIE 		// HTTP Cookies
$php_errormsg 	// 前一个错误信息
$HTTP_RAW_POST_DATA // 原生POST数据
$http_response_header // HTTP 响应头
$argc 			// 传递给脚本的参数数目
$argv 			// 传递给脚本的参数数组 
```

#### 变量的传递

##### 值传递

分配一个新的内存空间

```php
$obj="hello";
$obj2=$obj;
```

##### 引用(地址)传递

引用同一个内存地址。两个变量相互影响

```php
$obj3=&$obj;
```

----

### 常量

不能被修改的变量，常量不能被释放

#### 常量的定义

常量的命名可以不用 $ 开头，且一般大写字母开头。定义的同时就需要进行赋值	

##### 使用函数定义常量

这种方法可以用特殊字符命名常量，但是访问也应该使用函数

```php
define("PI",3.14,true);//=>有第三个参数 ，用来设置常量名称是否不区分大小写,默认区分
define("^-^","笑脸");//设置特俗名称的常量
echo '<br/>';
echo Pi;
echo '<br/>';
echo constant("^-^");// 使用函数访问特俗名称的变量
```

##### 关键字 const 定义常量

**const 关键字定义常量必须处于最顶端的作用区域**，因为用此方法是在编译时定义的。这就意味着不能在函数内，循环内以及 if 语句之内用 const 来定义常量。

```php
	const PII=3.14159;
```

#### 系统常量

php中有很多系统定义好的常量

```php
    FILE 		//当前PHP文件的相对路径
    LINE 		//当前PHP文件中所在的行号
    FUNCTION 	//当前函数名，只对函数内调用起作用
    CLASS 		//当前类名，只对类起作用
    PHP_VERSION //当前使用的PHP版本号
    PHP_OS 		//当前PHP环境的运行操作系统
    TRUE 		//与true一样
    FALSE		//与false一样
    M_PI 		//圆周率常量值
    M_E 		//科学常数e
    M_LOG2E 	//代表log2
    M_LOG10E 	//代表lg
    M_LN2 		//2的自然对数
    M_LN10 		//10的自然对数
    E_ERROR 	//最近的错误之处
    E_WARNING 	//最近的警告之处
    E_PARSE 	//剖析语法有潜在问题之处
    METHOD 		//表示类方法名，比如B::test
```

----

### 数据类型

php和js一样。弱类型语言，变量本身是没有数据类型，这里说的类型都是针对变量值。

##### 四种标量类型

◦  boolean（布尔型）  
◦  integer（整型）  
◦  float（浮点型，也称作 double)  
◦  string（字符串）  

##### 三种复合类型

◦  array（数组）  
◦  object（对象）  
◦  callable（可调用，就是函数呗）  

##### 两种特殊类型

◦  resource（资源=》外部数据，如文件、数据库）  
◦  NULL（无类型就是空呗） 

#### 类型转换

##### 自动转换

```php
$x='3nu';
$y=2*$x;//对字符串做某些运算，会自动先把字符串转化成数值类型
echo $y;
```

##### 强制转换（手动转换）

```php
$num='12xia';
$rnum=(int)$num;
echo '<br/>',$rnum;
/*  
	◦ (int), (integer) - 转换为整形 integer 
    ◦ (bool), (boolean) - 转换为布尔类型 boolean 
    ◦ (float), (double), (real) - 转换为浮点型 float 
    ◦ (string) - 转换为字符串 string 
    ◦ (array) - 转换为数组 array 
    ◦ (object) - 转换为对象 object 
    ◦ (unset) - 转换为 NULL (PHP 5) 
    并不一定能转换成功，需要有一定的规则
*/
```

##### 判断是否为某个类型

is_typeName()    比如：is_int($x);

```php
	$re=is_int($x);
```

##### Set/Gettype

得到  / 设置某个变量的数据类型

```php
Settype($re,'int');//两种类型能强制转换才能这样用
echo Gettype($re);
```

#### 运算符

```php
	// 赋值运算 =
	// 算数运算 + - * / % 
	// 比较运算 > >= < <= == !=  ===全等于 !==不全等于
	// 逻辑运算 && || !
	// 连接运算符 
	// 		. 连接两个字符串,相当于其他语言的 +
	// 		.= 将右边与自身相连接，并赋值给自己 $a.=$b; 相当于 $a=$a.$b; 
	// 错误抑制符 @ =》相当于cath，对可能出错的运算进行抑制 @(4/0);
	// 三目运算符：bool?val1:val2 =>bool为真取val1 否则取值val2
	// 自操作运算符：++ -- : $a++ ++$a
	// 衍生的操作符：+= -= *= /= %=
	// 位运算符 针对二进制数据的运算
	// 		取反=》符号位不变，其他位取反
	//		取补=>反码加1
	// 		对十进制的整数进行位运算的顺序:得到二进制源码=》反码=》补码=》位运算=》反码=》源码=》换			   算成十进制
	// 		&:按位与=>	都真才真,有一假则假
	// 		|:按位或=>	一个真就是真,全假则假
	// 		!:安位非=>	有真就是假,全假则为真=>和按位或刚好相反
	// 		^:按位异或=>	相同则真,不同则假
	// 		<<:按位左移，右边补 0=>其实就是*2的操作，arm上有讲
	// 		>>:按位右移，左边补符号位（符号位，正数的符号位是 1 负数的符号位是 0）
	// 运算符的优先级：参考手册
```

---

### 逻辑结构

顺序、选择、分支、循环结构，和其他语言的一样

```php
if else 
switch
for
do while
while
foreach=》对数组、对象的循环
```

#### 循环控制

```php
//continue =>停止本次循环，执行下次循环。
//break=》停止、并退出当前的循环体。默认退出当前的循环体，break + 数字。表示退出几层循环体
//exit("message")/die("message");=>终止这个程序的运行
```

##### continue 

停止本次循环，执行下次循环。

##### break

停止、并退出当前的循环体。默认退出当前的循环体，**break + 数字。表示退出几层循环体**

##### exit / die("message")

终止这个程序的运行

---

### 函数

#### 函数的定义

函数的定义和js一样

```php
function functionName([参数]){
		//执行的代码
    //[return something]
}
```

#### 函数的调用

函数的调用也和 js 一样

```php
functionName();
```

#### 函数内部作用域

与其他语言一样的是：函数内部是一个独立的作用域，外部不能使用函数内部的数据。与其他语言不一样的是：**函数内部如果想要使用全局变量，需要进行一个声明 ，global 全局变量名**，全局常量是可以直接在函数内部直接使用，不需要声明

```php
const AGE=18;//全局常量
$name="xiamin";//全局变量
function showName(){
    echo '<br/>';
    global $name;//声明 使用全局变量
    echo $name,' ',AGE;//直接使用全局 常量
};
showName();
```

#### 静态变量

在函数内部定义的一个变量，定义的同时使用关键词 static 。相当于 js  中使用闭包，**函数中的某个变量不会随着函数的执行结束被销毁**，而需要手动进行销毁，或直到程序结束。

```php
function mycount(){
    static $sum=0;
    $sum++;
    echo '<br/>第'.$sum.'次执行mycount函数';
};
mycount();// 1
mycount();// 2
mycount();// 3
mycount();// 4
```

#### 函数的参数

##### 按引用传递参数

和 c 语言一样，传递的是一个地址，函数内部可以直接操作这个地址的数据

```php
$qq=15322;
function updateqq(&$num){
    $num++;
};
updateqq($qq);
echo '<br/>'.$qq;
```

##### 参数默认值

给函数设置默认值，和 js 一样，就是定义函数时对参数进行赋值，调用时未传参就使用默认值参数

##### 参数列表

 php和 js 一样，实参和形参个数可以不一致，实参数目大于形参数目时，函数能正常执行，并截取和形参数目相同的实参，按顺序赋值给形参；当实参数目小于形参数目时，函数也能执行，但会给出警告消息：缺少参数。 通过函数 ： func_get_args() 返回值就是参数数组，但是可以直接 使用参数代表索引获取 对应索引值的数据。

```php
function nopar(){
    echo '<br/>';
    var_dump(func_get_args());//返回值是一个数组，里面是所有实参的值
    echo '<br/>';
    echo func_get_arg(1);//参数是数组的索引值，返回值是该索引值对应参数列表的值
    echo '<br/>';
    echo func_num_args();//返回值是参数的个数
	};
```

#### 可变函数变量

可变变量 引申 可变函数 =>函数名作为变量的值，通过变量就可以调用函数

```php
$funname="nopar";
$funname('','哇，我明明是变量，竟然加个括号就变成函数了');
```

#### 函数的递归

在函数内部再次调用自己本身，一定要有终止递归的判断，否则会变成死循环

---

### 数组

#### 数组的分类

1. 索引数组=》通过下标获取数组的值
2. 关联数组=》通过别名获取值=》其实就是修改类默认的索引值（不就是对象嘛）

#### 数组的创建

##### 索引赋值

```php
//可以自己写索引，最好别写索引，好恐怖，1就没有了，直接 0 2 3
$student[0]='xiamin';
$student[2]=18; 
//也可以不写索引，系统会按顺序添加，默认加到数组后面
$student[]='男'; 
var_dump($student);
print_r($student);
```

##### 关联赋值

```php
$boy["name"]="虚拟";
$boy['age']=18;
$boy['sex']='男';
var_dump($boy);
```

##### 通过函数

```php
//索引数组
$man=array('sisi',18,'女');
var_dump($man);
//关联数组
$girl=array(
    'name'=>'minmin',
    'age'=>18
);
var_dump($girl);
echo $girl['name'];
```

#### 遍历数组

##### for 循环

普通 for 循环只能遍历 索引数组，不能遍历 关联数组。

```php
//获取数组长度的函数 count(arrname)
echo '<br/>count=';
echo count($man);
for($i=0;$i<count($man);$i++)
{
    echo "<br/>";
    echo $man[$i];
}
```

##### foreach

任意类型的数组都能遍历.

```php
foreach($boy as $key=>$val){// key可以不写，默认就是val, 即  $boy as $val
    echo "<br/>";
    echo $key."=》".$val;
}
```

#### 预定义变量

下面这些系统预定义的变量，都是数组

```php
	//$GLOBALS:包含了全部变量的全局组合数组。变量的名字就是数组的键
		var_dump($GLOBALS);
	//$_SERVER: 是一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等  		等信息的数组
		var_dump($_SERVER);
	//$_GET:通过 URL 参数传递给当前脚本的变量的数组
	
	//$_POST: HTTP POST 请求的 Content-Type 是 application/x-www-form-urlencoded 或 			<multipa>	</multipa>rt/form-data 时，会将变量以关联数组形式传入当前脚本
	
	//$_REQUEST:默认情况下包含了 $_GET，$_POST 和 $_COOKIE 的数组
	
	//$_COOKIE:通过 HTTP Cookies 方式传递给当前脚本的变量的数组
	
	//$_SESSION:当前脚本可用 SESSION 变量的数组
	
	//$_FILES:通过 HTTP POST 方式上传到当前脚本的项目的数组
	
	//$_ENV:通过环境方式传递给当前脚本的变量的数组
```

---

### date 日期时间

这里的日期与时间不是指的电脑的日期时间，而是指定时区的时间，即会将电脑的时间转换为指定时区的时间。

##### 设置时区

```php
//默认时区 不是中国的时区，我们设置时区为 中国上海的时区，没找到北京的时区
ini_set('date.timezone','Asia/Shanghai');
```

##### 获取当前时间戳

```php
//时间戳：是一个以秒为单位的代表从 1970.1.1 00:00 开始到某个时间的 秒数
//获取当前时间戳 time() =>从1970.1.1 00：00开始到当前时间的秒数
$nowtime=time();
echo $nowtime;
echo '<br/>';
```

##### 获取当前时间戳的微秒数

```php
//microtime()
echo microtime(true); //138197510.25139300  返回一个浮点数
echo microtime(); //0.25139300 1138197510   返回一个字符串，分两部分，一个是小数部分，一个是整数部分
```

##### 获取指定日期时间戳

```php
//获取指定时间的时间戳：mktime(18,28,30,5,26,2020);// 时 分 秒 月 日 年
$time2=mktime(18,28,30,5,26,2020);//2020.05.26 18:28:30 的时间戳
```

#### 时间戳转换为字符串

时间戳是一个数字，看不出时间是什么时候，但是我们存储时间的时候一般都是存储时间戳，因为方便进行一系列的操作，但是显示日期时间，不能用时间戳，别人看不懂。这时候就需要把时间戳转换成日期字符串。

```php
//第一个参数是 格式参数 
//第二个默认就是当前的时间戳，如果你要的就是但当前时间可以省略
$res=date("Y-M-d G:i:s",time());
```

##### 格式化参数如下

- d - 一个月中的第几天（从 01 到 31）
- D - 星期几的文本表示（用三个字母表示）
- j - 一个月中的第几天，不带前导零（1 到 31）
- l（'L' 的小写形式）- 星期几的完整的文本表示
- N - 星期几的 ISO-8601 数字格式表示（1表示Monday[星期一]，7表示Sunday[星期日]）
- S - 一个月中的第几天的英语序数后缀（2 个字符：st、nd、rd 或 th。与 j 搭配使用）
- w - 星期几的数字表示（0 表示 Sunday[星期日]，6 表示 Saturday[星期六]）
- z - 一年中的第几天（从 0 到 365）
- W - 用 ISO-8601 数字格式表示一年中的星期数字（每周从 Monday[星期一]开始）
- F - 月份的完整的文本表示（January[一月份] 到 December[十二月份]）
- m - 月份的数字表示（从 01 到 12）
- M - 月份的短文本表示（用三个字母表示）
- n - 月份的数字表示，不带前导零（1 到 12）
- t - 给定月份中包含的天数
- L - 是否是闰年（如果是闰年则为 1，否则为 0）
- o - ISO-8601 标准下的年份数字
- Y - 年份的四位数表示
- y - 年份的两位数表示
- a - 小写形式表示：am 或 pm
- A - 大写形式表示：AM 或 PM
- B - Swatch Internet Time（000 到 999）
- g - 12 小时制，不带前导零（1 到 12）
- G - 24 小时制，不带前导零（0 到 23）
- h - 12 小时制，带前导零（01 到 12）
- H - 24 小时制，带前导零（00 到 23）
- i - 分，带前导零（00 到 59）
- s - 秒，带前导零（00 到 59）
- u - 微秒（PHP 5.2.2 中新增的）
- e - 时区标识符（例如：UTC、GMT、Atlantic/Azores）
- I（i 的大写形式）- 日期是否是在夏令时（如果是夏令时则为 1，否则为 0）
- O - 格林威治时间（GMT）的差值，单位是小时（实例：+0100）
- P - 格林威治时间（GMT）的差值，单位是 hours:minutes（PHP 5.1.3 中新增的）
- T -  本机所在的时区 
- Z - 以秒为单位的时区偏移量。UTC 以西时区的偏移量为负数（-43200 到 50400）
- c - ISO-8601 标准的日期（例如 2013-05-05T16:34:42+00:00）
- r - RFC 2822 格式的日期（例如 Fri, 12 Apr 2013 12:01:05 +0200）
- U - 自 Unix 纪元（January 1 1970 00:00:00 GMT）以来经过的秒数

---

### string 

#### 字符串操作方法

#####  字符串长度

**strlen()**函数返回字符串的长度，以字符计  strlen(stringName)

#####  反转字符串

**strrev()**函数返回一个字符串，是源字符串的反转字符串  strrev(stringName)

#####  检索字符串

```php
strpos($str,search,[int])//函数用于检索字符串内指定的字符串。如果找到，则会返回首个匹配的字符位置。
strrpos($str,search,[int])//查找search在$str中的最后一次出现的位置从int开始
//如果未找到匹配，则将返回 FALSE。int 可以省略表示从字符串头部开始
```

#####  **提取子字符函数**

```php
submit($str,int start[,int length]) //str中strat位置开始提取[length长度的字符串]。省略 第三个参数则提取到字符串的结尾
strstr($str1,$str2)//str1(第一个的位置)搜索$str2并从它开始截取到结束字符串;若没有则返回FALSE
stristr()//功能同strstr，只是不区分大小写。
strrchr()//从最后一次搜索到的字符处返回；用处：取路径中的文件名
```

#####  替换字符串

用一个字符串替换字符串中的某些子串。 

```php
str_replace(search,replace,$str)//从$str中查找search用replace来替换
strtr($str,search,replace)//这个函数中replace不能为"";
substr_replace($Str,$rep,$start[,length])//$str原始字符串,$rep替换后的新字符串,$start起始位置,$length替换的长度，该项可选
```

#####  **比较字符函数** 

```php
//返回值 $str1>=<$str2分别为正1,0,-1
strcmp($str1,$str2)
strcasecmp() //同上不分大小写
strnatcmp("4","14") //按自然排序比较字符串
strnatcasecmp() //同上，区分大小写
```

#####  **分割成数组函数** 

```php
//把$str按len长度进行分割返回数组
str_split($str,len)
//把$str按search字符进行分割返回数组int是分割几 次，后面的将不分割
split(search,$str[,int])
```

#####  **去除空格** 

```php
//ltrim()、rtrim()、trim()
//分别是去 左边、右边、两端的空格
```

#####  **加空格函数** 

 **chunk_split($str,2)** 	向$str字符里面按2个字符就加入一个空格; 

#####  **字符大小写转换函数** 

```php
strtolower($str) //字符串转换为小写
strtoupper($str) //字符串转换为大写
ucfirst($str) //将函数的第一个字符转换为大写
ucwords($str) //将每个单词的首字母转换为大写
```

#####  **HTML代码有关函数** 

```php
nl2br()//使\n转换为<br>
strip_tags($str[,'<p>'])//去除HTML和PHP标记
htmlspecialchars($str[,参数])//页面正常输出HTML代码参数是转换方式
```

#####  **数据库相关函数** 

```php
addslashes($str)//使str内单引号（'）、双引号（"）、反斜线（\）与 NUL字符串转换为\',\",\\
magic_quotes_gpc = On //自动对 get post cookie的内容进行转义
get_magic_quotes_gpc（）//检测是否打开magic_quotes_gpcstripslashes() 去除字符串中的反斜杠
```

##### 原样字符串

```php
//特别说明一个：定义一个字符串的特别方式,里面的字符原样输出，不需要转义字符，格式一定要这样，不要缩进之类
$str=<<<STRING
'''vsdsdj'''dki""dvcsjv""askljf""
STRING;
	//而mysqli有一个函数可以对一些特殊字符进行转义，可以配合使用，在对数据库存入数据，有大量特殊字符时使用
	//mysql_real_escape_string();
	echo $str;
```

----

### 图像处理

##### 头部声明

如果你要把图片直接输出到网页中，就需要声明一下，否则浏览器以为是文本

```php
header('Content-type:image/jpeg');
```

##### 创建图像（画布）

相当于创建一个画布，之后就在画布上画图

```php
//1.1、创建一个新的真彩色图像=》空的图像，图像的数据类型是资源型
	$img=imagecreatetruecolor(200,200);//返回一个资源型的对象，参数是画布的宽高
//1.2、打开一个已经存在的图像
	$img=imagecreatefromjpeg("sisi.jpg");//参数是图片的路径
```

##### 绘制图像

对刚刚创建的画布进行绘图

```php
$color1=imagecolorallocate($img,255,0,0);//创建颜色
$color2=imagecolorallocate($img,50,50,50);//创建颜色
imagefill($img,50,50,$color1);//用某个颜色填充图像，第二、三个参数是 开始区域的左上角位置
```

##### 输出图像

保存或是直接输出到网页中

```php
imagejpeg($img);//=>输出到网页
imagejpeg($img,'sisi.jpg');//保存图片在项目文件夹下
```

##### 释放图像资源

```php
imagedestroy($img);
```

##### 具体应用

动态验证码 、 图片添加水印  参考文件 08-2-VerCode.php  、08-3-water.php。写的还不错。

----

### 文件、目录、路径

#### 文件、目录的信息

```php
//1、判断给定文件名是不是普通文件（不存在或者不是普通文件都返回 false）
	var_dump(is_file("sisiw.jpg"));
//2、判断给定文件名是不是一个目录（不存在或者不是目录都返回 false）	
	var_dump(is_dir("../php"));
//3、检查给定的文件名是否真的存在（只要存在，不管是普通文件还是目录都返回 true）
	var_dump(file_exists("t1.html"));
//4、取得普通文件的大小=》返回值是以字节为单位
	var_dump(filesize('sisi.jpg'));
//5、查看文件、目录的读、写权限
	var_dump(is_readable('sisi.jpg'));
	var_dump(is_writable('sisi.jpg'));
//6、获取文件、目录的创建、上一次修改、上一次访问时间
	ini_set('date.timezone','Asia/Shanghai'); //设置一下时区为中国
	var_dump(date("Y-M-d G:i:s",filectime('sisi.jpg')));//返回创建时间的时间戳
	var_dump(date("Y-M-d G:i:s",filemtime('sisi.jpg')));//返回上一次修改的时间戳
	var_dump(date("Y-M-d G:i:s",fileatime('sisi.jpg')));//返回上一次访问的时间戳
//7、获取文件、目录的大部分信息=>上面的信息基本都在这里面
	var_dump(stat("sisi.jpg"));
```

#### 路径信息的操作

```php
//1、关于路径、目录的几个魔术常量 
	echo __FILE__."<br/>";//当前文件所在的完整的路径名
	echo __DIR__."<br/>";//当前文件所在的目录路径
//2、返回路径中的文件名部分=》就是返回最后一个斜杠后的部分嘛
	echo basename(__FILE__)."<br/>";
	echo basename(__DIR__)."<br/>";
//3、返回路径中的目录部分=》就是返回最后一个 / 之前的部分嘛
	echo dirname (__FILE__)."<br/>";
	echo dirname(__DIR__)."<br/>";
//4、返回路径的基本信息=》上面的两个信息当然被包含在上面了
	//filename 、extension、basename、dirname
	var_dump(pathinfo(__FILE__));
	
```

#### 目录的操作

打开 目录，读取文件列表中文件的基本信息，可以用循环，读取到文件的信息，再对文件进行操作

```php
//1、打开一个目录并读取目录资源				
	//1.1、打开一个目录资源/目录句柄=>只能打开目录，返回的是一个资源对象
		$dir=opendir("../prog1");
	//1.2、从刚刚打开的目录句柄中取出下一个文件
		//应该是由类似游标的方式，每打开一个文件，游标自动下移，直到末尾返回 false
		var_dump(readdir($dir));//第一个文件是自己本身 .
		var_dump(readdir($dir));//第二个是文件的上一级目录 ..
		var_dump(readdir($dir));//第三个文件开始 就是该目录下的第一个文件
		rewinddir($dir);//=>重置游标，从头开始
		var_dump(readdir($dir));//=》又是自己本身
		closedir($dir);//=>关闭目录句柄
//3、新建一个空目录
	//第一个参数是目录的路径，第二个是权限 linux的写法,第三个参数指定是否可以多级目录，创建成功返回true 否则 false
	//mkdir("image",0777,false);
	//mkdir("photo/png",0777,true);
//4、删除一个空目录=>只能一个一个删，且只能删除空目录
	//rmdir("photo");
//5、列出指定目录下的文件列表=》返回值是一个数组，就是目录句柄的文件顺序
	var_dump(scandir('../prog1'));
```

#### 文件的操作

对文件内容进行读、写、重命名、复制

```php
//1、打开一个文件资源--资源句柄=》不存在会自己创建这个文件
	// r+=>不清空，文件头开始替换
	// w+=>清空再写入
	// a+=>不清空，文件尾部追加
	$file=fopen("aa.txt","a+");
	var_dump($file);
//2、读取文件资源的数据
	//应该也是类似游标的机制，读取后会自动后移
	//每次读取指定字节数
	echo fread($file,3);
	//每次读取一行的内容
	echo fgets($file);
	//检测游标是否移动到文件的末尾=>到达返回 true
	var_dump(feof($file));
//3、写入文件
	//移动文件的指针=》fseek($file,字节数，参考点);把指针移动到距参考点多少字节位置
	rewind($file);//=>重置文件的游标，因为刚刚读了文件，游标移动了
	fwrite($file,"思");
	fwrite($file,"思");
//4、锁定文件=》在你操作的某个文件时，不希望别人在这期间进行访问
	if(flock($file,2)){
	fwrite($file,"小虚拟");
	flock($file,3);//=>释放文件，开锁
	}
//5、关闭一个已经打开的文件
	fclose($file);
	
//6、不用打开文件直接操作文件
	//将一个文件的内容读取到一个数组中，每一行是一个元素
	var_dump(file("aa.txt"));
	//将一个文件读入到一个字符串中
	echo file_get_contents("aa.txt");
	//将字符串写入到文件中,会清空原内容
	file_put_contents("aa.txt","我是不打开文件，直接写入的内容");
	//读入一个文件的内容放到缓冲区中
	readfile("aa.txt");
	//复制一个文件
	copy("aa.txt","bb.txt");
	//重命名一个文件
	rename("a.txt","aa.txt");
```

#### 下载文件

客户端下载服务器的文件到自己的电脑

```php
//判断该文件是否存在、是否为普通文件
		if(file_exists($filename)&&is_file($filename)){
		//1、用一个扩展的函数获取被下载的文件的类型MIME 主类型/副类型比如 text/html
			$fi = new finfo(FILEINFO_MIME_TYPE); 
			$filetype=$fi->file($filename);
		//2、告诉html我们将要给出的数据类型
			header("Content-type:".$filetype);
		//3、指定下载文件的描述
			header("Content-Disposition:attachement;filename=".$filename);
		//4、指定文件大小
			header("Content-Length:".filesize($filename));
		//5、将指定文件读入 缓冲区
			readfile($filename);
		}
//不存在则返回错误信息
		else
		{
			echo "该文件已经不提供下载，或者文件名有错";
		}
```

#### 上传文件

客户端上传文件到服务器所在的电脑

```php
//1、在php.ini配置上传相关的设置=》是否可以接收上传、脚本最大的内存、最大post数据的大小、临时文件的保存路径
//2、从临时文件夹移动文件
	var_dump($_FILES);//=>预定义超全局数组=》二维的数组,客户端上传文件信息保存的数组
	/*
	array (size=1)
  'myfile' => 
    array (size=5)
      'name' => string '暑期学习plan.md' (length=19)
      'type' => string 'application/octet-stream' (length=24)
      'tmp_name' => string 'C:\wamp64\tmp\phpDF51.tmp' (length=25)
      'error' => int 0
      'size' => int 532
	*/
	//移动之前可以进行一次判断是否该文件上传成功,判断数组是不是空的
	if(count($_FILES)!=0){
		if(is_uploaded_file($_FILES['myfile']['tmp_name'])){
			copy($_FILES['myfile']['tmp_name'],$_FILES['myfile']['name']);
			echo "文件保存成功";
		}
		else
			echo "文件没有保存成功";
	}
	else
		echo "文件没有上传成功";
```

参考文件  09-3-downfile.php   09-4-upfile.php

----

### cookie、session

#### cookie

默认情况下同一个项目下都是共用一个cookie，html中用js设置的cookie也可以拿到,可以设置path来设置cookie的作用范围.**cookie是存在用户的浏览器上的，并不是在服务器里。**

##### cookie操作

```php
//1、设置cookie,cookie是键值对形式存在，存放在一个超全局关联数组中
		setcookie("name","xiamin",time()+1000*3600);
//2、得到cookie=》超全局数组：$_COOKIE 所有的cookie都在这里边
		var_dump($_COOKIE);
//3、删除cookie =》就是设置时间为过去的
		//sleep(1000*20);
		setcookie("name","xiamin",time()-1);
```

#### session

session和cookie不同在于，cookie是将数据保存在用户的浏览器中，**而session是将数据保存在服务器中。在 tmp 文件夹中**。session依赖于cookie。

##### session原理

当你开启session时服务器会自动生成一个cookie，cookie中保存 PHPSESSID，当下次访问时，开启session，会去cookie中找到PHPSESSID，在服务器中把id对应的数据取出来。

##### session操作

```php
//1、开启一个新会话，如果已经开启过，那就是返回一个已存在的会话
	session_start();
	
//2、设置session的数据=>超全局数组=》$_SESSION
	$_SESSION["myname"]="夏敏";
	$_SESSION["mypw"]="153";
//3、删除session=》只要用到session 都需要先开启session
	//1、释放session对象在内存中的空间
		session_unset();
	//2、删除session的所有数据=》那个文件
		session_destroy();
	//3、删除cookie的PHPSESSID。注意 PHPSESSID 是全局的，删除的时候要设置全局
		setcookie(session_name(),"",time()-1,'/');
```

----

### mysql

##### mysql操作

```php
//1、连接数据库
$mysql = new mysqli('127.0.0.1', 'root', '123',"bookms",3308);
//判断是否连接成功
if($mysql->connect_errno)
    die('连接错误' . $mySQLi -> connect_error);//失败则打印错误信息并结束程序
//否则继续操作 
//2、设置字符编码	
$mysql -> set_charset('utf8');
//4、编写sql语句
$sql="select * from books";
//5、使用数据库对象执行sql语句，并将得到的结果集存储在$res中
$res=$mysql -> query($sql);
//6、将数据从结果集中取出
$data=$res->fetch_all(MYSQLI_ASSOC);//以关联数组形式取出全部数据
//如果不想一次性把数据全部返回给客户端，参考 prog2/backend/t2.php,对数据进行分组获取，需要提供页码、每页数据的条数。
echo json_encode($data,JSON_UNESCAPED_UNICODE);//转换成json格式的字符串返回给请求的页面
//7、释放存储结果集的变量、关闭数据库连接
$res -> free();
$mysql-> close();
```

