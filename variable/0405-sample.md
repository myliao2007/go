# 04.05-範例程式

這裡有個範例程式，由使用者輸入一個數字，並將這個數乘以 2：

```go
package main

import "fmt"

func main() {
    fmt.Print("Enter a number: ")
    var input float64
    fmt.Scanf("%f", &input)
    
    output := input * 2
    
    fmt.Println(output)    
}
```

我們用 `fmt` package 裡的另一個函式來讀取使用者的輸入（`Scanf`），`&input` 在之後我們將會說明，目前我們只需要知道 `Scanf` 會將我們輸入的數字填在 input。
