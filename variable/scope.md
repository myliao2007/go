# 04.02-Scope（變數的作用範圍）

回到我們在本章一開始所討論的程式：

```go
package main

import "fmt"

func main() {
    var x string = "Hello World"
    fmt.Println(x)
}
```

用另一種方式來寫這個程式，類似這樣：

```go
package main

import "fmt"

var x string = "Hello World"

func main() {
    fmt.Println(x)
}
```

注意，我們將變數移到 main 函式的外部，這表示其它函式都可以存取這個變數：

```go
var x string = "Hello World"

func main() {
    fmt.Println(x)
}

func f() {
    fmt.Println(x)
}
```

`f` 函式現在可以存取 `x` 變數了，現在我們改成這樣：

```go
func main() {
    var x string = "Hello World"
    fmt.Println(x)
}

func f() {
    fmt.Println(x)
}
```

如果你執行這個程式，你應該會看到一個錯誤：

```
.\main.go:11: undefined: x
```

編譯器告訴你 `f` 函式裡的 `x` 變數不存在，它只有在 `main` 函式裡面，你可以使用 `x` 的範圍就稱為這個變數的 scope。依據語言的規範，Go 是以區塊範圍的區隔（“Go is lexically scoped using blocks”）。基本上，這表示變數存在於最接近的大括號裡 `{` `}` （一個區塊），包含任何巢狀的大括號，但不在大括號外面。一開始會對 scope 有點困惑，不過只要我們多看些 Go 的範例，應該就會比較清楚了。
