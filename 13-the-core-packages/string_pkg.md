# 13.01-字串

Go 語言在 `strings` package 提供大量的字串處理函式：

```go
package main

import (
    "fmt"
    "strings"
)

func main() {
    fmt.Println(    
        // true
        strings.Contains("test", "es"), 

        // 2
        strings.Count("test", "t"),

        // true
        strings.HasPrefix("test", "te"), 

        // true
        strings.HasSuffix("test", "st"), 

        // 1
        strings.Index("test", "e"), 

        // "a-b"
        strings.Join([]string{"a","b"}, "-"),

        // == "aaaaa"
        strings.Repeat("a", 5), 

        // "bbaa"
        strings.Replace("aaaa", "a", "b", 2),

        // []string{"a","b","c","d","e"}
        strings.Split("a-b-c-d-e", "-"), 

        // "test"
        strings.ToLower("TEST"), 

        // "TEST"
        strings.ToUpper("test"), 

    )
}
```

我們有時會需要將字串做為二進位資料使用，為了將字串轉換為 slice 的資料，需要這麼做（反之亦然）：

```go
arr := []byte("test")
str := string([]byte{'t','e','s','t'})
```

\
