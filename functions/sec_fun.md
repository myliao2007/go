# 07.01-你的第二個函式



這是第6章的程式：

```go
func main() {
    xs := []float64{98,93,77,82,83}
    
    total := 0.0
    for _, v := range xs {
        total += v
    }
    fmt.Println(total / float64(len(xs)))
}
```

這個程式計算一串數字的平均值，找出這類平均值是很常見的問題，所以比較理想的方式是將這段程式定義為函式。

`average` 函式需要使用一個 `float64` 型別的 slice，並能夠傳回 `float64`，我們在 `main` 函式前面增加這段程式碼：

```go
func average(xs []float64) float64 {
    panic("Not Implemented")
}
```

函式的開頭是 `func` 關鍵字，後面跟著函式的名稱。函式的參數（輸入）可像這樣定義： `name type, name type, …`。我們這個函式有一個參數（一串分數），我們將它命名為 `xs`。在此參數之後的是傳回值的型別。函式的參數與傳回值型別則是所謂函式的特徵值（signature）。

最後，在大括號之間的函式的主體中會有一些陳述句，我們在函式的主體中呼叫一個內建的 `panic` 函式，這會產生一個執行期的錯誤訊息（本章稍後會再介紹 panic）。寫一個大函式可能會比較難，所以比較好的方式是將程式流程分成幾段比較好管理的小區塊，而不是直接寫成一大段程式碼。

現在我們將 main 函式中的一些程式碼搬到 average 函式中：

```go
func average(xs []float64) float64 {    
    total := 0.0
    for _, v := range xs {
        total += v
    }
    return total / float64(len(xs))
}
```

要注意的是，我們將 `fmt.Println` 改成了 `return`，return 會讓函式立即停止，並將傳回值送給它的呼叫者，將 `main` 修改如下：

```go
func main() {
    xs := []float64{98,93,77,82,83}
    fmt.Println(average(xs))
}
```

執行此程式應該會讓你得到與原本程式相同的結果，有些事要記得：

* 參數的名稱不用與原本呼叫函式代入的變數名稱相同，例如下列方式：

```go
func main() {
    someOtherName := []float64{98,93,77,82,83}
    fmt.Println(average(someOtherName))
}
```

而且我們的程式仍然可以運作。

* 函式無法存取呼叫者的任何變數（除非透過指標），像下列的方式無法正常運作：

```go
func f() {
    fmt.Println(x)
}
func main() {
    x := 5
    f()
}
```

我們也可以這樣寫：

```go
func f(x int) {
    fmt.Println(x)
}
func main() {
    x := 5
    f(x)
}
```

譯者註：特別注意，func main() 中的 x 與 func f()中的 x ，雖然變數名稱相同，但是它們是分別屬於 main() 與 f() 的區域變數（local variable，或稱自動變數，auto variable），在main() 中的 x 變數之可視範圍（scope）僅限於 main() 函式中，而 f() 中的 x 變數可視範圍也僅限於 func() 函式中。

或是這樣：

```go
var x int = 5
func f() {
    fmt.Println(x)
}
func main() {
    f()
}
```

函式是在堆疊（stack）中建立的，以下列的程式為例：

```go
func main() {
    fmt.Println(f1())
}
func f1() int {
    return f2()
}
func f2() int {
    return 1
}
```

我們可以將上述的程式碼以具體的方式呈現如下：

<figure><img src="https://web.archive.org/web/20200228061942im_/https://sites.google.com/site/applezugointroduction/_/rsrc/1401643358907/07-han-shi/07-02.png" alt=""><figcaption></figcaption></figure>

我們每次呼叫函式時，我們就會將函式置入堆疊（push），而從函式返回時，則將函式從堆疊中移出（pop）。

我們也可以明確指定回傳值的資料型別與名稱：

* ```go
  func f2() (r int) {
      r = 1
      return
  }
  ```
