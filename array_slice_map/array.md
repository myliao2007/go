# 06.01-陣列（Array）



陣列是一個有著編號的序列，裡頭的每個元素（element）都有相同的單一型別（type）。在 Go 語言中，陣列的樣式看起來如下所示：

```
var x [5]int
```

`x` 是一個陣列的範例，由 5 個 `int` 型別組成，我們試著執行下列的程式：

```go
package main

import "fmt"

func main() {
    var x [5]int
    x[4] = 100
    fmt.Println(x)
}
```

你應該會看到這樣的執行結果：

```
[0 0 0 0 100]
```

`x[4] = 100` 應該讀為「將陣列的第 5 個元素設定為 100」。可能會覺得奇怪， `x[4]` 為什麼代表第 5 個元素，而不是如字面所示的第 4 個元素呢？因為陣列的索引值是從 0 起算的，所以陣列的存取方式也是如此。我們可以將 `fmt.Println(x)` 改成 `fmt.Println(x[4])`，這樣我們會得到 100。

這個程式示範如何使用陣列：

```go
func main() {
    var x [5]float64
    x[0] = 98
    x[1] = 93
    x[2] = 77
    x[3] = 82
    x[4] = 83
    
    var total float64 = 0
    for i := 0; i < 5; i++ {
        total += x[i]
    }
    fmt.Println(total / 5)
}
```

此程式會計算一串測驗成績的平均值，執行程式之後應該會看到結果是 `86.6`。我們來看看這段程式碼：

* 我們先建立一個長度為 5 的陣列來儲存這些測驗成績，接著將分數填入每個元素中。
* 再來使用一個迴圈來計算成績的總和。
* 最後我們將成績的總和除以元素的數量，以取得平均值。

此程式可以正常運作，但是 Go 有提供一些功能可以讓我們來改進這個程式。在一開始的兩個地方：`i < 5` 與 `total / 5` ，若我們想要將成績的數量從 5 個改成 6個，則會需要同時修改這兩個地方，因此建議可以改成使用陣列長度：

```go
    var total float64 = 0
    for i := 0; i < len(x); i++ {
        total += x[i]
    }
    fmt.Println(total / len(x))
```

修改並執行程式，你會看到發生一個錯誤：

```
$ go run tmp.go
# command-line-arguments
.\tmp.go:19: invalid operation: total / 5 (mismatched types float64 and int)
```

問題在於 `len(x)` 與 `total` 的型別不同，`total` 的型別是 `float64`，而 `len(x)` 的型別是 `int`，所以我們需要將 `len(x)` 強制轉型為 `float64`：

```
fmt.Println(total / float64(len(x)))
```

這是一個型別轉換的範例，通常使用型別的名稱來進行型別轉換，就像是函式一樣。

另一個可以改的地方是使用特殊的 for 迴圈格式：

```go
var total float64 = 0
for i, value := range x {
    total += value
}
fmt.Println(total / float64(len(x)))
```

這個 for 迴圈中的 `i` 表示目前正在處理的陣列元素，而 `value` 則與 `x[i]` 相同，我們使用 `range` 這個關鍵字，並接著一個變數名稱（迴圈的終止條件）。

執行此程式會產生另一個錯誤：

```
$ go run tmp.go
# command-line-arguments
.\tmp.go:16: i declared and not used
```

Go 編譯器（compiler）不允許你建立用不到的變數，由於我們在迴圈中沒有用到 `i`，所以我們要稍微修改程式碼：

```go
var total float64 = 0
for _, value := range x {
    total += value
}
fmt.Println(total / float64(len(x)))
```

可以用單個 `_`（底線）來告知編譯器我們不需要這個變數（在此範例中，我們不需要 iterator 變數）

在 Go 可以用另一個較簡短的語法來建立陣列：

```
x := [5]float64{ 98, 93, 77, 82, 83 }
```

我們不用指定型別，因為 Go 自己知道。像這樣的陣列有時可能會太長而無法用一行來表示，所以 Go 也可以讓我們用下列方式來分行：

```go
x := [5]float64{ 
    98, 
    93, 
    77, 
    82, 
    83,
}
```

要注意在 `83` 後面有一個結尾的  `,`  符號，在 Go 語言必須要這樣寫，因為這樣就能透過在前頭加上註解，隨意移除陣列元素：

```go
x := [4]float64{ 
    98, 
    93, 
    77, 
    82, 
    // 83,
}
```
