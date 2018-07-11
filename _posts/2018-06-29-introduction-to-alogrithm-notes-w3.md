---
layout: post
title: "Introduction to Algorithm - 3"
description: "介紹排序的演算法"
date: 2018-07-01
tags: [Algorithm]
comments: true
share: true
---
---


## 爲什麼要排序

#### 以尋找中位數爲例 

如果有排序過，找中位數的時間複雜度只要 $$O(1)$$
Array = [1, 2, 3, 3, 3]

```
median = Array[len(Array)/2]
```
其他的資料如果有排序過就可以用`Binary search`，只需要 $$O(\log{n})$$ 的時間。

總之，如果要找東西，還是先考慮排序。




#### 其他運用

比方說資料壓縮處理，可以透過排序找出重複的，或者找出獨特的資料，或運用在電腦視覺上等。

<br>

## 排序的演算法

### Insertion Sort 插入排序法

> Using pairewise swap to find the correct position

有一組數列A, 裏面的元素從 i ~ i + n ，從第i個元素開始，如果 A[i] < A[i - 1]，那 A[i] 就和 A[i - 1] 交換位置(pairswap), 如果 A[i] > or = A[i - 1], 那麼 i = i + 1;

最糟的情況是對一個反向排序的list做排序，那麼每一次比較後，都會要做位置交換，而且是一路換到底。

![Insertion Sort](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0f/Insertion-sort-example-300px.gif/220px-Insertion-sort-example-300px.gif)

![Insertion Sort](https://upload.wikimedia.org/wikipedia/commons/2/25/Insertion_sort_animation.gif)

##### 時間複雜度

* Worst: $O(n^2)$
* Best: $O(n)$
* Average: $O(n^2)$

##### 空間複雜度

* $O(n)$, extra space $O(1)$



##### Python

```Python
def insert_sort(lst):
    n = len(lst)

    # base case
    if n == 1:
        return lst

    # sort from the second element
    for i in range(1, n):
        j = i

        # if current is less than its previous
        # swap them and reassign current to previous
        while j > 0 and lst[j] < lst[j-1]:
            lst[j], lst[j-1] = lst[j-1], lst[j]
            j = j - 1

    return lst
```



##### with binary search

另一種變形就是使用二分查找來幫忙對左邊已經排序好的部分尋找適合插入的位置。如果比較的成本很高，binary search是一個好的替代方案。但是binary search只有減少比較的成本，互換的成本還是在，因爲完成插入後，整個列表要往右移，所以還是少不了交換的成本。



##### 使用時機

* 當要排序的總數不多時，可以用插入排序法，記得插入排序不適合用在資料量大的地方。

<br>



### Merge Sort 合併排序

運用divide and conquer的方式，遞迴的排序。

如果對兩組已經排序好的Array，要對他們進行排序合併，順序會是這樣的，先比對兩個列表最前面，看誰小，建立一個新的列表把它放進去。

假設 List A : [1, 2, 3], List B: [0, 5, 7]，那麼第一回合後，我們會有一個新的Array [0], 因爲$$ 0 < 1$$, 所以把 $0$ 從List B中被移除，

##### Round 1

`merge List [0]`<br>
`List A [1, 2, 3]`<br>
`List B [5, 7]`<br>

##### Round 2...n

繼續比較，然後合併。可以看到一開始兩個列表都是排序好的，從這個邏輯來看，最終是要拿到的是兩個排好的列表, 再合併，那如何拿到這兩個列表呢？就是再把各自切成兩個更小的列表下去排序，假設一共有4個Array要排，那要怎麼排呢？就是繼續切`(divid)`，一直切到每個列表只剩一個元素, 就可以從下面開始傳回排序好的回來。

看這個動態圖應該會非常清楚啦。

![Merger sort](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)



##### 時間複雜度

- Worst: $O(n \log{n})$
- Best: $O(n \log{n})$, typical $O(n)$
- Average: $O(n \log{n})$

##### 空間複雜度

最糟的情況 О(*n*) total with O(*n*) auxiliary, O(*1*) auxiliary with linked lists 1

<br>

### Quick sort

待續

### heap sort
待續

### Radix sort
待續





##### 參考資料

[Wikipedia]( https://en.wikipedia.org/wiki/Merge_sort)

