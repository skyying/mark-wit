---
layout: post
title: "Nested Structure in SCSS and the Symbol &"
description: "什麼是SCSS的巢狀結構？還有這個詭異的符號 & 又是什麼意思？"
date: 2018-06-21
tags: [SCSS/CSS]
comments: true
share: true
---

---
### 巢狀結構

SCSS 是爲了一套css preprocessor, 讓我們再寫css上更有效率，管理上也更方便。
其中的一個特點，就是nested structure, 什麼是巢狀結構呢？簡單而言，就是與 `html` 語言類似，一層一層的包起來。
而裏面的孩子，與外層是有血緣關係的，看下面的範例。

```scss
 .panel {

    color: white;

 }

.head {

    color: red;

    .panel {

           color: blue;

    }

}

```
<br>
上面的這`css class`會被`Compile`成

```css
.panel {

    color: white;

}

.head {

     color: read;

}

.head .panel {

    color: blue;

}

```

<br>

在`.head` 內嵌 `.panel`, 因此, 第二個 `.panel` 是指在 `.head` 這個類別下的,如果有其他元素的`class` 是`.panel`則套用這個`style`
`BUT` 還有一個特別的寫法。看看這裏

```scss
.head {

   color: red;

   .panel {

      color: blue;

   }

   /* & means the wrapper class, in this case it means .head */
   .panel & {

      color: yellow;

   }

}

```

<br>
最後的包在`.head`下的 `.panel & ` 則會被`Compile`成
```css
.panel .head {

    /* css code here */

}
```

<br>
而不是想像中的
```css
.head .panel .head{

    /* css code here */

}
```
<br>
## & 的意思
`&` 可以有許多用途，但他是指父層類別，通常拿來寫一些僞類別時很好用，看下面範例：

```scss

.link {

    color: blue;

    &:hover {

         color: grey;

    }

    &:active{

         color: blue;

    }
    
}

```

避免一再重複的打父類別，就可以直接用`&`這個符號代替。


