# 07.03-參數個數可變的函式（Variadic Function）

在 Go 語言的函式中，有一種特殊格式可以使用：

```go
func add(args ...int) int {
    total := 0
    for _, v := range args {
        total += v
    }
    return total
}
func main() {
    fmt.Println(add(1,2,3))
}
```

在函式的最後一個參數的型別之前，使用 `...` 表示這個函式可以接受零個或零個以上的參數，依此規則，我們可以使用零個或零個以上的 `int` 參數，呼叫這種函式的方式與其它函式一樣，差異在於這類函式可以傳遞任何我們想傳遞的參數數量。

下列為 `fmt.Println` 函式的實作方式：

```go
func Println(a ...interface{}) (n int, err error)
```

`Println` 函式可接受任意型別、任意數量的參數值（後續會在第九章討論特殊的 `interface{}` 型別）

我們也可以傳遞一個 `int` 的 slice，只要在 slice 之後接著 `...`：

```go
func main() {
    xs := []int{1,2,3}
    fmt.Println(add(xs...))
}
```

