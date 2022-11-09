# 13.07-伺服器

使用 Go 語言來設計網路伺服器是很簡單的，我們先看如何建立一個 TCP 伺服器：

```go
package main

import (
    "encoding/gob"
    "fmt"
    "net"
)

func server() {
    // listen on a port
    ln, err := net.Listen("tcp", ":9999")
    if err != nil {
        fmt.Println(err)
        return
    }
    for {
        // accept a connection
        c, err := ln.Accept()
        if err != nil {
            fmt.Println(err)
            continue
        }
        // handle the connection
        go handleServerConnection(c)
    }
}

func handleServerConnection(c net.Conn) {
    // receive the message
    var msg string
    err := gob.NewDecoder(c).Decode(&msg)
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println("Received", msg)
    }
    
    c.Close()
}

func client() {
    // connect to the server
    c, err := net.Dial("tcp", "127.0.0.1:9999")
    if err != nil {
        fmt.Println(err)
        return
    }

    // send the message
    msg := "Hello World"
    fmt.Println("Sending", msg)
    err = gob.NewEncoder(c).Encode(msg)
    if err != nil {
        fmt.Println(err)
    }

    c.Close()
}

func main() {
    go server()
    go client()
    
    var input string
    fmt.Scanln(&input)
}
```

這個範例使用了  `encoding/gob` package，這個 package 可以很容易的對 Go 值進行編碼，使得其它 Go 程式（或是本例中的 Go 程式）可以讀值。其它的編碼方式可取自 `encoding` （如 `encoding/json`）以及第三方的 packages（例如：我們可以使用  `labix.org/v2/mgo/bson` 取得 bson 的支援）。

\


#### HTTP <a href="#toc-http" id="toc-http"></a>

HTTP 伺服器更易設定於與使用：

```go
package main

import ("net/http" ; "io")

func hello(res http.ResponseWriter, req *http.Request) {
    res.Header().Set(
        "Content-Type", 
        "text/html",
    )
    io.WriteString(
        res, 
        `<doctype html>
<html>
    <head>
        <title>Hello World</title>
    </head>
    <body>
        Hello World!
    </body>
</html>`,
    )
}
func main() {
    http.HandleFunc("/hello", hello)
    http.ListenAndServe(":9000", nil)
}
```

`HandleFunc` 透過呼叫提供的函式來處理一個 URL route (`/hello`)，我們也可以使用 `FileServer` 處理靜態檔案：

```
http.Handle(
    "/assets/", 
    http.StripPrefix(
        "/assets/", 
        http.FileServer(http.Dir("assets")),
    ),
)
```

#### RPC <a href="#toc-rpc" id="toc-rpc"></a>

`net/rpc`（remote procedure call）以及 `net/rpc/jsonrpc` packages 提供了一個簡單的方式可以揭露 methods 的存在，使得能夠透過網路執行呼叫（並非只是在呼叫它們的程式中執行）

```go
package main

import (
    "fmt"
    "net"
    "net/rpc"
)

type Server struct {}
func (this *Server) Negate(i int64, reply *int64) error {
    *reply = -i
    return nil
}

func server() {
    rpc.Register(new(Server))
    ln, err := net.Listen("tcp", ":9999")
    if err != nil {
        fmt.Println(err)
        return
    }
    for {
        c, err := ln.Accept()
        if err != nil {
            continue
        }
        go rpc.ServeConn(c)
    }
}
func client() {
    c, err := rpc.Dial("tcp", "127.0.0.1:9999")
    if err != nil {
        fmt.Println(err)
        return
    }
    var result int64
    err = c.Call("Server.Negate", int64(999), &result)
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println("Server.Negate(999) =", result)
    }
}
func main() {
    go server()
    go client()
    
    var input string
    fmt.Scanln(&input)
}
```

此程式與 TCP 範例類似，只是我們現在有建立一個物件（object）來承載我們想要揭露的每個 method 與在客戶端（client）呼叫的  `Negate` method，細節請參考 `net/rpc` 中的文件。
