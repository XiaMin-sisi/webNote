#  Nodejs是什么

## nodejs介绍

nodejs不是一门语言，不是一个框架。是一个JavaScript的运行时环境，可以解析执行JavaScript代码。

但是nodejs中运行的js和浏览器上的js代码作用不同，不再是操作Dom\Bom的js。只是使用JavaScript语法实现。nodejs为JavaScript提供了服务器级别的操作API：

* 文件读写
* 网络服务的构建
* 网络通信
* http服务
* ...等等

## nodejs特性

* 使用事件驱动机制
* 非阻塞（异步）IO模型
* 轻量高效

## nodejs能做什么

* web服务器后台

* 命令行工具
  * npm
  * git
  * 等等

* 游戏服务器
* 对于web前端工程师，最多使用的是nodejs提供的命令行工具
  * webpack
  * npm

## 安装Nodejs

* 官网下载、安装
* 检查是否安装成功 命令行输入 node --version  看是否输出版本号
* 环境变量

---

# Hello nodeJS

## 第一个node程序

1. 编写第一个nodejs程序
   * 建立一个后缀为js的文件
   * 编写js代码

2. 运行程序
   * 命令行进入文件所在目录
   * 执行命令 node + 文件名

3. 注意事项
   * js文件不能命名为 node.js
   * js代码只能使用JavaScript基础语法，没有浏览器的dom、bom元素
   * 但是node环境中，JavaScript有在浏览器中不具备的能力如：文件的操作等

## 模块的引入

nodejs提供了很多模块，以扩展JavaScript的功能，如果我们需要使用这些功能，就需要在程序中引入他们的核心模块。

nodejs中模块有三种：

1. 具名的核心模块，如：fs 、http，不需要下载、安装
2. 自定义的文件模块。需要说明的是，node中没有全局作用域，只有模块作用域，一个文件就是一个模块，别的文件访问不到自己文件的数据。如果需要暴露自己的数据，需要把数据放在 exports对象上，别的文件require时会得到exports对象。
3. 第三方模块：比如Express、art-template

### 模块加载规则：

+ 模块优先从缓存加载，一个模块A被加载后，会被放入缓存中，另一个模块B再次加载A模块时，会直接从缓存中得到A的数据。而无需再执行模块A的代码。
+ require("模块标识符")，模块标识符分为两种
  - 路径形式的模块标识符： 
    + ./	当前路径
    + ../   上一级路径
    + /      文件夹根路径下
    + C:/xxx   绝对路径
  - 非路径形式模块标识符
    - 核心模块的标识符就是直接模块名字 require("fs");
    - 第三方模块的标识符是包名，过程如下：
      - 先找到 node_module中的包名对应的文件夹
      - 找到该文件夹下的 package.json 文件
      - 再找到package.json 中的 main 属性，main 属性记录了该模块的入口模块文件
      - 找到该入口模块文件并且加载该文件，入口文件中会导入该文件夹下的其他模块，所以只要加载了入口模块就加载了整个第三方模块
      - 如果没有找到 package.json 或者main.js 就会寻找该目录下的 index.js,如果连 index.js也没有，则返回上一级目录，即node_module 寻找package.json ->main.js / index.js,直到磁盘根目录，没找到就报错
      - 当然，第三方包也可以使用路径加载，但是没必要。
      - 建议在每个项目的根目录生成一个 package.json 记录项目所依赖的包，和vue中的步骤一样

+ 所以最终的加载顺序是：缓存=》核心=》路径形式=》第三方模块

代码示例：使用文件的核心模块操纵文件

```javascript
//引入文件操作的核心模块 - fs
var fs=require('fs');
//使用该模块的功能
fs.readFile("./hellonode.js",function(error,data){
    if(error)
    console.log(error);
    else
    //读取到的是二进制文件，被转换成了十六进制，我们需要转成字符串
    console.log(data.toString());
});
```

代码示例：使用http的核心模块建立最简单的服务器

```javascript
//引入http的核心模块
var http=require("http");
//使用http创建一个服务器实例
var servise=http.createServer();
//定义服务器请求处理函数
servise.on("request",function(request,response){
    console.log("收到了客户端的请求");
    //第一个参数request是客户端请求的数据，包括请求的地址
    console.log(request.url);
    //第二个参数是对请求的回应，可以写入东西，返回给客户端
   response.write("hello");
   response.write("xiamin");
   //最后要结束回应，否则客户端会一直等待
   response.end();
});
//绑定端口号，开启服务器
servise.listen(3000,function(){
    console.log("服务器开启成功,你可以通过http://localhost:3000/进行访问");
});
```

代码示例：引用自己的定义的文件（在一个文件中，执行另一个文件的代码）

模块文件代码：

```javascript
console.log("我是 moduleA.js 的代码");
let name="夏敏";
//导出自己的数据，让其他模块使用，其他模块会得到exports对象
exports.name=name;
exports.age=18;

//你可以认为，每个模块文件都是一个module对象，module对象有一个成员对象 exports 
//module最后有一句
//return module.export;
//所以，如果你想直接暴露一个方法、一个变量、一个对象那你就可以这样，但是只能暴露一个东西
// module.exports=name;而不能是 exports=name;
//export只是 module.exports的引用，你给exports直接赋值就是重新实例化exports，那么exports将不
//再和module.exports共享地址，但是最后返回的是 module.exports
//好处就是，别人不需要使用对象.属性的方法拿数据，拿到的直接就是数据。
```

引用该模块：

```javascript
//加载该模块文件=>只执行该文件的代码
//require("./moduleA");
//加载该模块文件，并得到该模块暴露的数据=>既执行该模块的代码，又得到暴露的数据
let data=require("./moduleA");
console.log(data);
```

## 对后台的外链资源请求

一个html页面中，所有的外链资源[^外链资源]都需要对服务端进行一次请求，而不是直接写上路径就能访问到，我们需要对每一次请求进行处理，html页面才能拿到想要的数据。所以为了方便静态外链资源的请求，我们会把所有的资源放在根目录下的一个文件夹 public 中，html页面中的请求地址，要写成 /public/XXX，表示根路径 即 127.0.0.1:3000/下的public/XXX，后台再统一解决以  /public/ 开头的请求,其实node.js中，对资源的请求路径都不是文件路径，都是url路径。或者说，在node中，路径都是假的，路径只是一个口令，真正要资源还是得通过后台去别的地方取出来。

[^外链资源]:不在html页面同级的或子级的资源，就是不和html页面在同一个文件夹，需要使用 ../才能访问的资源

```javascript
 //处理静态外链资源
   if(req.url.indexOf("/public")===0){
        fs.readFile("./"+req.url,function(err,data){
            if(err)
            console.log("index.html");
            else
            res.end(data);
        })
   }
   //处理网页文件
   else{
    //拼接文件的路径
    let fileUrl="./www"+req.url;
    //如果没有明确文件名=》默认访问该路径下的index.html
    if(path.extname(fileUrl)==='')
        fileUrl=fileUrl+'index.html';
    //读取该文件的内容
    fs.readFile(fileUrl,function(err,data){
        if(err)
            data="404 Not found!";
        res.end(data);
    })
   }
```

## 网页重定向

网页重定向，直白一点就是网页跳转。比如后台处理完某个表单请求后，需要跳转到其他页面，就可以使用重定向进行网页的跳转。

1. 设置状态码为302=》告诉客户端，我们需要临时重定向了，301=》永久重定向
2. 在响应头中通过location告诉客户端需要跳转到哪个页面

代码：

```javascript
res.statusCode=302;
res.setHeadr("Location","/");//这里的 / 代表根路径 即 127.0.0.1:8080/
```

## 热重启插件

安装一个第三方工具--nodemon,可以在我们修改node代码后自动重启服务，即重新编译代码。

1. 安装插件

```cmd
npm i nodemon -g
```

2. 使用插件

```javascript
nodemon js文件
```

## nodejs的文件操作相对路径

```javascript
let fs=require("fs");
let path=require("path");
//两个关于文件路径的常量，类似于 php
//__dirname=>当前文件所在目录的绝对路径
console.log(__dirname);
//__filename=》当前文件所在的绝对路径
console.log(__filename);

//nodeJs中对文件路径的误解
//比如：读取文件时的文件路径，如若写相对路径，相对的并不是该js文件，而是执行js文件的终端所在的位置
//一般情况，我们开启服务都会进入项目文件夹，和js文件同级的目录，所以一般路径都没有错
fs.promises.readFile("./app.js").then((data)=>{
    console.log(data.toString());
},(err)=>{
    console.log("error----"+err);
})
//解决方法=》使用绝对路径处理 文件的读写,推荐以后的文件操作都，包括express的静态资源文件的路径都这样写
fs.promises.readFile(path.join(__dirname,"/app.js")).then((data)=>{
    console.log(data.toString());
},(err)=>{
    console.log("error----"+err);
})

```



# NodeJS的核心API

以后专门系统的学习一下 nodejs 的核心api

## 文件处理系统：fs

## Http服务：http

## 网页Url处理：url

## 文件路径处理：path





# Express的使用

1. 下载express
   - npm i express -S

2. 引入并使用express快速创建一个http服务器

```javascript
//引入模块
let express=require("express");

//创建一个服务器
let app=express();

//使用了框架后不需要自己去判断路径，框架会帮你处理，你只需要知道你想处理什么路径的请求就行

//定义服务器接收到get请求的且url 为 / 时处理函数
app.get('/',function(req,res){
    res.send("hello express");
});

//开启服务
app.listen(3000,function(){
    console.log("Runing ...");
});
```

3. 配置最简单的路由

   ```javascript
   //get代表get请求
   //第一个参数是url的地址，/ 代表根路径，第二个参数就是处理接收到该请求的处理函数
   app.get('/',function(req,res){
       res.send("hello express");
   });
   
   //post代表post请求
   //第一个参数是url的地址，/ 代表根路径，第二个参数就是处理接收到该请求的处理函数
   app.post('/',function(req,res){
       res.send("hello express");
   });
   ```

   

4. 使用express自动处理外链资源请求

```javascript
//处理 public 文件夹中的静态资源请求 =》公开一个文件夹的资源,自动处理html中对外链的请求
//指定当请求的url 以 /public/ 开头时，去当前文件夹的 public 去解析获取需要的外链资源
app.use("/public/",express.static("./public"));

//可以省略第一个参数，但是请求资源的时候，url就需要省略 /public/ 
//比如请求 /public/img/p1.jpg =>img/p1.jpg
//因为第一个参数其实不是真实路径，这只是一个url标识，用来验证请求的一个标识而已，第二个参数才是真的资源地址。

```

5. express中使用模板引擎
   1. 安装模板引擎 express-art-template

       
    ```
//express-art-template 是专门为了在express中使用的模板引擎，但是依赖art-template
//所以需要先安装 art-template
npm i art-template -S 
       npm i  express-art-template -S
    ```

​		   2. 使用模板引擎渲染文件

```javascript
//1、配置模板引擎=>告诉express使用的模板引擎是什么
//第一个参数是处理的文件的后缀名，可以改成html  
app.engine('art',require("express-art-template"));

//2、使用render函数渲染并且发送渲染后的页面给服务端
app.get('/',function(req,res){
//你书写的时候不要带路径，直接文件名，但是你的html页面必须放在根目录的views文件夹下,express会自动去views文件夹下找该文件，因为 views是默认的渲染文件夹
    
    res.render("index.art",{name:"xiamin",age:20});
    
    //如果你想修改默认的路径，则可以 
   // app.set("views",路径名称);
});
```

6. express的重定向

```javascript
app.get('/',function(req,res){
	res.redirect("url");//url中， / 就代表根路径
});
```

7. express中对post请求的处理---中间件的使用

   中间件就是类似于插件，中间件 body-parser 可以在express中帮助拿到 post 请求发送的参数

   7.1 安装中间件 body-parser

   ```javascript
   npm i body-parser -S
   ```

   7.2 引入、配置中间件

   ```javascript
   //引入中间件
   	let bodyParser=require("body-parser"); 
   //配置中间件 body-parser 
       app.use(bodyParser.urlencoded({extended:false}));
       app.use(bodyParser.json());
   ```

   7.3获取post请求的参数

   ```javascript
    app.post("/submit",function(req,res){
           var per=req.body;
           console.log(per);
           res.render("index.html",per);
       	//res.redirect("/");
   });
   ```

   

8. express中对 get 请求的处理

   ```javascript
   //get请求的参数不需要通过其他中间件处理，express内置了获取该参数的方法
   app.post("/submit",function(req,res){
           var json=req.query;
   });
   ```


9. express对路由模块的分离

   就是把对请求的处理放到其他文件中去，app.js只做一些服务的定义启动

*  路由文件的编写

  ```javascript
//1、引入一个express，但是不创建服务,只是用来包装路由
    let express=require("express");
//2、得到一个路由容器 router
    let router=express.Router();
//3、把路由都挂载到容器中
    router.get("/",function(req,res){
        res.send("router.js 模块加载成功：127.0.0.1:3030/");
    })
    router.get("/login",function(req,res){
        res.send("router.js 模块加载成功:127.0.0.1:3030/login");
    })
    router.get("/show",function(req,res){
        res.send("router.js 模块加载成功:127.0.0.1:3030/show");
    })
//4、把路由容器暴露出去
    module.exports=router
  ```

* 主模块加载路由模块的所有路由

```javascript
//1、得到路由容器
let router=require("./router")
let express=require("express");

//创建一个服务器
let app=express();

//2、路由处理交给 router.js,把路由挂载到服务当中
app.use(router);

//开启服务
app.listen(3000,function(){
    console.log("Runing ...");
});

//app模块只负责创建服务、开启服务。服务的请求处理都交给router.js
```

10. express对404页面的处理

    express中对路径的判断不是靠 if  else 进行判断，就是配置了的页面就有处理函数，那么对于没有配置的路径怎么做到统一处理呢？

```javascript
//不配置路径=》默认处理not found page=》写在所有处理请求的后面
app.use(function(req,res){
    //to do 
});
```



---

# 回调函数

**Node 所有 API 都支持回调函数**

如果想要在异步操作中，得到异步操作的结果，那就必须写回调函数。

```javascript
//回调函数就是用来处理 异步操作的结果，因为不知道何时才能拿到结果，所以不能在外部进行处理。
//但是处理的过程又不能写死，需要调用的时候来决定怎么处理
function getRandom3(callback){
    setTimeout(() => {
        var random=Math.random();
        callback(random);
    }, 3000);
}
//调用
getRandom3((random)=>{
    console.log(random);
});
```

# MongoDB

### 非关系型数据库

+ mongodb是非关系型数据库，与nodeJs、JavaScript可以很好的配合
+ 不用提前设计表结构，或者说没有表，非常的灵活
+ 有的非关系型数据库就是 键值对的形式
+ Mongodb是最像关系型的非关系型数据库
  - 关系型数据库=》非关系型数据库
  - 数据表=》集合、数组
  - 表记录=》文档对象

### 关系型数据库

+ 关系就是表，或者说，关系就是表与表之间的联系
+ 关系型数据库在操作前需要设计表结构
+ 而且数据表还支持约束

### MongoDB的安装、使用

#### 安装

+ 官网下载、复制下载链接到迅雷下载，浏览器太慢了
+ 安装不能闭着眼睛 ``next``,后面又一步 把 下载 mongoDBCompil.. ，一个数据库的图形化界面的 √ 去掉，下载太慢了
+ 检测是否安装成功 查询一下版本 mongod --version
+ 在C:根目录下建立一个文件夹  /data/db，因为默认数据库就是存储在根目录下的data/db中，如果你是在其他盘符下，启动数据库，就建立在其他盘符的根目录下

#### 使用

##### 启动数据库服务

```cmd
mongo	//默认连接
mongo mongodb://xiamin:123456@127.0.0.1:27017/admin //指定的用户名连接
```

##### 关闭数据库服务

CTRL + C   或者直接关闭控制台

##### 注册为服务

```cmd
管理员权限进入安装目录下的bin目录并下执行
mongod.exe --config "C:\Program Files\MongoDB\Server\4.2\bin\mongod.cfg" --install --serviceName "MongoDB"
查看服务中是否有 mongodb 的服务
进入浏览器 进入http://localhost:27017/
是否出现 
It looks like you are trying to access MongoDB over HTTP on the native driver port.
那就成功，可以像mysql一样在服务中打开、关闭mongobd服务
```

##### navicat连接mongoDB

连接选择 mongoDB =》建立连接就行

#### 基本命令

1. 查看所有数据库: ``show dbs``
2. 查看当前所在的数据库: ``db``
3. 切换到/新建指定的数据库：``use dbname`` 有则切换，无则新建
4. 插入数据：``db.集合名称.insertOne(数据)`` 集合有则使用，没则新建，数据可以是单个的对象，也可以是对象数组。

5. 查询某个集合的数据
   1. 查询某个数据库下的所有集合  ``show collections``
   2. 查询某个集合的数据 ``db.student.find()``

### node操作mogo

使用第三方包--mongoose 操作mongo数据库

下载第三方包：``npm i mongoose -S``

#### 基本操作

```javascript
//1、引入模块
let mongoose=require("mongoose");
//2、建立连接
mongoose.connect("mongodb://localhost/test",{});
//3、建立一个模型=》建立一个集合结构，集合名叫做 cat =>会自动转成小写
const Cat = mongoose.model('Cat', { name: String });
//4、实例化一个集合=》就是创建一个可以添加进该表的记录
const kitty = new Cat({ name: 'tom' });
//5、持久化该实例，将该记录保存在数据库中
kitty.save().then(() => console.log('meow'),()=>{ console.log("error")});
```

#### 建立集合模型--增

mongodb很灵活，没有表结构，也可以有表结构，可以建立某些约束

```javascript
//3、建立一个模型=》建立一个文档结构模型
    //3.1、建立集合约束
    var catsca = new mongoose.Schema({
        name:{//多个约束就写对象
            type:String,//类型约束
            required:true,//不为空约束
            unique:true//唯一值约束
        },
        age:Number,//只有类型约束直接写
        sex:{
            type:String,
            default:"男",//默认值约束
        }
    });
    //3.2、发布文档模型,第一步可以直接写对象在这里
    //第一个参数要求 首字母大写，会自动转成小写，会自动添加 s
    //第二个参数就是约束
    //返回值是一个构造函数，用来实例化对象
    const Cat = mongoose.model('Cat', catsca);
```

#### 查询语句

```javascript
//1、引入模块
let mongoose=require("mongoose");
//2、建立连接
mongoose.connect("mongodb://localhost/test");
//3、建立一个模型=》建立一个文档结构模型，不要求一模一样，至少属性不能少
const cat = mongoose.model('Cat',{name:String,sex:String,age:Number}); 
//4、查询=>第一个参数是条件，可以省略，就是查询全部
cat.find({name:"tom"},(err,data)=>{
    if(err)
    console.log("error",err);
    else
    console.log(data);
})
```

#### 删除语句

```javascript
//1、引入模块
let mongoose=require("mongoose");
//2、建立连接
mongoose.connect("mongodb://localhost/test");
//3、建立一个模型=》建立一个文档结构模型
const cat = mongoose.model('Cat',{name:String,sex:String,age:Number});  
//4、删除=>和查询语句差不多
cat.deleteMany({name:"tomm"},(err,res)=>{
    if(err)
    console.log("删除失败");
    else
    console.log("删除成功");
});
```

#### update语句

```javascript
//三个参数，第一个是条件，可以省略，代表集合的全部对象都被选择更新
//第二个参数是更新的数据
cat.updateMany({sex:"男"},function(err,res){
    if(err)
    console.log("更新失败");
    console.log(res);
});
```

#### 语法总结

增删改查的语法都差不多，find、remove、detele、update,打出来看下提示基本就知道什么意思。另外，参考手册就可以解决大部分问题。

在使用模块化开发的时候，增删改查的操作和定义数据库、建立模型分开写的话，只需要把建立的文档模型 暴露 出去，增删改查只需要得到那个文档模型（相当于得到了数据表）就行。

# mysql

下载第三方包--mysql

```cmd
npm i mysql -S
```

#### 使用

```javascript
//1、引入操作 mysql 的核心模块
let mysql=require("mysql");
//2、建立数据库连接
var connection = mysql.createConnection({
    host     : 'localhost',
    user     : 'root',
    password : '123',
    database : 'girls'
  });
connection.connect();
//操作数据库 connection.query(sql，function(){});=>增删改查都是这个函数
connection.query("select * from beauty",function(err,res,fileds){
    if(err)
    console.log("error=>查询失败！！",err);
    else
    console.log(res);
});
//关闭连接
connection.end();
```

# Promise

在node中基本异步的操作都支持promise，不需要自己去封装，比如：

+ 文件操作
+ 数据库操作

**你确定???**

# 中间件

中间件其实就是对路由请求的处理函数

#### 中间件原理

处理函数：分模块写在了另一个文件上

```javascript
//就是导出来一个函数，该函数可以拿到两个参数，并可以在那两个参数上添加属性
module.exports=function sum(req,res){
    req.sum={name:"xiamin",age:18};
    res.sum={name:"sisi",age:22};
};
```

调用过程：

```javascript
let sum=require("./middleware/sum");
let http=require("http");

http.createServer(function(req,res){
    //中间件就是一个方法，处理某件事情的方法，不同的是，中间件会把处理后的结果挂载到其他对象上
    sum(req,res);//给res 、req 添加属性
    if(req.url=="/")
    {
        console.log(req.sum,res.sum);
    }
}).listen(3000,()=>{
    console.log("port 3000 is Runing ...");
});

```

#### express的中间件

```javascript
//引入模块
let express=require("express");
let app=express();

//配置中间件
//app.use()=》知道服务器什么请求触发什么中间件，当然也可以用来配置路由请求啊
//同一个请求的req、res是同一个，所以中间件把处理的结果挂载到这两个对象身上后，你再处理请求，拿到的req、res就是有额外属性的对象了
//1、任何请求都会触发的中间件=>一般放在最后面，当作处理404的中间件
    //中间件有三个参数 请求对象、响应对象、下一个中间件
    app.use(function(req,res,next){
        console.log(`我是任何请求都会触发的方法1`);
        req.name="xiamin";
        res.name="sisi";
        next();//不调用是不会进入下一个中间件的，当然包括app.get()/post();他们只是严格的中间件
    });

//2、对路径有要求的中间件，对请求方式没有要求
app.use("/a",function(req,res,next){
    console.log(`/a/请求触发的中间件`);
    req.age=28;
    next();//不调用是不会进入下一个中间件的，或者真正处理请求的函数中比如app.get();
});

//3、app.get()、app.post()就是严格的app.use(),对路径、请求方式都有要求
app.get("/a",function(req,res){//也有next参数，但是我们一般用来配置路由，一个请求就一个处理就行了，
    console.log("message:"+req.name,res.name,req.age);
    res.send("hello express hello express");
});

//express特殊的中间件=》全局处理错误的中间件
    //可以是以上三种的任意一种，不同的是有四个参数
    //触发的条件就是 上一个发生出错的请求 使用 next(error);带上参数，这个中间件也要写在后面
    app.use(function(err,req,res,next){
        console.log(err);
    })

//开启服务
app.listen(3000,function(){
    console.log("Runing ...");
});
```

