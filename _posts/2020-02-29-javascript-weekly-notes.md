---
layout: post
title: "Javascript Weekly - Some notes"
description: "My reading notes"
date: 2020-02-29
tags: [js, reading]
comments: true
share: true
---
Some reading notes of this weeks' javascript weekly
---

## Make your test fail
blog: https://kentcdodds.com/blog/make-your-test-fail
video: https://egghead.io/lessons/jest-make-your-test-fail?pl=kent-s-blog-posts-as-screencasts-eefa540c

一個滿值得注意的寫test的概念。你的 test 都 pass 了, 先別太開心, 如果你回去改了 source code 後, tests 沒有 fail, 其實這樣的 test 更糟, 因爲他給你盲目的信心。

> And this is why it’s so important that once your test is passing, you go to the source and ensure that if you break the functionality you’re testing, that your test will fail. Otherwise, someone could inadvertently break your code and the tests wouldn’t catch that. Those kinds of tests are worse than worthless because not only do they not give you confidence, but they give you a false sense of security which means you won’t think to write good tests either.





https://www.swyx.io/writing/js-tools-metrics-logs-traces/

## React 16.13.0 is released
[React 16.13.0](https://reactjs.org/blog/2020/02/26/react-v16.13.0.html)

修了一些bug, 還有新增一些 deprecation warning 爲下一版的 major release 做準備。


* 目前支援在同一個 component 內 render 時 setState, 如果是不同 component 會噴警告。如果要在不同的 component 內 render 時 setState, 請用 useEffect 。
* warning for conflict style rules
* warning for some deprecated string ref
* ...

## Metrics, logs and traces in javascript tools
### Javascript metrics
 * Build size: 噴警告常受到忽略
 > Tools that hold the line and don’t let things get worse are so powerful
 * Speed (speed regression) 值得注意何時你的程式碼開始慢下來, 透過 bundlers or log execution time or [The User Timing API](https://developers.google.com/web/tools/lighthouse/audits/console-time), [performance.now()](https://developer.mozilla.org/en-US/docs/Web/API/Performance/now)
 > We want to be alert to regressions in speed, and we want to notice when our app slows down as a function of input or code size as that is predictive of future performance deterioration.

### Javascript logging
* 老是 console.log 不是辦法, node developer 可以`fs.createWriteStream('file.txt')`
* structure log 有特定 format，表格式的 log
* log level, 有意義的 log 層級, 幫忙過濾資訊

### traces and events
* 介紹一些 node 的 trace API call and event 的 tools



