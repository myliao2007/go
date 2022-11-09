# 07.07-Panic & Recover

我們之前已經建立了一個名為 `panic` 的函式，此函式會產生執行期（run-time）的錯誤。我們也能使用內建的 `recover`  函式來處理執行期的 panic。`recover` 會停止 panic 並將傳遞給  `panic` 呼叫的參數值傳回。我們可以透過如下的方式來使用它：

```go
package main

import "fmt"

func main() {
    panic("PANIC")
    str := recover()
    fmt.Println(str)
}
```

可是在這個案例中， `recover` 絕對不會執行到，因為在呼叫 `panic` 時已經暫停執行函式。所以我們必須搭配使用  `defer`：

```go
package main

import "fmt"

func main() {
    defer func() {    
        str := recover()
        fmt.Println(str)
    }()
    panic("PANIC")
}
```

通常一個 panic 代表的是一個程式設計師的錯誤（例如想要存取超出陣列邊界的索引值、忘記對一個 map 進行初始化之類），或是有難以還原的例外情況發生（所以才稱之為 panic）。
