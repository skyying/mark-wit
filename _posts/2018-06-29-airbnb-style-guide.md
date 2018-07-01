# Airbnb React Style guide - Part I 


## Class VS React.createClass vs stateless

如果有這個元件內部有 ==state or ref==, 用`class extends React.Component`好過`React.createClass`

<br>
### With state

✅  **用 class extends React.Component** 

```
class Listing extends React.Component {
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
}
```

👎  bad ~~React.createClass~~

```
const Listing = React.createClass({
	//...
	render(){
		return <div>{this.state.hello}</div>
	}
});

```
<br>
### Stateless or without Ref
✅ 用**一般函式 function...** 

```
funtion Listing({ hello }) {
	return <div>{hello}</div>;
}

```
👎 bad ~~classes~~

```
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}

// bad (relying on function name inference
   is discouraged)

const Listing = ({ hello }) => (
  <div>{hello}</div>
);

```
<br>
## Mixins

 ❌ 別用
 
 > Why? Mixins introduce implicit dependencies, cause name clashes, and cause snowballing complexity. Most use cases for mixins can be accomplished in better ways via components, higher-order components, or utility modules.
 
<br>


 
## Naming

#### ▪️組件副檔名爲 `.jsx` 
#### ▪️檔名用PascalCase，像是 `ReservationCard.jsx`
#### `Reference`的名稱用 PascalCase, 他們的`instance`用camelCase


✅ 用 **R**eservation**B**ard

```
import ReservationCard from './ReservationCard`;

```
👎 bad ~~reservationCard~~

```
import reservationCard from './ReservationCard';
```

<br>
#### ▪️ 組件命名
名稱和**檔名**相同，`root component` 則用 `index.jsx`, 當用`index.jsx`命名時，`React`可允許只要輸入資料夾名稱即可匯入。



✅ 注意匯入的組件檔名省略了`index.jsx`

```
import Footer from './Footer';
```
👎 bad

```
import Footer from './Footer/Footer';
import Footer from './Footer/index';

```

<br>
#### ▪️ HoC - Higher-order Component 命名

引用HoC組件的命名應該**結合傳進來的組件名稱**，方便Debug辨識傳進來的組件與HoC中間的關係，舉例，有一個HoC, withFool(), 當傳入一個叫做Bar的組件, 被**實例化**的這個HoC組件會有`displayName`的Property, 其值爲`withFool(Bar)`。

✅ 有`displayName`，裏面顯示傳進來的組件名稱

```
export default function withFoo(WrappedComponent) {
	function WithFoo(props) {
		return <WrappedComponent {...props} foo/>
	}
	
	const wrappedComponentName = 
		WrappedComponent.displayName ||
		WrappedComponent.name || 
		'Component';
	
	WithFool.displayName = `withFool(${wrappedComponentName}`;
	
	return WithFoo;
}


```


👎 bad 沒有`displayName`

```
export default function withFoo(WrappedComponent) {
	function WithFoo(props) {
		return <WrappedComponent {...props} foo/>
	}
}

```

<br>
#### ▪️ Props 命名

✅ 別用 DOM 上的屬性名稱 (style, className...)

```
<MyComponent variant="fancy" />

```



👎 bad ~~Dom Component props name~~

```
<MyComponent style="fancy" />

<MyComponent className="fancy" />

```

<br>
<br>


## 宣告

不用`displayName`來命名組件，用`reference`。



✅ good

```
export default class ReservationCard extends React.Component {
   //
}
```


👎 bad 

```
export default React.createClass({
	displayName : 'ReservationCard`,
	//

});

```

<br>
<br>


## 對齊

3 個對齊的規則。 

* tag 結尾的位置應斷行
* 如果加完`props`位置還夠，就一行它
* 孩子要縮排

✅ tag 結尾的位置應斷行

```
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>
```

👎 bad 結尾位置不對

```
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />
```


✅ 如果加完`props`位置還夠，就一行它

```
<Foo bar="bar" />
```

✅ 縮排的孩子

```
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>
```


<br>
<br>


## 括號們

`JSX ` 用雙引號，其他 `JS` 用 單引號

✅ `JSX` 用雙引號

```
<Foo bar="bar" />
```
✅ 其他`JS`

```
<Foo style={{ left: '20px' }} />

```



<br>
<br>


## 間距
結尾的`tag`前留一個空白格

✅ `tag`最後要留白

```
<Foo />

```

👎 `tag`靠很緊，留很多白，或不該斷時斷行都不妙

```
<Foo/>

<Foo                 />

<Foo
 />
```


✅ {這裏面要靠緊}

```
<Foo bar={baz} />
```

👎 { 沒靠緊 } 
```
<Foo bar={ baz } />
```

<br>
<br>



(待續...)
























