# 04.03-常數（Constant）

Go 也支援常數，常數基本上是值無法更動的變數。建立常數的方式與變數一樣，但是不需使用 `var` 關鍵字，而是使用 `const` 關鍵字：

```go
package main

import "fmt"

func main() {
    const x string = "Hello World"
    fmt.Println(x)
}
```

這個：

```
    const x string = "Hello World"
    x = "Some other string"
```

結果在編譯時會發生錯誤：

```
.\main.go:7: cannot assign to x
```

在程式裡，常數是重新使用一般值的一種好方法，因為可以不用每次都將值寫出來，例如：在 `math` package 的 `Pi` 就是定義為常數。
