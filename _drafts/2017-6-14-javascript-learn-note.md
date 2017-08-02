---
layout: post
title:  "《Javascript高级程序设计》读书小结"
date:   2017-6-14
categories: javascript
---

##前言：

博文旨在记录书中的要点，达到复习的效果。

## 第一章 JavasScript简介

ECMA：European Computer Manufacturer's Asspciation 欧洲计算机制造商协会。

W3C：World Wide Web Consortium 万维网联盟，这个联盟指定了浏览器的DOM、BOM标准。

Javascript（以下简称JS）本来叫LiveScript，由Netscape公司的布兰登·艾奇开发，为了搭上媒体热炒的Java的顺风车，临时把名字改成了JS。

1997年，ECMA协会为了解决两种不同JS版本并存的局面，制定了ECMAScript（以下简称ES）脚本语言标准ECMA-262。

ECMA-262是ECMAScript的规范。

ES是JS的标准。

Web浏览器只是ES的宿主环境之一，其他宿主包括Node、ActionScript。

DOM和BOM是ES在Web浏览器中的扩展。

DOM是针对XML但经过扩展用于HTML的API，提供访问和操作网页的方法和接口。

BOM提供了和浏览器交互的接口。

ES规定了：语法、类型、语句、关键字、保留字、操作符、对象。

浏览器中的JS包括ES、DOM、BOM。

## 第二章 在HTML中使用JS

同步加载和异步加载：以`<script sync>`为例，如果没有`sync`属性，JS脚本是和网页其他内容一起同步加载的，同步加载的问题是如果JS文件很大，会阻塞后面内容的加载，所以我们通常把JS放在页脚避免阻塞HTML的加载。而加载`sync`属性，就表示脚本可以异步加载。这里的异步和现实中的“同步”（A和B都在18：30下班，可以说他们是同步下班的）很像，表示多个线程分别在运行。这时一个线程在加载JS文件，一个线程继续加载其他内容，两边“同时”加载，就是异步加载。`sync`的译为中文也是“同步”的意思。

经常看到很多网页把JS代码直接内联在HTML中，为什么这么做？
	在初学前端的时候就会被告知，不要随意写行内和内联代码，因为很难维护。
但随着模块化和打包工具的出现，让这种方式成为一种选择。
内联JS代码的好处：
1.减少http请求
2.在特定情况下让内嵌的js代码优先执行

## 第三章 基本概念

如果没有其他语言学习经验，在学习JS语法时，要多花很多功夫。

标识符：变量、函数、属性的名字。

'use strict'是一个编译指示，告诉支持JS的引擎切换到严格模式。

以可维护性为标准来衡量`;`和`{}`在JS中的使用。

### 基本数据类型

ES中有5种基础数据类型：`undefined`、`null`、`boolean`、`number`、`string`。

ES中有1种复杂数据类型：`object`。

Object的本质是由一组无序名值对组成的数据。

可以使用操作符typeof来变量的类型。

`typeof null` 会返回`object`，是因为特殊值null被认为是一个空对象的引用。

如果定义的变量是用来保存对象的，最好将变量初始化为null，这样后面就可以判断是否为null来确认变量是否已经保存了一个对象的引用。

实际上undefined是由null派生出来的，所以undefined == null //true，但在技术上他们在ES中的类型是不一样的，所以undefined === null //false。

### Number

保存浮点数值所需内存是整数值的两倍，所以ES会不失时机地将浮点数转换为整数。

对于极大和极小的数字可以用e来表示，比如31250000 === 3.125e7，0.0000003 === 3e-7

JS中浮点数的最高精度是17位小数，但在算数计算时其精确度远远不如证书，基于IEEE754数值的浮点计算通病，会发现0.1+0.2的结果是0.30000000000000004，由于这个误差而无法测试特定的浮点数，所以永远不要测试某个特定的浮点数值。

NaN（Not a Number），这个特殊数值用来表示本应该返回数值的操作数没有返回数值的情况。

为了避免出现意外，指定parseInt()的第二个参数（进制数）非常有必要。

parseFloat()只解析十进制数，其他进制的数都会被转换成0。

ES中的对象其实就是一组数据和功能的集合。

### Object

Object类型是所有它的实例的基础，所具有的属性和方法同样存在于更具体的对象中。

Object每个实例都具有下列属性和方法：

*  constructor：保存着用户创建当前对象的函数。对于Object而言，构造函数就是Object()。
*  hasOwnProperty(propertyName)：用于检查给定的属性当前对象实例中（不是在实例的原型中）是否存在。propertyName必须是是字符串。
*  isPrototypeOf(object)：用于检查传入的对象是否是当前对象的原型。
*  propertyIsEnumerable(propertyName)：用户检查给定的属性是否能够使用for-in语句枚举。propertyName必须是是字符串。
*  toLocaleString()：返回对象的字符串标识，该字符串与执行环境的地区对应。
*  toString()：返回对象的字符串表示。
*  valueOf()：返回对象的字符串、数值或布尔值表示。通常与toSrting()方法的返回值相同。

### 操作符

一元操作符：只能操作一个值的操作符

递增和递减操作符，又分前置和后置。执行前置递增和递减时，变量的值都是在语句被求值以前改变（副作用）。后置递增和递减是在包含它们的语句被求值之后才执行的。

### 循环语句

do-while语句是一种后测试循环语句，只有在循环体中的代码执行之后，才会测试出口条件。所以do-while至少会执行一次。

while语句属于前测试循环语句，在循环体内的代码被执行之前，就会对出口条件求值。所以循环体内的代码可能永远都不会执行。

for(initalizaption;expression;post-loop-expression) statement（初始化表达式、控制表达式、循环后表达式）都是可选的，如果三个表达式都省略，将会创建一个无限循环。

使用for in语句可以把一个对象的属性全部循环出来，但是碰到null或者undefined就不会执行循环体，所以在循环之前可以检查一下对象的值是不是null或者undefined。

给for循环增加一个label标记可以使用break和continue语句来控制嵌套for循环的退出。

switch语句可以在case中传入表达式；switch语句在比较值的时候是使用全等操作符的，所以不会发生类型转换。

### 函数

函数的主要作用是封装程序语句。

函数参数arguments只是与数组类似然而，然而它并不是数组的实例，只是可以通过方括号访问，用length来计算参数数量。

没有指定返回值的函数会默认返回一个undefined。

由于不存在函数签名，ES函数不能重载。（跟其他语言的区别）

## 第四章

### 基本类型和引用类型

ES变量包含两种不同的数据类型值：基本类型和引用类型。

基本类型是指简单的数据段（字符串、数值、布尔值、null、undefined），而引用类型只那些可能由多个值构成的对象（数组对象、json对象、自定义对象）。

引用类型的值是保存在内存中的对象。与其他语言不同，JS不允许直接访问内存中的位置，也就是不能直接操作对象的内存控件。所以我们在JS中复制保存着对象的某个变量时，操作的是对象的引用。但在为对象添加属性时，操作的实际是对象。

基本类型的变量被复制之后，复制变量和被复制变量是独立的，并不相互依赖。（感觉叫做clone比较合适）

引用类型的变量被复制之后，同样会将储存在变量对象中值复制一份到为新变量分配的空间中。不同的是，这个值实际上是一个指针，而这个指针指向存储在堆中的一个对象。所以改变其中任一变量，都会相互影响。

在向参数传递基本类型值时，被传递的值会被复制给arguments对象。在向参数传递引用类型的值时，会把这个值在内存中的地址复制给arguments对象，因此arguments中的对象发生变化会直接反映在函数外部。

检测引用类型值的类型可以使用instanceof操作符。

### 执行环境和作用域

执行环境定义了变量或函数有权访问的其他数据，决定了它们各自的行为。每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。

每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入到一个环境栈中。而在函数执行完之后，栈将其环境弹出，把控制权返回给之前的执行环境。

当代码在一个环境中执行时，会创建变量对象的一个作用域链。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的最前端是当前执行的代码所处的执行环境的变量对象。如果这个环境是函数，则将其活动对象作为变量对象。

概念区分 ：

执行环境 - 定义变量或函数的访问权限和行为，分为全局执行环境和函数执行环境。

变量对象 - 与执行环境关联的对象，保存了变量和函数的对象，但只在后台使用到。

活动对象 - 环境为函数时，会创建一个对象，这个对象初期只包含arguments对象。

作用域链  - 代码在环境中执行时，会把有权访问的变量对象串联起来，保证有序访问。

作用域 - 变量的有效范围。

this - this对象是在代码运行时基于函数的执行环境绑定的，在全局函数中this===window，而当函数作为某个对象的方法调用时，this===该对象。


执行上下文：为了管理执行上下文，JS引擎创建了执行上下文栈（Execution context stack，ECS）来管理执行上下文。


### 第五章 引用类型

#### Object

在ES中，引用类型是一种数据结构，用于将数据和功能组织在一起，它和一些面相对象语言里的类很像。

使用 var o = {} 时实际上不会调用new Object()。

#### Array

arr[arr.length] = 'new item'，利用数组的length可以方便的在数组末尾添加新项。

Array.isArray()可以方便的检测数组。

Array.sort()，这是数组自带的排序函数，可以传入两个参数(a,b)进行比较，返回负数则a在b前，返回0则a等于b,返回正则b在a之前。

Array的某个位置不存在数值时，访问时会返回undefined。

contact()方法，会先创建一个当前数组的副本然后将接受到的参数添加到副本的末尾，最后返回新数组。

slice()方法，接受一或两个参数，即要返回项的起始和结束位置，并不会影响原始数组。

splice()方法支持删除、插入、替换，支持三个参数起始位置、删除数量(可以为0)、插入的项。

数组有多个迭代方法：
every()，传入的函数返回值都为true则返回true。
filter()，返回 传入的函数 返回值为true的项组成的数组。
forEach()，对每一项都运行传入的函数且没有返回值。
map()，返回 传入的函数 返回的结果组成的数组。
some()，传入的函数返回值只要有true，则返回true。

数组有两个归并方法：
reduce()、reduceRight()，传入的方法接受四个参数(prev,current,index,array)，reduceRight从相反的方向返回。


#### Date


Date.parse()方法可以根据传入的日期字符串返回相应的毫秒数


#### RegExp

g：全局模式，所有字符串都会被匹配
i：不区分大小写模式
m：多行模式

\：表示下一个字符是特殊的，一般用来转义。
^：匹配输入的开始，支持m。
$：匹配输入的结束，支持m。
*：匹配前一个表达式0次或多次，等价于{0,}。
+：匹配前一个表达式1次或多次，等价于{1,}。
?：匹配前一个表达式0或1次，等价于{0,1}。
.：匹配除换行符之外的任何单个字符。
(x)：匹配'x'并且记住匹配项，括号被称为捕获括号。
(?:x)：匹配'x'但不记住匹配项，括号被称为非捕获括号。
x(?=y)：匹配'x'仅仅当'x'后面跟着'y'，这种叫做正向肯定查找。
x(?!y)：匹配'x'仅仅当'x'后面不跟着'y'，这种叫做正向否定查找。
x|y：匹配'x'或者'y'。
{n}：n是一个正整数，匹配了前面一个字符刚好发生了n次。
{n,m}：n和m都是正整数。匹配前面的字符至少n次，最多m次。如果n或m为0，这个值被忽略。
[xyz]：一个字符集合。匹配方括号中的任意字符，包括转义序列。你可以使用破折号（-）来指定一个字符的范围。对于点（.）和星号（*）这样的特殊符号在一个字符集中没有特殊意义，这意味着你不必对它们进行转义，不过转义后也起作用。
[^xyz]：一个反向字符集。匹配任何没有包含方括号中的字符。你可以使用破折号（-）来指定一个字符范围。
[\b]：匹配一个退格（U+008）。
\b：匹配一个词的边界。
\B：匹配一个非单词边界。
\cX：当X是处于A到Z之间的字符的时候，匹配字符串中的一个控制符。
\d：匹配一个数字。等价于[0-9]。
\D：匹配一个非数字字符。等价于[^0-9]。
\f：匹配一个换页符（U+000C）。
\n：匹配一个换行符（U+000A）。
\r：匹配一个回车符（U+000D）。
\s：匹配一个空白字符，包括空格、制表符、换页换行符。等于[ \f\n\r\t\v\u00a0\u1680\u180e\u2000-\u200a\u2028\u2029\u202f\u205f\u3000\ufeff]。
\S：匹配一个非空白字符。
\t：匹配一个水平制表符（U+0009）。
\v：匹配一个垂直制表符（Y+000B）。
\w：匹配一个单字字符（字母、数字或者下划线）。
\W：匹配一个非单字字符。等价于[^A-Za-z)-9_]。
\n：当n是一个正整数，一个返回引用到最后一个与有n插入的正值表达式匹配的副字符串。


#### Function

function 是 Function对象的实例

Global对象和Math对象是ES中内置的，大多数ES实现中都不能直接访问Gloabl对象。全局变量和函数都是Global对象的属性，在浏览器中window实现了Global对象作用。


### 面向对象的程序设计

对象是无序键值对属性的集合。

可以使用Object.defineProperty()来定义对象的getter和setter。

创建对象的方式：

1、Object构造函数 var object = new Object()

2、字面量方式 var object = {}

这两种方式都有缺点就是，当你需要创建多哥对象时就会产生重复代码。

例：

var person = {
	name:oldliu,
	age:18
}

var person2 = {
	name:wuyanzu,
	age:40
}

var person3 = {
	name:xxx,
	age:50
}

3、工厂模式

function Factory(prop1,prop2,func1){
	var obj = new Object()
	obj.prop1 = prop1;
	obj.prop1 = prop1;
	obj.func1 = function(){
		//do sometthing
	}
	return obj;
}

当你创建很多同类对象时，就需要用到工厂模式。

4、构造函数模式

function Construtor(prop1,prop2,func1){
	this.prop1 = prop1;
	this.prop2  = prop2;
	this.func1 = function(){
		//do something
	}
}

var object = new Construtor(foo,foo,bar);
var object1 = new Construtor(foo,foo,bar);

构造函数是利用函数可以创建类型这个特性来创建对象的，属于用户自定义对象，JS中有内置对象如Object、Function。并且构造函数模式是依赖于new 操作符创建对象的，如果不使用new操作符，这就是一个首字母大写的函数而已。

使用new操作符创建自定义对象时会发生以下几个步骤：
（1）创建对象
（2）将构造函数的作用域赋给新对象，这个时候this会指向对象。
（3）执行构造函数中的代码（为对象添加属性什么的）
（4）返回新的对象

而由构造函数创建的对象中会有一个construtor属性，这个属性会指向构造函数。

构造函数创建的优势是，这种创建方法和创建“类”很像，构造函数可以当成一种标识，也即“类”的名字，这样可以很清晰知道这个对象是从哪儿来的。

以构造函数创建的对象是定义在Global对象中的，在浏览器也即是window对象。

构造函数的缺点呢，就是每个方法都会在实例上重新创建一遍。

因为function实际上是Function的实例，所以在自定义构造函数中添加的方法在每个new出来的实例中都是不同的。
也即是object.func1 !== object1.func1。
这样new的实例越多，方法就越多，占用的内存也就越多。

5、原型模式

所有我们创建的函数都有一个prototype属性，这个属性包含了调用的构造函数的对象实例的原型对象。

原型对象的好处是可以让所有实例共享它所包含的属性和方法，换句话说，你可以把所有属性和方法都放进prototype中。

function Constructor(){}
Constuctor.prototype.prop1 = prop1;
Constuctor.prototype.prop2 = prop3;
Constuctor.prototype.func1 = function(){
	//do something
};

构造函数、原型对象、对象实例之间的关系：
构造函数有一个属性指向原型对象。
原型对象有一个属性指向构造函数。
而new出来的对象实例会包含一个[[prototype]]的指针，这个属性指向构造函数的原型对象，在浏览器中可以通过__proto__访问。
使用Object.getPrototypeOf()可以访问对象的原型。

function Constructor(){}
Constructor.ptototype = {...}
实际上这句代码等于：Constructor.ptototype = new Object();
这样就相当于把自定义构造函数的原型的构造函数属性指向了Object，这个你查看Constructor的构造函数也会发现指向的是Object。
解决方法就是：

Constructor.ptototype = {
	constructor:Constructor
}

在使用这种字面量写入原型对象时，把构造函数属性也写进去，并且自定义指向函数。

6、组合构造函数和原型模式

所有写入原型对象中的属性都是共享的，这个时候会有一个问题就是当属性的值是引用类型时，就会导致一个实例改变，而其他实例都跟着变。

而组合使用前面说到的构造函数和原型模式，可以完美解决这个问题。
function Constructor(name,age){
	this.name = name;
	this.age = age;
}

Constructor.prototype = {
	constructor:Constructor,
	sayName:function(){
		console.log(this.name);
	}
}

这种方法是使用最普遍的构造对象的方法。

7、动态原型模式

function Constructor(name,age,sayName){
	this.name = name;
	this.age = age;
	if(typeof this.sayName != 'function'){
		Constructor.prototype.sayName = function(){
			console.log(this.name)
		}
	}
}

8、寄生构造函数模式

function Construtor(name,age){
	var obj = new Object();
	obj.name = name;
	obj.age = age;
	obj.sayName = function(){
		console.log(this.name)
	}
	return obj;
}

很少用。

9、稳妥构造函数模式

function Constructor(name,age){
	var obj = new Object();
	obj.name = name;
	obj.age = age;
	obj.sayName = function(){
		console.log(name)
	}
	return obj;
}

var object1 = Constructor('xx',20)

稳妥就是指没有公共属性，方法也不引用this对象。
适合在一些禁止this和new的环境中使用。

#### 继承

##### 原型链继承：

function A(){
	this.name = 'a';
}

A.prototype.sayName = function(){
	console.log(this.name)
}

function B(){
	this.name = 'b'
}

B.prototype = new A();

var b = new B();

b.sayName(); // 'b'

每个对象的实例都会包含一个指向原型对象的指针，如果B对象的原型对象等于A对象的实例，这就相当于把A的对象原型指向了B对象的对象原型，这样就可以说是B继承了A，但同时也会继承实例所拥有的属性和方法。

所有对象的原型的默认原型都是Object(),所以你总是能在所有的对象里发现最初的原型对象是Object()

原型继承会有一些问题，那就是当你继承的父对象的属性中有引用类型的值，那当你修改子类型的这个属性的时候，同时也会修改父类型的属性。

function A(){
	this.color = ['red','blue','yellow'];
}

function B(){
	A.call(this);	
}

##### 借用构造函数继承：

借用构造函数就是在构造函数B中执行A构造函数，然后把A中所绑定到this的属性都绑定到B上来。
这样即使是引用类型的值，也可以在子对象实例中随意修改了。

但是借用构造函数也有点问题，就是之前构造函数中存在的问题，没法共享。

##### 组合继承：

这个时候就要用组合继承了，就是构造函数和原型对象一起用起来。

function A(){
	this.color = ['red','blue','yellow'];
}

A.prototype.drawColor = function(){
	console.log(this.color)
}

function B(){
	A.call(this);	
	this.xxx = xxx;
}

B.prototype = new A();

B.prototype.xxx = function(){
	// do something
}

##### 原型式继承：

function object(obj){
	function F(){}
	F.prototype = obj;
	return new F();
}

##### 组合寄生模式

function inheritPrototype(subType, superType){
	 var prototype = Object(superType.prototype); //创建对象
	 prototype.constructor = subType; //增强对象
	 subType.prototype = prototype; //指定对象
}

function SuperType(){
	this.name = 'super';
}

SuperType.prototype.sayName = function(){
	console.log(this.name)
}

function SubType(){
	SuperType.call(this)
	this.name = 'sub';
}

inheritPrototype(SubType,SuperType)

