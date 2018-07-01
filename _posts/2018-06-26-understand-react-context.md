# Context in react

> Context provides a way to pass data through the component tree without having to pass props down manually at every level.

總之就是一種在組件之間傳遞資料的方式。



### 什麼時候可以用context ? 

`React`傳遞資料的方式一直都是從上到下的，比方說有爸爸跟兒子，爸爸要傳資料給兒子很容易，只要在兒子上面設一個屬性如`say="hi son"`，把內容填上去，到了兒子這一層時，兒子如果想看爸爸給自己傳了啥碗糕，只需要用一個`this.props.say`就可以神奇的把`hi son`給拿來運用了。

但是這個有一個缺點，一等親的傳遞`hen`容易，只要用`this.props`就扣以，但是二等親(含)以上，就很麻煩了。

像是姐姐要傳給妹妹，得先傳給爸爸，再委託爸爸傳給妹妹，或者阿公要傳給孫子，得先傳給兒子，再叫兒子傳給孫子。

多麻煩阿，但是儘量避免只因爲要傳超過兩層就使用`context`，如果要傳遞是相同的而且可能很多`components`都會需要`access`，那就是用`context`的好時機


> Don’t use context just to avoid passing props a few levels down. Stick to cases where the same data needs to be accessed in many components at multiple levels.


像是`React`官方文件上的這個例子。

```javascript
class App extends React.Component {
    render(){
    
              // 爺爺
       return <Toolbar theme="dark" />
  }
}

const Toolbar(props) {
     return (
         <div>
           // 爸爸
           <ThemedButton theme={props.theme}/>
         </div>
     ); 
 }
  
  
cosnt ThemedButton(props){
  
              // 兒子
  		return <Button theme={props.theme} />;
  }
```

如果其他組件也會需要用到`Button`，那可能到時候很多組件都會有相同的`properity`，最後`code`就會變`hen`髒，記得`Rule No 1` 就是


> **Don't Repeat yourself**


### 怎麼用Contenxt?

直接`create`一個context的`React object`，把值傳進去， 把它包在要發送資料者的外層。

```javascript

const ThemeContext = React.createContext('light');

class App extends React.Components {
	render(){
		return(
			<ThemeContext.Provider value="dark">
			    <Toolbar />
			</ThemeContext.Provider>
		);
	}
}

const Toolbar(props) {
     return (
         <div>
             //注意這裏把原本的props.theme拿掉了
             <ThemedButton/>
         </div>
     ); 
}


cosnt ThemeButton(props){
    return (
        <ThemeContext.Consumer>
              
              // 這裏的theme其實就是ThemeContext.Provider內一開始設
              // 定的value 
              // { value => ... }   
                 
              {theme => <Button {...props} theme={theme} />}
        </ThemeContext.Consumer>
        
        );

}

```

### API

#### React.createContext

```javascript
const {Provider, Consumer} = React.createContext(defulatValue);

```
當`React render` 一個 `context consumer`時，會從這個`consumer`的上層開始找`context provider`,如果都找不到，則會直接傳遞一開始設定的`defaultValue`給`consumer`。


#### Provider

```
<Provider value={/* some value */}>

一個`Provider`可以傳遞給多個`Consumer`
```

#### Consumer

> A React component that subscribes to context changes


需要內嵌一個`function`，這個函數會以`context value`當成變數，並且回傳一個`React node`。

> All Consumers that are descendants of a Provider will re-render whenever the Provider's value changes.



# 使用範例

可以參考`React`的官方文件。

[React Context Examples](https://reactjs.org/docs/context.html)



### Udpating Context from a Nested Component

有時候需要從很下層`update context`，這時候可以讓`Provider`帶一個函數去給`consumer`更新。









 
