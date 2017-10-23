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

### 3. 声明语句  
var(*es6 let const*) 和 function 都是声明语句, 他们声明变量或者函数. 这些语句定义标识符(变量名和函数名)并给其赋值  
#### 3.1 var  
用var定义的变量无法通过delete删除  
如果只声明,未进行赋值操作,那么变量的初始值为undefined(*在es6中,建议在声明变量的时候就对其进行赋值操作*)  
>提升   

对变量和函数的声明会被提升至**当前作用域**的顶端,赋值及其他的操作则不会. (***函数优先** 函数会先于变量被提升*)  
声明本身会被提升，但不是赋值，即便是函数表达式的赋值，也 不会 被提升
#### 3.2 函数 function  
```
    //函数表达式
    var foo = function() {
        console.log(1);
    }
    //函数声明式
    function foo() {
        console.log(1);
    }

    //递归函数
    function factorial(n) {
        if(n < 1) return 1;
        return n * factorial(n -1);
    }
```  
避免在块中声明函数  
### 4. 条件语句  
条件语句是通过判断指定表达式的值来决定执行还是跳过某些语句  
#### 4.1 if  
```
 if(true) console.log(1);  
 //当在if语句后只跟一条语句时,不需要写花括号.  当有多条语句需要执行时, 用花括号将多条语句合并成一条
```  
#### 4.2 switch  
```
switch(exp) {
    case 1:      //表达式exp === 1 ,从这里开始执行
        //代码块1
        break;   //停止执行switch语句
    case 2: 
        //代码块2
        break;
    //...
    default:    //如果所有条件都不匹配, 执行default
        //代码块..
        break;
}

//另外一种思路
    switch (true) {
        case true :    //如果为真, 从这里开始执行
            //代码块1
            break;
        case true ：
            //代码块2
            break;
    }
```  
break语句可以使解释器跳出switch语句或循环语句  
### 5. 循环  
#### 5.1 while  
```
while(exp)
    //...
```  
#### 5.2 do while  
```
//do while循环 至少会执行一次
do 
    //...
while(exp)
```  
#### 5.3 for  
```
for(var i = 0; i < arr.length; i++){
    //.....
}

{
    let i, j;
    for(i = 0, j = 0; i < 10; i++, j++)
        sum += i*j;
}
```  
#### 5.4 for/in  
for/in循环方便地遍历对象  
```
for(var i in obj)       //将属性名赋值给变量i
    console.log(obj[p]);  //输出属性
```  
for...in循环遍历的是可枚举对象属性
#### 5.5 for...of  
for...of循环可以使用的范围包括数组、Set 和 Map 结构、某些类似数组的对象（比如arguments对象、DOM NodeList 对象）、后文的 Generator 对象，以及字符串  
```
const arr = [1,2,3];
for(let i of arr) console.log(i); //1 2 3
arr.forEach(function(ele, index){
    console.log(ele); //1 2 3
})
```
for...of 循环可以替代数组实例的forEach方法
相比for in 循环只能获取对象键名, for...of循环,遍历获得键值  

### 6. 跳转  
#### 6.1 标签语句  
```
flag: while(exp) {
    //...
    continue flag;
    //break flag;
    //...
}
```  
#### 6.2 break  
单独使用break语句的作用是立即退出内层循环或switch语句  
```
for(var i = 0; i < a.length; i++) {
    if(a[i] == target) break;
}
//当break和标签一起使用时,程序将跳转到这个标签所标识的语句块的结束, 或者直接终止这个闭合语句块的执行
break flag; //语句标签
```  
#### 6.3 continue  
使用方法和break相同, 效果是跳转到执行下一次循环  
```
//报错机制, 当产生一个错误时跳过当前循环的后续逻辑
for(let i = 0; i < data.length; i++){
    if(!data[i]) continue; //不能处理undefined数据
    sum += data[i];
}

```
#### 6.4 return  
函数调用是一种表达式, 所有的表达式都有值. 函数中return语句就是就是指定函数调用之后的返回值.在没有return语句时,函数的返回值是undefined.

#### 6.5 throw   
抛出异常,   
```
throw exp;

(function(x){
    //如果输入参数非法,就抛出一个异常
    if(x > 0) throw new Error('x不能是正数');
    return x*12; 
})(12);
```  
解释器会一直向上寻找相关联的异常处理程序.如果没有处理错误的try /catch /finally, JavaScript会把异常当作程序错误来处理,并报告给用户  
#### 6.6 try / catch / finally 语句  
>try /catch / finally 是JavaScript的异常处理机制  

try 从句定义了需要处理的异常所在的代码块  
catch 从句跟在try后面,当try语句块内发生异常,将执行catch内的逻辑  
finally finally 中的逻辑总是会执行(无论是否有异常)  
```
    try {
        //正常执行时, 这段代码不会产生任何问题  
        //发生异常时, 用throw语句直接抛出异常  
        //或者调用一个方法来间接抛出异常
    }
    catch (e) {
        //*当且仅当* try语句抛出异常,才会执行catch  
        //可以通过局部变量e获得Error对象或抛出的其他值得引用  
        //可忽略或处理这个异常  
        //还可以通过throw 重新抛出异常 
    }
    finally {
        //不管try语句是否抛出了异常, 这里的逻辑总是会执行, 终止try语句块的方式有: 
        // 1) 正常终止, 执行完语句块的最后一条语句  
        // 2) 通过break, continue或者return 语句
        // 3) 抛出一个异常, 异常被catch从句捕获
        // 4) 抛出一个异常, 异常未被捕获, 继续向上传播
    }
```
catch后的圆括号内是一个标识符, 这是一个局部变量
```
try {
    //要求用户输入一个数字
    var n = Number(prompt('请输入一个正整数', ''));
    //输入合理, 计算阶乘
    var f = function factorial(n){
                if(n <= 1) return n;
                return n * factorial(n-1);
            });
    //显示结果
    console.log(n + '的阶乘是' + f(n));
}
catch (e) {
    //如果输入不合理, 将执行这里
    console.log(e) //输出错误信息
}
```  
### 7. 其他语句类型  
#### 7.1 debugger  
debugger 语句通常什么都不做.在调试模式下产生一个断点(breakpoint)  
#### 7.2 'use strict'  
严格模式  
- 禁止使用with语句  
- 变量先声明才能使用,如果对未声明的变量进行赋值操作会报错  
- 调用函数中的this值是undefined (非严格模式中, 调用函数的this值总是指向全局对象)  
- call 和 apply 调用函数时, this值就是通过call() 或apply传入的第一个参数  
- 给只读属性赋值和给不可扩展的对象创建新成员都将抛出一个错误
- 传入eval()的代码不能调用程序所在的上下文中声明变量或定义函数  
- delete 运算符后跟非法标识符(变量 函数 函数参数)将会报语法错误异常(非严格 什么也不做, 返回false)
- 在一个对象直接量中定义两个或多个同名属性将产生一个语法错误
- 不允许使用八进制整数直接量

### 8. JavaScript语句小结  
| 语句            | 语法              | 用途            |
|-----            |:----             |:----            |
|debugger         | debugger         | 断点调试         |
|default          | default          | switch默认语句    |
|empty            | ;                | 什么都不做       |
|for...in         | for(var in object  )statment| 遍历对象的一个属性|
|label            | label: statment  | 指定statment名字|
|return           | return [exp]     | 指定函数返回值   |
|throw            | throw exp        | 抛出异常        |
|try              | try{statments} <br> [catch{handler statmens }] <br> [finally {cleanup statments }]   | 捕获异常        |
|use strict       | 'use strict'     | 对脚本和函数应用严格模式|

## 五. 对象  
无序属性的集合

