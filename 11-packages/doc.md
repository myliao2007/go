# 11.02-文件

Go 語言可以自動產生 package 的文件，類似標準的 package 文件。可以在終端機中執行下列指令：

```go
godoc golang-book/chapter11/math Average
```

應該會看到我們所寫的該函式相關資訊，我們可以在函式前面新增一些註解來改善此文件：

```
// Finds the average of a series of numbers
func Average(xs []float64) float64 {
```

若你在 `math` 資料夾中執行 `go install`，接著重新執行 `godoc` 指令，你應該會在函式的定義下方看到我們的註解。此文件也可以透過執行下列指令取得：

```
godoc -http=":6060"
```

並將此 URL 輸入在你們瀏覽器上：

```
http://localhost:6060/pkg/
```

你應該可以瀏覽你系統安裝的每個 package。
