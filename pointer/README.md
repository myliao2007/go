# 08-指標

當我們在呼叫一個函式時帶入一個參數，則這個參數會被複製到函式中：

```go
func zero(x int) {
    x = 0
}
func main() {
    x := 5
    zero(x)
    fmt.Println(x) // x is still 5
}
```

在這個程式中，`zero` 這個函式不會動到 `main` 函式中的 `x` 變數值，可是如果我們想要改，該怎麼做呢？一種方式是使用一個特殊的資料型別，即所謂的指標（pointer）：

```go
func zero(xPtr *int) {
    *xPtr = 0
}
func main() {
    x := 5
    zero(&x)
    fmt.Println(x) // x is 0
}
```

指標可以取得儲存變數值的記憶體位置，而不是變數值本身（或是指向某物的指標值）。透過指標 (`*int`)，`zero` 函式可以修改原本的變數值。
