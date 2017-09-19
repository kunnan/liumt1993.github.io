---
layout: post
title:  "《Javascript设计模式》笔记"
date:   2017-8-15
categories: my blog
---

## Constructor（构造器）模式

在其他OOP语言中，Constructor是一种在内存已分配给该对象的情况下，用于初始化新创建对象的特殊方法。

在JS中，我们可以利用JS自带的Object()构造器创建对象，也可以使用自定义构造器创建对象。

<script>
	function Cat(name){
		this.name = name
	}
	var tom = new Cat('tom')
	console.log(tom)
</script>

## Module（模块）模式

模块模式是帮助我们清晰的分离和组织项目中代码的方式。

Module模式使用闭包来封装私有属性，再把公有属性暴露出来。

优点：公私方法分离，使代码更整洁和安全。

缺点：公私有属性的转换非常麻烦，需要在每一个使用到的地方修改。扩展性会差一点。

<script>
	var module = (function(){

		var _private = 0;

		var expt = {};

		expt.write = function(){
			console.log(_private)
		}

		expt.add = function(num){
			_private += num;
		}

		return expt;
	})()

	module.add(1)

	module.add(2)

	module.write()
</script>

## Revealing Module（揭示模块）模式

与Module模式的区别是，它返回一个对公共属性命名更具体的匿名对象。

优点：改善了模块模式的可读性

缺点：

<script>
	var module = (function(){

		var _private = 0;

		var publicWrite = function(){
			console.log(_private)
		}

		var publicAdd = function(num){
			_private += num;
		}

		return {
			write: publicWrite,
			add: publicAdd
		};

	})()

	module.add(1)

	module.add(2)

	module.write()

</script>

## Singleton（单例）模式

单例模式创建的对象只会实例化一次，以后再调用这个对象，只会指向已经实例化的对象，而不会再次创建。

单例对象通常用来协调其他对象，用来储存一些公共的工具方法或者变量等。

<script>
	// 用对象字面量创建的实例对象只会初始化一次，所有是单例对象
	var st1 = {
		foo:function(){
			console.log('foo')
		},
		bar:function(){
			console.log('bar')
		}
	}

	st1.foo()
	
	var st2 = (function(){
		
		var instance;

		var public = {
			foo:function(){
			console.log('foo')
			},
			bar:function(){
				console.log('bar')
			}
		}

		if(!instance){
			instance = public
			return public
		}else{
			return instance
		}

	})()

	st2
</script>

## Observer（观察者）模式

观察者模式定义了一种一对多的关系，它让多个观察者对象同时收听某一个主题对象，当主题对象的状态发生改变时就会通知所有观察者。

观察者模式的使用场景：当一个对象的改变需要同时改变其他对象，并且不知道具体有多少对象需要改变的时候。