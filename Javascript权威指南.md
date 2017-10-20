# Javascript 权威指南  
## 一. 词法结构  
Javascript程序是用Unicode字符集编写的  
区分大小写  
直接量 就是在程序中直接使用的数据值  
 >数字  
 字符串  
 布尔值  
 正则表达式  
 null  
 ## 二. 类型,值和变量  
 >基本类型  
number string 布尔值 null undefined  

 >引用类型  
 数组 对象 函数  

 ### 1 number  
 javascript 中所有的数字都用浮点数来表示  
 Math函数 Math.round(), Math.floor(), Math.random(), Math.ceil()  
 时间和日期 const now = new Date(); 
const day  = now.getDate();  
### 2 类型转换  
#### 2.1 显示类型转换  
Number('3');  
String(false);  
Boolean([]);
Object(3);  
#### 2.2 对象转换为原始值  
toString();
valueOf();
#### 2.3变量作用域  
局部变量的优先级高于同名的全局变量,如果在函数内部声明的一个局部变量或者函数参数中带有的变量和全局变量重名,那么全局变量就被局部变量所遮盖
## 三. 表达式和运算符  
### 1 函数定义表达式  
函数定义表达式可称为"函数直接量"  
var foo = function() {console.log(1)};  
### 2 对象创建表达式  
var obj = new Object();
### 3 关系表达式  
'==' 和 '==='
在'===' 下  
null和undefined都和他们本身相等
NaN和任何值都不相等  
#### 3.1 in 运算符  
in运算符左操作数是一个字符串或者可以转换为字符串,右操作数是一个对象, 如果右侧的对象拥有一个名为左操作数值的属性名,返回true
```
var data = [1, 2, 3];
1 in data;    //true;
3 in data;    //false
```
#### 3.2 instanceof 运算符  
instanceof 运算符左操作数是一个对象, 右操作数标识对象的类  
如果左侧对象是右侧类的实例, 则表达式返回true, 否则返回false  
```
var arr = [1, 2, 3];
arr instanceof Array;    //true  
arr instanceof Object;   //true
```
### 4 逻辑表达式  
'&&', '||', '!'  
'&&'的行为有时候称作'**短路**', 
```
    //两段代码是完全等价的
    if( a === b ) stop();
    ( a ===b ) && stop();
```  
### 5 赋值表达式  
a = 5;  //把5赋值给变量a  
'=' 运算符左操作数是一个左值: 一个变量或者对象属性(或数组元素); 右操作数 为任意值  
> es6  
解构赋值  
let [a,b,c] = [1,2,3];  
### 6 其他运算符  
#### 6.1 条件运算符(三目/三元 运算符)  
a > 0 ? a-- : a++;  
#### 6.2 delete运算符  
用来删除对象属性或者数组元素  
```
    var obj = {
        title: 'news',
        name: 'article'
    }
    delete obj.title;
    'title' in obj //false
    obj['title']  //undefined  

    var arr = [1, 2, 3];
    delete arr[2];
    2 in arr   //false;
    arr.length    //3 delete没有改变数组长度
```  
## 四. 语句
条件语句 , 循环语句, 跳转语句  
### 1. 表达式语句  
>>赋值语句 greeting = 'hello' + name;  
>>函数调用   
### 2. 复合语句和空语句 
用花括号将多条语句括起来,连成**复合语句**(compound statement).
```
    {
        //es6中花括号,即形成块级作用域 ,let声明,只在此代码块中生效;
        let title = 'space';
        title.length;
        console.log(title);
    }
```  
1. 语句块的结尾不需要分号, 块中原始语句必须以分号结束.
2. 块中的语句都要缩进  

空语句(empty statement), 允许包含0条语句的语句  
```
;
```
创建一个具有空循环体的循环时, 空域句是很有用的
```
//初始化一个数组arr
for(var i = 0 ; i< arr.length; a[i++] = 0 ) ;
```  
javascript循环体中至少包含一条语句. 所以,这里只用了一个分号来表示一条空语句.

