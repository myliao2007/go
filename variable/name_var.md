# 04.01-如何命名變數

變數命名是軟體開發很重要的一部分，命名必須以字母開頭，而且有可能會包含字母、數字或 `_` （底線）符號。Go 編譯器不會管你如何命名變數，所以為了你好（及別人），應該要使用能清楚表達變數用途的名稱，假設如下：

```go
    x := "Max"
    fmt.Println("My dog's name is", x)
```

在此例子中，x 變數名稱就不是很好，好的命名應該如下所示：

```go
    name := "Max"
    fmt.Println("My dog's name is", name)
```

或者：

```go
    dogsName := "Max"
    fmt.Println("My dog's name is", dogsName)
```

在上例中，我們使用特殊的方式來表達變數名稱，即所謂的 lower camel case（也是所謂的 mixed case、bumpy caps、camel back 或 hump back）。字首的第一個字母是小寫的，接下來的文字其第一個字母是大寫的，而其它全部的字母都是小寫的。
