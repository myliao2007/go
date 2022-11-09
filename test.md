# 12-測試



程式設計並不容易，即使是最好的程式設計師，也無法在想寫程式時就可以寫出來。因此，軟體開發過程中的一個重點就是測試。為自己的程式碼設計測試程式在確保程式的品質與可靠度上，是一個很好的方式。

Go 語言有一個特殊的程式，可以比較容易地設計測試程式。所以我們在上一章用這個 package 建立了一些測試程式。在 `math` 資料夾中，`chapter11` 建立了一個檔名為 `math_test.go` 的新檔案，內容如下：

```go
package math

import "testing"

func TestAverage(t *testing.T) {
    var v float64
    v = Average([]float64{1,2})
    if v != 1.5 {
        t.Error("Expected 1.5, got ", v)
    }
}
```

執行這個指令：

```
go test
```

你應該會看到下列的執行結果：

```
$ go test
PASS
ok      golang-book/chapter11/math      0.032s
```

&#x20;`go test` 指令會尋找目前資料夾中的任何測試程式，並且執行它們。測試程式的辨別方式是有一個 `Test` 起始函式，並有一個  `*testing.T` 型別的參數。在我們的範例中，因為我們正在測試 `Average` 函式，所以我們將測試函式命名為 `TestAverage`。

只要我們完成了測試函式的設定，我們就可以設計測試程式來測試程式碼。以此例而言，我們知道 `[1,2]` 的平均值應該是 `1.5`，所以我們就可以這樣檢查。測試不同的數字組合可能是個好主意，所以我們稍微修改我們的測試程式：

```go
package math

import "testing"

type testpair struct {
    values []float64
    average float64
}

var tests = []testpair{
    { []float64{1,2}, 1.5 },
    { []float64{1,1,1,1,1,1}, 1 },
    { []float64{-1,1}, 0 },
}

func TestAverage(t *testing.T) {
    for _, pair := range tests {
        v := Average(pair.values)
        if v != pair.average {
            t.Error(
                "For", pair.values, 
                "expected", pair.average,
                "got", v,
            )
        }
    }
}
```

這是常見的建立測試方法（可以在 Go 語言的 packages 程式原始碼中找到大量的範例）。我們建立一個 `struct` 來儲存函式的輸入與輸出。然後我們建立一串 `struct` (成對的)。再來我們透過迴圈處理每一組，並執行函式。

#### 問題 <a href="#toc" id="toc"></a>

* 設計一個好的測試套件並不是每次都很簡單，不過設計測試程式的過程中，通常會遭遇比初次了解時更多的問題。例如：在我們的 `Average` 函式中，若你傳遞一個空的串列 (`[]float64{}`) 會發生什麼事呢？就這個案例來說，我們如何修改函式，使得函式會傳回 0 呢？
* 幫你在前幾章寫的 `Min` 與 `Max` 函式設計一些測試程式。
