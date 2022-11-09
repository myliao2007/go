# 13.08-解析命令列參數

當我們在終端機執行指令時，可能需要傳遞參數給指令，如下列的 `go` 指令所示：

```
go run myfile.go
```

run 與 myfile.go 都是參數，我們也可以將旗標(flag)傳遞給參數：

```
go run -v myfile.go
```

flag package 可以讓我們的程式解析參數與旗標，這裡有一個範例程式，可以產生一個 0 \~ 6 的數字，我們透過將旗標（-max=100）傳遞給程式，以更改最大值（max value）：

```go
package main

import ("fmt";"flag";"math/rand")

func main() {
    // Define flags
    maxp := flag.Int("max", 6, "the max value")
    // Parse
    flag.Parse()
    // Generate a number between 0 and max
    fmt.Println(rand.Intn(*maxp))
}
```

不屬於旗標的那些額外參數可以使用 `flag.Args()` 進行解析，而這個函式會傳回一個 `[]string`。
