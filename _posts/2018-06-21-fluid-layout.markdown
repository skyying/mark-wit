---
layout: post
title: "Magic Formula for Fluid Layout"
description: "怎麼用一個簡單的公式來實現流動式佈局呢?"
date: 2018-06-21
tags: [SCSS/CSS]
comments: true
share: true
---

流動式佈局就是固定寬高的反義詞，當`designer`的設計稿裏面的`element`, `layout`充滿固定尺寸時，我們要如何實現
流動式佈局呢？

在`Responsive Web Design with HTML5 and CSS3` 這本書中的第三章有提出一個公式可以換算成實習流動佈局的百分比。

## Magic Formula
` target / context = result `

看上面這公式不懂是正常的，翻成白話文的意思就是，

這裏填你想要計算他寬度的元件的寬度 / 這個元件被放在誰裏面的這個誰的寬度 = 得到的元件的寬度百分比。

頭暈，有沒有這麼複雜，但，仔細想想，這不就是**兩個元件之間的寬度比例換算**。

` a / b = c ` 

什麼!!! 🤔 就這樣 ? 是的。

<br>

## 來看看下面的例子

```html

<section class='main'>
   <article>
        something ...
   </article>
</section>

```

<br>
如果拿到的設計稿, 假設`section`的寬度爲 `920px`, `article`的寬度爲 `600px`, 那要怎麼得到 `article` 正確的動態寬度呢？

```css

article {

   width:  0.652173913%;  /* (600 / 920) */

}

```

這個這麼不好記的百分比其實就是**父子兩的寬度比例**。

如果是最外層的`wrapper`, 可以視需求，讓他的寬度是100%, 其他的皆照固定寬度換算出接近的百分比即可。


