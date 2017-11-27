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
无序属性的集合.每个属性都是键值对  
属性名是字符串, 因此我们可以把对象看成是从字符串到值的映射  
除了保持自有的属性, JavaScript 还可以从原型继承属性. 对象的方法通常是继承的属性, **原型继承是JS的核心特征**  
JavaScript对象是动态的, 可新增和删除属性  
除字符串, 数字, true, false, null, undefined外, JavaScript中的值都是对象  
> 对象常见的用法是创建, 设置, 查找, 删除, 检测, 枚举    

每个属性都有属性特征:
- 可写, 表明是否可以设置该属性的值  
- 可枚举, 表明是否可以通过for...in循环返回该属性  
- 可配置, 表明是否可以删除或修改该属性  

每个对象还拥有三个相关的对象特征:  
- 对象的原型(prototype)指向另一个对象,本对象的属性继承自它的原型对象
- 对象的类是(class)一个标识对象类型的字符串
- 对象的扩展标记(extensible flag) 指明了是否可以向该对象添加新属性  

最后, 我们用下面的这些术语来对三类JavaScript对象和两类属性做区分:
- 内置对象(native object) ES规范定义的对象或者类. eg,数组, 函数, 日期, 正则表达式都是内置对象 
- 宿主对象(host object) 由JavaScript解释器所嵌入的宿主环境(如web浏览器)定义的. 客户端JavaScript中表示网页结构的HTMLElement对象均是宿主对象. 既然宿主环境定义的方法可以当成普通的JavaScript函数对象, 那么宿主对象也可以当成内置对象.  
- 自定义对象(user-defined object) 由运行中JavaScript代码创建的对象  
- 自有属性(own property) 是直接在对象中定义的属性 
- 继承属性(inherited property) 是在对象的原型对象中定义的属性  

### 1. 创建对象  
#### 1.1 对象直接量  
创建对象最简单的方式就是在JavaScript中使用对象直接量,  
属性名中可以是字符串直接量(包含空字符串)
```
    var obj = {}; //创建一个空对象
```  

对象直接量是一个表达式,这个表达式的每次运算都创建并初始化一个新的对象.
#### 1.2 new运算符  
这里的函数称构造函数,用来初始化一个新对象.原始类型都包含内置对象
```
var obj = new Object();
var arr = new Array();
var date = new Date();
var reg = new RegExp('a-z');
```  

#### 1.3 原型  
通过对象直接量, 可通过Object.prototype获取对象原型的引用, new运算符,构造函数调用创建的对象的原型就是构造函数的prototype属性的值  
#### 1.4 Object.create()  
创建一个对象, 其中第一个参数就是对象的原型  
Object.create()是一个静态函数, 不提供给某个对象调用的方法.  
传入原型对象
```
    var obj = Object.create({x:1});
    var obj = Object.create(Object.prototype); //创建一个空对象
```  

### 2. 属性的查询和设置  
```
    //访问 
    obj.title //访问obj的title属性
    obj['title']
    //赋值
    obj.title = 'sda';
```  

#### 2.1 作为关联数组的对象  
object.property  
object['property']  
第二种语法访问对象,这个数组元素是通过字符串索引而不是数字索引, 这就是我们所说的关联数组, 也称作散列, 映射或字典. JS对象都是关联数组   
> 使用数组的写法,更加灵活,可以通把数组索引写成变量来访问  

#### 2.2 继承  
```
    var obj = {}; //创建对象obj, 从Object.prototype继承对象的方法
    obj.x = 1; //定义一个属性x
    var p = Object.create(obj); //p 继承obj和Object.prototype
    p.y = 2; //给p定义一个属性y
    var q = Object.create(p); // q 继承p, Object.prototype
    q.z = 3;
    var s = q.toString(); //toString继承自Object.prototype
    q.x + q.y   //3 , x和y继承自obj和p
```  
> 如果对对象obj属性x赋值, 如果obj存在x属性(非继承,即自有属性),赋值操作只改变x值. 如果obj不存在x属性, 那么赋值操作就给obj添加了x属性,如果x属性是继承来的, 那么这个继承的属性x就被新创建的同名属性值所覆盖.  
**同时并不修改原型对象(如对q的x属性进行赋值操作, 并未影响到obj的x属性值)的属性**

.
> 只有在查询(访问)属性时才会体会到继承的存在, 设置(赋值操作)属性则和继承无关  

#### 2.3 属性访问错误  
查询一个不存在的对象属性值返回undefined  
```
    //一种更简练的常用方法，获取对象属性  短路运算
    var len = book && book.title && book.title.length 
```  
### 3. 删除属性  
delete 运算符可以删除对象的属性。delete只是断开属性和宿主对象的联系， 而不会去操作属性中的属性  
delete运算符只能删除自有属性， 不能删除继承属性  
### 4. 检测属性  
判断某个属性是否存在某个对象中  
使用in运算符, hasOwnPreperty()和propertyIsEnumerable()方法来完成  
>hasOwnPreperty 方法检测给定的名字是否是对象的自有属性.对继承对象将返回false  

.
>propertyIsEnumerable检测是否是自有属性及是否可枚举  

### 5. 枚举属性  
- for...in  
- Object.keys(obj), 返回一个数组,由可枚举的自有属性组成  
- Object.getOwnPropertyNames(), 返回一个数组, 由自有属性组成  
### 6. 属性getter和setter  
对象属性由名字,值和一组特征组成.属性值可以用一个或者两个方法来替代(*getter和setter*), 由getter和setter定义组成的属性称作'存取器属性'(accessor property), 它不同于'数据属性'.  

程序查询存取器属性时, JS调用getter方法(无参数), 这个方法返回的就是属性存取表达式的值. 当程序设置一个存取器属性的时候,JS调用setter方法,将赋值表达式右侧的值当作参数传入setter  

和数据属性不同, 存取器属性不具有可写性.
如果一个属性同时拥有getter和setter方法, 那么它是一个只读/只写属性,  
```
    var obj = {
        //普通的数据属性
        data_prop: value,
        //存取器属性都是成对定义的函数
        get accessor_prop() {//...},
        set accessor_prop(value) {//...}
    }
    //
    var serialnum = {
        $n: 0,
        get next() {return this.$n++},
        set next(n) {
            if(n >= this.$n) this.$n = n;
            else throw "序列号的值不能比当前值小";
        }
    }
```   
.
```
    //这个对象有一个可以返回随机数的存取器属性
    //
    var random = {
	get octet() {return Math.floor(Math.random()*256);},
	get uint16() {return Math.floor(Math.random()*65536);},
	get int16() {return Math.floor(Math.random()*65536)-32768;}
}
```  

### 7. 属性的特征  
除了名称和值之外, 属性还包含了一些标识他们可写, 可枚举和可配置的特性  
> **数据属性**包含四个特征: 值(value), 可写性(writable), 可枚举性(enumerable), 可配置性(configurable).  

.存取器属性不具有值(value)特性和可写性,它的可写性是由setter方法存在与否决定的
>  **存取器属性**包含四个特性:  读取(get), 写入(set), 可枚举性, 可配置性  

属性描述符 (这个对象,代表了数据属性/存取器属性的特性), 通过Object.getOwnPropertyDescriptor()可以获取某个对象特定属性的描述符
```
    Object.getOwnPropertyDescriptor(random, 'octet')
    //返回{set:undefined, enumerable:true,configurable: true,get: ƒ octet() }
```

想设置属性的特性, 需调用Object.definePeoperty()
```
    var obj = {};
    Object.defineProperty(obj, 'x', {
	value: 1,
	writable: true,
	enumerable: false,
	configurable: true
})
``` 

**Object.defineProperty()或Object.defineProperties使用规则** 
> - 对象不可扩展, 则可编辑已有的自有属性,但不能添加新属性
> - 属性不可配置, 则不能修改可配置性和可枚举性
> - 存取器属性不可配置, 则不能修改getter和setter方法, 也不能将其转化为数据属性
> - 数据属性不可配置, 则不能转换为存取器属性
> - 数据属性不可配置, 则不能将其可写性从false修改为true, 但可从true改为false
> - 数据属性不可配置且不可写, 则不能修改它的值. 可配置但不可写属性的值是可以修改的  

```
    /*
     *在Object.prototype上添加一个不可枚举的extend()方法
     *这个方法继承自调用它的对象,将作为参数传入的对象的属性一一复制  
     *除了值之外, 也复制属性的所有特性, 除非在目标对象中存在同名的属性
     *参数对象的所有自有对象(包括不可枚举属性)也会一一复制  
     */

    Object.defineProperty(Object.prototype,
        'extend',    //定义Object.prototype.extend
        {
            writable: true,
            enumerable: false,  //不可枚举
            configurable: true,
            value: function(o) { 
                //得到所有自有属性
                var names = Object.getOwnPropertyNames(0);
                //遍历
                for(var i= 0; i < names.length; i++){
                    //如果属性已存在, 跳过
                    if(names[i] in this) continue;
                    //获得o中属性的描述符
                    var desc = Object.getOwnPropertyDescriptor(o, names[i]);
                    //用他给this创建一个属性
                    Object.defineProperty(this, names[i], desc);
                }
            }
        }
    )
```   

### 8. 对象的三个属性  
原型(prototype), 类(class), 可扩展性(extensible attribute)  
#### 8.1 原型属性  
对象的原型是用来继承属性的  
要想检测,一个对象是否是另一个对象的原型(或处在原形链中), 请使用isPrototypeOf()  
```
    var p = {x: 1};
    var o = Object.create(p);
    p.isPrototypeOf(o)  //true p继承自o
    Object.prototype.isPrototypeOf(o)  //true p继承自object.prototype
```  

#### 8.2 类属性  
对象的类属性是一个字符串, 用以表示对象的类型信息  
调用对象的toString方法,获取对象的类

```
    function classof(o){
        if(o === null) return 'Null';
        if(o === undefined) return 'Undefined';
        return Object.prototype.toString.call(o).slice(8, -1);
    }
    //
    classof({}) //Object
```  

#### 8.3 可扩展性  
对象的可扩展性用以表示是否可以给对象添加新属性  
所有的内置对象和自定义对象都是显式可扩展的
用Object.esExtensible() 判断对象是否可扩展  
若要转换成不可扩展, 需要调用Object.preventExtensions() **不可扩展不可向可扩展转换**  
Object.Seal 将对象设置为不可扩展,同时将对象的自有属性都设置为不可配置的  
用Obeject.isSealed()来检测对象是否封闭  
Object.freeze() 将更严格的锁定对象(*冻结*), 不单将对象设置为不可扩展的和将其属性设置为不可配置的之外, 还将所有的自有数据属性设置为只读
Object.isFrozen() 检测对象是否冻结  
```
    //创建一个封闭对象, 包括一个冻结的原型和一个不可枚举的属性
    var seal = Object.seal(Object.create(Object.freeze({x: 1}),{y: {value: 2, writable: true}}));
```  

### 9. 序列化对象  
> 对象序列化(serialization)是指将对象的状态转换为字符串, 也可将字符串还原为对象  

- JSON.stringify(obj) 将对象的状态转换为字符串 
- JSON.parse()将字符串还原成对象  
*都用JSON作为s数据交换格式*, JSON的全称"JavaScript Object Notation"-JavaScript对象表示法
```
    var obj = {x: 1, y: {}};
    var s = JSON.stringify(obj) //
    var p = JSON.parse(s) //p 是obj的深拷贝
```  

### 10. 对象方法  
#### 10.1 toString方法  
toString方法没有参数, 它讲返回一个表示调用这个方法的对象值的字符串. 在需要将对象转换为字符串的时候, JavaScript都会调用这个方法. 如, 在使用 "+" 连接一个字符串和一个对象时或者在希望使用字符串的方法中使用对象时,都会调用toString();  
#### 10.2 toLocalString()方法  
这个方法返回一个表示这个对象本地化字符串. 对Number,Date有定制, 可以用来对数字, 日期和时间做本地化的转换  
#### 10.3 toJSON()  
对要执行序列化的对象来说, JSON.stringify()方法会调用toJSON()方法   
#### 10.4 valueOf()  
当JavaScript需要将对象转换为某种原始值而非字符串的时候才会调用他
Date.valueOf()  
## 六. 数组   
值的有序集合  
### 1. 稀疏数组  
稀疏数组就是包含从0开始的不连续索引的数组。
如果数组是稀疏的， length属性值大于元素个数  
```
    var arr = new Array(5);  //数组没有元素，但是长度是5
    var a = [];
    a[1000] = 1; //赋值添加一个元素，但是设置length为1001
```  

.在数组直接量中省略值时不会创建稀疏数组, 省略的元素在数组中是存在的.值为undefined, 这和数组元素不存在是有区别的, 我们通过in操作符就能看出两者的区别  
```
    var arr = [,,,];
    var arr2 = new Array(3);
    0 in arr   //true arr在索引0处有一个元素
    0 in arr2  //false  arr2在索引0处没有元素
```  

### 2. 数组长度  
每个数组有一个length属性, 这个属性使得数组区别于常规的JavaScript对象.  
设置数组length属性小于当前长度的非负整数n,当前数组中索引大于或等于n的元素将从数组中删除
```
    var arr = [1, 2, 3, 4, 5];
    arr.length = 3; //arr = [1, 2, 3]
    arr.length = 0; //arr= [],将数组置空

```  

### 3. 数组元素的添加和删除  
**push**方法在数组末尾添加一个或多个元素  
**unshift**在首部插入一个元素  
**delete** 删除指定的数组元素,但是并不改变数组长度  
```
    var arr = [1, 2, 3];
    delete arr[1];
    1 in arr  //false
    arr.length = 3;
```  

**pop** 从数组末尾删除一个元素, 使数组长度减1,并返回被删除的元素  
**shift** 从数组首部删除一个元素, 数组长度减1, 返回删除的元素  
> splice通用的插入, 删除或替换数组元素  
splice(start, delele, additem1, additem2, ...)
splice 接受三个及更多参数   
>    - start 代表起始位置 (无论是添加还是删除)  
>    - delele 代表要删除的数组元素个数, 从start位置开始算起  
>    - additem 代表要添加的数组元素  

```
    var arr = [1, 2, 3];
    arr.splice(1); // [2,3] 返回被删除元素组成的数组 只传入起始位置则, 从索引值为1元素都被删除
    arr.splice(1, 123); // delele值大于剩余元素个数,也会把剩余元素都删除
    arr.splice(1, 0, 1,23); // 删除0个元素, 同时在索引值为1的元素之后插入两个值1, 23
```  

### 4. 数组遍历  
forEach(); for...of  
### 5. 数组方法  
#### 5.1 join  
Array.join()将数组中所有元素都转化为字符串拼接在一起,可传入一个参数指定字符串的分隔符, 默认逗号  
```
    var arr = [1, 2, 3];
    arr.join(); //'1,2,3'
    arr.join('|') // '1|2|3'
    var arr2 = new Array(10);
    arr2.join('-'); //'---------'
```  
#### 5.2 reverse  
Array.reverse() 将数组中的元素颠倒,返回逆序数组  
#### 5.3 sort  
Array.sort() 将数组排序并返回排序后的数组  
要按照指定方式排序,则需要给sort传入一个比较函数  
**排序规则:** 
> 第一个参数要排在前, 比较函数返回一个小于0的值.  
反之, 第一个参数在后, 比较函数返回大于0的值  
如果,两个值相等(无所谓前后), 函数返回0 
```
    var arr= [1,23,2,4];
    arr.sort(function(a, b){
        return a-b;
    }) //[1,2,4,23]
```  

#### 5.4 concat  
Array.concat() 创建并返回一个新数组  
arr.concat(4, [5]);  
#### 5.5 slice  
Array.slice()方法返回数组的一个片段或子数组  
```
    var arr = [1,2,3,4,5];
    arr.slice(0, 3);  //[1,2,3]
    arr.slice(3);     //[4,5]
    arr.slice(1, -1); //[2,3,4]
    arr.slice(-3, -2); //[3]
```  
#### 5.6 forEach  
遍历数组 Array.forEach(function(ele,index){//...}) 
#### 5.7 map   
map()方法调用数组的每个元素传递给指定的函数, 返回一个数组
#### 5.8 filter  
filter()方法返回的数组元素是调用的数组的一个子集  
```
    var arr = [1, 2, 3, 4, 5];
    var small = arr.filter(function(x){ return x < 3; }); //[2, 1]
```  

#### 5.9 every和some  
every()和some()是数组的逻辑判定: 它们对数组元素应用指定的函数进行判定, 返回true或false  
```
    var arr = [1, 2, 3, 4, 5];
    arr.every(function(x){return x < 10;});  //true 所有值都<10
    arr.every(function(x){ return x % 2 === 0}); //false 不是所有的值都是偶数
    //some
    arr.some(function(x){ return x%2 === 0; }); //true arr包含偶数
    arr.some(isNaN) //false arr不包含NaN
```  

#### 5.10 reduce和reduceRight  
reduce()和reduceRight 方法使用指定的函数将数组元素进行组合,生成单个值。
```
    var arr = [1, 2, 3, 4, 5];
    var sum = arr.reduce(function(x, y){ return x+y;}); //数组求和

```  
#### 5.11 indexOf和lastIndexOf  
indexOf()和lastIndexOf()搜索整个数组中指定的元素,返回找到的第一个元素的索引，没找到返回-1， indexOf从头至尾, lastIndexOf从尾至头  

### 6. 数组类型  
Array.isArray()  
## 七. 函数  
### 1. 函数调用  
- 作为函数
- 作为方法
- 作为构造函数
- 通过call()和apply()方法间接调用  
#### 1.1 间接调用  
call() apply()  
### 2. 作为命名空间的函数  
```
    (function(){
        //模块代码
    }())
```  

### 3. 闭包  
函数对象可以通过作用域链互相关联起来, 函数体内部的变量都可以保存在函数作用域内, 这种特性被叫做'闭包'
```
    var scope = 'global scope';  //全局变量
    function checkscope() { //
        var scope = 'local scope';  //局部变量
        function f() {return scope;} //在作用域中返回这个值
        return f;
    }
    checkscope()();  //'local scope'
```  

.
```
    function counter() {
        var n = 0;
        return {
            count: function() {return  n++;},
            reset: function() {n = 0;}
        }
    }

    var c = counter(), d = counter(); //创建两个计数器
    c.count();  // 0
    d.count();  // 0 
    c.reset();  //
    c.count();  // 0 
    d.count();  // 1
```  

### 4. 函数属性, 方法和构造函数  
#### 4.1 length  
在函数体内, arguments.length表示传入函数的实参的个数  
#### 4.2 prototype  
每个函数都包含一个prototype属性, 这个属性是指向一个对象的引用, 这个对象叫'原型对象'  
#### 4.3 call和apply  
call()和apply()的第一个实参是要调用函数的母对象, 它是调用上下文, 在函数体内通过this来获得对它的引用. 想要以对象obj的方法来调用f(),可使用call()和apply()  
```
    f.call(obj);
    f.apply(obj);
    //
    f.call(obj,1,2) //以对象obj的方法来调用f(),并传入两个参数1, 2
    f.aplly(obj,[1,2]) //
```  
#### 4.4 bind  
将函数绑定至某个对象 
```
    function f(y){return this.x + y}  //待绑定函数
    var obj = {x:1}; // 要绑定的对象
    var g = f.bind(obj); // 通过调用g(x)来调用o.f(x) 
    g(2) // 3
    //
    function bind(f, o){
        if(f.bind) return f.bind(o);
        else return function() {
            return f.apply(o, arguments);
        }
    }
```  
#### 4.5 Function()构造函数  
var foo = new Function('x', 'y', 'return x*y;');   
### 5. 函数式编程  
#### 5.1 使用函数处理数组  
```
    //使用map和reduce函数来计算平均值和标准差
    var sum = function(x, y){return x+y};
    var square = function(x){return x*x};
    var data = [1,2,3,4,5];
    var mean = data.reduce(sum)/data.length;
    var deviations = data.map(function(x){return x-mean;});
    var stddev = Math.sqrt(deviations.map(square).reduce(sum)/(data.length-1))
```  

#### 5.2 高阶函数  
> 高阶函数, 操作函数的函数,接收一个或多个函数作为参数,并返回一个新函数  
```
    /* 返回一个新的可以计算的f(g(...))的函数
     * 返回的函数h()将它所有的实参传入g(), 然后将g()的返回值传入f()
     * 调用f()和g()时的this值和调用h()
     *    
     */
    function compose(f, g) {
        return function() {
            return f.call(this, g.apply(this, arguments));
        };
    }

    var square = function(x) {return x*x;};
    var sum = function(x, y){
        return x+y;
    }
    var squareofsum = compose(square, sum);
    squareofsum(2, 3)  //
```  
#### 5.3 不完全函数  

<!--20171122-->

## 八. 类和模块  
### 8.1 类和原型  

类的所有实例对象都从同一个原型对象上继承属性  
### 8.2 类和构造函数  

使用new调用构造函数会自动创建一个新对象  
调用构造函数一个重要特征是，构造函数的prototype属性被用作新对象的原型  
这意味着通过一个构造函数创建的所有对象都继承自同一个对象，因此他们是同一个类的成员  

```
    function Range(from, to) {
        //存储
        this.from = from;
        this.to = to;
    }
    // 所有的'子对象'都继承自这个对象
    Range.prototype = {
        //
        includes: (x)=> this.from <= x && x <= this.to;
    }
```  

在定义类时 默认首字母大写  

#### 8.2.1 constructor  
每个javascript函数都自动拥有一个protortype属性,这个属性的值是一个对象, 这个对象包含唯一一个不可枚举属性constructor. constructor属性的值是一个函数对象  

```
    var F = function() {}; //函数对象
    var pro = F.protptype; //这是与f相关的原型对象  
    var cons = pro.constructor; //这是与原型相关联的函数
    cons === F // true  对于任意函数f.prototype.constructor == F    
```  

在构造函数的原型中存在预先定义好的constructor属性, 这意味着对象通常继承的constructor均指代他们的构造函数. 由于构造函数是类的'公共标识', 因此这个**constructor属性为函数对象提供了类**  

```
    var o = new F(); // 创建F类的一个对象
    o.constructor === F; // true constructor属性指代这个类 
```  

在创建类的时候 更多的去使用预定义的原型对象是(而不是重写prototype对象, 重新定义的原型对象同时也需要将constructor属性重新定义), 预定义的原型对象包含constructor属性, 然后依次给原型对象添加方法  

```
    Range.prototype = {
        constructor: Range, //
        includes: function(x) {return this.from <= x && x <= this.to;}
    };
    //
    //扩展预定义的Range.prototype对象, 而不重写之
    // 这样就自动创建Range.prototype.constructor属性
    Range.prototype.includes = function(x) { return this.from <= x && x <= this.to;};
```  

### 8.3 JAVA式的类继承  
定义类:  
1. 定义一个构造函数, 并设置初始化新对象的实例属性. 
2. 给构造函数的prototype对象定义实例的方法. 
3. 给构造函数定义类字段和类属性. 

### 8.4 类的扩充  
Javascript中基于原型的继承机制是动态的: 对象从其原型继承属性, 如果创建对象后原型属性发生变化, 也会影响到继承这个原型的所有实例对象. 所以我们可以通过添加新方法来扩充Javascript类  
可以给数字, 字符串, 数组, 函数等数据类型添加方法  

### 8.5 类和类型  
检测任意对象类的方法 : instanceof运算符 constructor属性 构造函数名称 
#### 8.5.1 instanceof 运算符  

```
    function F() {

    }
    var f = new F();
    f instanceof F // true
```

构造函数是类的公共标识, 但原型是唯一的标识. 尽管instanceof 运算符的右操作数是构造函数, 但实际计算过程是检测了对象的继承关系, 而不是检测创建对象的构造函数  

#### 8.5.2 constructor属性  
识别对象是否属于某个类






















