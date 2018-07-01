


# Single Node Rule, React Fragment, and Conditional Clauses in React

## Single Root Node

React element 或 Component `return` 的物件必須只有一個主節點。

#### 錯誤範例
```
return (
   <div> element 1 </div>
   <div> element 2 </div>
  )
```

如果要回傳多個節點，應該最外層再用一層 `HTML tag` 包起來。

#### 正確的範例
```
return (
   <div>
     <div> element 1 </div>
     <div> element 2 </div>
   </div>
  )
```

爲什麼會這樣?，其實是因爲 `javascript` 的 `return statement ` 本來就只允許 `return` 一個 `value`


## React Fragment

如果真的有需要return多個平行的html element, 那可以考慮用React Fragments

```
render(){
  return (
    <React.Fragment>
        <div> first element </div>
        <div> second element </div>
    </React.Fragment>
  )
}
```

實際上在DOM上建立的`Element`如下

```
<div> first element </div>
<div> second element </div>
```

而`<React.Fragment>` 也可以用空tag表示，寫法如下

```
<>

// html element here

</>
```

有時候如果需要用`map function` 來建立 `React.Fragment`，目前`React`能傳給`React.Fragment`的屬性就只有`key`而已。

看下方例子


```
  return (
       <div>
          { props.items.map(item => (
                <React.Fragment key={item.id}>
                    <div> first element </div>
                    <div> seocnd element </div>
                </React.Fragment>
            ))}
       </div>
       )
```






## Conditional Clauses

在 `React` 中怎麼寫`if statement` ?

`React element` 的 `attribute `內可以接受 `if expression` , 但無法接受`if statement`.

這什麼意思呢？

```
let active = (condition) ? true : false；

```

其中`(condition) ? true : false；`這一串就是`expression`, 上面是正確的寫法。

但如果寫成`if statement`

```
let active = if(condition) {
   return true;
}else{
   return false;
}
```

很明顯，編譯器會報錯。

所以在 `react` 內，`assign property value` 至多也只能寫成 `expression` 的方式。

```
render(){
   return (
        <div className={condition? "yes" : "no"}>
            Hello
        </div>
     )
}
```

如果邏輯複雜，那還是把判斷搬出去外面。

```
render(){
   let className;
   if(condition){
      className = "yes";
   }else{
     className = "No";
   }

   return (
        <div className={className}>
            Hello
        </div>
     )
}
```
