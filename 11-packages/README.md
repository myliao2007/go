# 11-Packages



Go 語言的設計是要鼓勵軟體工程師實作。高品質軟體的其中一個要素是重複使用程式碼（精神是不要重複做一樣的事情）。

如我們在第七章所示，函式是重複使用程式碼的第一層。此外，Go 語言還提供另一個重複使用程式碼的機制：即 package。幾乎我們看到的每個程式都有這一行：

```
import "fmt"
```

`fmt` 是 package 的名稱，包含各種螢幕輸出與格式的相關函式，用這個方式打包程式碼有三個目的：

* 可以減少命名重疊的機會，這樣可以讓我們的程式碼簡潔明瞭。
* 可以組織程式碼，容易找出我們想要重複使用的程式碼。
* 可以加速編譯器，只需要重新編譯程式的一小部份。雖然我們一直用到 `fmt` package，不過我們不用在每次修改程式時就重新編譯這個 package。
