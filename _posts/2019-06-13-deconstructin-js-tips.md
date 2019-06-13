---
layout: post
title: "destructuring JS tips"
description: "destructuring from object and reassign"
date: 2019-06-13
tags: [js]
comments: true
share: true
---
解構賦值的小撇步
---

```js

const person = {
  name: "David",
  age: 16
}

// destructuring person

const {name: firstName, age} = person;
console.log(firstName); // "David"

```


