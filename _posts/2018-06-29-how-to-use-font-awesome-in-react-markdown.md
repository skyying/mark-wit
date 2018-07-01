
[Font Awesome](https://fontawesome.com/) 是一套免費的`css icon library`, 我是看直播才知道這麼方便，就填個`class`, `icon`就神奇的出現了，看得我嚇到吃手手，拿~麼方便的東西，我要趕緊記下來。

樓下是我的筆記。


## Install

先安裝, 在專案的根目錄下執行這個打開 `commnad line` 輸入以下指令

```
npm install --save font-awesome
```

<br>

## Import

接着把它`import`到專案的index.js下，就是你專案的entry point

```
import 'font-awesome/css/font-awesome.min.css';

```
<br>
## 如何使用

經過正確的安裝和匯入`css`檔後，只需要在`html/jsx`上先用一個`i`的`tag`, 記得要設定對正確的`class`名稱, `jsx`的話請使用`className`, 這樣就可以了。


#### 查詢Class Name

先到[官網](https://fontawesome.com/icons?d=gallery)，點選你需要的`icon`, 進入後頁面下方就會有使用範例。

![example](/images/fa.png)


```

//html
<i class="far fa-smile">smile</i>


// jsx
<i className="far fa-smile">smile</i>


```

<br><br>

## 第二選擇

這個方式比 font-awesome 官網上的 [how to use - React](https://fontawesome.com/how-to-use/on-the-web/using-with/react) 安裝設定方便


先安裝3個package

```
npm i --save @fortawesome/fontawesome-svg-core@prerelease \
npm i --save @fortawesome/free-solid-svg-icons@prerelease \
npm i --save @fortawesome/react-fontawesome@prerelease

```


接着在App.js import 

```
import { library } from '@fortawesome/fontawesome-svg-core'
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
import { faStroopwafel } from '@fortawesome/free-solid-svg-icons'

library.add(faStroopwafel)
```


<br>

可以看到最後一個是`faStroopwafel`,需要把這個`faStroopwafel`加入剛第一個`import`的`library`中，如果你要用的`icon`很多，得逐一匯入, 好處應該是可以節省空間，壞處是要一一查詢`icon`在`react-fonawesome module內`的名字，偏偏這個名字的格式大小寫跟官網的`class name`又不一樣，不能複製貼上就是有那麼一點麻煩阿! 
就這麼一波30%的加到library後，從此這個faStroopwafel就變成一個有用的東西。
<br>


```
import React from 'react'
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'

export const Food = () => (
  <div>
    Favorite Food: <FontAwesomeIcon icon="stroopwafel" />
  </div>
)

```


<br>
後來想想，其實也沒這麼麻煩啦，我想應該也可以去list出這些名稱，然後把他們自動加入library內，這樣就不用手動一一輸入了，而且還可以把這個做成一個`react component`來使用...。








