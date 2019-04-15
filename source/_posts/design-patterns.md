---
title: design patterns - JavaScript设计模式
date: 2017-05-25 17:16:06
tags: [JavaScript]
categories: 知识点
---

哎，最不想整理的就是这一块了

<div align=center>
![“封面”](/images/bg/0040.jpeg)
</div>
<!--more-->
最初在设计模式 一书中，许多设计模式都鼓励使用松散耦合。在更改一个代码片段时，就会发生问题，系统其他部分 —— 曾认为完全不相关的部分中也有可能出现级联破坏。该问题在于紧密耦合 。系统某个部分中的函数和类严重依赖于系统的其他部分中函数和类的行为和结构。您需要一组模式，使这些类能够相互通信，但不希望将它们紧密绑定在一起，以避免出现联锁。
# 工厂模式
## 简单工厂模式
```js
	function BuyHero(name,type,price){
		var obj = {};
		obj.name = name;
		obj.age = type;
		obj.price = price;
		obj.sayName = function(){
			return this.name;
		};
		return obj;
	}
	var h1 = new BuyHero('Teemo','ADC','6300');
	var h2 = new BuyHero('Amumu','Jungle','3100');
	//返回都是object 无法识别对象的类型，哪个对象的实列
    console.log(typeof h1);  // object
    console.log(typeof h2);  // object
    console.log(h1 instanceof Object); // true
```
## 复杂工厂模式
```js
	// 定义英雄池的构造函数
	var League = function(name){
		this.name = name;
		this.method = function(){
			return this.name;
		}
	};
	League.prototype = {
		constructor: League,
		/*
		 * 买英雄这个方法
		 * @param {name} 英雄名字
		 */
		buyHero: function(name){
			var hero = this.createHero(name);
			// 执行Q、W...技能，哦，业务逻辑
			hero.Q();
			hero.W();
			return hero;
		},
		createHero: function(model){
			throw new Error("父类是抽象类不能直接调用，需要子类重写该方法");
		}
	};
	// 实现原型继承
	function extend(Sub,Sup) {//Sub表示子类，Sup表示超类
		var F = function(){};// 首先定义一个空函数
		F.prototype = Sup.prototype;// 设置空函数的原型为超类的原型
		Sub.prototype = new F();// 实例化空函数，并把超类原型引用传递给子类
		Sub.prototype.constructor = Sub;// 重置子类原型的构造器为子类自身
		Sub.sup = Sup.prototype;// 在子类中保存超类的原型,避免子类与超类耦合
		if(Sup.prototype.constructor === Object.prototype.constructor) {
			Sup.prototype.constructor = Sup;// 检测超类原型的构造器是否为原型自身
		}
	}
	var HeroChild = function(name){
		this.name = name;
		// 继承构造函数父类中的属性和方法
		League.call(this,name);
	};
	// 子类继承父类原型方法
	extend(HeroChild,League);
	// BicycleChild 子类重写父类的方法
	HeroChild.prototype.createHero = function(){
		var Q = function(){
			console.log("执行Q业务操作");
		};
		var W = function(){
			console.log("执行W业务操作");
		};
		return {
			Q: Q,
			W: W
		}
	};
	var Teemo = new HeroChild("提莫");
    console.log(Teemo);
    console.log(Teemo.name);//提莫
    Teemo.buyHero();
```
## 理解
> 父类是一个抽象类，不能被实列化,将其成员对象的实列化推迟到子类中，子类可以重写父类接口方法以便创建的时候指定自己的对象类型。
子类之间是相互独立的。

## 优点
解决多个类似对象声明的问题;解决实列化对象产生重复的问题。在父类中编写一些相同的方法代码,在子类中重写该父类的方法，去实现具体的业务逻辑。
### 1/
弱化对象间的耦合，防止代码的重复。在一个方法中进行类的实例化，可以消除重复性的代码。
### 2/
重复性的代码可以放在父类去编写，子类继承于父类的所有成员属性和方法，子类只专注于实现自己的业务逻辑。
## 缺点
无法获取对象类型
# 单体模式
## 封装单体模式
```js
	// 写法一
	var Singleton = function(name){
		this.name = name;
		this.instance = null;
	};
	Singleton.prototype.getName = function(){
		return this.name;
	};
	// 获取实例对象
	function getInstance(name) {
		if(!this.instance) {
			this.instance = new Singleton(name);
		}
		return this.instance;
	}
	// 写法二
	var Singleton = function(name){
        this.name = name;
    };
    Singleton.prototype.getName = function(){
        return this.name;
    }
    // 获取实例对象
    var getInstance = (function() {
        var instance = null;
        return function(name) {
            if(!instance) {
                instance = new Singleton(name);
            }
            return instance;
        }
    })();
	// 测试单体模式的实例
	var a = getInstance("aa");
	var b = getInstance("bb");
	console.log(a===b);// true,b的实例就是a的实例
```

## 使用代理实现单体模式
具体的单体模式中的实例化类的事情交给代理函数去处理，这样做的好处是具体的业务逻辑分开了，代理只管代理的业务逻辑，在这里代理的作用是实例化对象，并且只实例化一次; 创建div代码只管创建div，其他的不管；
```js
	//创建一个div
	//第一种
	var CreateDiv = function(html) {
		this.html = html;
		this.init();
	};
	CreateDiv.prototype.init = function(){
		var div = document.createElement("div");
		div.innerHTML = this.html;
		document.body.appendChild(div);
	};
	// 代理实现单体模式
	var ProxyMode = (function(){
		var instance;
		return function(html) {
			if(!instance) {
				instance = new CreateDiv("rawraw hello");
			}
			return instance;
		}
	})();
	//第二种
    // 代理实现单体模式
    var ProxyMode = (function(){
        var instance;
        return function(html) {
            if(!instance) {
                instance = document.createElement("div");
                instance.innerHTML = "rawraw hello";
                document.body.appendChild(instance);
            }
            return instance;
        }
    })();
	var a = new ProxyMode("aaa");
	var b = new ProxyMode("bbb");
	console.log(a===b);// true
```

## 综合
```js
	// 创建div
	var createWindow = function(){
		var div = document.createElement("div");
		div.innerHTML = "我是弹窗内容";
		div.style.display = 'none';
		document.body.appendChild(div);
		return div;
	};
	// 创建iframe
	var createIframe = function(){
		var iframe = document.createElement("iframe");
		document.body.appendChild(iframe);
		return iframe;
	};
	// 获取实例的封装代码
	var getInstance = function(fn) {
		var result;
		return function(){
			return result || (result = fn.call(this,arguments));
		}
	};
	// 测试创建div
	var createSingleDiv = getInstance(createWindow);
	document.getElementById("test").onclick = function(){
		var win = createSingleDiv();
		win.style.display = "block";
	};
	// 测试创建iframe
	var createSingleIframe = getInstance(createIframe);
	document.getElementById("test").onclick = function(){
		var win = createSingleIframe();
		win.innerHTML = "rawraw hello";
	};
```

## 理解
> 单体模式是以对象字面量的方式来创建单体模式一个用来划分命名空间并将一批属性和方法组织在一起的对象，如果它可以被实例化，那么它只能被实例化一次。
以对象字面量的方式来创建单体模式。
>> 适用场景：弹窗

## 优点
## 缺点
# 模块模式
```js
var singleMode = (function(){
    var privateNum = 112;// 创建私有变量
    // 创建私有函数
    function privateFunc(){
        // 实现自己的业务逻辑代码
    }
    // 返回一个对象包含公有方法和属性
    return {
        publicMethod1: publicMethod1,
        publicMethod2: publicMethod1
    };
})();
```

模块模式使用了一个返回对象的匿名函数。在这个匿名函数内部，先定义了私有变量和函数，供内部函数使用，然后将一个对象字面量作为函数的值返回，返回的对象字面量中只包含可以公开的属性和方法。这样的话，可以提供外部使用该方法；由于该返回对象中的公有方法是在匿名函数内部定义的，因此它可以访问内部的私有变量和函数。
## 增强的模块模式
适合那些单列必须是某种类型的实例，同时还必须添加某些属性或方法对其加以增强的情况。
```js
	function CustomType() {
		this.name = "rawraw";
	}
	CustomType.prototype.getName = function(){
		return this.name;
	};
	var application = (function(){
		var privateA = "aa";// 定义私有
		function A(){}// 定义私有函数
		var object = new CustomType();// 实例化一个对象后，返回该实例，然后为该实例增加一些公有属性和方法
		object.A = "cc";// 添加公有属性
		// 添加公有方法
		object.B = function(){
			return privateA;
		};
		return object;// 返回该对象
	})();
	console.log(application);
	console.log(application.A);// cc
	console.log(application.B()); // aa
	console.log(application.name); // rawraw
	console.log(application.getName());// rawraw
```

## 理解
> 模块模式的思路是为单体模式添加私有变量和私有方法能够减少全局变量的使用；
>> 适用场景：必须创建一个对象并以某些数据进行初始化，同时还要公开一些能够访问这些私有数据的方法

## 优点
## 缺点
# 代理模式


## 理解
>
>> 适用场景：图片预加载

## 案例
```js
// 不使用代理的预加载图片函数如下
var myImage = (function(){
    var imgNode = document.createElement("img");
    document.body.appendChild(imgNode);
    var img = new Image();
    img.onload = function(){
        imgNode.src = this.src;
    };
    return {
        setSrc: function(src) {
            imgNode.src = "http://img.lanrentuku.com/img/allimg/1212/5-121204193Q9-50.gif";
            img.src = src;
        }
    }
})();
// 调用方式
myImage.setSrc("https://img.alicdn.com/tps/i4/TB1b_neLXXXXXcoXFXXc8PZ9XXX-130-200.png");
var myImage = (function(){
    var imgNode = document.createElement("img");
    document.body.appendChild(imgNode);
    return {
        setSrc: function(src) {
            imgNode.src = src;
        }
    }
})();
// 代理模式
var ProxyImage = (function(){
    var img = new Image();
    img.onload = function(){
        myImage.setSrc(this.src);
    };
    return {
        setSrc: function(src) {
                         myImage.setSrc("http://img.lanrentuku.com/img/allimg/1212/5-121204193Q9-50.gif");
        img.src = src;
        }
    }
})();
// 调用方式
ProxyImage.setSrc("https://img.alicdn.com/tps/i4/TB1b_neLXXXXXcoXFXXc8PZ9XXX-130-200.png");
```

## 优点
1.代理对象可以代替本体被实例化，并使其可以被远程访问；
2.它还可以把本体实例化推迟到真正需要的时候；对于实例化比较费时的本体对象，或者因为尺寸比较大以至于不用时不适于保存在内存中的本体，我们可以推迟实例化该对象；
## 缺点
# 职责链模式
```
```
## 理解
## 优点
## 缺点
# 命令模式
```
```
## 理解
## 优点
## 缺点
# 模板方法模式
```
```
## 理解
## 优点
## 缺点
# 策略模式
```
```
## 理解
## 优点
## 缺点
# 发布-订阅模式(观察者模式)
```
```
## 理解
## 优点
## 缺点
# 中介者模式
```
```
## 理解
## 优点
## 缺点
http://www.cnblogs.com/tugenhua0707/p/5198407.html