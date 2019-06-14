---
layout: post
title: "What is javascript static methods"
description: "所謂的靜態方法，到底是怎麼回事？"
date: 2019-06-14
tags: [javascript]
comments: true
share: true
---
一切都跟 Javascript 全部都是 object 有關。
---

什麼是靜態方法呢？

`Javascript`是個`prototype-based`的`language`, 而不是`class-based`的語言，如果要實例化一個`object`, 可以使用`new`這個`keyword`，可以達到類似`OOP`要做的事。

而`prototype`是怎麼運作的呢？如果你從一個`object`的實例化中去`access`他的`member`像是`methods, attributes, constant`等，會從`prototype chain`一路找下去，一直要麻找到想找的`member`, 不然就是往下一個`prototype`的屬性開始找。



```js
foo = {bar: "baz"};
console.log(foo.bar); // logs "baz"

foo = {};
console.log(foo.bar); // logs undefined

function Foo(){}
Foo.prototype = {bar: "baz"};
f = new Fool();
console.log(f.bar);
// print "baz", 因爲f找不到bar這個屬性，所以往prototype object去找

f.bar = "buzz";
console.log(f.bar); // buzz, 因爲直接在f.bar找到了，所以就不繼續往下找

```

在`Javascript`中，所有的東西都是`object`。

```javascript
function Foo(){}
```

上面這個不單只是定義一個新的`function`, 同時也是定義一個新的`function object`可以用`Foo`來`access`它。

這就是爲什麼可以用`Foo.prototype`來`access Foo`的`prototype`

或你也可以`assign new functions`給`Foo`
```javascript
Foo.talk = function(){
  alert("hello world!");
};
```
這個`function`可以被用`Foo.talk()`來`invoke`

```js
// create a class instance
f = new Foo();

// defined a shared method for the class
Foo.prototype.bar = function(){
  // code here
}

// defined a public static method for the class
// 公開可以取用的屬性
Foo.baz = function(){
  // code here
}
```

ECMAScript 2015 用了一個語法糖來做到上面這三件事

```javascript

class Foo {
  bar (){
    // code here
  }
  //讓這個方法可以不需實例化就被呼叫，實例後則無法用實例來呼叫這個static method
  static baz () {
    // code here
  }
}
```

所以如果要access bar, 就可以用
```javascript
const f = new Foo();
```

如果要access baz, 可以用下面的語法
```javascript
Foo.baz();
```




#### 參考資料
* https://stackoverflow.com/questions/7694501/class-vs-static-method-in-javascript
* https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Classes/static


