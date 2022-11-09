# 13.06-雜湊＆加解密

雜湊函式（hash function）採用一組資料，並將資料縮減為較小的固定尺寸。通常會將雜湊應用於設計查詢資料上，以能容易地偵測變動。Go 語言中的雜湊函式可分為兩類：

加密與非加密。

非加密式雜湊函式可以在 hash package 中找到，包含 `adler32`、`crc32`、`crc64` 與 `fnv`。這裡是一個使用 `crc32` 的範例：

```go
package main

import (
    "fmt"
    "hash/crc32"
)

func main() {
    h := crc32.NewIEEE()
    h.Write([]byte("test"))
    v := h.Sum32()
    fmt.Println(v)
}
```

`crc32` 雜湊物件實做了 `Writer` 介面，所以我們可以使用與其它資料相同的方式，透過 `Writer` 寫入資料。只要我們將資料完全寫入，我們就可以呼叫 `Sum32()` 來傳回一個 `uint32` 型別的值。`crc32` 的常用方式是用來比較兩個檔案，若兩個檔案的 `Sum32` 值都相同，若兩個檔案的 `Sum32` 值都相同，則表示這兩個檔案高度相似（不一定 100% 相同）。若兩個檔案計算的值不同，則可以確定檔案的內容不同：

```go
package main

import (
    "fmt"
    "hash/crc32"
    "io/ioutil"
)

func getHash(filename string) (uint32, error) {
    bs, err := ioutil.ReadFile(filename)
    if err != nil {
        return 0, err
    }
    h := crc32.NewIEEE()
    h.Write(bs)
    return h.Sum32(), nil
}

func main() {
    h1, err := getHash("test1.txt")
    if err != nil {
        return
    }
    h2, err := getHash("test2.txt")
    if err != nil {
        return
    }
    fmt.Println(h1, h2, h1 == h2)
}
```

加密的雜湊函式與其相對應的非加密雜湊函式類似，不過加密的雜湊函式有增加一些難以逆轉的屬性。一組經過雜湊加密的資料是很難得知使用哪種雜湊方式。這些雜湊通常是在安全性相關的應用程式上使用。

其中一種常見的加密雜湊函式是所謂的 SHA-1，下列是它的用法：

```go
package main

import (
    "fmt"
    "crypto/sha1"
)

func main() {
    h := sha1.New()
    h.Write([]byte("test"))
    bs := h.Sum([]byte{})
    fmt.Println(bs)
}
```

這個範例與 `crc32` 的範例類似，因為 `crc32` 與 `sha1` 都有實做 `hash.Hash` 介面，主要的差異在於：`crc32` 是計算一個 32 位元的雜湊，而 `sha1` 是 160 個位元。由於沒有原生的型別可以表示 160 個位元的數字，所以我們改成使用一個 20 bytes 的 slice 來代替。
