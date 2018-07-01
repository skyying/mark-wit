
### First class objects
在`javascript`中, `function` 是`first class objects`意思是他們可以被指定成變數，也可以被當成參數來傳遞給其他`function`。而這個接受`function`爲參數，並且對他加料後再回傳的`function`，就叫做`higher-order-function(HoF)`

<br>

#### Higher-order-functions(HoF)

`HoF`的範例

```
const add = ( x, y ) => x + y

const log = func => (...args) => {
   console.log(...args)
   return func(...args)
}

const logAdd = log(add)

```

<br>
這裏有兩個`function`，第一個是`add`, 第二個是`log`第二個function就是`higher order functions`，可以看他就是接受一個`function`當參數，加料後再回傳，回傳的`function`是一樣的，但是會再加上其他行爲。


爲什麼這Higher-order-function的概念很重要？因爲在`react`中，有個東西叫`Higher-order-component`。
<br><br>

#### Purity

`pure function`是`functional programming`一個重要的概念，也就是`不變性`，意思就是進去後，又出來，不會對環境造成傷害。如果一個`function`執行後有變更到本身scope外的變數，那他就是**不純**。

##### 純與不純

```
//純
const add = (x, y) => ( x + y )

let x = 0;

//不純
const add = y => ( x = x + y )

```

<br>
上面這個**不純**的範例，就是因爲`call`這個`function`後，即使傳入相同的參數，也會得到不同的值。

> Pure Function don't mutate the state

 
<br><br>

#### Immutability 不變性

> In FP, a function, instead of changing the value of a variable, creates a new variable with a new value and return it. 

這意思就是，不要改直接改變數的值, 而是創造一個新的變數，看一下反例，

```
let arr = [1]
const myArr = val => arr.push(val)

myArr(1) // [1, 1]
myArr(1) // [1, 1, 1]

```

上面這個範例，執行之後都會改變外面變數的值。

<br><br>

如何改成`immutable`呢？

```
const addArr = arr => arr.concat(1)

```
這樣寫，無論是傳什麼`Array`進來，都不會改變該`Array`的值了。

<br><br>

#### Currying 咖喱

> Currying is the process of converting a function that takes multiple arguments into a function that takes one argument at a time, returning another function.


把多個參數變成只需要一個參數，然後回傳另一個`funcion`，來看看範例


```
//原本的add function如下

const add = (x, y) => x + y

//加了咖喱之後

const add = x => ( y => x + y )
```

<br>
原本要傳x, y進去，現在只傳x, 結果變成

```
//創造一個新變數來產生新的值
const add1 = add(1)

```

<br>

這時 `add1` 其實會回傳一個新的`function, y => x + y`

上面的這個`1`被帶入原本的函數就等於

```
const add = (1) => y => 1 + y

add1 
add1(1) // 2
add1(2) // 3
...

```


<br>
<br>

# Reusable Components

### stateless function

> Components that are not able to receive any props from the parents are not particularly useful, and the stateless functional components can receive props as parameters:


```
props => <button>{props.text}</button>
```

上面這個方法可以把傳進來的`props`變成一個`return jsx element`。

##### ES2016 (es6) 的寫法

```
({text}) => <button>{text}</button>

```

這種寫法叫做[解構賦值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)。

`props`是指從父元素傳遞給子元素的資料，而一個`stateless`組件除了接受`props`當成參數，還會接受一個另一個參數`context`, `context`是組件另一種接受資料的方法，組件接受的資料不一定要都要從`props`來。



#### what is context? 

可以參考這篇文章 [Understand react context](/2018-06-26/understand-react-context.md)。



