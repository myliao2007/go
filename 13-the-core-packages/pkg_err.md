# 13.04-錯誤訊息

Go 語言有一個內建型別可供錯誤訊息使用（`error`型別），我們可以使用 `errors` package 中的 `New` 函式建立自己的錯誤訊息：

```go
package main

import "errors"

func main() {
    err := errors.New("error message")
}
```

\
