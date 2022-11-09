# 03.02-字串



如我們在第2章所見，字串是一連串用來表示文字的字元，有固定的長度。Go 的字串是由個別的 byte 組成，通常一個字元是一個 byte（其它語言的字元，如中文，是用一個以上的 byte 來表示）。

可以用兩個雙括號或單括號來建立字串，如：`"Hello World"` 或 `` `Hello World` ``，差異在於雙括號不能有換行符號，但是雙括號可以有特殊的跳脫字元，比如： 表示換行符號，而  表示 tab 字元。

有幾個常見的字串操作，包含找出字串長度：`len("Hello World")`、存取字串中的特定字元：`"Hello World"[1]`，以及兩個字串的連接符號：`"Hello " + "World"`。讓我們來修改之前建立的程式來測試這些功能：

```go
package main

import "fmt"

func main() {
    fmt.Println(len("Hello World"))
    fmt.Println("Hello World"[1])
    fmt.Println("Hello " + "World")
}
```

有些要注意的事情：

* 空格也是字元，所以 "Hello World" 的字串長度是 11，而不是 10，且第三行是 `"Hello "` 而不是 `"Hello"`。
* 字串從 0 開始進行索引（index）而不是 1。`[1]` 表示第二個元素（element），而不是第一個。還要注意，你在執行程式時看到 "Hello World"\[1] 印出的是 `101` 而不是 `e`。這是因為字元是用一個 byte 來表示（記得一個 byte 就是一個整數）。可以將索引想成這樣：`"Hello World"1`，可以讀成 "Hello World 字串的子項目 1"、"在 Hello World 字串索引 1 的位置" 或者 "Hello World 字串的第二個字元"。
* 連接字串的符號跟加法一樣，Go 編譯器認為依據參數決定型別，因為 `+` 的左右兩邊都是字串，所以編譯器認為你的意思是要連接字串，而不是加法（對字串做加法運算是沒有意義的）。
