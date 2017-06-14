---
layout: post
title:  "《Javascript高级程序设计》读书小结"
date:   2017-6-14
categories: javascript
---

##前言：

博文旨在记录书中的要点，达到复习的效果。

##第一章 JavasScript简介

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

##第二章 在HTML中使用JS

同步加载和异步加载：以`<script sync>`为例，如果没有`sync`属性，JS脚本是和网页其他内容一起同步加载的，同步加载的问题是如果JS文件很大，会阻塞后面内容的加载，所以我们通常把JS放在页脚避免阻塞HTML的加载。而加载`sync`属性，就表示脚本可以异步加载。这里的异步和现实中的“同步”（A和B都在18：30下班，可以说他们是同步下班的）很像，表示多个线程分别在运行。这时一个线程在加载JS文件，一个线程继续加载其他内容，两边“同时”加载，就是异步加载。`sync`的译为中文也是“同步”的意思。

经常看到很多网页把JS代码直接内联在HTML中，为什么这么做？
	在初学前端的时候就会被告知，不要随意写行内和内联代码，因为很难维护。
但随着模块化和打包工具的出现，让这种方式成为一种选择。
内联JS代码的好处：
1.减少http请求
2.在特定情况下让内嵌的js代码优先执行

##第三章 基本概念

如果没有其他语言学习经验，在学习JS语法时，要多花很多功夫。

标识符：变量、函数、属性的名字。

'use strict'是一个编译指示，告诉支持JS的引擎切换到严格模式。

以可维护性为标准来衡量`;`和`{}`在JS中的使用。

ES中有5种基础数据类型：`undefined`、`null`、`boolean`、`number`、`string`；一种复杂数据类型：`object`

Object的本质是由一组无序名值对组成的数据。

可以使用操作符typeof来变量的类型。

`typeof null` 会返回`object`，是因为特殊值null被认为是一个空对象的引用。

如果定义的变量是用来保存对象的，最好将变量初始化为null，这样后面就可以判断是否为null来确认变量是否已经保存了一个对象的引用。

实际上undefined是由null派生出来的，所以undefined == null //true，但在技术上他们在ES中的类型是不一样的，所以undefined === null //false。

保存浮点数值所需内存是整数值的两倍，所以ES会不失时机地将浮点数转换为整数。

对于极大和极小的数字可以用e来表示，比如31250000 === 3.125e7，0.0000003 === 3e-7

JS中浮点数的最高精度是17位小数，但在算数计算时其精确度远远不如证书，基于IEEE754数值的浮点计算通病，会发现0.1+0.2的结果是0.30000000000000004，由于这个误差而无法测试特定的浮点数，所以永远不要测试某个特定的浮点数值。


NaN（Not a Number），这个特殊数值用来表示本应该返回数值的操作数没有返回数值的情况。

为了避免出现意外，指定parseInt()的第二个参数（进制数）非常有必要。

parseFloat()只解析十进制数，其他进制的数都会被转换成0。

ES中的对象其实就是一组数据和功能的集合。

Object类型是所有它的实例的基础，所具有的属性和方法同样存在于更具体的对象中。

Object每个实例都具有下列属性和方法：

*  constructor：保存着用户创建当前对象的函数。对于Object而言，构造函数就是Object()。
*  hasOwnProperty(propertyName)：用于检查给定的属性当前对象实例中（不是在实例的原型中）是否存在。propertyName必须是是字符串。
*  isPrototypeOf(object)：用于检查传入的对象是否是当前对象的原型。
*  propertyIsEnumerable(propertyName)：用户检查给定的属性是否能够使用for-in语句枚举。propertyName必须是是字符串。
*  toLocaleString()：返回对象的字符串标识，该字符串与执行环境的地区对应。
*  toString()：返回对象的字符串表示。
*  valueOf()：返回对象的字符串、数值或布尔值表示。通常与toSrting()方法的返回值相同。