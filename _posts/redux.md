## redux 筆記



集中管理state的工具，React是管理View，Redux則是管理資料。

把所有的資料集中在一個大的javascript object中。called the state or state tree



#### understand pure function

只有計算，不會亂Call 一些東西。





可以把一個application照需要的資料(state)跟view component做分類，以一個計數器來講，view的部分可能需要 + ,  - 按鈕，顯示目前數量。而以資料來講，只需要目前的數量。



感覺需要想每個頁面需要管理的State有那些，然後把這些資料放進redux裏面



```
const counter = (state = 0, action) => {
    switch (action.type) {
        case "INCREMENT":
        	return state + 1;
        case "DECREMENT":
        	return state - 1;
        default: 
        	return state;
    }
}
```





#### create store

```javascript
const {createStore} = Redux;
// same as import {createStore} from 'redux';

const store = createStore(counter);

// store method
1. getState() 
store.getState() //get current state

2. dispatch()
store.dispatch({type: "INCREMENT"});
// 和setState類似，送一個action過去更新目前State的狀態

3. subscribe()
store.subscribe( () => document.body.innertText = store.getState())
```





Redux的object是不能被直接改變，只能透過重新Return一個新的object的方式來取代原本的值。



有兩個lib可以用, deepfreeze, 跟 jest jasmine, 

object.assign

Concat, slice, 等



有一個管理全部Action的object



![image-20180717215809189](/var/folders/53/jqmxy0dj4bq0f9j399wxt3lr0000gn/T/abnerworks.Typora/image-20180717215809189.png)



先寫測試，

用Deepfreezen把原本的state Freeze住

測試before and after 這樣就知道之後要怎麼寫function

object or array都可以用這種方式來return 一個new obj

```
let state = []
reutrn [...state, something you want to add here...]
```



```
let state = {id: 1}
return {...state, {id: 2}}

```





redux

管理state的工具

state App互動跟資料的狀態

action是一個js object, 

```
{ type: 'ADD_TODO', text: 'Go to swimming pool' }
```



reducer, 一個function 接受state, 並回傳新的state, 請用pure function來做action

reducer 只是一个接收 state 和 action，并返回新的 state 的函数。 对于大的应用来说，不大可能仅仅只写一个这样的函数，所以我们编写很多小函数来分别管理 state 的一部分



三大原則

### 单一数据源

