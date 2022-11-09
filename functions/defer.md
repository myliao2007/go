# 07.06-Defer, Panic & Recover

Go 有一個特殊的陳述句，稱為 `defer` 會在一個函式執行完畢之後，將該函式呼叫加入排班，請見下列的範例：

```go
package main

import "fmt"

func first() {
    fmt.Println("1st")
}
func second() {
    fmt.Println("2nd")
}
func main() {
    defer second()
    first()
}
```

此程式會先印出 `1st`，並接著印出 `2nd`，基本上 defer 會將呼叫移到函式尾端的 `second`。

```go
func main() {
    first()
    second()
}
```

`defer` 通常用於需要以某種方式釋放資源時，例如：當我們開啟一個檔案時，我們需要能夠確定之後會關閉檔案。使用 `defer`：

```go
f, _ := os.Open(filename)
defer f.Close()
```

這樣有三項優點：(1) 讓我們的 `Close` 呼叫可以靠近我們的 `Open` 呼叫，使得易於了解呼叫的用處 (2) 若我們的函式有多個 return 陳述句時（或許 `if` 裡面有一個，而 `else` 裡面也有一個） `Close` 會在這兩個 return 之前執行 (3) 受到 defer 的函式即使在執行期當掉了，也能運作。
