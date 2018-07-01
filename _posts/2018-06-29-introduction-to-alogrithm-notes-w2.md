
## Random Access Machine (RAM) 

* Random access memeory (RAM) :

- 基本上就是一個很大的Array, 這Array的每一格都有自己的地址。
- 在`O(1)`的時間，可以載入`O(1)`的資料(`a word`)，做`O(1)`的計算，存`O(1)`的資料(`a word`)
- `O(1) register`


### What is a word menas here ?
-  give an input, a bunch of things which are words. `w bits`, and `w` should be log(size of memory). 爲了要知道是存在array的哪裏。

## Pointer Machine:
有時候並不是每個計算都需要用到`Array`, 另一個常見的model就是Dynamiclly allocated objects。
Object has O(1) fields, and a field has either a word(like an interger) or a pointer.那麼執行這些計算也會只會花O(1)的時間。

A pointer is something that points to another object or `None` in python, `null` or `nil`, 另外一個對`pointer`的名稱是`reference`

Link list 就是體現 pointer 的 data strucutre.

## Python model
 
 * python's list is array instead of linked list

can do RAM model in O(1)
 
```python
L[i] = L[j] + 5 # O(1)  

```

or can do Pointer machine with Objects 如果你的 Object 的確只有 O(1) 的attribute, 那麼操作remain O(1),但如果是上百萬，那就要注意，操作不會是constant time o(1).


```python
x = x.next # O(1)
```

幾乎所有的操作都能夠被抽象化成用這兩個`model`來計算`cost`。

### 新增一個元素到Array內？

```python
L.append(x)
```

要對原本的陣列多存一筆資料，可以創造一個new array, copy舊的，在把新的加上去。但這樣`cost`就是o(n), 因此在`python`有另一種方法叫做`table doubling`, 這種方法，簡單的說就是並不是每次都`resize array space`，只有在需要的時候才`resize`。而這種`table doubling`的做法讓`List append`可以減少到`O(1)`

### 兩個`list`相加？
```
L = L1 + L2 
```

建議可以用first order princile rule來想，如果現在什麼都沒有，要把兩個`list`相加，可以怎麼做？

```
create a empty list L []
for x in L1:      
   L.append(x)       
for x in L2:      
	L.append(x)    
```

`L.append(x)`這個操作要花O(1), 總共要做 O(len(L1) + len(L2) + 1) 次。

### for x in List (array)

`O(n)`, 因爲 `array` 沒有被排序過，所以要偏歷全部來搜尋

### Size of List (array)
built in counter, so only takes `O(1)`

### Sort a List (array)

O(n logn) compared sort

### Dictionary/Dict 

`D[key] = value `

Implemented by hash table
cost: `O(1)`


 ### Long
 
 ` x` is `|x|` words long, `y` is `|y|` words long. 

* `x + y ` 
will cost `O(|x| + |y|)`

* `x * y`
$O( |x|+|y| )^{(lg^3)}$, log base 2 of 3, 約1.6, 比n^2好一點。

## Document distance

D1, D2, and compute the distance between them.

假設你想要比較這D1, D2 這兩個文件是否相同，D1是a sequence of words, a word is a string, 

#### Idea
找看兩個文件共同有的Words有多少，用`shared words`來計算是否相同。

也可以把D1, D2想成 vector, D[w] = w出現在該文件的次數

用兩個例子
D1 = "The Cat"
D2 = "The Dog"

畫一個3維的向量空間，x("the"), y("Cat"), z("dog")，中心點是0, D1的座標是(1, 1, 0), 會與
center(0, 0, 0)形成一個向量, D2也是，D1與D2之間的角度可以用這個公式來計算 

cosθ =  $\frac{({\displaystyle {\overrightarrow {u}}} • {\displaystyle {\overrightarrow {v}}})}{(||{\displaystyle {\overrightarrow {u}}}|| ||{\displaystyle {\overrightarrow {v}}} ||)}$

$\vec{D1}$ = x + y 

$\vec{D2}$ = x + z

帶入公式，就可以發現 $cosθ=\frac{1}{2}$ , D1, D2 的角度是60度，如果他們之間是0度,則表示他們是完全相同，如果是90度，則表示完全不同。







