# 06.02-Slice

Slice 是在一個陣列中的一個區段（segment），與陣列一樣，slice 是可以透過索引存取的，而且也有長度。但與陣列不同的是，slide 的長度是可以改變的，下列是一個 slice 範例：

```
 var x []float64
```

&#x20;Slice 與陣列的唯一差別是，在中括號之間沒有表示長度的數字。以此例而言，`x` 的長度為 `0`。

若你想建立一個 slice，則你應該使用內建的  `make` 函式：

```
x := make([]float64, 5)
```

這樣會建立一個 slice（這個 slice 與底層長度為 5 的 `float64` 陣列有關連），slices 必定會與某個陣列有關聯，而且它們的長度不僅不會超過陣列長度，還可以更小。`make` 函式可以使用第三個參數：

```
x := make([]float64, 5, 10)
```

10 代表 slice 所指向的底層陣列之空間：

\


<figure><img src="https://web.archive.org/web/20200228061932im_/https://sites.google.com/site/applezugointroduction/_/rsrc/1401643397770/06-arrays-slices-and-maps/06-01.png" alt=""><figcaption></figcaption></figure>

另一個建立 slice 的方式是使用 `[low : high]` ：

```go
arr := [5]float64{1,2,3,4,5}
x := arr[0:5]
```

`low` 是 slice 的起點之索引值，而 `high` 是 slice 的結束點（但是 slice 並不包含這個結束點的索引值），例如：在 `arr[0:5]` 會傳回 `[1,2,3,4,5]`，而 `arr[1:4]` 則傳回 `[2,3,4]`。

為了便利，我們也可以忽略 `low`、`high`，甚至可以同時忽略 `low` 與 `high`。`arr[0:]` 等同於 `arr[0:len(arr)]`、 `arr[:5]` 等同於 `[0:5]`、以及 `arr[:]` 等同於 `arr[0:len(arr)]`。

#### Slice 函式 <a href="#toc-slice-functions" id="toc-slice-functions"></a>

Go 語言有兩個內建的 slice 函式：`append` 與 `copy`。下列是一個 `append` 範例：

```go
func main() {
    slice1 := []int{1,2,3}
    slice2 := append(slice1, 4, 5)
    fmt.Println(slice1, slice2)
}
```

在執行程式之後，`slice1` 是 `[1,2,3]`，而 `slice2` 則是 `[1,2,3,4,5]`。`append` 利用現有的 slice（在第一個參數）建立一個新的 slice，並將後續的參數附加在 這個 slice 之後。

下列是一個 copy 範例：

```go
func main() {
    slice1 := []int{1,2,3}
    slice2 := make([]int, 2)
    copy(slice2, slice1)
    fmt.Println(slice1, slice2)
}
```

在執行此程式之後，`slice1` 是 `[1,2,3]`，而 `slice2` 是 `[1,2]`，將 `slice1` 的內容複製到 `slice2`，不過因為 `slice2` 的空間只能容納兩個元素，所以只有複製 `slice1` 的前兩個元素。
