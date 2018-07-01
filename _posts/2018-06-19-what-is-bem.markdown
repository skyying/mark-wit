---
layout: post
title: "What is BEM?"
description: "BEM是一種撰寫CSS的方式，主打這種寫法跟命名架構能夠讓CSS更模組化，也較傳統的寫法好維護。"
date: 2018-06-19
tags: [SCSS/CSS]
comments: true
share: true
---

---

`BEM` 這三個字來自`Block`, `Element`, `Modifier`

### Block

區塊，就算是只有自己一個區塊存在也不會出事的，就是Block

像是`header`, `container`, `menu`, `checkbox`, `input`

### Element

`Block` 的一部分，不能獨立存在，和`Block`有語義上的關連

像是
`menu item`, `list itme`, `checkbox caption`, `header title`

### Modifier

`Block` or `Element` 的 `flag`

像是`disabled`, `highlighted`, `checked` 等等

![BEM](/images/bem.png)

# 爲什麼要用BEM?

* 模組化的概念
  減少`cascading`的寫法
  模組化後，之後可以轉移到其他專案

* 重複利用性高
* 結構化之後，好維護


# 怎麼用BEM呢？

拿`button` 當範例，看官網上提供的兩個範例，把狀態跟元素分開。


`HTML`

```html
<button class="button">
	Normal button
</button>
<button class="button button--state-success">
	Success button
</button>
<button class="button button--state-danger">
	Danger button
</button>
```


`CSS`
```css
.button {
	display: inline-block;
	border-radius: 3px;
	padding: 7px 12px;
	border: 1px solid #D5D5D5;
	background-image: linear-gradient(#EEE, #DDD);
	font: 700 13px/18px Helvetica, arial;
}
.button--state-success {
	color: #FFF;
	background: #569E3D linear-gradient(#79D858, #569E3D) repeat-x;
	border-color: #4A993E;
}
.button--state-danger {
	color: #900;
}

```


# 如何命名？

```html
<div class="block">
  <span class="block-element"></span>
</div>
```

如果最外層是`block`, 那裏面的`element`元件應該和他有語義上的關聯。像是下面的這個範例

```html
<div class="menu">
  <span class="menu-item"></span>
</div>
```

如果是額外的`Modifier`, 則應該有自己的`class`,


`Block` 最好是從 `DOM Node` 架構拆分出來，以一個下拉式選單 `selector` 爲例。

`BEM` 架構的 `class` 規劃如下


```
Block select
   Modifier disabled
   Modifier multiple
     ELEMENT optgroup
     ELEMENT option
        Modifier disabled
        Modifier selected
```

`selector` 是一個 `Block`, 但這個Selector 有幾種屬性，整個下拉式選單`disable`了，或多選，這個`disable` or `multiple` 就是這個 `selector` 的 `modifier`, 所以他們自己也有 `class`。

而`optgroup`, `option`是這個`selector`的`element`，因此他們也有自己的`class`，然後這寫`element`也有自己的`modifier`, 所以延伸下去。


## 命名潛規則

* 儘量簡短和有語義上的關聯
* 僅使用拉丁字，dash `-`, 或數字
* 其他：`block` 和 `element` 的連接通常用雙下線 `__`, 而 `element` 或 `block` 和 `modifier`的連接則使用單下線`_`或`--`，主要是團隊內自己有共識即可。


```css
.b-heading
.b-text-input
.b__heading--light
```

這裏的`.b` 是指`block`的意思，預設的block寫法。
