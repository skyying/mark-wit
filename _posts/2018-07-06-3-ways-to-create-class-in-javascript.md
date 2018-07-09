---
layout: post
title: "3 ways to define class in javascript"
description: "在還沒有es6的class之前，看看可以怎麼定義Javascript的類別"
date: 2018-07-06
tags: [javascript]
comments: true
share: true
---

這篇文章是我閱讀這篇 [3 ways to define a javascript class](http://www.phpied.com/3-ways-to-define-a-javascript-class/#more) 原文之後做的整理，有興趣的人建議可以直接讀[原文](http://www.phpied.com/3-ways-to-define-a-javascript-class/#more)哦

---

## 1.1 使用function

不要在`function`外面宣告`method`, 這樣這些`method`都是全域的，最後可能會產生命名上的衝突。

```javascript


function Apple( type ) {

	this.type = type;
	this.color = "red";
	this.getInfo = getAppleInfo;
}

// bad, 錯誤範例, 在consturctor外面宣告
function getAppleInfo() {
  return this.color + " " + this.type + " apple";
}

```

正確使用`function create class`的方式

```javascript
// good

function Apple (type) {
	this.type = type;
	this.color = "red";
	this.getInfo = function (){
		return this.color + " " + this.type + "apple";
	}
    
}

```

<br>

## 1.2 add method to the prototype

第一個方法是，每次 `new` 一個實例都會重新創造一次 `getInfo` 這個方法, 對於有些用不到這個`getInfo`的實例 ,這樣就會有點浪費，所以可以需要的時候，再加到 `Apple` 的 `prototype` 下就可以。一加到 `ClassName.prototype` 下，則所有的實例可享有`getInfo`這個方法了。


```javascript

function Apple (type) {
	this.type = type;
	this.color = "red";
}

Apple.prototype.getInfo = function() {
    return this.color + " " + this.type + "apple";

}

```

<br>

## 2. Using Object literals

建一個空的 `object`

```javascript
let o = {};
```

建立一個空的 `array`

```javascript
let a = [];
```

建立一個空的 `class`

```javascript
var apple = {
	type: "mac",
	color: "black",
	getInfo: function(){
		return this.color + " " + this.type + "apple";
	}
}
```


使用這種方法建立, 這個 `object` 就叫做 `singleton`, 在一些語言像 `Java` 中, `singleton`的意思是

> you can only have one single instnace of this class at any time, you cannot create more objects of the same class.


<br>
## 3. Singleton using a function

> use a function to define a signleton object

```javascript
var apple = new function(){
    this.type = "mac";
    this.color = "black";
    this.getInfo = function () {
    		return this.color + " " + this.type  + " apple";
    }
}
```


`new function(){...}` 同時做兩件事，創造一個匿名的 `function`, 然後用 `new invoke`。


