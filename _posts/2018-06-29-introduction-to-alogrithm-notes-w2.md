---
layout: post
title: "Introduction to Algorithm - 2"
description: "介紹一些演算法的基本操作大概要花費多少時間，組合起來又會花多少時間。另外也介紹如何更快的比對兩個文件是否完全相同"
date: 2018-06-29
tags: [Algorithm]
comments: true
share: true
---


介紹一些演算法的基本操作大概要花費多少時間，組合起來又會花多少時間，也介紹document distance的算法

---


## Random Access Machine (RAM) 
- 一個很大的陣列, 陣列的每一格都有自己的地址。
- 在$$O(1)$$的時間，可以載入$$O(1)$$的資料(`a word`)，做$$O(1)$$的計算，存$$O(1)$$的資料(`a word`)
- $$O(1)$$ register


#### What is a word menas here ?
> given an input, a bunch of things which are words. `w bits`, and `w` should be log(size of memory). 

基本上a word 只是一個單位，用來說明RAM的處理。

<br>

## Pointer Machine

有時候並不是每個計算都需要用到陣列, 另一個常見的模型就是Dynamiclly allocated objects。

> Object has $$O(1)$$ fields, and a field has either a word(like an interger) or a pointer.

那麼執行這些計算也會只會花$$O(1)$$的時間。

> A pointer is something that points to another object or `None` in python, `null` or `nil` 

另外一個對`pointer`的名稱是`reference` , 而 Linked list 就是體現 pointer 的 data strucutre.

<br>

## Python model

介紹Python的各種資料結構操作的時間複雜度

>  python's list is array instead of linked list, can do RAM model in $$O(1)$$

Python的list不是鏈表而是陣列,容易讓人搞混。但陣列的操作可以在$$O(1)$$內完成

<br>

```python
L[i] = L[j] + 5 # O(1)  
```

<br>

>  Use Pointer machine with Objects 

如果你的物件只有 $$O(1)$$ 的屬性, 那麼使用Pointer model操作一樣是 $$O(1)$$ ),但如果是上百萬，那就要注意，操作不會是constant time $$O(1)$$.


```python
x = x.next # O(1)
```

幾乎所有的操作都能夠被抽象化成用這兩個模型(ram, pointer)來計算時間複雜度。

<br>

### 執行基本動作的時間成本

#### 新增一個元素到陣列內的複雜度 O(1)

```python
L.append(x)
```

要對原本的陣列多存一筆資料，可以創造一個新的陣列, 複製舊的，把新的加上去。但這樣複雜度就是$$O(n)$$, 因此在`python`有另一種方法叫做`table doubling`, 這種方法，簡單的說就是並不是增加或減少元素時，都去變動陣列的長度，只有在需要的時候才變動。而這種`table doubling`的做法讓增加元素到列表的時間複雜度可以減少到$$O(1)$$

<br>

#### 兩個列表相加的複雜度 O(len(l1) + len(l2) + 1)

```python
L = L1 + L2 
```

可以試試用第一性原則來想，如果現在什麼都沒有，要把兩個列表相加，可以怎麼做？


```
create a empty list L []
for x in L1:      
   L.append(x)       
for x in L2:      
	L.append(x)    
```


`L.append(x)`這個操作要花$O(1)$, 總共要做 $O(len(l1) + len(l2) + 1)$ 次。

<br>

#### 遍歷列表的成本 O(n)

當陣列沒有被排序過，會需要O(n)的時間，因爲要全部遍歷歷過一次來搜尋

```python
for x in listA:
	if x == target:
	   # do something
```


<br>

#### 查詢陣列的長度  O(1)

如果要知道陣列的長度，因爲python有內建計數器，所以只需要$O(1)$

<br>

#### 陣列排序 $O(n\log{n})$

可以看第三週的排序介紹心得。

<br>

#### Seach by Dictionary/dict O(1)

```python
D[key] = value 
```
用嘻哈表(hash table) 實作的字典，只需要$O(1)$

<br>

#### Add or multiply x, y long words

當 <span>$x$</span> 是 $x$ 個字長，而 $y$ 是 $y$ 個字長時，<span>$x + y$ </span> 的成本是 <span> $O(|x| + |y|)$ </span>，而<span> $x\*y$</span> 的成本則是<span>$O(|x|+|y|)^{\log_2{3}}$</span> 約1.6, 比 $n^2$ 好一點。

<br>

## Document distance

假設你想要比較這D1, D2 這兩個文件是否相同，D1, D2是n, m 個長度不等的字串。可以怎麼做？

<br>

#### 想法，找看看這兩個文件共同的文字有幾個。

試着找看看兩個文件共同有的文字有多少，相同的字越多，代表文件越相似。

也可以把D1, D2想成向量, D[w] = w出現在該文件的次數

用兩個例子來說明，假設D1, D2的內容如下，

D1 = "The Cat"<br>
D2 = "The Dog"

我們可以畫一個3維的向量空間，$x, y, z$分別代表這三個字，$x(the), y(Cat), z(dog)$，中心點是 $(0, 0, 0)$, D1的座標是 $(1, 1, 0)$ , 會與中心點形成一個向量$\vec{D1}$, D2的座標是$(1, 0, 1)$，也會與中心點形成另一個向量$\vec{D2}$，而文件到底相不相同就可以用2個向量之間的角度來算。公式如下：




$$
cosθ = ({\displaystyle {\overrightarrow {u}}} • {\displaystyle {\overrightarrow {v}}}) / (||{\displaystyle {\overrightarrow {u}}}|| ||{\displaystyle {\overrightarrow {v}}}||)
$$


把D1, D2帶入公式，就可以發現 $cosθ=\frac{1}{2}$ , D1, D2 的角度是60度，如果他們之間是0度,則表示他們是完全相同，如果是90度，則表示完全不同。









