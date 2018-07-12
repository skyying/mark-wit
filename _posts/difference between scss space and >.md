## difference between scss space and >

在scss中, 可以看到這樣的選擇寫法

```css
A > B {

}
```

```css
A B {

}
```

這兩個的差別就是， A > B 的這個B是直接在A下的第一個小孩。 
所以如果對下面的html, 寫A > B是選不到C後面的B的，如果要選擇C後面的B，必須要寫成 A B，中間格一個空格
的寫法。
A B是指，A底下全部的 B 的意思。而A > B是指A底下第一個小孩，而且小孩是B。

```html

<div class="A"> 
    <div class="C"> oh </div>
    <div class="B"> hi </div>
<div> 

```