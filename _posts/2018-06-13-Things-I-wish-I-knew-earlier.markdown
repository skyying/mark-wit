---
layout: post
title: "Some Vim Tips"
description: "一些提高 VIM 生產力的小方法"
date: 2018-06-13
tags: [vim]
comments: true
share: true
---

---


### 讓你的手跟上你的頭腦
* 使用`.`直接重複上一個動作，有機會比`Insert Mode`的`regex`更快
* 用`gn`可以選取到下一個符合結果的位置，用`cgn`加`.`可以快速取代找到的某些`pattern`
* 進入`insert mode`有更多選擇, 多用`S, o, O, a, A, I`, `S`可以刪除整行並進入`insert mode`
* `[[`, `]]`, `((`, `))`, `{{`, `}}` 多用這些來跳來跳去


### 🔣 容易打錯的符號
* 有些符號特別難打，如`]`, `|`, `$`, `&`，可以爲他們在`insert mode`重新`map`

可在`~/.vimrc`內放, 當然如果是縮寫的設定最好還是配合`autocmd filetype`一起服用

```
put this in your ~/.vimrc

"每次打 or 就會出現 ||
iab or ||

"每次打 and 就會出現 &&
iab and &&
```
### ⌨️ 打的更快, 關於`Insert Mode`的`Key mapping`
#### 好用
* `ctrl-w`往後刪除一整個字
* `ctrl-h`往後刪除一個字元
* `ctrl-u`刪除一整行
* `ctrl-i` 等於`tab`
* `ctrl-c`, `ctrl-o` 離開insert mode

### 好好練習
* `ctrl-r` 在`insert mode`輸入`ctrl-r`後加上`+` 可以直接貼上剛剛`yank`的。

### 好好想想
* `VI` 之所以叫`VI` 是有原因的，那就是儘量遠離`V` 和 `I` 這兩個 `mode`。


