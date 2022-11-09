# 13.05-Container 與 Sort

在 Go 語言中，除了 list 與 map，在 container package 中還有幾個可用的套件。我們會先以 `container/list` 為例進行探討。

List

&#x20;`container/list` package 實做了一個雙向鏈結串列（doubly-linked list），一個鏈結串列是一種如下所示的資料結構：\


<figure><img src="https://web.archive.org/web/20200228062138im_/https://sites.google.com/site/applezugointroduction/_/rsrc/1401643502089/13-the-core-packages/13-01.png" alt=""><figcaption></figcaption></figure>

串列中的每個節點都會包含一個值（此例為1、2或3）以及一個指向下一個節點的指標。因為這是一個雙向鏈結串列，所以每一個節點還會使用一個指標來指向前一個節點，可使用下列的程式建立一個這樣的串列：

```go
package main

import ("fmt" ; "container/list")

func main() {
    var x list.List
    x.PushBack(1)
    x.PushBack(2)
    x.PushBack(3)

    for e := x.Front(); e != nil; e=e.Next() {
        fmt.Println(e.Value.(int))
    }
}
```

數值為零的 `List` 是一個空的串列（而 `*List` 也能使用 `list.New` 來建立）。可以使用 `PushBack` 將值附加到串列後方，我們使用迴圈從串列的第一個元素（element）開始，依序取得串列中的每個節點值，直到遇到結尾的 nil 為止。&#x20;

#### Sort <a href="#toc-sort" id="toc-sort"></a>

Sort package 有一些能夠排序任意資料的函式。有幾個預先定義好的排序函式（供 int 與 float 的 slice 使用），此處有一個範例，示範如何排序你自的資料：

```go
package main

import ("fmt" ; "sort")

type Person struct { 
    Name string
    Age int
}

type ByName []Person

func (this ByName) Len() int {
    return len(this)
}
func (this ByName) Less(i, j int) bool {
    return this[i].Name < this[j].Name
}
func (this ByName) Swap(i, j int) {
    this[i], this[j] = this[j], this[i]
}

func main() {
    kids := []Person{
        {"Jill",9},
        {"Jack",10},
    }
    sort.Sort(ByName(kids))
    fmt.Println(kids)
}
```

在 `sort` 中的 Sort 函式接收一個 `sort.Interface`，並對它進行排序，`sort.Interface` 需要三個 methods：分別是 `Len`、`Less` 與 `Swap`。為了定義我們自己的排序，我們會建立一個新的型別（`ByName`），並且讓它等於我們想要排序的一個 slice。接著我們定義這三個 methods。

接著要將我們的 people 串列進行排序就如同要將串列強制轉型為我們的新型別一樣簡單，我們可以這樣來依據年齡（age）進行排序：

```go
type ByAge []Person
func (this ByAge) Len() int {
    return len(this)
}
func (this ByAge) Less(i, j int) bool {
    return this[i].Age < this[j].Age
}
func (this ByAge) Swap(i, j int) {
    this[i], this[j] = this[j], this[i]
}
```

\
