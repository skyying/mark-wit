# 誰用了這組熱鍵？

使用 `vim` 時，常會安裝好幾個 `plugin` 有時候 `plugin` 之間的熱鍵會**互沖**
比方說像前端開發利器 `emmet` 和 `youCompeleteMe` 之間的 `tab` 之戰。

今天來介紹一個好方法，當設定`~/.vimrc` 時，使用把熱鍵跟功能配對時，有時候會*歪腰*，如果想知道現在到底是那個`plugin`或哪裏的鬼設定``正在使用這組`hotkey`，只需要再底下的 `command line` 打入`map ` + 你要查詢的hotkey即可

比方說，我想要知道誰正用`ctrl - b`的組合熱鍵，範例如下。

```
:map <c-b>
```

![Command for query mapping key biding](./images/2018/06/query-key-binding.png)

按下`enter`後，就會出現`ctrl + b`是`mapping`到什麼功能的說明。

![Result](./images/2018/06/result.png)
