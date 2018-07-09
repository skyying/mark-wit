---
layout: post
title: "Javascript Design Pattern - Constuctor Pattern"
description: "這篇介紹3種創造物件的方式，4種設定物件屬性的方式，還有如何讓各種實例之間共享方法"
date: 2018-07-06
tags: [javascript, design pattern]
comments: true
share: true
---
這篇是我的[Javascript Design Pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#writingdesignpatterns)的閱讀筆記, 有興趣的人也可以直接閱讀原文。

---

## Constructor Pattern
Constructor是一個特殊的method用來初始化一個新創立的物件。除了準備好讓這個物件可以被使用之外，也可以接受一堆參數值作爲物件的屬性值。

#### 3種建立物件的方法

```javascript 

let Obj = {};

//or

let Obj = Object.create( Object.prototype );

// or

let Obj = new Object();

```

<br>
#### 4種 `assign key value pair` 的方式

```javascript
// 1. 用dot .

Obj.someKey = "hi";


// 2. 用square bracket []

Obj[someKey] = "hi";


// 3. Object.defineProperty

Obj.defineProperty(Obj, "someKey", {
    value: "value",
    writable: true,
    readable: true,
    configurable: true,

})


// 也可以建立一個函數來做這件事，提高可讀性

var defineProp = function(obj, key, value) {
    var config = {
        value: "value",
        writable: true,
        enumerable: true,
        configurable: true,
    };
    Object.defineProperty( obj, key, config);
};

// 要使用的話，我們先建立一個空的"person" object

var person = Object.create( Object.prototype );

defineProp( person, "car", "Delorean" );
defineProp( person, "hasBeard", false );

// return object
// {car: "Delorean", hasBeard: fasle}


// 4. Object.defineProperties

Object.defineProperties( Obj, {
    "someKey" : {
        value: "hi",
        writable: true
    },
    "anotherKey" : {
        value: "hey",
        writable: true
    }
});

```

<br>
上面 3，４的方法，也可以拿來給繼承的object使用

```javascript

var driver = Object.create( person );

defineProp(driver, "speed", "100");

// driver.car
// "Delorean"

// driver.speed
// 100
```


<br>
## Basic Constructors

```javascript

function Car( model, year, miles ) {
	this.model = model;
	this.year = year;
	this.miles = miles;
	
	this.toString = fucntion (){
		return this.model + "has done " + this.miles + " miles";
	}
}

// 用法
// 可以創造Car的實例

var civic = new Car( "Honda Civic", 2009, 20000);
var mondeo = new Car( "Ford Mondeo", 2010, 5000);

// civic.toString();
// return "Honda Civic has done 20000 miles"

// mondeo.toString();
// return "Ford Mondeo has done 5000 miles"

```

這裏可以看到`toString`基本上是共享的，所有實例的`toString`功能都相同，其實不需要每次初始化都建立一次。

更好的`Pattern`如下

```javascript

function Car( model, year, miles ) {
	this.model = model;
	this.year = year;
	this.miles = miles;
	
}

Car.prototype.toString = function(){
     return this.model + "has done " + this.miles + " miles";
}

```
所有實例現在都共享這個`toString`的函數了。
