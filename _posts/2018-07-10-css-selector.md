---
layout: post
title: "CSS Selectors"
description: "要怎麼才能選到心目中的那個它？讓我們來看看"
date: 2018-07-06
tags: [javascript]
comments: true
share: true
---

簡介一下關係選擇符, 和屬性選擇符。

---

## CSS選擇符



### 關係選擇符

#### 包含選擇符 `空格`

`A B` ，選擇 `A` 元素下的所有 `B` 元素。

使用**空格**符號, 看下方例子，這會選取`<div>`下的 **所有**` <p>` , 注意, 孫子跟後代都會被選取。

```css
div p {
   color: red;
}
```



```html
<div> 
    
	<P> 
		will be selected 
	    
        <P> 
	    	will also be selected 
	    </p>
        
	</p>
    
	<P> 
		will be selected 
	</p>
    
</div
```



#### 子選擇符 `>`

`A > B` ，選擇 `A` 元素下的**子**元素 `B`

使用 > 符號來選擇**子**元素，注意這**只會選到子元素**，孫子跟其他後代不會被選到。以下面範例，只會選擇`<div`下的`<p>`, `<p>`內的`<p>`不會被選到



```css
div > p {
   color: red;
}
```



在`<P>`內的`<P>`的字不會變色

```html
<div> 
    
	<P> 
		will be selected 
	    
        <P> 
	    	THIS WONT BE SELECTED!!!
	    </p>
        
	</p>
    
	<P> 
		will be selected 
	</p>
    
</div>
```



#### 相鄰選擇符 `+` 

`A + B`，選擇緊鄰在`A`之後的`B`元素, `A` 與 `B` 與元素必須屬於同一個層級。



```css
div + p {
   color: red;
}
```



```html
<div>
    <div> </div>
    <P> only this will be selected </P>
    <P> </P>
</div>
```



#### 兄弟選擇符 `~`

`A ~ B`，選擇`A`元素後面所有兄弟元素`B`, 元素`A` `B`必須是同一層級。

跟上面相鄰選擇符不同的地方是，這個`~`會選擇所有符合的統一層級元素。

```css
div ~ p {
   color: red;
}
```

```html
<div>
    <div> </div>
    <P> this will be selected </P>
    <P> this will be selected </P>
</div>
```



### 屬性選擇符

#### A[att]

`A[att]` 選擇具有`att` 屬性的`A`元素

如下，第一個`a`因爲有`alt`的屬性，因此可以被選到。

```css
a[alt] {
   color: red;
}
```

```html
<div>
	<a href="#" alt="test"> will be selected </a>
	<a href="#"></a>
</div>
```



#### A[att="val"]

選擇具有`att`屬性，且值等於`val`的`A`元素，如下範例，因爲第二個`<a>`雖然也有`alt`屬性但是其值不是`test`因此沒有被套用樣式。

```css
a[alt="test"] {
   color: red; 
}
```

```html
<div>
	<a href="#" alt="test"> will be selected </a>
	<a href="#" alt="link"></a>
</div>
```



這種選擇法，最長用在選擇某一類特殊的`<input>`中，如選擇輸入框等。

```css
input[type="text"]{   
    font-size：16px;
}
```



#### A[att~="val"]  `~`

這裏的`~="val"`是指具有`att`屬性，並且屬性的值中，被空白隔開的值有一個是`val`的`A`元素。

如下，`a[class~="show"]`會選擇class名稱包含`show` 的`<a>`元素

```css
a[class~="show"] {
   color: red; 
}
```

```html
<div>
	<a class="show link" href="#" alt="test"> will be selected </a>
	<a class="show" href="#" alt="link">will be selected</a>
	<a class="link show" href="#" alt="link">will be selected</a>
</div>
```



#### A[att^="val"] `^`

選擇具有`att`屬性，且值爲`val`**開頭**的`A`元素，下面的例子只有**前**面倆個`<a>`會被選取。

```css
a[class^="s"] {
   color: red; 
}
```

```html
<div>
	<a class="show link" href="#" alt="test"> will be selected </a>
	<a class="show" href="#" alt="link">will be selected</a>
	<a class="link show" href="#" alt="link"></a>
</div>
```



#### A[att$="val"] `#### 

選擇具有`att`屬性，且值爲`val`**結尾**的`A`元素，下面的例子只有**後面**倆個`<a>`會被選取。

```css
a[class$="w"] {
   color: red; 
}
```

```html
<div>
	<a class="show link" href="#" alt="test"></a>
	<a class="show" href="#" alt="link">will be selected</a>
	<a class="link show" href="#" alt="link"> will be selected </a>
</div>
```



#### A[att\*="val"] `*`

選擇具有`att`屬性，且值爲**包含**`val`的`A`元素，下面的例子所有的`<a>`都會被選取。

```css
a[class*="o"] {
   color: red; 	
}
```

```html
<div>
	<a class="show" href="#" alt="test">will be selected</a>
	<a class="shadow" href="#" alt="link">will be selected</a>
	<a class="overlay" href="#" alt="link"> will be selected </a>
</div>
```



#### A[att|="val"] `|`

選擇具有`att`屬性，其值是以`val`做爲開頭，並且以連接符`-`分開的A元素，如果值只有`val`, 也會被選取，如範例，前面三個都會被選取，因爲符合值只有`panel`或以`panel-`開頭的條件。

```css
a[class|="panel"] {
   color: red; 		
}
```

```html
<div>
	<div class="panel">will be selected</div>
	<div class="panel-title">will be selected</div>
	<div class="panel-content">will be selected</div>
	<div class="panel_content"></div>
</div>
```

