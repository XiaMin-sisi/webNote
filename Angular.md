## һ��AngularJS����

?	MVXģʽ�������ݡ����ַ���
?	���ã��������Ա�ĸ���
?	��չ��html�Ĺ��ܣ��߸��ԡ�����չ
?	M:	model	 ģ�� -����
?	V:	View 	��ͼ-���ֲ�
?	C:	Controller	 ������-ҵ���߼�

## ����ָ��

### 	����

?				��չ��html�Ĺ��ܣ�������E: elementԪ�ؼ���ǩ  C:class ��   A:attribute ����  M��ע��

### angular�г��õ�ָ�

?            ����������ָ�д�ڱ�ǩ�ڵ�ָ��

#### 	ng-app=""

?			ָ����Angular�����÷�Χ������html��ǩ�о���ȫ�ַ�Χ��������

#### ng-model="������"��

?			˫��� ʹ��ĳ���������ı�ĳ�������� ͨ���ñ�ǩ���������Ӱ�������ֵ �����ط��ı������ֵҲ��Ӱ���ֵ�ڱ�ǩ�еģ�һ��д��input ������� ��ô��ʱ�ñ�����ֵ�������������ݣ�

#### ng-bind="������":

?			����󶨡�ʹ��ĳ�����������ñ�������ʾ�������ǩ�С�������һЩ�򵥵����㣬����ÿ�α������»�Ѹñ�ǩ�ڵ�������������������Ƽ�ʹ�ñ��ʽ���� bind

#### {{}}���ʽ��

?			{{������һЩ����}} ��ͨ�ַ�{{������һЩ����}}����angular�Լ��������ﲻ��Ҫʹ�ñ��ʽ����html��������ʹ�ñ�������Ҫ�ñ��ʽ{{}}

#### ng-init="a=0;b=0;":

?			��ʼ��Angular�ı�����д�ڸ�Ԫ�صı�ǩ�ϻ����Լ���ǩ��Ҳ��

#### ng-cloak:

?			��angular���ʽû�м��س���������£�����ʾ��ǩ�ĸ�����

#### ng-repeat: 

?			ѭ�����ظ�  ���������顢json���� in ѭ��=��ѭ������һ����ǩ�����ӱ�ǩ

value in json  Ĭ����ѭ��value��(key��value��in json ���������Ļ�����һ����key �ڶ�����value������Ļ�key�����±�����

���������ظ���ֵ�ͻ����:��Ϊangular���ÿһ��ֵȡһ��������������û��key��value����key�������ظ������ˡ�

���������$index =����ϵͳ���ı��� ����ѭ�����ڼ����ˡ�value in arr track by $index �������±���׷��ѭ��
ng-repeat��ng-click��һ������һЩ���⣬ֱ���ñ��ʽ��ʧЧ����һ���������ɾͿ����ˡ�
ѭ���е�ϵͳ������

 				$index: val=n ��n��ѭ��	
		 		$first: val=true ��һ��ѭ��ʱ������ʱ�򶼵��� false 	
		  	   $last: val=true ���һ��ѭ��ʱ������ʱ���� false
		  	   $middle:val=true ���ǵ�һ�κ����һ��ѭ��ʱ������ʱ���� false
			 	$even:val=true �����±���ż��ʱ��Ҳ����˵��������ѭ��ʱ
		 	    $odd:��$even�෴

#### ng-repeat-start/end��

?			ng-repeat-start��ng-repeat-endѭ�����Ǽ����ֵܱ�ǩ

����ʾ����

```html
<div ng-repeat-start="val in [1,2,3]">1</div>
<div>2</div>
<div ng-repeat-end>1</div>
```

#### ng-controller��

?	������ �߼�����ı༭,������$scope�����÷�Χ���������ϸ����

#### ng-src:

ָ��src��ַ

#### ng-href:

ָ�����ӵ�ַ

#### ng-class:

ָ��Ԫ�ص�class���ԣ�����д��   =��ָ����ʹ��angular�ı�����Ҫʹ�ñ��ʽ {{ ������ }}

?		1��һ�����飬��������class������
?		2��һ��json,   key��class���֣�value�ǲ���ֵ��true������Ӹ��ࣨ����������Ҳ�������ַ�ʽ������˵�����漰�ж�һ��ֵ�Ƿ���Ҫ���ڵ�ʱ��Ϳ�����һ������

#### ng-style:

һ��json��json�ĸ������Զ�Ӧ��css����=������������- ���� font-style ��ôkeyֵ��Ҫ����'' �����ָ����ʹ��angular�ı�����Ҫʹ�ñ��ʽ {{ ������ }}

#### ng-attr-��������

��ǩ�кܶ����ԣ���������� href ��title ��src��angular����ÿ����ר��дһ��ָ��������ͨ�õ�

ʾ������

```
ng-attr-href 
ng-attr-title 
```

#### ng-show="����":

����Ϊ��ʱԪ����ʾ����������Ԫ��

#### ng-hide="����":

����Ϊ��ʱ����Ԫ�أ�������ʾԪ�� �����һ����ǩ��ͬʱ����ng-show �� ng-hide ִ�е���Ϊ��hideΪ׼��

#### ng-if="����":

����Ϊ��ʱ���Ԫ�أ�����ɾ��Ԫ��

#### ng-switch on="����"��

ѡ��ṹ

```html
<div ng-init="sw=24" ng-switch on="sw">
			<h1 ng-switch-when="22">1</h1>
			<h1 ng-switch-when="23">2</h1>
			<h1 ng-switch-default >3</h1>
</div>
```

#### ����֤�е�����ָ��:

����ʾ����

```html
<form name="myform" ng-init="fr=153224">
<input type="email" name="myemail" ng-model="fr"  required ng-minlength="5" ng-maxlength="8" ng-pattern="/^[\d]+$/"/>
<p>{{myform.myemali.$valid }}</p>
<p>{{myform.myemali.$invalid}}</p>
<p>{{myform.myemali.$pristine}}</p>
<p>{{myform.myemali.$dirty}}</p>
<p>{{myform.myemail.$error}}</p>
	</form>
```

form����֤�е�����ָ�
		required:�������Ϊ�գ�����$error����ֱ�����Ϣ
		ng-minlength/ ng-maxlength:������ַ�������С/������ƣ���������$error����ֱ�����Ϣ
		ng-pattern��������ʽ����֤��������ֵ�����ϱ��ʽ��$error����ֱ�����Ϣ
form����֤�е�ϵͳ������
		$valid/$invalid��������е��Ƿ���Ź涨
		$pristine/$dirty��������е�ֵ�Ƿ�Ϊ��ʼֵ
�����ĸ���������Ӧ���ĸ��࣬.ng-valid/.ng-invalid/... ���Լ����Ա༭�⼸�������css��ʽ������������ʱ��	�������������Ӹ���
$error��������еĴ�����Ϣ����ֵʱ����û�д�

#### ��Ŀ���㣺

��ԭ����jsһ��ʹ��

......
(����ָ��ο�angular�ֲ�)

---

### angular�Զ���ָ��

#### ����

�Զ����ǩ �Զ������ =>��������

#### ����

```javascript
let mod1=angular.module("a1",[])
		mod1.directive("mydir",function(){
		let json={
				restrict:"C",
				template:"<ng-transclude></ng-transclude><div>mydirective</div>",
				replace:false,//һ�㲻д������ԣ�ֻ��ע�͵�ʱ���д
				transclude:true
			}
				return json;
		});
```

#### ʹ��

```
restrict:Լ�� ָ��ָ��ļ������� ��
E: elementԪ�ؼ���ǩ  C:class ��   A:attribute ����  M��ע�� =���������ʹ��
ʲô���͵ļ�����������ô��=�������뿴����
```

## ����controller��������

### ����

 �߼�����ı༭,������=������ע�������

### ��������ʹ��

1���õ�angular�ĺ���module��	

```javascript
var mod1=angular.module("ng-appName",[]);
```

2�����壺�õ�һ��controller��һ��module������úܶ��controller

```javascript
mod1.controller("controllerName",function($scope){ //$scope��angular��������angular���е����ݶ����� $scope��
			$scope.a=12;
			})
```

ѹ�������������ᱻ��д ����$scope ���ܻᱻѹ���� $s ����angular�Ͳ���ʶ������
���������
mod1.controller("controllerName",["����1"��"����2"��function(�β�1���β�2){}])	��

�����β�дʲô������Ӧ��������������ǰ�漸������(��˳���Ӧ),��Ϊ�ַ��ǲ��ᱻѹ���ģ�ֻ�б������Żᱻѹ����
3��������Ҫ�õ�����a��Ԫ�صĸ�������controller ng-controller="controllerName"

### angular�Դ���������

#### $scope:������

angular���еĶ�����������������������������С�

 AngularJS��JavaScriptһ�㲻��ͨ ��ͨ��$scope������󣬿���ʵ��js��angular�Ļ�ͨ
 ʾ������ js��alert()������angular��

```javascript
	$scope.alert=function(msg){alert(msg);}
```

##### $scop���ӷ���

$watch��$apply()

##### $watch():

�Ա����ļ������

```javascript
$scope.$watch('������'��function(){
			//����ֵ�����ı�ʱ ��Ҫ���Ĵ���
			},true)
�����������������Ƿ�Ϊ��ȼ�أ��������顢����ı���ĳһ������ֵ������Ҫ��ȼ�ز��ܼ�ص�
```

##### $apply()

��angular֮��ĳ�����������ı�ʱ��$watch()�Ǽ�ز����ģ�ʹ�� $apply()�����ֶ�����angularĳ��ֵ�����˱仯��û�в�����

#### $interval:��ʱ��

```javascript
var timer=$scope.$inetrval(function(){},time);
$interval.cancle(timer);//�رն�ʱ��
```

####  $timeout:��ʱ��

```javascript
var timer=$scope.$timeout(function(){},time);
$timeout.cancle(timer);//�ر���ʱ��
```

#### $inter:���ʽ�ķ���

#### $http:ajax

```javascript
1��var mod1=angular.module("ng-appName",[]);
		2��mod1.controller("controllerName",function($scope,$http){ 
		//get()	
		//��һ�ַ���,get/post ���ص���һ��promise,������res��data��
			$http.get('fileName',{param:{���ݸ���̨�����ݣ�responseType��json,��������}).then(functiion(res){
			console.log(res.data);
			},functiion(){});
			})
		//�ڶ���������res��
			$http.get('fileName',{���ݵĲ���}).success(function(res){
				console.log(res);
			}).error(functiom(){});
		//post�����⣬angularjs���õĲ������ݷ�ʽ��json ����ͳ�Ĵ��䷽ʽ�� a=2&b=3��һ�����������֧��json�Ĵ����ʽ
			�����
				1���������ã�
				

		//jsonp	
			$http.jsonp("����ĵ�ַ",{params��{
			���ݸ���̨������
			cb:'JSON_BACK'           =���ص�����������д������
			}}).success(function(){}).error(function(){})
```

---

#### ����������

����angularԤ�����������ο��ֲ�

### Provider �ṩ��

������ṩ�ߣ��Է������ĳЩ����

#### �����ṩ�ߵ���������

```javascript
��������+Provider ����
$http���ṩ�� $httpProvider ��������post��������ݴ����ʽ
$interpolate���ṩ��$interpolateProvider �������ñ��ʽ�����˷�����ʲô
```

#### ���÷���

```javascript
var mod1=angular.module("ng-appName",[]);
		mod1.config(function(�����ṩ��1�������ṩ��2){
			//ToDo �ο�Ajax�� $httpProvider ����post��������ݴ����ʽ
			});
```

---

### �Զ������

#### ����������

```javascript
����һ��factory
			app.factoty("��������"��function(){
			return something;
			});
			��������ʲô��������ʲô���������Է���һЩֵҲ���Է��غ���
��������provider=>�Ƽ�ʹ�� ��Ϊ���Զ�̬���ã�������ʹ��config����ͨ�������ṩ�߽��з��������
			app.provider("��������"��functiom(){
			return{
				myname:"xiamin",
				setname:function(newName){this.mynam=newName;},
				$get:function(){return this.myname;}//=�����񱻵��õ�ʱ�򣬾�ֻ�����������������ĺ��������õ�ʱ���õ�
			};
			})
			�͹������ ��������Ҫ�ѷ��صĶ������� $get��
��������service 
			app.service("",function(){
			//����Ҫreturnʲô ��������ﶨ����ʲô ֱ�ӾͿ����� ��������
			let name=""xiamin";
			});
�����ģ�constant ����=>�������β��ǲ��ܸı���ֵ
			app.constant("��������"��"ֵ");
�����壺value ����
			app.value("��������"��"ֵ");
```

#### �������޸�

```javascript
�������޸ģ�װ�Σ���decorator ���޸�ԭ��������
		app.decorator("������"��function($delegate){
		//$delegate����ԭ���������������������޸�
		$delegate.name="sisi";
		//�����޸��������������
		return $delegate;
		})
������������������� ֻ�ᱻ����һ��=�������ڶ�����������ǹ����
```

#### ���������ݵĹ���

##### ���ӿ�����

```javascript
�ӿ������Ḵ�Ƹ���������$scope�����ԡ������Ǹ��ƣ����߶�ĳ�����Խ����޸Ĳ���Ӱ��Է�
		��Ϣ���ƣ�
			$scope.$emit("����","����"); =�����Ϸ���
			$scope.$broadcast("����","����");=�����¹㲥
			$scope.$on("����","����");=������������߷��͵�����
			ʾ����
				$scope.$on("aa1",function(event,data){
				console.log(event,data);
				//�Ѹ������͹��������ݱ������Լ�����������
				this[event.name]=data;
				console.log(this.aa1);
				}); 
```

##### �޹ؿ�����

�Զ��������������ʵ�����ݹ���=���Ƽ�ʹ��provider���з���Ķ��壬����ͬ����ͨ�����ø��� 

---

## filter������

���ã����֮ǰ�����ݽ���ĳ�ִ���
�﷨��data|����������

### ��������ʹ��

```javascript
���ʽ��ʹ��angular�Դ��Ĺ�������
	currency����һ����Ǯ���д���Ĺ�����  99.3|currency =��$99.30
	date����һ���������Ķ����ڽ��д���Ĺ�����{{times|date:"yyyy-MM-dd-hh-mm-ss"}}=>2020-04-	 24-03-33-15  (����y������� - ԭ�����)

js��ʹ��angular�Դ��Ĺ��������������������� $filter
	$filter("������������")������Ҫ��������ݡ���������������
```

### �Զ��������

```javascript
mod1.filter("myfilter",function(){
			return function(input){
				//TODO �Դ����Ķ������в���
				input=input+"-myfilter";
				//���ش���������
				return input;
				}
			          });
```

---

## module:ģ��

###    ����һ��ģ�飺

�뿴����

###     ʹ��һ��ģ�飺

�����뿴����

?	ʹ��һ��ģ��󣬾Ϳ���ʹ�ø�ģ������� controller filter directive ...

---

## router��·��

������ͼ ����������ÿһ����ͼ�ļ�����һ���������ļ� �����ļ�ֻ��Ҫ���þͿ���

### ʹ��·��

```javascript
1������route.js
2������route ��ģ��
		let mod1=angular.module("main",["ng-Route"]);
3������ģ�飺
		mod1.config(function($routeProvider){
4������Route��	
		$routeProvider.when()
		})
...�뿴��������ļ�
```

[route��ʹ��](file:///C:/11/t1.txt)

