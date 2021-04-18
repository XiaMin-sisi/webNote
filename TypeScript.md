### typescript简介

typescript：是JavaScript的超集，集成了es5 +es6  加强了js的语法

typescript的强类型：=》js是一种弱类型的语言

#### 安装typescript环境

使用typescript,需要安装编译环境

```javascript
//全局安装 typescript
npm install typescript -g    
```

#### 编译 typescript文件

```cmd
tsc filename
```

#### vs 自动编译

```cmd
//1.生成配置文件 tsconfig.json
	tsc --init
//2.修改配置文件中的 outDir  即编译后的js文件放在哪里，默认就是当前文件夹下
//3.编译一次
//4. 点击 终端  -》运行任务 -》typescript  -》tsc监视
//修改保存ts文件后，会自动编译、保存js文件
```

-----

### 数据类型

typescript中为了使编写的代码更规范，更有利于维护，增加了类型校验，在typescript中 主要给我们规定了变量的数据类型

#### 基本数据类型

1. 布尔类型( boolean)

   ```typescript
   let flag:boolean=true;
   ```

2. 数字类型( number)

   ```typescript
   let num:number=6;//不区分 int float
   let num:number=NaN;
   ```

3. 字符串类型(string)

    ```typescript
   var str:string="xiamin";
   ```

4. 数组类型(array)

   ```typescript
   //两种方法都可以，要求数组中类型与指定类型一致，数组泛型可以使用联合类型指定数组的类型
   let arr:number[]=[1,2,3];
   let sarr:Array<string>=["xiamin","18","man"];
   let arr3:Array<string|number>=[1,2,3];
   ```

5. 元组类型(tuple)：*特殊的数组,数组里元素的类型可以不一样，要指定每一种的数据类型*，就像是表示函数的参数一样。

   元组类型允许表示一个**已知元素数量和类型的数组**。

   **使用 ？代表可选，可选必选放在后面**

   ```typescript
   let yarr:[number,string]=[22,"sisi"];
   
   let yarr2:[number,?string,?boolean];
   	yarr2=[2]
   	yarr2=[2,"2"]
   	yarr2=[2,"2",true]
   
   yarr[3]="xiamin"//低版本的好像可以越界添加元素，现在会编译出错。最好也不要越界。如果确定不了数量就使用数组嘛。
   ```

6. 枚举类型( enum)：

   将数值、字符串语义化，比如我们经常使用的状态码，statuscode=number;200代表正确，100代表错误。光看代码很难联想到 这两个数值的语义。所以我们可以用字符串来表示数值。

   ```typescript
   /*  
   enum 枚举名{
   标识符[=整型常数]，
   标识符[=整型常数]，
   标识符[=整型常数]，
   }
   */
   
   //定义一个状态码枚举类型  200 表示 ok   404 表示 notFound
   	enum statu{
       	ok=200,
       	notFound=404，
   	};	
   //正常情况下 返回1
       return statu.ok;
   //不正常情况下 返回404
   	return statu.notFound;
   
   //定义一个状态颜色枚举
   	enum colorEnum{
       	primary="blue",
       	dangerous="red",
       	success="green"
   	}
   	let dangerous:colorEnum=colorEnum.dangerous;
   	console.log(colorEnum.primary)
   
   //不进行赋值的话，值就等于索引值,如果上一个赋值了，就是上一个值 +1
   enum color{red,blue,green=5,black};//1 2 5 6
   //如果上一个不是数值，那么下一个就一定需要赋值
   enum test{tt='xx',yy=22};
   ```

7. 任意类型 any

   *可以是任意一种类型。如果你要定义一个js中的对象，就需要使用 any，**typascript没有 object 类型***  ,虽然说没有对象这种数据集类型，但是并不妨碍我们使用，**js怎么定义、使用对象，typescript就怎么使用**。

   ```typescript
   let obj:any=window;
   ```

8. null和undefined

   **null 和 undefined 是其他数据类型的子类型，就是说可以使用这两个给其他类型赋值**

   ```typescript
   //可以和其他类型一起写
   //如果你不赋值会报错，写上空类型就不会
   let ss:null|undefined|string;
   ```

9. void类型

   声明一个`void`类型的变量没有什么大用，因为你只能为它赋予`undefined`和`null`，一般用于函数的返回值。

   ```typescript
   //没有任何类型，一般用于函数没有返回值 定义函数使用，表示没有返回值
   function showss():void{
   	console.log(ss);
   };
   ```

10. never类型

    *从不会出现的类型=>null、undefined是它的子类型*

    ```typescript
    //一般用在不知道会是什么类型的情况，比如抛出异常的返回值之类，很少有函数
    ```

11. 未指定类型

    定义变量时没有指定数据类型，也没有初始化，默认为 any。

    ```typescript
    let any;	// 	let any:any;
    ```

    定义变量时未指定数据类型，但是进行了初始化操作，默认为初始化时的数据类型。

    ```typescript
    let name="xiamin";	//	let name:string='xiamin'
    ```

#### 非基本数据类型 --对象

**object** 类型，就是我们所熟悉的对象，不是基本数据类型。

```tsx
let person:object={
    name:'xiaMin'
}
console.log(person)
```

如果想要约束对象属性的数据类型，则可以使用接口。

#### 类型断言

有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。

通过*类型断言*这种方式可以告诉编译器，“**相信我，我知道自己在干什么**”。 类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。 TypeScript会假设你，程序员，已经进行了必须的检查。

类型断言有两种形式。 其一是“尖括号”语法：

```typescript
let obj:string|number;

fun=():string|number=>{return  "13"}

obj=fun();

//此时编译的时候 tsc 不知道 obj 是 string 还是 number ，length不是两种类型的数据共有的数据，所以编译会报错 
//console.log(obj.length)

//使用断言
console.log((<string>obj).length)
```

另一个为`as`语法：

```typescript
let obj:string|number;

fun=():string|number=>{return  "13"}

obj=fun();//此时编译的时候 tsc 不知道 obj 是 string 还是 number ，length不是两种类型的数据共有的数据，所以编译会报错  

console.log( (obj as string).length )
```

两种形式是等价的。 至于使用哪个大多数情况下是凭个人喜好；然而，**当你在TypeScript里使用JSX时，只有`as`语法断言是被允许的**。

### 函数

typescript的函数和高级语言一样 需要指定返回值类型,参数也需要指定类型。没有返回值类型就是 void

#### 非匿名函数

```javascript
function showName_Age(name:string,age:number):string{
		console.log(`name:${name},age:${age}`);
		return "success";
	};
showName_Age("夏敏",18);

//指定函数没有返回值=》void
function sayHello():void{
    console.log("hello");
};
sayHello();
```

#### 匿名函数

```typescript
let fn=function():void{
	console.log("fn");
}
fn();
```

#### 可选参数

js写法中形参和实参数目可以不一样，但是ts中必须一样。但是可以用配置可选参数 参数后面跟上 ? 代表可能没有

```typescript
function setMessage(name:string,age?:number):void{
		if(age)
		{
			console.log(`name:${name},age:${age}`);
		}
		else
		console.log(`name:${name},age:保密`);
	}
	setMessage("虚拟",18);
	setMessage("思思");
```

#### 剩余参数

和es6中的写法一样。把实参转换为一个数组，需要为数组指定类型，如果参数类型不确定就用 any

```typescript
function count(...arr:number[]):number{
		let sum:number=0;
		for(var i=0;i<arr.length;i++)
		sum=sum+arr[i]
		return sum;
	}
	console.log(count(1,2,3));//6
```

#### 重载

typescript的重载我觉得不是很好，需要自己通过参数个数、类型去判断到底执行哪个函数。

```typescript
function test(name:string):void;
function test(age:number):void;
function test(par:any):void{
    if(typeof par=="string")
        console.log("我的名字是："+par);
    else
        console.log("我的年龄是："+par);
}
test(18);
```

### 类

#### 类的定义

```typescript
class Person{
		//属性的声明，默认是 public
		private	name:string;
		public	age:number;
		//构造函数的定义=》实例化时自动触发
		constructor(n:string,a:number){
			this.name=n;
			this.age=a;
		};
		//方法的定义 这里get /set 和es6中的不一样，单纯的成员函数，不会自动触发
		getName():string{
			return this.name;
		};
		setName(n:string):void{
			this.name=n;
		};
	}
```

#### 实例化对象

```typescript
let p1=new Person("夏敏",18);
console.log(p1.getName());//实例化的也对象只能访问public属性方法
console.log(p1.age);
```

#### 属性修饰符

public : 内部、外部、子类都能访问

protected : 内部、子类能够访问

private : 只有内部可以访问

#### 类的继承

和 java 一样，没记错的话。

##### 继承什么

public 和 protected 的属性方法都会被继承。

##### 重写方法

写同名的方法，就会覆盖父类的方法。

##### 重写方法时调用父类同名方法

super();这个函数就是父类的同名函数，参考下面代码，重写构造函数的代码，调用了父类的构造函数。

```typescript
class student extends Person{
		num:number;//子类自己的属性
		constructor(n:string,a:number,num:number){//可以重写构造函数
			super(n,a);//调用父类的构造函数
			this.num=num;
		}
	};
```

#### 类的静态方法、属性

通过关键字 static 定义的属性或者方法。称为 静态属性 。只能通过类名调用，**实例对象不能调用静态属性。静态方法中不能直接访问类的其他属性，只能访问静态属性**

```typescript
class test2{
		age:number;
		//定义静态属性
		static tname:string="虚拟";
		//定义静态方法=>静态方法中不能直接访问类的其他属性，只能访问静态属性
		static showname():void{
			console.log(test2.tname);
			//console.log(this.age);//=》报错
		}
		constructor(age:number){
			this.age=age;
		}
	}
//调用类的静态属性
console.log(test2.tname);
//调用类的静态方法
test2.showname();
```

#### 抽象类

由关键字abstract定义的类，不能实例化，**只能由子类进行实例化，子类必须实现父类的所有抽象函数**。**抽象类一定要含有抽象方法**，可以用已经实现的方法。**抽象方法只能在抽象类中出现**。

##### 抽象方法

抽象方法就是啥都没有就一个名字

```typescript
abstract class xuni{
	abstract saysomething():any;//抽象方法的定义
    //也可以用已经实现的方法
	sayhello():void{
		console.log("hello");
	}
}
```

##### 实现抽象类

实现抽象类就是继承抽象类，并且把抽象类中的抽象方法都进行实现。实现之后的类就是可以进行实例化的类

```typescript
//继承并实现抽象方法
class shili extends xuni{
	saysomething():void{
		console.log(`saysomething:no what hao say`);
	}
}
//实例化一个子类的对象
let sl1=new shili();
sl1.saysomething();
```

### 接口

行为和动作的规范。说白了就是**一种自定义的数据类型**。

##### 属性接口

就是规定了数据类型的 json。比如 定义个 名字的数据类型，由 姓  名 两部分组成，两部分都是 string类型

```typescript
interface FullName{
    //规定json的属性名、属性类型
    firstName:string;
    lastName:string;
    smallName?:string//=>接口中也可以设置可选参数
};
```

当你想要写一个人的姓名时，就去实现这个接口，按照规范进行赋值。即 定义一个这种类型的变量

```typescript
//定义一个变量 变量名：myname 变量类型： FullName  
let myname:FullName={
		firstName:"夏",
		lastName:"敏"
	}
//用属性接口 当作函数的参数。 就是函数的参数 类型是 FullName 呗
function showFullName(name:FullName):void{
    console.log(`fullname:${name.firstName}${name.lastName}`);
}
showFullName(myname);
```

###### 只读属性

如果你定义的某个对象，有些属性，只能在初始化时进行赋值，不能进行修改，我们可以设置属性为只读属性。

比如某个对象的其他属性都可以进行修改，只有 id 唯一标识不能进行修改。

```typescript
interface FullName{
    firstName:string;
    lastName:string;
    smallName?:string;
    readonly  id:string; //使用 readonly标识为只读
};
```

TypeScript具有`ReadonlyArray<T>`类型，它与`Array<T>`相似**，只是把所有可变方法去掉了**，因此可以确保数组创建后再也不能被修改：

```

let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
```

上面代码的最后一行，可以看到就算把整个`ReadonlyArray`赋值到一个普通数组也是不可以的。 但是你可以用类型断言重写：                

```
a = ro as number[];
```

##### 函数类型的接口

规定函数的参数个数、参数类型、返回值类型。就是说你要定义一个我这种类型的函数，就必须照着我的标准写。

```typescript
//定义函数接口
interface infn{
//括号里面是参数，规定参数的个数,类型，当然也可以用可选参数，参数名可以不一样，外面规定的是返回值的类型
	(par1:string,par2:number):string
}
//实现这种函数接口=》就是按照这种规范定义一个函数
let fun1:infn=function(name:string,age:number):string{
    return `名字：${name},年龄：${age}`;	
}
```

##### 索引接口

规定数组、对象的key和value的数据类型，第一个属性接口，是规定 key的名字，和value的类型，不一样。

```typescript
interface myarr{
	//约定了数组索引值(key)是数值类型，value是字符类型。但是吧，数组的索引可以是其他类型吗？
	[myindex:number]:string
}
let arr:myarr=["hello","xiamin"];

interface myarr{
	//约定了对象索引值(key)是string类型，value是字符类型。但是吧，对象的索引可以是其他类型吗？
	[myindex:string]:string
}
let arr:myarr={name:"xiamin"};
```

#### 类接口

对类进行约束，规定类的属性和方法的名称、类型，接口规定的一定要有，你也可以有自己的东西。

##### 类接口的定义

```typescript
interface animal{
		name:string;
		eat():void
}
```

##### 类接口的实现

使用关键字 implements 进行实现，接口中有的必须按照规范进行实现，也可以添加自己的属性方法。

```typescript
class dog implements animal{
		name:string="旺财";
		eat():void{
			console.log("旺财要吃?");
		};
		//添加自己的属性方法
		age:number=2;
		sayHello():void{
			console.log("汪汪汪~");
		}
	}
```

##### 类接口的继承

类接口可以继承，有叫做接口的扩展。

```typescript
interface Person extends animal{
		work():void;
}
//实现Person这个接口的时候就必须把animal的接口都实现
//而且一个类可以继承一个类的同时实现多个接口，和java差不多，java不支持多继承，但是支持多实现接口
```

### 泛型

泛型就是用一个变量暂时代替类型，调用的时候再由调用者传入泛型的值。如果想在调用函数的时候再指定函数的参数类型，返回值类型，就可以使用泛型。可以使用any代替泛型，但是不规范。不规范也能用。

#### 泛型函数

用变量暂时代替参数、返回值的类型，调用者调用时需要除了传入函数的参数，还需要传入泛型的类型。

##### 定义泛型函数

```typescript
//可以有多个泛型，用 ，分隔
function saysomething<T,X>(something:T):T{
		return something;
}
```

##### 调用泛型函数

```typescript
console.log(saysomething<string,number>("hello"));

 console.log(saysomething<number,number>(123));
```

#### 泛型类

类的某些属性类型不确定，类的函数参数、返回值类型不确定。用泛型代替。

```javascript
//可以有多个泛型，用 ，分隔
class test<T>{
    par1:T;
    constructor(p:T){
        this.par1=p;
    }
    getPar():T{
        return this.par1;
    }
}
//创建实例的同时，给泛型赋值
let obj=new test<number>(18);
```

#### 泛型接口

一样，就是用变量暂时代替类型，使用的时候需要传入泛型的值。

```typescript
interface myfn<T>{
		(par1:T):T
	}
//实现泛型接口,既要满足接口的条件，又要满足泛型的参数限制，比如参数和返回值的类型一致。注意，你要实现一个泛型接口，那么你要实现的是函数也好，类也好，也应该是一个泛型。就像下面这个 右边的实现函数也是一个泛型函数
	function show<T>(message:T):T{
		return message;
	}
	let fn:myfn<number>=show;
```

### 模块

和ES6的模块化一模一样。注意，我说的是一模一样

### 命名空间

typescript 就是为了解决大型项目中，因为多人协作之间出现问题，比如数据类型的接口、模块等。但是多人协作很有可能出现命名重复的事情，这时候就需要命名空间来解决问题了。

命名空间=>为了使变量不会出现命名冲突。**命名空间内部的东西都是私有的，外界需要使用的话，需要像模块一样export出去**

##### 定义命名空间

使用关键字 namespace 定义命名空间,把需要暴露的数据导出。

```typescript
namespace A{
	export let name:string="夏敏";
	export function showname(name:string):void{
		console.log(`我的名字是${name}`);
	}
}
```

#### 外部使用命名空间的数据

```typescript
// 命名空间.属性/方法名
A.showname("sisi");
```

##### 和模块搭配使用

模块的使用就是为了多人协作，难免两个不同的模块可能会出现同名的属性，你在同一个模块中导入这两个模块就会出现命名冲突。但是如果我们模块导出的是命名空间，导入的模块只需要得到命名空间，就可以使用命名空间所有导出的数据，而且保证命名空间不重名相对简单，使用别人模块时带上命名空间前缀，就不会出现命名冲突问题

```typescript
//把命名空间导出，这个 export 是模块的导出
export namespace A{
	export let name:string="夏敏";
	export function showname(name:string):void{
		console.log(`我的名字是${name}`);
	}
}
//其他模块拿到命名空间，并使用该命名空间中暴露的属性方法。
import {A} from "./07-namespace"
A.showname(A.name);    
```

### 装饰

装饰器是一种特殊的声明类型，能够附加到类、方法、属性或参数上。可以修改类的行为。  通俗的讲，修饰器就是一个方法。

##### 定义装饰器

装饰器就是一个方法，方法怎么定义，装饰器就怎么定义。

##### 装饰器的使用

语法 ：在需要进行修饰类、属性、方法的前一行写上  @装饰器的名字

#### 类装饰器

不修改类的定义情况下修改类的结构，动态改变、扩展类的功能

##### 类装饰器的定义

```typescript
 function addsomethig(params:any):void{//注意这里面的参数params就是被装饰的类 即类本身
	//通过params给类的原型链添加属性
	params.prototype.name="夏敏";
	//通过params给类的原型链添加方法
	params.prototype.sayhello=function():void{
		console.log("hello");
	}
	//甚至可以重写这个类，
	// return class extends params{
	// 	//在这里重写这个类
	//};
}
```

##### 装饰某个类

```typescript
@addsomethig
class person{
	constructor(){}
}
let p=new person();
console.log(p.name);
p.sayhello();
```

#### 装饰器工厂

上面那种装饰器是一般的装饰器，没有办法传参，装饰器工厂可以进行传参。

##### 装饰器工厂的定义

```typescript
function add(name:string):any{//这里是自己要传入的参数
	
	return function(par:any){//这个参数就是被修饰的东西
		//通过params给类的原型链添加属性
		par.prototype.name=name;
		//通过params给类的原型链添加方法
		par.prototype.sayhello=function():void{
			console.log("hello"+name);
		}
	};
}
```

##### 装饰器工厂的使用

```typescript
@add("夏敏")
class dog{
	constructor(){}
}
let d=new dog();
console.log(d.name);
d.sayhello();
```

#### 属性装饰器

##### 属性装饰器的定义

```typescript
//参数一：如果是静态属性那么这个参数代表类的构造函数，如果是普通成员属性，那么这个属性就代表 类的原型，即类本身。毫无疑问我们又可以改变类的结构了
//参数二：自然就是装饰的属性名(写在哪个属性的上一行，属性名就是谁)
function add(par1:any,par2:any){
    console.log(par1);
    console.log(par2);
    //通过原型链可以修改属性的值
    par1[par2]="夏敏";
    //添加其他属性
    par1["age"]=18;
}
```

属性装饰器的使用

```typescript
class Per{
    @add
    name:string;
    constructor(){}
}
let pp=new Per();
console.log(pp.name);//夏敏
console.log(pp.age); //18
```

同样，如果想带参数，就使用装饰器工厂。

#### 类方法修饰器

##### 类方法修饰器的定义

```typescript
//第一个参数:如果是静态属性那么这个参数代表类的构造函数，如果是普通成员属性，那么这个属性就代表类的原型，即类本身
//第二个参数:函数的名字
//第三个参数:方法的描述
function add2(par1:any,par2:any,par3:any){
    console.log(par1);
    console.log(par2);
    console.log(par3.value);//=>par3是一个对象，里面有一个参数value，就是该方法
    //修改装饰的该方法
    //1、保存原先的方法
    let me=par3.value;
    //2、修改该方法
     par3.value=function(){
     //还可以把原来的方法放到型方法中执行。
     me();
     console.log("夏敏");
        }
}
```

##### 类方法修饰器的使用

```typescript
class Per2{
    constructor(){};
    @add2
    sayHello(){
        console.log("hello");
    }
}
let pp2=new Per2();
pp2.sayHello();
```

#### 装饰器的执行顺序

属性=》方法=》方法参数=》类。**如果有多个同级的装饰器，会先执行后面的**