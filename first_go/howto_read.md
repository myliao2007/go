# 02.01-如何讀 Go 程式

### How to Read a Go Program

我們先好好研究這個程式，由上而下、由左而右來讀 Go 程式，（跟讀英文書一樣），第一行這樣寫：

```
package main
```

這是所謂的 “package declaration”（套件宣告），每個 Go 程式都得用個 package declaration 當作開頭。Packages 是 Go 用來組成與重複使用程式碼的方式。有兩種 Go 程式：執行檔與函式庫。我們可以直接從終端機執行的應用程式（在 Windows 系統是用 `.exe` 結尾），函式庫（library）是我們將程式碼打包在一起的彙整，因而我們可以在其它程式中使用這些程式碼。我們之後會詳細的探討函式庫，現在只是要確定你寫的任何程式都有引用這行。

下一行是空白行，電腦以特殊字元來表示換行（或幾個字元）。換行、空格及 tab 都是所謂的空白（whitespace，因為我們看不到空白）。Go 大部分不會管空白，我們只用空白來排版，讓程式碼更好讀。（你可以移除這行，而程式也會以原本的行為正常運作）。

接著我們看看這行：

```
import "fmt"
```

關鍵字 `import` 用來將其它 packages 中的程式碼引用（include）到我們的程式裡。`fmt` package（format 的縮寫）實做了格式化輸入及輸出。用我們剛學到的 packages 概念，你認為 `fmt` package 的檔案會包含在它們之上嗎？

要注意到，上面的 `fmt` 有雙引號括起來，雙引號的用途類似所謂的 "string literal"，這是一種 "expression" 型別。在 Go 字串中表示有明確大小的一串字元（字母、數字、符號、...） 。字串在下一章會有詳細的說明，現在心裡記得的重要事項是：`"` 字元必須成對使用，而且它們中間只能放字串，而 `"` 字元本身不是字串。

以 `//` 開頭的是註解，Go 編譯器會忽略註解，註解存在的原因是為了你（或者是某個讀你程式碼的人）。Go 支援兩個不同類型的註解：`//` 表示在 `//` 之後與該行結尾以間的文字都是註解，而 `/* */` 註解表示在兩個 `*` 之間的部分都是註解（而且可能包含多行）。

之後你會看到一個函式宣告：

```go
func main() {
    fmt.Println("Hello World")
}
```

函式在一個 Go 程式中的定位類似積木，有輸入、輸出、以及依序執行一連串稱為 陳述句（statement）的步驟。全部的函式以 `func` 關鍵字起始，並接著函式名稱（此例為 `main`），可能沒有參數或是有一些由括號包圍起來的參數（parameter）、一個選配式的傳回型別（return type）、以及一個由大括弧包圍住的本體（body）。現在這個函式沒有參數，沒有傳回任何資料，只有一些陳述句。`main` 名字是很特別的，因為這是你執行程式時先被呼叫的函式。

我們的程式最後一段是這行：

```
    fmt.Println("Hello World")
```

這個 陳述句由三個元件所組成，我們先存取 `fmt` package 中的另一個名為 `Println` 的函式，（即 `fmt.Println` 這段，`Println` 表示印出這行），接著我們建立一個包含 `Hello World` 的新字串，並在呼叫這個函式時將這個字串做為它的參數。

此時，我們已經看過許多新名詞，而你可能有點無法負荷。有時刻意將程式唸出來是很有幫助的，現在將我們剛寫好的程式唸出來，大約類似這樣：

建立一個新的執行檔，它引用了 `fmt` 函式庫及包含一個名為 `main` 的函式，這個函式沒有參數，不會傳回任何值，且進行下列的工作：存取 `fmt` package 裡的 `Println` 函式，並搭配  `Hello World` 字串做為參數來呼叫這個函式。

`Println` 函式執行這個程式真正的工作，你可以在終端機輸入下列指令來查詢更多的資訊：

```
godoc fmt Println
```

在其它部分，你應該會看到這些：

```
Println formats using the default formats for its operands and writes to standard output. Spaces are always added between operands and a newline is appended. It returns the number of bytes written and any write error encountered.
```

Go 程式語言有很完整的文件，但是不好理解，除非你曾經學過其它程式語言。不過 `godoc` 指令相當好用，而且在你有問題時可以先從這裡查起。

回到我們手邊的這個函式，Go 文件告訴我們 `Println` 函式會將你給它的任何東西送到標準輸出（standard output，你正在使用的終端機輸出的名稱）。這個函式就是輸出 `Hello World` 的函式。

我們在下一章透過瞭解型別來探討 Go 如何儲存並表示如  `Hello World` 這類的資料。
