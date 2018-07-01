# 如何用border來Debug css layout

如果在切很複雜的版型時，經常會碰到複雜的間距調整、對齊等問題，此時有一個方法可以快速讓你找到問題。


在你的 `css` file 中，利用 `*` 這個 `css universal selector`來加`border`。

```
* {

   border: 1px solid red;

}
```

看起來會很複雜，但能夠快速提供視覺反饋，知道哪裏出了問題。


如下

![border-layout](/images/2018/06/border-layout.png)


其實也不一定要套用到 `Universal selector` 上，也可以針對只有問題的 `element`
設定即可。

```

.element {
    border: 1px solid red;
}

```

`Debug` 完記得移除。

