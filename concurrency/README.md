# 10-Concurrency（並行處理）

大型程式通常是由許多小程式組成的。例如，一個網頁伺服器會處理來自瀏覽器的請求，並提供 HTML 格式的網頁做為回應。每個請求的處理都像是執行一個小程式。

比較理想的方式是，讓這類程式可以同時執行它們的小元件（以網頁伺服器需要處理多個請求為例）。可以同步處理多個任務的能力即是所謂的並行處理。Go 語言透過 goroutine 與 channel 提供了相當多的並行處理功能。
