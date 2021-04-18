### typescript���

typescript����JavaScript�ĳ�����������es5 +es6  ��ǿ��js���﷨

typescript��ǿ���ͣ�=��js��һ�������͵�����

#### ��װtypescript����

ʹ��typescript,��Ҫ��װ���뻷��

```javascript
//ȫ�ְ�װ typescript
npm install typescript -g    
```

#### ���� typescript�ļ�

```cmd
tsc filename
```

#### vs �Զ�����

```cmd
//1.���������ļ� tsconfig.json
	tsc --init
//2.�޸������ļ��е� outDir  ��������js�ļ��������Ĭ�Ͼ��ǵ�ǰ�ļ�����
//3.����һ��
//4. ��� �ն�  -���������� -��typescript  -��tsc����
//�޸ı���ts�ļ��󣬻��Զ����롢����js�ļ�
```

-----

### ��������

typescript��Ϊ��ʹ��д�Ĵ�����淶����������ά��������������У�飬��typescript�� ��Ҫ�����ǹ涨�˱�������������

#### ������������

1. ��������( boolean)

   ```typescript
   let flag:boolean=true;
   ```

2. ��������( number)

   ```typescript
   let num:number=6;//������ int float
   let num:number=NaN;
   ```

3. �ַ�������(string)

    ```typescript
   var str:string="xiamin";
   ```

4. ��������(array)

   ```typescript
   //���ַ��������ԣ�Ҫ��������������ָ������һ�£����鷺�Ϳ���ʹ����������ָ�����������
   let arr:number[]=[1,2,3];
   let sarr:Array<string>=["xiamin","18","man"];
   let arr3:Array<string|number>=[1,2,3];
   ```

5. Ԫ������(tuple)��*���������,������Ԫ�ص����Ϳ��Բ�һ����Ҫָ��ÿһ�ֵ���������*�������Ǳ�ʾ�����Ĳ���һ����

   Ԫ�����������ʾһ��**��֪Ԫ�����������͵�����**��

   **ʹ�� �������ѡ����ѡ��ѡ���ں���**

   ```typescript
   let yarr:[number,string]=[22,"sisi"];
   
   let yarr2:[number,?string,?boolean];
   	yarr2=[2]
   	yarr2=[2,"2"]
   	yarr2=[2,"2",true]
   
   yarr[3]="xiamin"//�Ͱ汾�ĺ������Խ�����Ԫ�أ����ڻ����������Ҳ��ҪԽ�硣���ȷ������������ʹ�������
   ```

6. ö������( enum)��

   ����ֵ���ַ������廯���������Ǿ���ʹ�õ�״̬�룬statuscode=number;200������ȷ��100������󡣹⿴����������뵽 ��������ֵ�����塣�������ǿ������ַ�������ʾ��ֵ��

   ```typescript
   /*  
   enum ö����{
   ��ʶ��[=���ͳ���]��
   ��ʶ��[=���ͳ���]��
   ��ʶ��[=���ͳ���]��
   }
   */
   
   //����һ��״̬��ö������  200 ��ʾ ok   404 ��ʾ notFound
   	enum statu{
       	ok=200,
       	notFound=404��
   	};	
   //��������� ����1
       return statu.ok;
   //����������� ����404
   	return statu.notFound;
   
   //����һ��״̬��ɫö��
   	enum colorEnum{
       	primary="blue",
       	dangerous="red",
       	success="green"
   	}
   	let dangerous:colorEnum=colorEnum.dangerous;
   	console.log(colorEnum.primary)
   
   //�����и�ֵ�Ļ���ֵ�͵�������ֵ,�����һ����ֵ�ˣ�������һ��ֵ +1
   enum color{red,blue,green=5,black};//1 2 5 6
   //�����һ��������ֵ����ô��һ����һ����Ҫ��ֵ
   enum test{tt='xx',yy=22};
   ```

7. �������� any

   *����������һ�����͡������Ҫ����һ��js�еĶ��󣬾���Ҫʹ�� any��**typascriptû�� object ����***  ,��Ȼ˵û�ж����������ݼ����ͣ����ǲ�����������ʹ�ã�**js��ô���塢ʹ�ö���typescript����ôʹ��**��

   ```typescript
   let obj:any=window;
   ```

8. null��undefined

   **null �� undefined �������������͵������ͣ�����˵����ʹ�����������������͸�ֵ**

   ```typescript
   //���Ժ���������һ��д
   //����㲻��ֵ�ᱨ��д�Ͽ����;Ͳ���
   let ss:null|undefined|string;
   ```

9. void����

   ����һ��`void`���͵ı���û��ʲô���ã���Ϊ��ֻ��Ϊ������`undefined`��`null`��һ�����ں����ķ���ֵ��

   ```typescript
   //û���κ����ͣ�һ�����ں���û�з���ֵ ���庯��ʹ�ã���ʾû�з���ֵ
   function showss():void{
   	console.log(ss);
   };
   ```

10. never����

    *�Ӳ�����ֵ�����=>null��undefined������������*

    ```typescript
    //һ�����ڲ�֪������ʲô���͵�����������׳��쳣�ķ���ֵ֮�࣬�����к���
    ```

11. δָ������

    �������ʱû��ָ���������ͣ�Ҳû�г�ʼ����Ĭ��Ϊ any��

    ```typescript
    let any;	// 	let any:any;
    ```

    �������ʱδָ���������ͣ����ǽ����˳�ʼ��������Ĭ��Ϊ��ʼ��ʱ���������͡�

    ```typescript
    let name="xiamin";	//	let name:string='xiamin'
    ```

#### �ǻ����������� --����

**object** ���ͣ�������������Ϥ�Ķ��󣬲��ǻ����������͡�

```tsx
let person:object={
    name:'xiaMin'
}
console.log(person)
```

�����ҪԼ���������Ե��������ͣ������ʹ�ýӿڡ�

#### ���Ͷ���

��ʱ������������������������TypeScript���˽�ĳ��ֵ����ϸ��Ϣ�� ͨ����ᷢ�����������֪��һ��ʵ����б����������͸�ȷ�е����͡�

ͨ��*���Ͷ���*���ַ�ʽ���Ը��߱���������**�����ң���֪���Լ��ڸ�ʲô**���� ���Ͷ��Ժñ����������������ת�������ǲ�������������ݼ��ͽ⹹�� ��û������ʱ��Ӱ�죬ֻ���ڱ���׶������á� TypeScript������㣬����Ա���Ѿ������˱���ļ�顣

���Ͷ�����������ʽ�� ��һ�ǡ������š��﷨��

```typescript
let obj:string|number;

fun=():string|number=>{return  "13"}

obj=fun();

//��ʱ�����ʱ�� tsc ��֪�� obj �� string ���� number ��length�����������͵����ݹ��е����ݣ����Ա���ᱨ�� 
//console.log(obj.length)

//ʹ�ö���
console.log((<string>obj).length)
```

��һ��Ϊ`as`�﷨��

```typescript
let obj:string|number;

fun=():string|number=>{return  "13"}

obj=fun();//��ʱ�����ʱ�� tsc ��֪�� obj �� string ���� number ��length�����������͵����ݹ��е����ݣ����Ա���ᱨ��  

console.log( (obj as string).length )
```

������ʽ�ǵȼ۵ġ� ����ʹ���ĸ�������������ƾ����ϲ�ã�Ȼ����**������TypeScript��ʹ��JSXʱ��ֻ��`as`�﷨�����Ǳ������**��

### ����

typescript�ĺ����͸߼�����һ�� ��Ҫָ������ֵ����,����Ҳ��Ҫָ�����͡�û�з���ֵ���;��� void

#### ����������

```javascript
function showName_Age(name:string,age:number):string{
		console.log(`name:${name},age:${age}`);
		return "success";
	};
showName_Age("����",18);

//ָ������û�з���ֵ=��void
function sayHello():void{
    console.log("hello");
};
sayHello();
```

#### ��������

```typescript
let fn=function():void{
	console.log("fn");
}
fn();
```

#### ��ѡ����

jsд�����βκ�ʵ����Ŀ���Բ�һ��������ts�б���һ�������ǿ��������ÿ�ѡ���� ����������� ? �������û��

```typescript
function setMessage(name:string,age?:number):void{
		if(age)
		{
			console.log(`name:${name},age:${age}`);
		}
		else
		console.log(`name:${name},age:����`);
	}
	setMessage("����",18);
	setMessage("˼˼");
```

#### ʣ�����

��es6�е�д��һ������ʵ��ת��Ϊһ�����飬��ҪΪ����ָ�����ͣ�����������Ͳ�ȷ������ any

```typescript
function count(...arr:number[]):number{
		let sum:number=0;
		for(var i=0;i<arr.length;i++)
		sum=sum+arr[i]
		return sum;
	}
	console.log(count(1,2,3));//6
```

#### ����

typescript�������Ҿ��ò��Ǻܺã���Ҫ�Լ�ͨ����������������ȥ�жϵ���ִ���ĸ�������

```typescript
function test(name:string):void;
function test(age:number):void;
function test(par:any):void{
    if(typeof par=="string")
        console.log("�ҵ������ǣ�"+par);
    else
        console.log("�ҵ������ǣ�"+par);
}
test(18);
```

### ��

#### ��Ķ���

```typescript
class Person{
		//���Ե�������Ĭ���� public
		private	name:string;
		public	age:number;
		//���캯���Ķ���=��ʵ����ʱ�Զ�����
		constructor(n:string,a:number){
			this.name=n;
			this.age=a;
		};
		//�����Ķ��� ����get /set ��es6�еĲ�һ���������ĳ�Ա�����������Զ�����
		getName():string{
			return this.name;
		};
		setName(n:string):void{
			this.name=n;
		};
	}
```

#### ʵ��������

```typescript
let p1=new Person("����",18);
console.log(p1.getName());//ʵ������Ҳ����ֻ�ܷ���public���Է���
console.log(p1.age);
```

#### �������η�

public : �ڲ����ⲿ�����඼�ܷ���

protected : �ڲ��������ܹ�����

private : ֻ���ڲ����Է���

#### ��ļ̳�

�� java һ����û�Ǵ�Ļ���

##### �̳�ʲô

public �� protected �����Է������ᱻ�̳С�

##### ��д����

дͬ���ķ������ͻḲ�Ǹ���ķ�����

##### ��д����ʱ���ø���ͬ������

super();����������Ǹ����ͬ���������ο�������룬��д���캯���Ĵ��룬�����˸���Ĺ��캯����

```typescript
class student extends Person{
		num:number;//�����Լ�������
		constructor(n:string,a:number,num:number){//������д���캯��
			super(n,a);//���ø���Ĺ��캯��
			this.num=num;
		}
	};
```

#### ��ľ�̬����������

ͨ���ؼ��� static ��������Ի��߷�������Ϊ ��̬���� ��ֻ��ͨ���������ã�**ʵ�������ܵ��þ�̬���ԡ���̬�����в���ֱ�ӷ�������������ԣ�ֻ�ܷ��ʾ�̬����**

```typescript
class test2{
		age:number;
		//���徲̬����
		static tname:string="����";
		//���徲̬����=>��̬�����в���ֱ�ӷ�������������ԣ�ֻ�ܷ��ʾ�̬����
		static showname():void{
			console.log(test2.tname);
			//console.log(this.age);//=������
		}
		constructor(age:number){
			this.age=age;
		}
	}
//������ľ�̬����
console.log(test2.tname);
//������ľ�̬����
test2.showname();
```

#### ������

�ɹؼ���abstract������࣬����ʵ������**ֻ�����������ʵ�������������ʵ�ָ�������г�����**��**������һ��Ҫ���г��󷽷�**���������Ѿ�ʵ�ֵķ�����**���󷽷�ֻ���ڳ������г���**��

##### ���󷽷�

���󷽷�����ɶ��û�о�һ������

```typescript
abstract class xuni{
	abstract saysomething():any;//���󷽷��Ķ���
    //Ҳ�������Ѿ�ʵ�ֵķ���
	sayhello():void{
		console.log("hello");
	}
}
```

##### ʵ�ֳ�����

ʵ�ֳ�������Ǽ̳г����࣬���Ұѳ������еĳ��󷽷�������ʵ�֡�ʵ��֮�������ǿ��Խ���ʵ��������

```typescript
//�̳в�ʵ�ֳ��󷽷�
class shili extends xuni{
	saysomething():void{
		console.log(`saysomething:no what hao say`);
	}
}
//ʵ����һ������Ķ���
let sl1=new shili();
sl1.saysomething();
```

### �ӿ�

��Ϊ�Ͷ����Ĺ淶��˵���˾���**һ���Զ������������**��

##### ���Խӿ�

���ǹ涨���������͵� json������ ����� ���ֵ��������ͣ��� ��  �� ��������ɣ������ֶ��� string����

```typescript
interface FullName{
    //�涨json������������������
    firstName:string;
    lastName:string;
    smallName?:string//=>�ӿ���Ҳ�������ÿ�ѡ����
};
```

������Ҫдһ���˵�����ʱ����ȥʵ������ӿڣ����չ淶���и�ֵ���� ����һ���������͵ı���

```typescript
//����һ������ ��������myname �������ͣ� FullName  
let myname:FullName={
		firstName:"��",
		lastName:"��"
	}
//�����Խӿ� ���������Ĳ����� ���Ǻ����Ĳ��� ������ FullName ��
function showFullName(name:FullName):void{
    console.log(`fullname:${name.firstName}${name.lastName}`);
}
showFullName(myname);
```

###### ֻ������

����㶨���ĳ��������Щ���ԣ�ֻ���ڳ�ʼ��ʱ���и�ֵ�����ܽ����޸ģ����ǿ�����������Ϊֻ�����ԡ�

����ĳ��������������Զ����Խ����޸ģ�ֻ�� id Ψһ��ʶ���ܽ����޸ġ�

```typescript
interface FullName{
    firstName:string;
    lastName:string;
    smallName?:string;
    readonly  id:string; //ʹ�� readonly��ʶΪֻ��
};
```

TypeScript����`ReadonlyArray<T>`���ͣ�����`Array<T>`����**��ֻ�ǰ����пɱ䷽��ȥ����**����˿���ȷ�����鴴������Ҳ���ܱ��޸ģ�

```

let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
```

�����������һ�У����Կ������������`ReadonlyArray`��ֵ��һ����ͨ����Ҳ�ǲ����Եġ� ��������������Ͷ�����д��                

```
a = ro as number[];
```

##### �������͵Ľӿ�

�涨�����Ĳ����������������͡�����ֵ���͡�����˵��Ҫ����һ�����������͵ĺ������ͱ��������ҵı�׼д��

```typescript
//���庯���ӿ�
interface infn{
//���������ǲ������涨�����ĸ���,���ͣ���ȻҲ�����ÿ�ѡ���������������Բ�һ��������涨���Ƿ���ֵ������
	(par1:string,par2:number):string
}
//ʵ�����ֺ����ӿ�=�����ǰ������ֹ淶����һ������
let fun1:infn=function(name:string,age:number):string{
    return `���֣�${name},���䣺${age}`;	
}
```

##### �����ӿ�

�涨���顢�����key��value���������ͣ���һ�����Խӿڣ��ǹ涨 key�����֣���value�����ͣ���һ����

```typescript
interface myarr{
	//Լ������������ֵ(key)����ֵ���ͣ�value���ַ����͡����ǰɣ��������������������������
	[myindex:number]:string
}
let arr:myarr=["hello","xiamin"];

interface myarr{
	//Լ���˶�������ֵ(key)��string���ͣ�value���ַ����͡����ǰɣ��������������������������
	[myindex:string]:string
}
let arr:myarr={name:"xiamin"};
```

#### ��ӿ�

�������Լ�����涨������Ժͷ��������ơ����ͣ��ӿڹ涨��һ��Ҫ�У���Ҳ�������Լ��Ķ�����

##### ��ӿڵĶ���

```typescript
interface animal{
		name:string;
		eat():void
}
```

##### ��ӿڵ�ʵ��

ʹ�ùؼ��� implements ����ʵ�֣��ӿ����еı��밴�չ淶����ʵ�֣�Ҳ��������Լ������Է�����

```typescript
class dog implements animal{
		name:string="����";
		eat():void{
			console.log("����Ҫ��?");
		};
		//����Լ������Է���
		age:number=2;
		sayHello():void{
			console.log("������~");
		}
	}
```

##### ��ӿڵļ̳�

��ӿڿ��Լ̳У��н����ӿڵ���չ��

```typescript
interface Person extends animal{
		work():void;
}
//ʵ��Person����ӿڵ�ʱ��ͱ����animal�Ľӿڶ�ʵ��
//����һ������Լ̳�һ�����ͬʱʵ�ֶ���ӿڣ���java��࣬java��֧�ֶ�̳У�����֧�ֶ�ʵ�ֽӿ�
```

### ����

���;�����һ��������ʱ�������ͣ����õ�ʱ�����ɵ����ߴ��뷺�͵�ֵ��������ڵ��ú�����ʱ����ָ�������Ĳ������ͣ�����ֵ���ͣ��Ϳ���ʹ�÷��͡�����ʹ��any���淺�ͣ����ǲ��淶�����淶Ҳ���á�

#### ���ͺ���

�ñ�����ʱ�������������ֵ�����ͣ������ߵ���ʱ��Ҫ���˴��뺯���Ĳ���������Ҫ���뷺�͵����͡�

##### ���巺�ͺ���

```typescript
//�����ж�����ͣ��� ���ָ�
function saysomething<T,X>(something:T):T{
		return something;
}
```

##### ���÷��ͺ���

```typescript
console.log(saysomething<string,number>("hello"));

 console.log(saysomething<number,number>(123));
```

#### ������

���ĳЩ�������Ͳ�ȷ������ĺ�������������ֵ���Ͳ�ȷ�����÷��ʹ��档

```javascript
//�����ж�����ͣ��� ���ָ�
class test<T>{
    par1:T;
    constructor(p:T){
        this.par1=p;
    }
    getPar():T{
        return this.par1;
    }
}
//����ʵ����ͬʱ�������͸�ֵ
let obj=new test<number>(18);
```

#### ���ͽӿ�

һ���������ñ�����ʱ�������ͣ�ʹ�õ�ʱ����Ҫ���뷺�͵�ֵ��

```typescript
interface myfn<T>{
		(par1:T):T
	}
//ʵ�ַ��ͽӿ�,��Ҫ����ӿڵ���������Ҫ���㷺�͵Ĳ������ƣ���������ͷ���ֵ������һ�¡�ע�⣬��Ҫʵ��һ�����ͽӿڣ���ô��Ҫʵ�ֵ��Ǻ���Ҳ�ã���Ҳ�ã�ҲӦ����һ�����͡������������ �ұߵ�ʵ�ֺ���Ҳ��һ�����ͺ���
	function show<T>(message:T):T{
		return message;
	}
	let fn:myfn<number>=show;
```

### ģ��

��ES6��ģ�黯һģһ����ע�⣬��˵����һģһ��

### �����ռ�

typescript ����Ϊ�˽��������Ŀ�У���Ϊ����Э��֮��������⣬�����������͵Ľӿڡ�ģ��ȡ����Ƕ���Э�����п��ܳ��������ظ������飬��ʱ�����Ҫ�����ռ�����������ˡ�

�����ռ�=>Ϊ��ʹ�����������������ͻ��**�����ռ��ڲ��Ķ�������˽�еģ������Ҫʹ�õĻ�����Ҫ��ģ��һ��export��ȥ**

##### ���������ռ�

ʹ�ùؼ��� namespace ���������ռ�,����Ҫ��¶�����ݵ�����

```typescript
namespace A{
	export let name:string="����";
	export function showname(name:string):void{
		console.log(`�ҵ�������${name}`);
	}
}
```

#### �ⲿʹ�������ռ������

```typescript
// �����ռ�.����/������
A.showname("sisi");
```

##### ��ģ�����ʹ��

ģ���ʹ�þ���Ϊ�˶���Э��������������ͬ��ģ����ܻ����ͬ�������ԣ�����ͬһ��ģ���е���������ģ��ͻ����������ͻ�������������ģ�鵼�����������ռ䣬�����ģ��ֻ��Ҫ�õ������ռ䣬�Ϳ���ʹ�������ռ����е��������ݣ����ұ�֤�����ռ䲻������Լ򵥣�ʹ�ñ���ģ��ʱ���������ռ�ǰ׺���Ͳ������������ͻ����

```typescript
//�������ռ䵼������� export ��ģ��ĵ���
export namespace A{
	export let name:string="����";
	export function showname(name:string):void{
		console.log(`�ҵ�������${name}`);
	}
}
//����ģ���õ������ռ䣬��ʹ�ø������ռ��б�¶�����Է�����
import {A} from "./07-namespace"
A.showname(A.name);    
```

### װ��

װ������һ��������������ͣ��ܹ����ӵ��ࡢ���������Ի�����ϡ������޸������Ϊ��  ͨ�׵Ľ�������������һ��������

##### ����װ����

װ��������һ��������������ô���壬װ��������ô���塣

##### װ������ʹ��

�﷨ ������Ҫ���������ࡢ���ԡ�������ǰһ��д��  @װ����������

#### ��װ����

���޸���Ķ���������޸���Ľṹ����̬�ı䡢��չ��Ĺ���

##### ��װ�����Ķ���

```typescript
 function addsomethig(params:any):void{//ע��������Ĳ���params���Ǳ�װ�ε��� ���౾��
	//ͨ��params�����ԭ�����������
	params.prototype.name="����";
	//ͨ��params�����ԭ������ӷ���
	params.prototype.sayhello=function():void{
		console.log("hello");
	}
	//����������д����࣬
	// return class extends params{
	// 	//��������д�����
	//};
}
```

##### װ��ĳ����

```typescript
@addsomethig
class person{
	constructor(){}
}
let p=new person();
console.log(p.name);
p.sayhello();
```

#### װ��������

��������װ������һ���װ������û�а취���Σ�װ�����������Խ��д��Ρ�

##### װ���������Ķ���

```typescript
function add(name:string):any{//�������Լ�Ҫ����Ĳ���
	
	return function(par:any){//����������Ǳ����εĶ���
		//ͨ��params�����ԭ�����������
		par.prototype.name=name;
		//ͨ��params�����ԭ������ӷ���
		par.prototype.sayhello=function():void{
			console.log("hello"+name);
		}
	};
}
```

##### װ����������ʹ��

```typescript
@add("����")
class dog{
	constructor(){}
}
let d=new dog();
console.log(d.name);
d.sayhello();
```

#### ����װ����

##### ����װ�����Ķ���

```typescript
//����һ������Ǿ�̬������ô�������������Ĺ��캯�����������ͨ��Ա���ԣ���ô������Ծʹ��� ���ԭ�ͣ����౾���������������ֿ��Ըı���Ľṹ��
//����������Ȼ����װ�ε�������(д���ĸ����Ե���һ�У�����������˭)
function add(par1:any,par2:any){
    console.log(par1);
    console.log(par2);
    //ͨ��ԭ���������޸����Ե�ֵ
    par1[par2]="����";
    //�����������
    par1["age"]=18;
}
```

����װ������ʹ��

```typescript
class Per{
    @add
    name:string;
    constructor(){}
}
let pp=new Per();
console.log(pp.name);//����
console.log(pp.age); //18
```

ͬ������������������ʹ��װ����������

#### �෽��������

##### �෽���������Ķ���

```typescript
//��һ������:����Ǿ�̬������ô�������������Ĺ��캯�����������ͨ��Ա���ԣ���ô������Ծʹ������ԭ�ͣ����౾��
//�ڶ�������:����������
//����������:����������
function add2(par1:any,par2:any,par3:any){
    console.log(par1);
    console.log(par2);
    console.log(par3.value);//=>par3��һ������������һ������value�����Ǹ÷���
    //�޸�װ�εĸ÷���
    //1������ԭ�ȵķ���
    let me=par3.value;
    //2���޸ĸ÷���
     par3.value=function(){
     //�����԰�ԭ���ķ����ŵ��ͷ�����ִ�С�
     me();
     console.log("����");
        }
}
```

##### �෽����������ʹ��

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

#### װ������ִ��˳��

����=������=����������=���ࡣ**����ж��ͬ����װ����������ִ�к����**