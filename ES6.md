### �����Ķ���

1. let:���������û��Ԥ�����������ڱ��������������ظ��������
2. const�����峣����������ʱ��ͱ���ø�ֵ���������ܸı�ֵ�������Զ��ڶ������ԵĲ��������ã��������push()���������������ݣ�������һ������freeze(��ʹ�����ܸı䣩
3. ʹ���������ַ�������ı��������������˿鼶������  {}
ע�⣺var ����ı�������window��let��const����

---
### �⹹��ֵ

**�ǳ������ر����������ݽ����Ķ���**

```javascript
	  //�����顢json�е�ֵ��ֵ������
	  let [a,b,c]=[12,56,65]	
	  let json={name:"xiamin",age:21};
	  let {name,age}=json;
	 //�����ȶ���ñ������ٽ⹹��ֵjson���ñ���
      let a,b;
      ({a,b}={a:"xiamin",b:"18"};)
	//����д{}ʱ,���ܻᱻ�����鼶�������﷨����ʱ����㲻��{}�����鼶�����������С���Ű�Χ����� 
```

---

### �ַ���ģ��

�ַ������ӣ����ÿ���˫���š������š����⻻��

```javascript
//��ʽ��`string1${string2}string3`
let name="xiamin";
let hello=`�������${name},�������`;
```

---

### �ַ�������

```javascript
string.includes("str");�ж��ַ������Ƿ���ĳ���ַ���������boolֵ
string.startsWith("str")���ж�ĳ���ַ����Ƿ���ĳ���ַ�����ͷ
string.endsWith("str")���ж�ĳ���ַ����Ƿ���ĳ���ַ�����β�����������ж��ļ����ĺ�׺
string.repeat(n);�ظ�ĳ���ַ������ٴ�
```
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### ����

##### 	Ĭ�ϲ���

1. function fname(par1=Ĭ��ֵ��par2=Ĭ��ֵ){}

2. �����Ĳ���Ĭ�����Ѿ�����ģ������ڲ������� let const�ظ�����

##### ... �����

��չ��չ����/  ����(ʣ��)�����(�����ʣ�����㣬�����ŵ����) **...** ��**...** ���԰�һ������չ����һ�����ı���

1. �Ѵ���ļ���������װ��һ������

```java
function ftname(...a){}
ftname(6,5,8,4,);
```

2. �Ѵ������������ֳ�һ�����������뺯��

```java
function ftname(a,b,c){}
arr=[1,2,3]
ftname(...arr);
```

3. ����ĸ�ֵ arr1=arr2;�������������ͣ�arr2�ı�ʱarr1Ҳ��䡣

```javascript
arr2=[1,2,3]  
arr1=[...arr2]
```

##### ��ͷ���� =>

�򻯺����Ķ���

��ʽ��let ftname=(par1,par2)=>{���}��

1. ������˼�ͷ�������ں����ڲ����������������������������ڲ���this���� ��˭���þ���˭�����ǿ���ͷ������this ��˭����ô���ڲ�������this����˭��

2. 
   ��ͷ������ **this** ָ��**����**��ʱ�����������ĵĶ����thisָ�򡣼�ES6��ͷ������this��ָ����������������thisָ��ֻ��**����**����thisָ������һ��ֻ��Ҫ����ͷ�������ĸ������б����壬�������ͷ��������ĸ������� **this** ָ��ż��û�������Ķ���this��ָ��window��
   
3. ��ͷ��������arguments����,������...����

4. ��ͷ�������ܵ����캯��

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### ����

#### ES5�����������

##### foreach()

```javascript
//��������
arr.foreach(
 function(val,index,arr){}, //��һ�������ص�����
 this//�ڶ���������thisָ��Ķ���һ�㲻���������
);
```

##### arr.map()

�÷���foreachһ������ͬ����map�����ڻص�������return ĳ��ֵ������ֵ�����һ�����飬������鷵��

```java
//arr.map()�ع����飬����һ������
var arr=[1,2,3]
let res2=arr.map(function(val,index,arr){
    console.log(val);
    return val+index;
});
//res2 ��arr�� ֵ���±�͵����� 1  3  5
```

##### arr.filter()

���ˡ��÷���foreach()һ������ͬ����ѭ����ʱ����Խ����жϣ��Ƿ����������������������true����᷵�ص�һ���������У���������������false������������������С���󷵻������顣

```java
let res3=arr.filter(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
					/* else
					return false; */ //����ʡ��return false
				});
```

##### arr.some()

�÷���foreachһ������ͬ�����ж������Ƿ����**ĳ��**Ԫ�ط���ĳ����������󷵻�boolֵ

```javascript
//ֻҪ��һ������������ return true
let res4=arr.some(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
	});
```

##### arr.every()

�÷���foreachһ������ͬ�����ж������Ƿ�**����**Ԫ�ض�����ĳ����������󷵻�һ��boolֵ

```javascript
//�������� return true �������� return false��ֻҪ��һ�� false ���� false
let res5=arr.every(function(val,index,arr){
					console.log(val);
					if(val>=5)
					return true;
					/* else
					return false; */ //����ʡ��return false
				});
```

##### arr.reduce()

�÷���foreachһ������ͬ���ǣ����Է���һ����ֵ������һ������ pre ,pre������һ�η��ص�ֵ��ֻ�����һ�εķ���ֵ�ܱ����յ���

```javascript
var sum=arr.reduce(function(prev,val,index,arr){//prev����һ�β������صĽ��
			return prev+val*val;//������������Ԫ�ص�ƽ����
			})
```

##### arr.reduceRight()

arr.reduce()һ�������ã����Ǽ�����ұߣ������β������ʼ��

#### ES6�����������

##### 	Array.from()

��һ��α����ת����һ������

```javascript
//��׼α����ת����������
let warr=document.querySelectorAll("div");
let arr2=[Array.from(warr)];
//let arr2=[...warr]; ��չ�����... Ҳ����ʵ�ֱ�׼α����ת����������

//����׼��α���飬���Ǳ���Ҫ��length����
let warr2={
    0:2,
    1:4,
    2:6,
    length:2//����д2 ��ôת��������鳤��ֻ��2
};
Array.from(warr2);
```

##### Array.of()

��һ��ֵת����һ�����飬���� ...�Ĺ��ܡ�Array.of()�����Ͽ����������Array()��newArray()�����Ҳ��������ڲ�����ͬ�����µ����أ��������ǵ���Ϊ�ǳ�ͳһ�� 

```javascript
//�Ƽ�ʹ�����ַ������� Array()��newArray()
var arr=Array.of(2,6,8,4,7);
```

##### arr.find()

���ص�һ������������Ԫ��

```javascript
//������һ������������ֵ����ֹͣ����Ѱ��
let res7=arr.find(function(val,index,arr){
					if(val>5)
					return true;
				});
```

##### arr.findindex()

���ص�һ������������Ԫ�ص��±�  return true ��ֹͣѭ��,�����ظ�Ԫ�ص��±�

```javascript
let res8=arr.findIndex(function(val,index,arr){
					if(val>5)
					return true;
				});
```

##### arr.fill(val,start,end)

�������,������ĳ��ֵ�滻�����ĳЩֵ������**���ܸı�����ԭ���ĳ���**��

```javascript
//��һ������ val ������������ֵ�� start ������Ŀ�ʼ����������end����������������������start,������end
arr.fill("41",3,5);//��41 �������ĵ�[3]��[5]������[5]
```

##### arr.includes(val)

�ж��������Ƿ����ĳ��Ԫ�أ���some()��࣬���Ǹ��򵥲���Ҫ�ص����������жϣ��׶˾��ǲ��ܶ�ֵ����������жϣ�ֻ���ж�Ԫ�ر����Ƿ���ڡ�

```javascript
let res9=arr.includes(9);//�ж����鳤�Ƿ���� 9
```

arr.indexOf(val)

���������и�ֵ���±ֻ꣬�ܷ��ص�һ���������ڸ�ֵ������-1

``` javascript
let res10=arr.indexOf(5);//���������У�ֵΪ 5 ��Ԫ���±�
```

####  ES2017��������ѭ��

for (let ... of ...)ѭ�����������鶼����ʹ������ѭ����

�����������˼������ԣ�
		arr.values()
		arr.keys()��������±��γɵ�����
		arr.entries()��������Ԫ��ֵ���±��γɵ����飬����ɵ����� �� [[val,key],[val,key],[val,key]]

```javascript
//Ĭ��ѭ���ľ��� ����/����� values()
for (let val of arr) {
    console.log(val);
}
//keys()ѭ��������±�
for (let index of arr.keys()) {
    console.log(index);
}
//entries()����ֵ���±���ɵ����� arr.entries()=[[index,val],[index,val],...]
for (let arr1 of arr.entries()) {
    console.log(arr1[0],arr1[1]);
}
```

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### ����

#### ����ļ���﷨

```javascript
let name=xiamin;
let age=18;
let show=function(){};

let json={
    name,	//�ȼ��� name:name
    age,	//�ȼ��� age:age
    show	//�ȼ��� show:function(){},��ò�Ҫ�ü�ͷ����,��ͷ�������ⲿ���壬this��Զָwindow
}
```

#### ��������ĺ���

#####  Object.is()

�ж����������Ƿ����,����һ�������,����������� �� == �жϵ������һ�¡�������Ҫѡ��ʹ��

```javascript
NaN==NaN   false	Object.is(NaN,NaN) true
+0==-0     true		Object.is(-0,+0)  false
```

##### Object.assign(obj��obj1,obj2,...)

1. �ϲ����������,���ϲ����Ŀ����󷵻أ�����������غϵģ�����ĻḲ��ǰ��ģ�obj��Ŀ����󣬻ᱻ�ı�ֵ�����汾��Ĳ���ı䡣
2. ֵ���ƶ��󣨰������飩��let newarr=Object.assign([],oldarr);

```javascript
//1�����÷���ֵ����ȡ�ϲ���Ķ���
let js5=Object.assign({},js2,js3,js4);//ǰ��дһ���ն��󣬷���js2,�ᱻ�ı�
//2��ֱ�Ӱ���������Ŀ�����λ��
Object.assign(js5,js2,js3,js4);
```

#### ES2017��������������

Object.values(obj)�������ֵ����
Object.keys(obj)�������key����
Object.entries(obj)����ֵ����������ɵ����� �� [[val,key],[val,key],[val,key]]

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Promise

#### ����

����첽�ص����⣬Ϊ�첽����ṩ��һ�ֽ������

#### ״̬

1. һ��������״̬���ֱ�Ϊpending�������У���fulfilled���ѳɹ�����rejected����ʧ�ܣ���
2. ֻ���첽�������Ծ�����ǰ���ڵ�״̬�������κ����������޷��ı����״̬��
3. һ��״̬�ı䣬�Ͳ����ڱ䡣״̬�ı�Ĺ���ֻ�����ǣ���pending��Ϊfulfilled�ʹ�pending��Ϊrejected�����״̬���������仯�󣬴�ʱ״̬�Ͳ����ڸı��ˣ���ʱ�ͳ�Ϊresolved���Ѷ��ͣ�

#### ʹ�ò���

1.����һ��promise����

```javascript
let promise=new Promise(function(resolve,reject){
   		if(����)
   		{resolve(message);}	//pending��Ϊfulfilled�ɹ�ʱ���ص���Ϣ�����Բ�������Ϣ���Ǳ���ִ���������״̬�Ż�ı�
   		else
   		{reject(message)��}	//pending��Ϊrejectedʱ���ص���Ϣ�����Բ�������Ϣ���Ǳ���ִ���������״̬�Ż�ı�
   		});
//ֻ��ִ���� resolve() reject()������״̬�Ż�ı�
```

2��ͨ��then�������ֱ�ָ��pending��Ϊfulfilled״̬��pending��Ϊrejected״̬�Ļص������������û�з����������仯 then��ĺ�������ִ�У�

 ```javascript
promise.then(function(success){
    //to do  something
},function(fail){
    //to do  something 
});
//�����ص�����,�ɹ�ʱ��resolved״̬��ִ�еĺ�������ʧ��ʱ��rejected��ִ�еĺ������ص������Ĳ�����promise����ʱ�������ִ��ʱ��resole/reject�������ص���Ϣ���ڶ����ص�����һ�㲻д��д��catch()��

//promise.catch(),����һ��Promise�����Ҵ���ܾ��������������Ϊ�����Promise.prototype.then(undefined, onRejected)��ͬ��
//�Ƽ�ʹ��catch��������Ҫ��then�����ж���rejected״̬�Ļص�������������Ϊʹ��catch�����Բ�����then����ִ���д��ڵĴ���
promise.then(function(data) { 
    // success to do something
}).catch(function(err) {
    // error to do something
});

//Promise.finally(),����һ��Promsie����ָ������һ�� promise ���н���������fulfilled���� rejected������ִ��ָ���Ļص��������÷����ʺϣ����۽����ζ�Ҫ���еĲ���������������ݡ�
Promise.finally(functin(){
       //ִ�д���
});
 ```

#### Promise.resolve(value)

��������һ���ɹ�״̬��promise����,���� value ��Ҫ�����¼��������

1. һ��Promiseʵ����ԭ�ⲻ���ķ��ظ�ʵ��

```javascript
var original = Promise.resolve('���ڵڶ���');
var cast = Promise.resolve(original);
cast.then(function(value) {
    console.log('value: ' + value);
});
console.log('original === cast ? ' + (original === cast));
// "original === cast ? true"
// "value: ���ڵڶ���"
```

2. һ��thenable������ָ����then�����Ķ���������thenable����ģ�������������״̬

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

3. ��ͨ���ݣ�[String|Array|Object|Number]��ֱ�ӽ�������������ս��������һ���µ�Promise

```javascript
let p = Promsie.resolve(123);
p.then(function(num) {
    console.log(num);
})
  // 123
```

4. �޲�����ֱ�ӷ���һ��resolved״̬��Promise����

```javascript
let p = Promsie.resovle();
p.then(function() {
    // do something here...
})
```

#### Promise.reject()��

��������һ��ʧ��״̬��promise����let promise=Promise.reject("message");

#### Promise.all(iterable)

iterable ������һ���ɵ��������� Array �� String����promise�������ӵ�һ�����������󷵻�һ��promise���󣬵��Ǳ�������promise��״̬���ǳɹ�״̬�����ǳɹ�״̬����ж��promise����״̬��ʧ�ܣ����صĴ�����Ϣ�ǵ�һ��ʧ�ܵ�promise�����

#### Promise. race(iterable)

��promise�������ӵ�һ�����������󷵻�һ��promise���󣬵���ֻҪ��һ��promise��״̬�ǳɹ�״̬�����ǳɹ�״̬

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### ģ��

ES6ͳһ����˺Ϳͻ��˵�ģ��淶

#### ģ�黯

�����Ϊ����Java��Java����һ����һ���ļ�����֮���໥������Ҫ����

#### ����ģ��

����ģ������: ʹ�ùؼ���  export ����ģ������

1. �����������ݣ� 

   �����ʱ��͵�����export  ���������������������

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

?	�ȶ����ٵ�����export �Ѿ�����õı�������������������

```javascript
let qq=154564;
export qq;
```

2. ����������

```java
//export {��������������������}
let  x=12;
let y=5;
let a=2;
let b=9;
export {x,y,a,b};
```

3. ����ʱȡ������ export  {������ as ������������ as ���������� as ����};ȡ�˱��������ݣ��Է������Ҫ���þͱ���ͨ����������

```javascript
let tel=1872083;
export {tel as pnum};
```

4. ����Ĭ�����ݣ�ÿһ��ģ��ֻ�ܵ���һ��Ĭ�����ݣ������Ҫ���Ĭ�����ݣ����ǽ���������ΪĬ�����ݵ����ݷ���һ��json�С�export default ������    Ҳ������������

```javascript
let teacher="sisi";
let age=18;
let json={
	teacher,
	age
};
//��������������
export default json;
//������������
export default{
teacher,
age
}
```

#### ʹ��ģ��

1. ������ģ���ļ������൱�������߼����Ե������� ����ִ�е���䶼д�����js�ļ��� ����ģ���൱����Ҫ�õ��������

<script src="ģ���ļ�·��" type="module"></script>
2. ��ģ���е�������ģ������ݣ� 

   + ��������Ҫ�����ݣ� import {��������������������} from '����ģ�������λ��'	

     ע�⣺��ʹ����ģ���ļ���ͬһ�ļ�����·��Ҳ��Ҫ ./�ļ���

   + import '����ģ�������λ��' �൱�������ļ�����֪��ʲô��˼��

   + ��������Ŀ���ļ���¶�������ݣ� import * as ���� from './model2.js'

   + ����Ĭ�ϵ����ݣ����������ļ�Ĭ�ϵ��������ݣ��������ļ�û�����õ���Ĭ����������ʹ��
import �������� from '����ģ�������λ��'
	
	+ ��̬����ģ�飺import()��Ĭ�������import�﷨������д�� if ֮�಻ȷ��������У���importֻ֧�־�̬���룬����ʱ����Ҫ������Ҫ��ģ���ļ��� ����import()����promise�淶����import()����һ��promise����
		?			          import("./model2.js").then(function(res){//res��һ�����󣬰�������Ŀ���ļ�����������
   	?			          console.log(res);
   	?			           });
   	
   + ȡ������import {������ as ������������ as ���������� as ����} from '����ģ�������λ��'��ȡ�˱�����ͱ���ͨ������ʹ�����ݣ�ԭ�������Ʋ�������
   
   + import ģ���λ�ÿ��������·��Ҳ�����Ǿ���·��
   
   + import ���������Ч�� �����Զ��ŵ�������ִ��
----------------------------------------------------------------------------------------------------------------------------------------------------------------

### ��

#### ��Ķ���

```javascript
	class  ClassName{
		//���캯��
		constructor(name) {
			this.name = name;
		}
		//��Ա����
		functionName(){}
		functionName(){}
		}
```

#### ���������

```javascript
	let ObjectName=new ClassName("xiamin");//ʹ����Ĺ��캯��
```

#### ��Ĵ�ȡ����

get��set�������Խ��д�ȡ������ʱ**�Զ�����**������������ ����ֻ����һ��get����û������set��������ô������Ծ���ֻ�����ԣ��޷���ֵ���ܵ�˵�������˵Ļ������������ã�Ҫ���Ͷ����������á�

```javascript
class student {
				constructor(name) {
						this.name = name;
					}
					set name(val){
						console.log(`��������name��ֵΪ��${val}`);
						name=val;//�����ĸ�ֵ������һ��
					}
					get name(){
						console.log(`������ͼ��ȡname��ֵ`);
						return name;//�õ��ľ����� return �Ķ��� 
					}
					[aa]() {
						console.log(this.name);
					}
			}
//��ȡֵ / ����Ҫ�ֶ��������������Զ�������ֻ��Ҫͨ�� obj.attribute ����
```

#### ��̬����

��ķ�����ͨ���������õķ���������֮ǰ��ԭ�����ԡ�
	���壺 static functionName(){}
	���ã�ClassName.functionName();

#### ��ļ̳�:

�ؼ��� extends

```JavaScript
class person{
    constructor(name) {
        this.name=name;
    }
    showmessage(){
        console.log(`������${this.name}`);
    }
    eat(){
        console.log(this.name+"�ڳԷ��ˡ�����");
    }

}
class student extends person{
    constructor(name,num) {
        super(name);//����Ĳ��������ø���Ĺ��캯����ֵ
        this.num=num;//�Լ��Ĳ����Լ���ֵ
    }
    //��д����ĺ���������Ҫ��д�ľͲ���д������ֱ�ӿ����á�
    showmessage(){
        super.showmessage();//�̳и���ĺ��������Բ��̳У�
        console.log("ѧ��:"+this.num);//����Լ��Ĵ���
    }
}
```
ע��:
 1��������������ĺ�����������������ʹ�ñ��ʽ�������������壬�� [ ] ������

 ```javascript
let abc="name";
let Obj={
[abc]:"xiaominmin"
};
console.log(Obj.name);
//xiaominmin 
 ```

 2����Ķ������û��Ԥ�������ܣ������ȶ�����ʹ��

-------------------------------------------------------------------------------------------------------------------------------------------------------
### symbol

һ���µ��������ͣ�symbol��һ���������������͡���������

##### ����

```javascript
let sym1=Symbol("somethig");//����new
```

##### Ψһ��

symbol()����ֵ��һ��Ψһֵ����ʦ˵������������һЩΨһ������˽�е�һЩ������

```javascript
let symb=Symbol("age");
//������ͬ����ͬ�Ĵ���õ��� symbol�����ǲ�һ����
for(let i=0;i<1;i++)
{
    let symb2=Symbol("age");	
    console.log(symb==symb2);//false
}
//��ʹ��ͬ����������ͬ�Ĵ���õ��� symbol����Ҳ�ǲ�һ����
let symb3=Symbol("age");
console.log(symb==symb3);//false

//ֻ��ͨ�� = ��ֵ�� symblo��������ȵ�
```

#### symbol��������

���symbol��Ϊһ���������������key������for in ѭ����ʾ����symbol���ڵ����Լ���������ֻ����ֱ����obj[symbol]�������ֵ������˵�����˽�����ԣ�

```javascript
//��Ϊsymbol��Ψһ�ԣ�ֻ�еõ�һ��ʼ�����symbol���ܷ��ʡ������㱩¶�����ͬʱ��symbol����Ҳ��¶��ȥ��������˾�ֻ�ܷ��������������������
let symb=Symbol("age");
let json={
    name:"xiamin",
    [symb]:"22",
    tel:123456,
			}		
//for ѭ����鲻��symbol��������������
    for (let key in json) {
        console.log(key+" "+json[key]);
    }
```

### iterator

#### ����

 iterator��һ ��**�ӿ�**���ƣ� Ϊ���ֲ�ͬ�����ݽṹ�ṩͳ-�ķ��ʻ���

#### ����

1. ���ݽṹ���ṩ-һ��ͳһ�ġ� ���ķ��ʽӿ�;

2. ʹ�����ݽṹ�ĳ�Ա�ܹ���ĳ�ִ�������

3. ES6������һ�����µı����� ��for...ofѭ����Iterator�ӿ� ��Ҫ��for... of���ѡ�����˵ֻҪ�ѽӿڲ���ĳ�������Ͼ���ʹ�� for  of ѭ��

####  ����ԭ��

1. ����һ��ָ�����(����������)��ָ�����ݽṹ����ʼλ�á���һ�ε���next������ָ���Զ�ָ�����ݽṹ�ĵ�һ ����Ա  

2. ���������ϵ���next������ָ���һ ֱ�����ƶ���ֱ��ָ�����һ����Ա

3. ÿ����next�������ص���һ ������value done�Ķ���{value: ��ǰ��Ա��ֵ, done: ����ֵ}

4. value��ʾ��ǰ��Ա��ֵ��done��Ӧ�Ĳ���ֵ��ʾ��ǰ�����ݵĽṹ�Ƿ����������
   ������������ʱ�򷵻ص�valueֵ��undefined, done ֵΪtrue,��ʾ�Ѿ�����������

####  ԭ������iterator������

���顢�ַ��� ��argument��set������map����

### generator

����첽�������Ƕ�ף����ú�promise��ࡣ������һ������ĺ��������ɵ���һ�� iterator����valueֵ����  yield ��һ��Ķ�����������һ�����ʽ������ִ�н����

#### ����generator

```javascript
var gen=show();
function * show(){//��ͬ���� ����ǰ����һ���Ǻ�
    n��� yield  ���
	n��� yield  ���
	n��� yield  ��� 
}
```

�������yield���ƴ����ִ�У�yield���ǰ��ûִ�еĴ���ȫ��ִ�У��Լ�yield�����һ�����ִ��
��yield��ִ�����ɺ���next()����ִ�У�ÿִ��һ��next()�ͻᰴ˳��ִ����һ��yield����顣

#### next()

next()��ֹ��������ͣ�ĺ���ִ����һ����������ָ����ǰִ����һ���ķ���ֵ���� value�������ã��첽�����Ľ���ǲ���ֱ�� return �ģ���Ϊ return ��Զ����첽�������죬����ֻ���ڻص����õ� �첽�Ľ�����ڻص��и������� return ���ݡ�����ֻ���� �ص��� ִ�� next(data) ������ȷ���첽ִ����ɺ�ִ����һ���첽���������ܰ��첽�����Ľ�������س�ȥ���е��첽��������������һ���첽�����Ľ����������Ҫ �첽��ȡ һ�����첽��ַ�����첽���������ַ��ȡ��Ҫ�����ݡ�����ο� generato.html ģ���̨�������ݡ�

#### �����ִ��

##### �Զ�ִ��

```javascript
//1������һ��ȫ�ֱ��� �õ�generator����  var gen=show();
//2������Ҫ�ȴ����������������һ��   gen.next();
//3����ͬ��˳���дgenerator���� ��yield �ָ���Ҫ�첽�Ĵ����
//4����ʼִ��generator���� ��ִ��		gen.next();
var gen=show();//��һ��			
function showname(reso){
    setTimeout(()=>{
        console.log("����");
        gen.next();//�ڶ���
    },4000);
}
function showage(){
    setTimeout(()=>{
        console.log("22");
        gen.next();//�ڶ���
    },3000);
}
function showtel(){
    setTimeout(()=>{
        console.log("1872083");
    },1000);
}
function * show(){//������
    console.log("�첽��̿�ʼ");
    yield showname();
    console.log("�첽��̼���");
    yield showage();
    console.log("�첽����ټ���");
    yield showtel();
}
gen.next();//���Ĳ�
```

##### �ֶ�����

obj.next();����һ��json,{value:value,done:false}����һ��ֵvalue��ִ�е�һ��yield���ķ���ֵ������Ҫreturn yield�������ʲô�ͷ���ʲô����value������һ��promis�������֡��ַ����ȡ� �ڶ���ֵdone�Ǵ������Ƿ�������ϣ��������Ƿ���yield���

```javascript
function * show2(){
    yield new Promise((reso)=>{
        setTimeout(()=>{
            console.log("����");
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
//�ֶ�ִ�� next()
g2.next().value.then(()=>{
    return g2.next().value;
}).then(()=>{g2.next();});
```

---

### async��await

#### ����

async function functionName(){
?		 await �첽����
?		 await �첽����
?		 await �첽����
?		 ... .... 
?		}
?	����ʹ���뿴�ļ� 10_ansync��await

#### ��generator���

�����ֶ����� next() ����ȥִ����һ���첽������ await�ȴ���ǰ�첽��ɺ���Լ�������һ���첽����������ֻ�ܺ�promise����ʹ�á�����˵��ʵ��ͨ���ж� �Ƿ�ִ���� resolve() ���ж��Ƿ�ִ����һ�� await�ȴ����첽��������ôgenerator �� next() ����ָ������ֵ����ô async  ��ôָ������ֵ�� ͨ��promise��resolve() ��reject()ָ������ֵ����Ȼ˵ֻ�ܺ�promise���ʹ�ã�������д�ķ�ʽ����ͬ�����룬����Ҫ���� promise��then()������

#### ʾ��

```javascript
 async function show() {
     let name=await new Promise((res, rej) => {//����һ��Promise����
         setTimeout(() => {
             console.log("���");
             res("xiamin");//ָ�����ص�����
         }, 3000);
     });
     await new Promise((res, rej) => {//����һ��Promise����
         setTimeout(() => {
             console.log(name);//ʹ����һ�����ص�����
             res();
         }, 1000);

     });
 }
show();//���� asycn����
```

#### �ص�

1. ���廯ǿ
2.  �����awaitֻ����async������ʹ��
3.  await�������䷵��ֵ������promise�������֡��ַ�����
4. async�������ص���һ��Promsie����
5. await�����Promise������reject״̬ʱ����ô����async�������жϣ�����ĳ��򲻻����ִ�У���������һ��ִֻ�� resolve()��������ʹ������Ҳִ�� resolve()��ͨ�������ж� �����첽����ɹ�û�С�����ʹ�õ�������˵�ġ�
6. ���������async���ص㣬���ǻ��õ��쳣������ƣ�ѧ��java�Ķ�֪����java�����쳣����try...catch...

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Set ��WeakSet

set�����������飬��ͬ�����飬�������ظ�ֵ,û���±�

#### ����set

new set([val,val,val]) Set�������Խ���һ�����飨����������Ķ�����Ϊ������������ʼ���������Ƕ��󣬲���֧�ֶ����ʱ��ֱ�Ӹ�ֵ�����ǿ�����add������Ӷ����ȥ

```javascript
let set=new Set();
let set1=new Set([1,2,"hello",2]);//����ʱ��ʼ��
```

#### set�Ĳ���

1. ���ֵ��set.add(val);

2. ɾ����set.delete(val);

3. �ж�set���Ƿ���ĳ��ֵ�� set.has(val);

4. ���set��set.clear();

5. set�Ĵ�С��set.size();

6. set��ѭ�������� ������ for ... of ...

7. ���ã�����ȥ��     arr=[...new set(arr)]��

8. setת���飬ת����֮������������һЩ������������ arr=[...set];

9. set�Ľ��������

   ```java
   let set2=new Set([1,2,3,5,9]);
   let set3=new Set([2,4,5,6,7]);
   //����
   let set4=new Set([...set2,...set3]);
   console.log(set4);
   //����
   let set5=new Set([...set2].filter((val)=>{
       if(set3.has(val))
           return true;
   }));
   console.log(set5);
   //� u1-u2=>��u1��ȥ��������ͬ�Ĳ���
   let set6=new Set([...set2].filter((val)=>{
       if(!set3.has(val))
          return true;
   }));
   ```

#### WeakSet

weakSet��Ԫ�ؿ����Ƕ��󣬲�֧�ֶ���ĵ�ʱ��ֱ�Ӹ�ֵ

```javascript
let weakObj = new WeakSet({a:1111})
console.log(weakObj)  // ����ֱ�Ӹ�ֵ�ᱨ��
//��ȷ���÷���
let weakObj = new WeakSet()
let obj = {a:123}
weakObj.add(obj)
console.log(weakObj) 
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Map��WeakMap

#### Map

Map������json,���в�һ�������磺key�������κ�ֵ����һ�����ַ���

##### ����Map

let map=new Map();

##### Map����

1. ���ֵ��Map.set(key,vaule);key�������κ�ֵ����һ�����ַ���
2. ��ȡֵ��Map.get(key);
3. ɾ��ֵ��Map.delete(key);
4. ���set��Map.clear();
5. �ж�Map���Ƿ���ĳ��ֵ�� Map.has(key);
6. ѭ�� for ... of ...  / forEach

#### WeakMap

WeakMap��Map��࣬����keyֻ�ܶ���

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### ���ֱ仯��Math����

#### ��������

�����ƣ�let a=0b0101;
�˽��ƣ�let a=0o1247;
ʮ�����ƣ�let a=0x78Ab

#### �����ı仯

**�ܶ�������ֵĺ���������Number����**����Щ����ԭ�������ڶ������ϣ��������ĺô��Ǳ��磺
Number.isNaN();�Ƿ���NaN
Number.isFinite();�Ƿ�������
Number.isInteger();�Ƿ�������
......
Number.parseInt();�ַ���ת����
.....
��ȫ������-(2^53-1) �� ��2^53-1��
Number.isSafeInteger();�ж��Ƿ�Ϊ��ȫ����
Number.MAX_SAFE_INTEGER   ���ȫ����
Number.MIN_SAFE_INTEGER	  ��С��ȫ����

#### Math

Math.trunce() =>��������
Math.sign()=>�ж�һ���������� ������1��������������-1����0������0��

------------------------------------------------------------------------------------------------------------------------

### Es2018

#### ��������

��������ʽ���ӱ��ʽ���԰�ƥ����ַ�����ֵ��һ������
�﷨��(?<������>���ʽ)
ʹ�ñ���:

1.ͨ��match()�õ�һ������groups��str.match(re).groups
2.�ո�������ı�������groups��������

```javascript
let str="2017-03-20";
//������2018������ 2020�����Ȼ��֧������д��������
let re=/(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
let obj=str.match(re).groups;
console.log(obj.year,obj.month,obj.day);
```

#### ���������������� ��

�ڱ��ʽ�з������ã�\k<������> ����ǰ�ķ������� \1 \2 ���,�������õ�ʱ����Ը��ӱ��ʽȡ����
��replace()�ڶ������������ã�$<������> ����ǰ�ķ������� $1 $2���

#### ������²�����

s ������s����������ʽ��dotAllģʽ����ģʽ�� Ԫ�ַ� .  ���Դ��������ַ����� \n \t ֮���ַ�

#### ��ǩ����

���壺 functiion fname(){}

���ã�fname \` ���� \`

-----------------------------------------------------------------------------------------------------------------------------------------------

### proxy

���������ģʽ��һ�� ����ģʽ��
���ã����ء�Ԥ������չ���ܡ�ͳ�ơ���ǿ����ȵ� ����get()��set() ���������� ������Ĵ�ȡ���������Զ�����
�﷨��let obj=new Proxy(������Ķ��󣬶Դ������Ĳ���handel );

##### handel������һЩ������	

handel{
		apply(){},//���غ����ķ���
		construct(){},
		defineProperty(){},
		deleteProperty(){},
		get(){},//��ȡ��������ֵʱ�Զ������ĺ���
		getOwnPropertyDescriptor(){},
		getPrototypeOf(){},
		has(){},//���ö�����ĳЩ�����Ƿ�����
		isExtensible(){},
		ownKeys(){},
		preventExtensions(){},
		set(){},//���ö�������ֵʱ�Զ������ĺ���
		setPrototypeOf(){}//����ԭ������ֵʱ�Զ������ĺ���
		}

����ʹ�òο� 16_proxy��reflect.html

### Reflect

���� 
Reflect.apply(function,this��ָ��,[arg1,arg2]) ������ call()

����ʹ�òο� 16_proxy��reflect.html