### 配置npm

npm作为一个下载工具，下载地址是国外的地址，在国内下载速度很慢，所以需要更换成国内的下载镜像地址。

使用工具 nrm 更换下载镜像地址

```javaspript
npm i nrm  //下载 nrm 工具	npm i -g nrm
nrm ls   //显示下载地址
nrm use 地址	//切换使用某个地址 nrm use taobao
```

### webpack是什么

webpack是基于nodeJs的一个前端构建（打包、压缩、合并、混淆）工具。

作用：解决包与包之间的依赖关系，处理

### npm安装包

#### 安装下载命令

npm install 包名	缩写： npm -i 包名

#### 安装范围

1. npm install -g： 全局安装 	缩写：npm -i g

2. npm install  --save ：项目（“打包”、发布到生产环境时）需要下载的包，包的信息会写pakeage.json的dependencies中。缩写 ：-S
3. npm instal --save-dev：项目构建（开发时、运行时）需要下载的包，包的信息会写在pakeage.json的devDependencies中。缩写 ：-D

### webpack的基本使用

1. 初始化项目 npm init -y =》得到两个文件pakeage.json、package-lock.json。第一个文件里会记录我们项目需要使用到的包，每在该项目下执行一次有关包的下载，都会有相关的记录。我们执行 npm install 就会下载这个文件里记录的包。所以，我们项目需要拷贝给其他同事的时候不需要把下载好的包传递给他，只需要运行这个命令就可以自动下载。 npm init -y 快速初始化（yes 表示一路默认创建，还有 -f 表示 force）

2. 安装合适的本地webpack	 npm install webpack@版本号  --save-dev  =》因为不同项目使用的webpack版本可能不一样，但是你只能安装一个版本的全局webpack。一般我们都会在项目中安装本地的webpack

3. 打包相关文件 webpack 源文件路径 目标文件路径

4. 配置webpack打包快捷键，在项目根下建立一个文件 webpack.config.js，配置关于打包的源文件、目标文件的默认信息，参看WebpackVueJS 下的该文件，配置好后直接执行 webpack 就会自动把源文件打包给目标文件。webpack是基于node的工具，配置文件中可以使用任意的node语法，包括最后配置文件也只是用node语法暴露出一个对象。

5. 

     ```javascript
     module.exports = {
     					//入口文件
     					entry: "./src/main.js",//该路径相对于根路径
     					//输出文件（目标文件）
     					output: {
     						//__dirname=》文件所在的绝对路径，不是项目根目录的绝对路径
     						path: path.resolve(__dirname, "dist"),
     						filename: "bundle.js",
     						//publicPath:"dist/"//设置公共的路径，否则file-loader打包的文件，路径不对，但是把html文件打包进该文件夹后就不需要这样设置了
     					}
     }
     /*
     当我们在控制台，直接输入 webpack命令执行的时候，webpack做了以下几步:
     1．首先，webpack发现，我们并没有通过命令的形式，给它指定入口和出口
     2. webpack就会去项目的根目录中，查找一个叫做‘webpack . config.js`的配置文件
     3．当找到配置文件后，webpack会去解析执行这个配置文件，当解祈执行完配置文件后，就得到了配置文件
     导出的配置对象
     4.当webpack拿到配置对象后，就拿到了配置对象中，指定的入口和出口，然后进行打包构建;
     /*
     ```

### 映射webpack命令

可以简写终端的命令，在pakeage.json文件中的脚本属性script里添加内容，"别名":"命令" 在终端运行 npm run 别名 执行的就是该命令。 这样做还有一个好处，只要你全局安装了webpack，不管你在哪儿打开的终端，运行有关webpack的命令，都是执行的的全局webpack的命令，如果你在脚本中映射了该命令 那么脚本会优先执行本地的webpack命令。改变webpack配置文件路径或者文件名后，打包需要添加参数   --config 配置文件路径  。很麻烦，所以我们会把这个命令写在脚本中。

```json
 "build": "webpack --config ./config/pro.config.js",
```

### webpack-dev -server
安装运行时webpack-dev -server 插件工具，安装这个东西可以运行一次命令之后，就会在项目改变保存之后自动打包保，不用手动打包，因为这个我们是局部安装的，所以要把这个命令映射到脚本中执行 。要注意的是 和 webpack的打包不同，webpack是把打包好的文件 boundle.js 存放到物理磁盘中，我们可以找到这个文件，但是 webpack-dev -server 会把打包好的文件存在根目下的内存中，我们看不到这个文件，如果想要一运行这个服务自动打开浏览器可以加参数
     --open 	运行自动打开浏览器
     --port 8088 	端口号为 8088
     --contenBase src	一开始运行进入的文件夹 默认为根目录
     --hot	设置改变后文件以补丁的形式进行生成，可以降低什么什么，还可以实现浏览器无，刷新改变=》没有实现
      也可以在配置文件中进行配置： webpackServer{open:true,....}，但是还需要在插件项配置一个东西，高版本貌似不需要

**需要注意的是**：这个插件只是模拟打包，并没有生成真正的打包文件，最后运行没错需要再次执行 webpack 打包生成打包文件。

### webpack插件配置plugin

webpack有许多自带的插件，不需要安装，只需要去配置就行。插件的配置都是在 plugins:[] 这是一个数组，
先需要获取webpack的一个依赖项 webpack

```javascript
const webpack=require('webpack');
```

#### 自带的插件	

  ```javascript
//BannerPlugin：在打包完成的js文件中，生成一个类似版权声明的文字
     	plugins:[
     		new webpack.BannerPlugin("版权归夏敏所有")
     		]
  ```

#### 非自带的插件

```javascript
//html-webpack-plugin:将一个html文件打包进dist目录，一般就是把我们的入口的 index.html 文件打包进去，同时还会插入一个script标签 引用我们的入口js文件 bundle.js
     	//1、引入对象：
        const htmlWebpackPlugin=require('html-webpack-plugin');
     	//2、配置：
        new htmlWebpackPlugin({template:'./src/index.html'})
//uglifyjs-webpack-plugin：丑化js的插件，对打包后的js进行压缩、简写。js文件变得很丑很难读懂，但是节约空间啊
		//1、引入对象：
     	const uglifyjs=require('uglifyjs-webpack-plugin');
		//2、配置：
     	new uglifyjs()
```

### loader

webpack本身只能处理 js文件，像css之类的文件是处理不了的，但是 loader 可以把这些文件转化成webpack可以处理的有效模块

css文件的处理：css文件也可以当作一个模块，在入口文件中引入 require/ import  css from 文件路径 即可，但是这类文件webpack处理不了，需要loader进行转化

```java
import css from "./css/bodycolor.css"
```

#### 安装loader

不同的文件需要使用不同的loader，具体进https://www.webpackjs.com/   webpack中文网查看API
     		   npm i css-loader -D =》开发过程依赖就行，打包时都是webpack处理好的文件了

#### 配置loader

webpack.config.js的module的rule中配置loader
安装配置完发现样式依然不起作用，但是打包已经不报错了。因为css-loader只负责解析css文件，不会把这些样式加入到html中。我们还需要用到另一个loader =》 style-loader 将模块的导出作为样式添加到 DOM 中

 ```javascript
module: {
     	    rules: [
     	      {
     	        //使用正则表达式，匹配到css文件时，使用哪些loader
     	        test: /\.css$/,
     	        use: ['style-loader','css-loader' ]//使用多个loader 时，使用的顺序是从右向左，所以css-loader放在右边，因为要先解析再添加给Dom元素
     	      }
     	    ]
     	}
 ```

##### less文件的处理

less文件的处理需要两个东西：less-loader=>加载less文件  less=》解析less文件
配置loader：

```javascript
module: {
						rules: [{
								//使用正则表达式，匹配到解析css文件时，use 使用哪些loader
								test: /\.css$/,
								use: ['style-loader', 'css-loader']
							},
							{
								test: /\.less$/,
								use: [{
									loader: "style-loader" // creates style nodes from JS strings
								}, {
									loader: "css-loader" // translates CSS into CommonJS
								}, {
									loader: "less-loader" // compiles Less to CSS
								}]
							},
}
//     	loader数组中写对象的好处是，可以添加其他参数选项
```

##### 图片处理

图片处理分为两种，配置loader时会多一个参数 limit =》限制大小，如果没超过限制就使用 url-loader,超过限制使用 file-loader。而且file-loader只需要下载安装，不需要配置，只需要配置 url-loader就行

##### es6语法的处理

webpack默认只能处理一部分的ES6语法，一些更高级的语法也是无法直接解析、转换的。要想能转换所有的ES6语法，就需要借助babel-loder

es6语法转成es5
	需要三个东西：
		babel-loader：一个多语言处理loader
		babel-core:一个多语言处理核心
		babel-preset-es2015/babel-preset-env:这是一个配置文件，直接下前一个不需要配置，后一个要手动配置

```javascript
test: /\.js$/,
//排除这两个文件夹的文件
exclude: /(node_modules|bower_components)/,
use: {
    loader: 'babel-loader',
        options: {
            presets: ['es2015']
        }
}
```





需要注意的是，不要让这个loder扫描到了node_modules中的js文件，太消耗资源了。

10、配置文件的分离：
	运行和打包都需要的配置、运行时需要的配置（不包含相同的部分）、打包时需要的配置（不包含相同的部分）=》三个文件
	运行的配置文件：共同+运行时需要的配置（不包含相同的部分）
	打包的配置文件：共同+打包时需要的配置（不包含相同的部分）
	怎么把两个配置文件合并呢？
	webpack-merge=>一个插件，将两个配置文件进行合并
	示例将共享+运行时需要的配置（不包含相同的部分）合并，步骤
	1、在运行的配置文件获取插件对象、共同配置文件的对象
		const Merge=require(webpack-merge);
		const exe=require(共同配置文件的路径);
	2、使用插件合并，
		module.exports=Merge(共同配置文件的对象,{

			//运行时独有的配置写这里，和以前的配置写法一致	
						
			})
	处理完后，执行的时候程序会找不到配置文件，因为默认的配置文件名是固定的。我们需要指定
	打包=》其实就是指令 webpack =》在脚本中指定参数 --config ./build/prod.config.js =>指令打包时的文件
	运行=》其实就是指令 webpack-dev-server=》在脚本中加参数  --config ./build/dev.config.js	
11、配置上的路径问题：
	配置时的相对路径都是相对于根目录。入口路径entry newhtmlWebpackPlugin({template:'./src/index.html'})模板上的路径都是相对于根目录而言
	使用绝对路径则不同，比如output，是什么就是什么。从C盘开始找起

### vue模块的引入：

​	1、下载vue 
​	2、引入vue import Vue from 'vue'
​	3、配置Vue 在wenpack的配置文件夹下配置，指定引入Vue的版本是 runtime-compiler=》运行时可以出现模板（就是自定义的组件标签），而不是runtime-only。
如果不进行配置，那么用渲染的方式也是可以实现添加组件进入页面的
vue文件的处理：
​	webpack处理不了.vue文件，想要使用vue文件要下载安装loader，并且配置
​	npm i vue-loader vue-template-compiler -D