# 如何爲 `React Component` 增加樣式？


把設計稿轉成轉換成 `HTML and CSS`, 是很花費時間的, 前提是手刻，現在也有很多工具來加速
整個開發流程，最近在學`React`,現在來記錄一下，可以爲`React Component`新增樣式的幾個方法


### 使用CSS StyleSheet

```
import React from "react";
import "./style.css";
const Example = () = (
    <div className="example"/>
)
export default Example
```


### Inline Styleing

直接在 `js file` 內寫好`style object`, 在 `return React Object`時，新增在`style`上

```
import React from "react";

cosnt pStyle = {
    line-height: "20px",
    font-size: "16px"
}

const Example = () = (
    <p style={pStyle}/>
)

export default Example;
```


### CSS Module

這個概念其實跟第一種 `import stylesheet`的方式類似，只是把 `stylesheet` 當成 `module`匯入

```
import React from "react";
import Style from './example.css'

const Example = () = (
    <p className={Style.paragraph}/>
)

export default Example;
```

### Styled-components

最近很常看到這種寫法，基本上就是把 `Style` 和 component
綁在一起，只要匯入這個Component,他就是style好的，用法，要先匯入`Styled-components`這個 `library`, 


在project路徑下安裝 `Styled-components` 

```
npm i styled-components --save
```

範例如下，主要是建立一個Style的變數，並且把它當成`React element`的`Tag`來使用就可以了。

```
import React from "react";
import styled from "styled-components";

const Div = styled.div`
    margin: 0;
    border: 2px solid green;
    
    &:hover {
        border: 1px solid black; 
    }
`;

const Example = () = (
    <Div className={Style.paragraph}/>
)

export default Example;
```
