# 13.09-Synchronization Primitives（同步處理原始物件）

在 Go 語言中，在並行（concurrency）與同步（synchronization）方面的處理上，建議使用使用第10章討論的 Goroutine 與 channel 方式。然而，Go 語言在 `sync` 與 `sync/atomic` package 中也有提供了較為傳統的多執行緒常式（multithreading routine）。

Mutexes（互斥鎖）

一個 mutex (mutal exclusive lock) 會將一段程式碼一次只鎖定給單個執行緒，可保護共用的資源在非原子式操作出現競速條件（race condition）。下列是一個 mutex 的範例：

```go
package main

import (
    "fmt"
    "sync"
    "time"
)
func main() {
    m := new(sync.Mutex)
    
    for i := 0; i < 10; i++ {
        go func(i int) {
            m.Lock()
            fmt.Println(i, "start")
            time.Sleep(time.Second)
            fmt.Println(i, "end")
            m.Unlock()
        }(i)
    }

    var input string
    fmt.Scanln(&input)
}
```

在 mutex (`m`) 處於上鎖狀態時，其他想要對此 mutex 進行上鎖的動作都會受到阻塞（block），直到此 mutex 已經被解鎖為止。在使用 `sync/atomic` package 中的 mutex 或同步處理原始物件（Synchronization Primitives ）時要非常謹慎。

以往要設計多執行緒程式是有難度的，因為很容易產生難以發現的錯誤。由於這些錯誤可能取決於非常特定的情況、極少發生，而且難以完成重現這些情況的條件。而 Go 語言最強大之處在於，它提供的並行功能比執行緒與互斥鎖更易於理解與使用。
