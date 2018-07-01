
在`.vimrc`的設定內，通常會依照個人習慣重新`mapping key`, 可以讓這個`mapping` 的設定只在某些模式下使用。

## Recursive or Non-recursive 

map的方法主要分爲`recursive` `and non-recursive` 
`recursive`的意思是，結果會被套用，被套用的結果也會被套用。我想我還是說原文。


> the mapping is expanded to a result, then the result is expanded to another result, and so on.

#### 範例如下
```
map j gg
map Q j
```

這時後打出`Q`其實會出現`gg`, 而不是`j`，如果是將一開始的 `j`, `gg` 設定如下

```
noremap j gg
noremap Q j
```

此時輸入`Q`, 會正確的出現 `j`。 這就是`non-recursive`, 意思是，設定只會波及該次，我還是說說原文。


> The mapping is only expanded once, and the result is applied/executed.

在`Learn vimscript the hardway` 這本書內建議，最好都是用`non-recursive`的方式來進行設定，除了 `leader key`的設定以外，
其他`mapping`建議都用`non-recursive`的方式來`mapping` 

## map, noremap and other mode

兩大`mapping mode`之首就是這兩個，一個是`map`, 一個是`noremap`, 所有`recursive`的`map mode`會都使用`map` 並且前綴代表該模式的字母。
而所有`non-recursive`的`map mode`則都會使用`noremap, no = non, re = recursive`。如果想指定在其他模式下進行`recursive or non-recursive`的 `mapping`，
就是在這兩個字前面加上代表該模式的字母就可以了。

#### 模式字母：

* n : normal only
* v : visual and select
* o : operator-pending
* x : visual only
* s : selection only
* i : insert
* c : command - line
* l : insert, command-line, regexp-search

比方說，`nmap`就是`normal mode recursive`的意思， `vnoremap` 就是`visual and select mode non-recursive`的`map`。
舉個例子，如果想對難按的 `<esc> key`重新配對，只想讓這個設定發生在`non-recursive`的`insert mode`，則可以在`vim`的`command-line` 鍵入 

```
:inoremap jk <esc>
```

一勞永逸的辦法則是直接把這行加入`~/.vimrc`檔案內。in your `~/.vimrc file`

```
inoremap jk <esc>    "remap ESC key
```



