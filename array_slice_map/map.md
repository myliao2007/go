# 06.03-Map

Map 是一個無排序的 key-value 配對集合，也是所謂的一個有關聯的陣列、一個雜湊表或是一個目錄。map 可以使用一個關聯的 key 來查值，下列是一個 Go 語言的 map 範例：

```go
var x map[string]int
```

Map 的型別是透過 `map` 關鍵字表示，後面接著中括號框著的 key 型別，最後則是 value 的型別。可以這樣念，「`x` 是一個 `string` 對 `int` 的 map」。

如同陣列與 slice，可以使用中括號來存取 map，請試著執行下列的程式：

```go
var x map[string]int
x["key"] = 10
fmt.Println(x)
```

你應該會看到類似如下的錯誤訊息：

```go
panic: runtime error: assignment to entry in nil map

goroutine 1 [running]:
main.main()
  main.go:7 +0x4d

goroutine 2 [syscall]:
created by runtime.main
        C:/Users/ADMINI~1/AppData/Local/Temp/2/bindi
t269497170/go/src/pkg/runtime/proc.c:221
exit status 2
```

到目前為止，我們只看到編譯期的錯誤。這是一個執行期的錯誤訊息，如其名所示，執行期的錯誤會在執行程式期間發生，而編譯期的錯誤則是在編譯程式期間發生的。

我們程式的問題是，必須在使用 map 之前先進行初始化，我們應該改成下面的寫法：

```go
x := make(map[string]int)
x["key"] = 10
fmt.Println(x["key"])
```

你執行此程式之後應該會看到有 `10` 出現，陳述句 `x["key"] = 10` 跟我們在使用陣列時類似，只是這裡是 key 而不是整數，而且是一個字串，因為這裡 map 的 key 型別是 `string`。我們也可以使用 `int` 型別做為 key 來建立 map：

```go
x := make(map[int]int)
x[1] = 10
fmt.Println(x[1])
```

這樣看起來很像是一個陣列，不過還是有些不同之處。首先，map 的長度（透過 `len(x)` 取得）是可以改變的，只要我們新增項目（item）就會改變。起初 map 建立時的長度為 0，而在我們執行 `x[1] = 10` 之後，長度就變成 1 了。第二個與陣列的差異是，map 並非循序的，例如在陣列中，當看到 `x[1]` 代表的是一定有 `x[0]` 的存在不過 map 卻不一定如此。

我們也可以使用內建的 `delete` 函式來刪除 map 中的項目：

```go
delete(x, 1)
```

接著來看一個 map 範例程式：

```go
package main

import "fmt"

func main() {
    elements := make(map[string]string)
    elements["H"] = "Hydrogen"
    elements["He"] = "Helium"
    elements["Li"] = "Lithium"
    elements["Be"] = "Beryllium"
    elements["B"] = "Boron"
    elements["C"] = "Carbon"
    elements["N"] = "Nitrogen"
    elements["O"] = "Oxygen"
    elements["F"] = "Fluorine"
    elements["Ne"] = "Neon"
    
    fmt.Println(elements["Li"])
}
```

`elements` 是一個 map，使用化學元素表的前十個元素符號做為 elaments 的索引值，這是常見的 map 用法：如同查表或是查字典。假設我們查詢了一個不存在的元素：

```
fmt.Println(elements["Un"])
```

若是執行上面這行程式，應該不會傳回任何資料。技術上，一個 map 會依據 value 的型別而傳回相對應的零值（比如字串就是傳回空字串）。雖然我們可以透過條件式來檢查零值（`elements["Un"] == ""`），不過 Go 語言有提供一個更好的方法：

```go
name, ok := elements["Un"]
fmt.Println(name, ok)
```

存取一個 map 中的一個元素可以傳回兩個值，第一個值是查詢的結果，而第二個值是告訴我們查詢是否成功。在 Go 語言中，我們通常會看到下列這樣的程式碼：

```go
if name, ok := elements["Un"]; ok {    
    fmt.Println(name, ok)
}
```

首先，我們試著存取 map 的值，若成功了，則執行區塊中的程式碼：

如同我們在介紹陣列時所見，也有比較簡潔的方式可以建立 map：

```go
elements := map[string]string{
    "H": "Hydrogen",
    "He": "Helium",
    "Li": "Lithium",
    "Be": "Beryllium",
    "B": "Boron",
    "C": "Carbon",
    "N": "Nitrogen",
    "O": "Oxygen",
    "F": "Fluorine",
    "Ne": "Neon",
}
```

一般會將 map 用來儲存通用的資訊，現在來修改我們的程式，使得元素不僅可以儲存名稱，還可以儲存其標準狀態（室溫狀態）：

```go
func main() {
    elements := map[string]map[string]string{
        "H": map[string]string{
            "name":"Hydrogen", 
            "state":"gas",
        },
        "He": map[string]string{
            "name":"Helium", 
            "state":"gas",
        },
        "Li": map[string]string{
            "name":"Lithium", 
            "state":"solid",
        },
        "Be": map[string]string{
            "name":"Beryllium", 
            "state":"solid",
        },
        "B":  map[string]string{
            "name":"Boron",
            "state":"solid",
        },
        "C":  map[string]string{
            "name":"Carbon",
            "state":"solid",
        },
        "N":  map[string]string{
            "name":"Nitrogen",
            "state":"gas",
        },
        "O":  map[string]string{
            "name":"Oxygen",
            "state":"gas",
        },
        "F":  map[string]string{
            "name":"Fluorine",
            "state":"gas",
        },
        "Ne":  map[string]string{
            "name":"Neon",
            "state":"gas",
        },
    }

    if el, ok := elements["Li"]; ok {    
        fmt.Println(el["name"], el["state"])
    }
}
```

要注意，我們的 map 型別已經從 `map[string]string` 改為 `map[string]map[string]string`。現在我們有一個兩層的字串 map ，外部的 map 用來查表（基於元素的符號），而內部的 map 則用來儲存與元素相關的通用資訊，雖然通常都會這樣使用 map，不過我們在第9章會再探討儲存結構化資訊的較好方法。
