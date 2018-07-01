
### Sort過幫助尋找更容易

#### 尋找中位數
如果有排序過，找中位數只需要 O(1)
Array = [1, 2, 3, 3, 3]

```
median = Array[len(Array)/2]
```
當sorting過就可以用`Binary search`，則只需要 $O(log n)$的時間。


##### Other applicatoin

比方說資料壓縮處理，可以透過排序找出重複的，或者找出identical的資料，或運用Computer graphic上等。

## Inserton Sort

> Using pairewise swap to find the correct position

有一組數列A, 裏面的元素從 i ~ i + n ，從第i個元素開始，如果 A[i] < A[i - 1]，那 A[i] 就和 A[i - 1] 交換位置(pairswap), 如果 A[i] > or = A[i - 1], 那麼 i = i + 1;

最糟的情況是對一個反向排序的list做排序，那麼每一次比較後，都會要做位置交換，而且是一路換到底。

![Insertion Sort](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0f/Insertion-sort-example-300px.gif/220px-Insertion-sort-example-300px.gif)

### Complexity

#### Time complexity
* $Worst$ = $O(n^2)$
* $Best$ = $O(n)$
* $Average$ = $O(n^2)$

### Space complexity
--
O(n), extra space O(1)


![Insertion Sort](https://upload.wikimedia.org/wikipedia/commons/2/25/Insertion_sort_animation.gif)


### Python
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
			

### Insertion Sort with binary search

另一種insertion sort的變形就是使用binary search來幫忙對左邊已經sort好的部分尋找適合Insert的位置。如果比較的成本很高，binary search是一個好的替代方案。但是binary search只有減少比較的成本，swap的成本還是在，因爲isnert後，整個list要往右移，所以還是少不了swap的成本。


### 運用Insertion sort的時機

* 要排序的總數不多，不適合用在資料量大的地方。



## Merge Sort

運用divide and conquer的方式，遞迴的排序。

如果對兩組已經排序好的Array，要對他們進行排序合併，順序會是這樣的，先比對兩個list最前面那位最小的Item是誰，並create一個新的array把它放進去。

假設 
`List A : [1, 2, 3], List B: [0, 5, 7]`
那麼第一回合後，我們會有一個新的`Array [0]`, 因爲` 0 < 1`, 所以把 $0$ 從`List B`中被移除，

##### Round 1

`merge List [0]`
`List A [1, 2, 3]`
`List B [5, 7]`

##### Round 2...n

繼續比較，然後合併。可以看到一開始兩個list都是排序好的，
從這個邏輯來看，最終是要拿到的是兩個排好的List, 再合併，那如何拿到這兩個list呢？就是再把各自切成兩個list下去排序，假設一共有4個Array要排，那要怎麼排呢？就是繼續切`(divid)`，一直切到每個`List`只剩一個`element`, 就就可以從下面開始傳回排序好的回來。




### Quick sort
待續

### heap sort
待續

### Radix sort
待續
