# 13.03-檔案與資料夾

為了使用 Go 語言開啟一個檔案，我們可以使用 `os` package 的 `Open` 函式，下列是一個範例，引導我們如何讀取一個檔案的內容，並將檔案內容呈現在終端機：

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("test.txt")
    if err != nil {
        // handle the error here
        return
    }
    defer file.Close()
    
    // get the file size
    stat, err := file.Stat()
    if err != nil {
        return
    }
    // read the file
    bs := make([]byte, stat.Size())
    _, err = file.Read(bs)
    if err != nil {
        return
    }

    str := string(bs)
    fmt.Println(str)
}
```

我們在開啟檔案之後要立刻使用 `defer file.Close()`，以確定檔案會在函式完成時盡快關閉。讀取檔案是常做的工作，因此有比較簡潔的方式來讀取檔案：

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    bs, err := ioutil.ReadFile("test.txt")
    if err != nil {
        return
    }
    str := string(bs)
    fmt.Println(str)
}
```

這裡示範如何建立一個檔案：

```go
package main

import (
    "os"
)

func main() {
    file, err := os.Create("test.txt")
    if err != nil {
        // handle the error here
        return
    }
    defer file.Close()

    file.WriteString("test")
}
```

為了取得目錄的內容，我們使用相同的 `os.Open` function，不過這次是提供一個目錄的路徑，而不是檔案名稱。接著我們呼叫 `Readdir` method：

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    dir, err := os.Open(".")
    if err != nil {
        return
    }
    defer dir.Close()

    fileInfos, err := dir.Readdir(-1)
    if err != nil {
        return
    }
    for _, fi := range fileInfos {
        fmt.Println(fi.Name())
    }
}
```

通常我們會用遞迴的方式來遍尋一個資料夾的內容（讀取資料夾的內容、全部的子資料夾、全部子資料夾的子資料夾、…）。為了更方便達成這項工作，我們可以使用　`path/filepath` package 中的 `Walk` 函式：

```go
package main

import (
    "fmt"
    "os"
    "path/filepath"
)

func main() {
    filepath.Walk(".", func(path string, info os.FileInfo, err error) error {
        fmt.Println(path)
        return nil
    })
}
```

會對根目錄（root，此例為 .）中的每個檔案與資料夾呼叫傳遞給 `Walk` 的函式。
