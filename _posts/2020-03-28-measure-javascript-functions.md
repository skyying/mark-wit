---
layout: post
title: "幾種測量 javascript functions 效能的方法"
description: ""
date: 2020-03-28
tags: [js, reading]
comments: true
share: true
---
Javascript weekly 筆記
---

## Measuring the Performance of JavaScript Functions
[文章連結](https://felixgerschau.com/measuring-the-performance-of-java-script-functions)

根據這份[報告](http://www.mcrinc.com/Documents/Newsletters/201110_why_web_performance_matters.pdf)有 88% 的顧客會因爲效能差的使用者體驗而沒有意願繼續使用。


如果能知道程式碼在那些地方導致效能差，是個有效改善的方法。下面介紹幾種方法來測量。

### Performnace.now

可以用這個 [API](https://blog.logrocket.com/how-to-practically-use-performance-api-to-measure-performance/) 來測量單一 `function` 執行的時間，類似 `python` 的 `time.time()`

```javascript
const t0 = performance.now();
for (let i = 0; i < array.length; i++) 
{
  // some code
}
const t1 = performance.now();
console.log(t1 - t0, 'milliseconds');
```

爲什麼不用 `Date.now()` 就好 ? 
`Date.now()` 參考的系統的時間，有時候需要對時，回傳的 `timestamp` 不一定會增加。

>This doesn't only mean that it's not as precise, but it's also not always incrementing.

### console.time

帶入同樣的字串就可以做測量了。`Date.now()` 是不同系統有可能有不同結果, 而 `console.time` 則是因瀏覽器不同而有可能不同。 

```javascript
console.time('test');
for (let i = 0; i < array.length; i++) {
  // some code
}
console.timeEnd('test');
```

### 其他值得注意的事

找到 `bottleneck` 或那段程式碼跑的比較慢，就用 `console.time('..')`來做測量。注意，可以對你要測量的 `function` 使用較真實的 `input`, 然後對 `function` 多跑幾次取平均值避免誤差


```javascript
function testForEach(x) {
  console.time('test-forEach');
  const res = [];
  x.forEach((value, index) => {
    res.push(value / 1.2 * 0.1);
  });

  console.timeEnd('test-forEach')
  return res;
}

function testFor(x) {
  console.time('test-for');
  const res = [];
  for (let i = 0; i < x.length; i ++) {
    res.push(x[i] / 1.2 * 0.1);
  }

  console.timeEnd('test-for')
  return res;
}
```

```javascript
const x = new Array(100000).fill(Math.random());
testForEach(x);
testFor(x);
```


```javascript
test-forEach: 27ms - timer ended
test-for: 3ms - timer ended
```

可以注意到 `ForEach` 比 `forloop` 慢, 而慢的程度也因 `browser` 而有不同, 這是因爲不同的瀏覽器有不同調整效能的方式。有時候可能覺得些微的差異跑在開發環境中或許還過得去，但要記得，開發機器通常比一般手機要來得快。
