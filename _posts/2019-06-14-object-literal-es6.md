---
layout: post
title: "ES6 Object literal"
description: "介紹 es6 object literal 特別的地方"
date: 2019-06-14
tags: [javascript]
comments: true
share: true
---
最近在看 ES6 的一些語法，記錄一下 Object literal
---

```js
var object = {
  __proto__: {a: "a"},
  // duplicate function
  ['__proto__']: {b: "b"},
  // shorthand for handler: handler
  handler, 
  // 之後可以用obj.toString來呼叫
  toString(){
    // code here
  },
  // dynamic property names
  // 可以動態計算key的名稱
  ["prop" + (() => 42)()]: 42
}
```