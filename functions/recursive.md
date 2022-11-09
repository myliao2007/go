# 07.05-遞迴（Recursive）

函式可以呼叫它自己，這裡是一個計算費伯納係數（factorial of a number）的方式：

```go
func factorial(x uint) uint {
    if x == 0 {
        return 1
    }

    return x * factorial(x-1)
}
```

`factorial` 呼叫它自己，使得函式進行遞迴（recursive），為了更了解此函式的運作，我們剖析 `factorial(2)` 的運作步驟：

* `x == 0` 成立嗎？否，（`x` 為 2）
* 找出 (2-1) 的費伯納係數
  * `x == 0` 成立嗎？否，（`x` 為 1）
  * 找出 (1-1) 的費伯納係數
    * `x == 0` 成立嗎？是，傳回 1。
  * 傳回 `1 * 1`
* 傳回 `2 * 1`

Closure 與遞迴是強大的程式設計技術，是所謂函式化程式設計（functional programming）的範例基礎。大多數的人會覺得函式化的程式設計比較難以理解，而覺得使用迴圈、if 陳述句、變數與簡易的函式會比較容易。
