---
layout: post
title: "Filter false value, random sort, and IIFE"
description: "Filter, Sort, and IIFE"
date: 2019-05-23
tags: [javascript]
comments: true
share: true
---

---

## How to filter false value in javascript array
這些`value`在Javascript中都會被視爲`false`
* `0`
* `false`
* `null`
* `undefined`
* `""`

<br/>

如果要快速的在陣列中 `filter` 他們，可以用下面這個方法
```javascript
let ary = ["", 1, 2, "abc", null, undefined, 0];
ary.filter(Boolean); // [1, 2, "abc"]
```

<br/>
<br/>

## How to use sort to return an randomizd array

只要隨機的返回0.5~-0.5之間的值即可。
陣列中的元素會根據sort的比較函式的回傳值來決定排序。
<br/>

### 比較函式的回傳值決定傳入`a, b`兩個`element`的排列順序
* 0 : a, b 的位置不會改變
* 小於 0 : a 排在 b 之前
* 大於 0 : b 排在 a 之前

<br/>

```javascript
let ary = [1, 2, 3, 4, 5]
ary.sort((a, b) => Math.random() - 0.5 );
```
<br/>
`Math.random()`會回傳 0 (包含) - 1中間的浮點數(`float point`)
爲了讓有每一次呼叫比較函式的時候，能有隨機的機會得到介於`0.5 ~ -0.5`之間的值
把此次`Math.random()`的數減0.5即可。

<br/>
<br/>

## Classic closure problem

以下會`print`出什麼？
```javascript
for(var i = 0; i < 3; i++){
  setTimeout(function() {console.log(i)}, 1000);
} 
```

答案是`3, 3, 3`。

<br/>
因爲`var` 的變數作用域範圍是 `function scope`,  若要順利印出 `0, 1, 2` 可以改用 `let`宣告

```javascript
for(let i = 0; i < 3; i++){
  setTimeout(function() {console.log(i)}, 1000);
}
```

由於`let`屬於`block scope`，因此可以順利的保護住自己的變數。

那還有除了`let`以外的解法嗎？

<br/>

其實也是可以把 `i`當成變數傳入，並且立即`invoke`，也就是`Immediately Invoked Functions Expressions`

```javascript
for(var i = 0; i < 3; i++){
	 setTimeout((function(x){console.log(x)})(i), 1000)
}
```

由於`IIFE`的關係, `(function(x){console.log(x)})(i)`，傳進來的`i`因爲當下`invoke` + 這個匿名函式有自己的`execution context` 的關係被保留，
也就可以正確的印出`0, 1, 2`了。

