本条目对于强迫症适用。

默认情况下 Dock 被一堆系统自带的应用占据着，而其中大部分我都很少使用，当我打开几个常用应用后，Dock 上会有很多图标，每个图标都会被挤得很小。所以我会把所有 Dock 上固定的图标都删掉，这样一来 Dock 上只有我打开的应用。

PS：Finder 图标是删不掉的。

除了一个一个删除图标，也可以通过这个命令来隐藏所有的固定图标：

```
defaults write com.apple.dock static-only -boolean true; killall Dock
```

恢复也非常简单：

```
defaults delete com.apple.dock static-only; killall Dock
```