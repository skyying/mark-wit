---
layout: post
title: "Javascript Coding style from idiomatic.js"
description: "特別記錄一下幾種idiomatic.js上正確的coding style"
date: 2018-07-05
tags: [javascript, coding style]
comments: true
share: true
---
關於這種會養成習慣的細節，還是越早知道越好。
---

這篇如原文附註，所有列出來的規範並不是教條，而是參考的javascript撰寫指南而已，這篇文章沒有包含全部，如果有興趣，建議優先看[原文](https://github.com/rwaldron/idiomatic.js)。特別記錄的用意是爲了要加強印象。


## 1. 用空格提升可讀性

### if statement

```javascript

if ( codition ) {
    // logic
}

```

<br> 
## 2. for loop 的宣告

在 loop 外先宣告變數


```javascript

let i, 
    length = 100;
	
for ( i = 0; i < length; i++ ) {
    // logic here
}

// 或

let i = 0,
    length = 100;
	
for ( ; i < length; i++ ) {
    // logic here
}


```
<br> 

## 3. 變數的宣告在函式作用域頂端


```javascript

// good
function foo() {
    var bar = "",
        qux;
    //logic here
}


// bad

function foo() {
    let foo, 
        bar;
    if ( condition ) {
        bar = "";
        // logic here
    }
}


// good

function foo() {
    let foo;
    if ( condition ) {
        let bar = "";
    }
}

```

<br>
## 4. 一致性

無論是引號或空格留白。

<br>
## 5. 直接型別的檢查

#### String

```javascript
typeof variable === "string"
```

#### Number

```javascript
typeof variable === "number"
```
#### Boolean

```javascript
typeof variable === "boolean"
```

#### Object

```javascript
typeof variable === "object"
```

#### **Array**

```javascript
Array.isArray( arrayLikeObject )
```

#### Node
```javascript
element.nodeType === 1
```

<br>
## 6. undefined的檢查

#### global variable

```javascript
type of variable === "undefined"
```

#### local variable

```javascript
variable === undefined
```

#### Properity

```
object.prop === undefine
object.hasOwnProperty( prop )
"prop" in object
```

<br>
## 7.轉換型別的範例

`parseInt`的範例

```javascript

let num = 8.9
parseInt( num, 10);

// 等於

~~num;
num >> 0;
num >>> 0;

//都是8


```

**負數總是不一樣**

```
let num = -8.9
~~num  
num >> 0 //都會是 -8


num >>> 0 

// 結果是 4294967294

```

<br>

## 8. if statement

#### 判斷array內有沒有東西

```javascript
// don't use this
if ( array.length > 0 ) ...

// good
if( array.length) ...

```

#### 判斷array是否爲空

```javascript
// don't use this
if (array.length === 0 ) ...

// good
if ( !array.length ) ..

```

### 判斷是否不是空字串

```javascript
// don't use this
if (string !== "" ) ...

// good
if ( string ) ..

```

### 判斷是否是空字串

```javascript
// don't use this
if (string === "" ) ...

// good
if ( !string ) ..

```

### 判斷變數爲真


```javascript
// don't use this
if (foo === true ) ...

// good
if ( foo ) ..

```


### 判斷變數爲假

```javascript
// don't use this
if (foo === false ) ... // 除非你要檢查的的確是boolean type的false

// good
if ( !foo ) ..

```

### 判斷爲null or undefine but not false or 0 or ""

```javascript
// don't use this
if (foo === null || foo === undefined ) ...


// good, 只用 == 會讓 null 等於 null and undefined 但不會是false or 0 or ""
if ( foo == null ) ..


```

`null == undefine // return true`



## 實用的撰寫風格


```javascript

(function( global) {

    var Module = (function(){
     		
        var data = "secret";
     		
        return {
            // comment here
            bool: true,
            // comment here
            string: "a string"
        
            getData: function() {
                // logic here     		
            },
            setData: function() {
                // logic here     		
            }
        };
     });
     
     // logic here
     
     // 把模組變成全域物件
     
     global.Module = Module;
    
})( this );

```

## 實用的constructor撰寫風格

```javascript

(function( global ) {
	
	function Ctor( foo ) {
		
		this.foo = foo;
		
		return this;
	}
	
	Ctor.prototype.getFoo = function() {
		return this.foo;
	}

	// 除了使用new 來呼叫construcotr之外的方法
	
	var ctor = function( foo ) {
		return new Ctor( foo );
	}
	
	// 把construtor 變成全域物件
	global.ctor = ctor;

})( this );


```

待續... 





