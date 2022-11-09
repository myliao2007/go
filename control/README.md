# 05-控制結構

我們目前知道如何使用變數了，所以該來寫點有用的程式。首先我們來寫個可以從 1 算到 10 的程式，我們用之前學到的語法，應該會這樣寫：

```go
package main

import "fmt"

func main() {
    fmt.Println(1)
    fmt.Println(2)
    fmt.Println(3)
    fmt.Println(4)
    fmt.Println(5)
    fmt.Println(6)
    fmt.Println(7)
    fmt.Println(8)
    fmt.Println(9)
    fmt.Println(10)
}
```

或是這樣：

```go
package main
import "fmt"

func main() {
    fmt.Println(`1
2
3
4
5
6
7
8
9
10`)
}
```

不過這兩個程式寫起來都很乏味，有什麼東西可以讓我們處理重複的事情呢？
