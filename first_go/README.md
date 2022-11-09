# 02-你的第一個程式

## Your First Program

不管你用哪個程式語言，通常第一個寫的程式是名為 "Hello World" 的程式： 一個單純將 `Hello World` 輸出到終端機的程式。我們用 Go 來寫一個。

你在第一章使用的安裝程式，會在你的個人資料夾建立一個名為 `Go` 的資料夾。我們這裡要再建立一個新的資料夾，用來儲存程式的地方，資料夾是 `~/Go/src/golang-book/chapter2`（這裡的 `~` 表示你的個人資料夾）你可以從終端機輸入下列的指令來完成這件工作：

```
mkdir Go/src/golang-book
mkdir Go/src/golang-book/chapter2
```

使用你的文字編輯器輸入下列的程式碼：

```go
package main

import "fmt"

// 這是註解

func main() {
    fmt.Println("Hello World")
}
```

確定你的檔案內容與上述相同，並將檔案 `main.go` 儲存在我們剛建立的資料夾中。開啟一個新的終端機，並輸入下列的指令：

```
cd Go/src/golang-book/chapter2
go run main.go
```

你應該會看到 `Hello World` 顯示在你的終端機。`go run` 指令會將後面的幾個（以空格隔開的）檔案編譯為一個可執行檔並存放在一個暫存資料夾中，然後執行程式。若你沒有看到 `Hello World` 顯示出來，可能是輸入的程式碼有錯誤的地方。Go 編譯器會給你一些提示，跟你說哪裡有錯誤。Go 編譯器跟多數的編譯器一樣，很嚴謹而且無法容忍有錯誤存在。
