# 13.02-輸入與輸出

在我們開始探討檔案處理之前，我們需要先了解 Go 語言的  `io` package。`io` package 有一些函式，不過多數的介面在其它 packages 也都會用到。兩個主要的介面是 `Reader` 與 `Writer`，`Reader` 提供的方法是透過 `Read` method，而 `Writer` 則提供透過 `Write` method 進行寫入的方式。Go 語言中的多數函式以 `Reader` 或 `Writer` 為參數。例如：`io` package 就有一個 `Copy` 函式，可以將資料從一個 `Reader` 複製到一個 `Writer`：

```go
func Copy(dst Writer, src Reader) (written int64, err error)
```

若要讀取或是寫入一個 `[]byte` / `string` 的資料，你需要用到使用在 `bytes` package 中找到的 `Buffer` struct。

```go
var buf bytes.Buffer
buf.Write([]byte("test"))
```

不需要對 `Buffer` 進行初始化以及 `Reader`／`Writer` 這兩個介面，我們可以透過呼叫 `buf.Bytes()` 來將它轉換為 `[]byte`。若你只需要讀取一個字串，則也可以使用 `strings.NewReader` 函式，這樣會比使用一個 buffer（緩衝區）更有效率。
