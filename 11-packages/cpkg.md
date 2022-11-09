# 11.01-建立 Package



只在另一個程式的上下文（context）使用 packages 是比較合理的。若沒有這個獨立的程式，我們就無法使用我們建立的 package 了。現在我們建立一個應用程式來使用我們撰寫的 package。在資料夾 `~/Go/src/golang-book` 中建立一個名為 `chapter11` 的資料夾，並在該資料夾中建立一個名為 `main.go` 的檔案，其內容如下：

```go
package main

import "fmt"
import "golang-book/chapter11/math"

func main() {
    xs := []float64{1,2,3,4}
    avg := math.Average(xs)
    fmt.Println(avg)
}
```

現在我們在 `chapter11` 資料夾中建立另一個名為 `math` 的資料夾，並在該資料夾中建立一個 `math.go` 的檔案，其內容如下：

```go
package math

func Average(xs []float64) float64 {
    total := float64(0)
    for _, x := range xs {
        total += x
    }
    return total / float64(len(xs))
}
```

開啟終端機，在 `math` 資料夾中執行 `go install`，這樣會編譯 `math.go` 程式，並建立一個可連結的物件檔（object file）：`~/Go/pkg/os_arch/golang-book/chapter11/math.a`（這裡的 `os` 類似 `windows`，而 `arch` 則類似 `amd64`）

現在我們回到 `chapter11` 資料夾，並執行 `go run main.go`，現在應該會得到 `2.5`。有幾點要注意的事項：

* `math` 是一個 package 的名稱，這是 Go 語言在標準發行版本的一部分內容，只是因為 Go 語言的 packages 可以是階層式的，所以我們能安全的在我們自己的 package 中使用同樣的名稱（原本的 `math` package 就是 `math`，而我們的則是 `golang-book/chapter11/math`）
* 當我們匯入（import）我們自己的 math 函式庫時，我們會使用它的全名（`import "golang-book/chapter11/math"`），只是在 `math.go` 檔案中，我們只會使用最後一部分的名稱（`package math`）。
*   當從我們的函式庫中參照到函式時，也可以只用 `math` 這個名稱。如果我們想要在同樣的程式中，同時使用這兩個函式庫時，Go 語言可以使用別名：

    ```go
    import m "golang-book/chapter11/math"

    func main() {
        xs := []float64{1,2,3,4}
        avg := m.Average(xs)
        fmt.Println(avg)
    }
    ```

    `m` 就是別名。
* 你可能注意到了，package 中的每個函式都是以大寫字母開頭的，這表示其它的 packages （以及程式）都可以看到它。如果我們將函式命名為 `average` 而不是 `Average`，則我們的 `main` 程式就無法看見這個函式。比較好的方式是只揭露我們 package 的一部份內容（我們想要開放給其它 package 使用的），而將其它內容隱藏起來。我們之後可以隨意更改，而不用擔心會破壞到其它程式，而且這樣可以讓我們的 package 易於使用。
* Package 的名稱會與它們所在的資料夾相同，還有一些方法，不過這個方式是最簡單的。
