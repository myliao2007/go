# 04-變數

到目前為止，我們只看過程式使用固定的值（數字、字串等），但是這樣的程式並不實用，所以如果要寫實用的程式，我們需要學習兩個新的概念：變數與控制流程。本章將詳細的介紹變數。

變數是一個儲存位置，有特定的型別及相關的名字，我們來改一下第二章寫的程式，讓它使用變數：

```
package main

import "fmt"

func main() {
    var x string = "Hello World"
    fmt.Println(x)
}
```

注意原本程式的字串值在這個程式裡依然會出現，但不是直接將字串送給 `Println` 函式，而是將字串指派給變數。Go 的變數是透過 `var` 關鍵字所建立的，接著指定變數名稱（`x`）為字串型別（`string`），最後將字串值 （`Hello World`）指定給變數，最後一個非必要的步驟，寫這個程式的另一種方式如下：

```
package main

import "fmt"

func main() {
    var x string
    x = "Hello World"
    fmt.Println(x)
}
```

在 Go 裡的變數類似代數的變數，但是有些微的差異：

首先，當我們看到 `=` 符號時，我們直覺會讀成 “x 等於 Hello World 字串”，用這個方法讀程式不會有什麼問題，但是更好的方式是讀成 “將 Hello World 字串代入 x” 或者 “將 Hello World 字串指定給 x”。這樣的區分是很重要的，因為變數值會隨著程式的執行而變動（如其名所示），請試試看執行下列的程式：

```
package main

import "fmt"

func main() {
    var x string
    x = "first"
    fmt.Println(x)
    x = "second"
    fmt.Println(x)
}
```

實際上你甚至可以這麼做：

```
var x string
x = "first "
fmt.Println(x)
x = x + "second"
fmt.Println(x)
```

如果你用代數定理來讀這個程式是不合理的，不過如果你將這個程式看成一連串的指令來讀，就可以說的通了。在我們看到 `x = x + "second"` 時，我們應該將它讀成 “將變數 x 的值與字串值 second 連接在一起”。`=` 右邊會先運算，再來才將結果指定給 `=` 左邊的變數。

`x = x + y` 的形式在程式語言是很常見的，不過 Go 有個特殊的指派符號：`+=`，我們可以將 `x = x + "second"` 寫成 `x += "second"`，這樣做的事情是相同的（別的運算符號用法也是一樣）。

Go 與代數的差異在於等式判斷的符號不同：`==`（兩個等號），`==` 跟 `+` 運算符類似，而且會傳回布林值（boolean），例如：

```
    var x string = "hello"
    var y string = "world"
    fmt.Println(x == y)
```

這個程式應該會印出 `false`，因為 `hello` 不等於 `world`，另一方面：

```
    var x string = "hello"
    var y string = "hello"
    fmt.Println(x == y)
```

這樣會印出 `true`，因為兩個字串一樣。

由於建立新變數時順便賦予初始值，在 Go 是很常見的，所以 Go 也支援了較短的寫法：

```
    x := "Hello World"
```

請注意，在 `=` 之前有 `:`，而且沒有指定型別。不需要型別的理由是因為 Go 編譯器可以依據你指定給變數的數值來推論出型別。（因為你指定字串數值，所以 `x` 的型別就是 `string`）。編譯器也可以推論使用 `var` 的句子：

```
    var x = "Hello World"
```

也適用於其它的型別：

```
    x := 5
    fmt.Println(x)
```

如果可以，你通常該用簡寫的格式。
