import scss file 



可以把Scss file拆成更小的檔案。

如果在檔名前面加上underline, 如_partial.scss, 那import時，只需要寫下列這樣即可。

```
@import "partial.scss"; 
```





變數

若要使用變數，在變數名稱前面加上$字號，像這樣

```
$primary-color: green;
```

就可以把變數帶入了

```
h1 {
    color: $primary-color;
}
```

之後只需要修改變數，就可以改變所有套用這個變數的值了。

要注意的幾點：



### 變數有scope範圍。

```

$primaiy-color: green;

h1{
    color: $secondary-color; //會產生錯誤，因爲secondary-color之後才宣告
}

h2{
    $secondary-color: blue;
    color: $secondary-color
}
```



變數也可以用在class的命名上

```
$wom: women-of-the-marvel-universe;

.#{$wom} {  
    content: "#{$wom}";
}



.${$wom}-text{
    color: blue;
}

```

上面會編譯成

```
 women-of-the-marvel-universe {
     content: "women-of-the-marvel-universe"
 }
 
 women-of-the-marvel-universe-text{
     color: blue;
 }
```



### scss built in function

Scss 的顏色都會被轉譯成hex value, scss支援rgb的寫法，其中內建幾個調整顏色的功能



```
$base-color: #a83b24;
$light-color: lighten($base-color, 30%);  //較base-color亮30%
$dark-color: darken($base-color, 20%);  //較base-color暗20%
$mix-color: mix($base-color, yellow, 20);   //混合兩個顏色 base-color, yellow

```

