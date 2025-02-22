---
description: Math
---

# 9 - Palindrome Number - Easy

## 釐清需求與邊界條件

* 輸入：一個整數 `x`
* 輸出：若 `x` 為回文數，則回傳 `True`；否則回傳 `False`
* 限制條件：
  * **負數**：任何負數皆不可能為回文數，因為負號不會在反轉後出現於末端。
  * **末位為 0 的數字**：若數字以 0 結尾但不為 0（例如 10、100 等），則不可能是回文數，因為回文數若以 0 開頭是不成立的。

## 口述解法

* **初步檢查：**
  * 檢查 `x` 是否小於 0，若是則直接回傳 `False`。
  * 檢查 `x` 的末尾是否為 0，但 `x` 不等於 0，若成立則回傳 `False`。\
    &#xNAN;_（這兩項檢查可快速排除不可能的情況。）_
* **逆轉數字一半：**
  * 初始化一個變數 `revertedNumber` 為 0，用於儲存逆轉後的後半段數字。
  * 使用 `while` 迴圈進行逆轉操作，其條件為：原始數字 `x` 大於 `revertedNumber`。
  * 在每次迴圈中：
    * 先取得 `x` 的最後一位數（`x % 10`），並將該數字加到 `revertedNumber` 的末尾（即 `revertedNumber = revertedNumber * 10 + x % 10`）。
    * 更新 `x` 為 `x // 10`，將最後一位數移除。
* **回文檢查：**
  * 當 `x` 小於或等於 `revertedNumber` 時，說明我們已逆轉了一半或超過一半的數字。
  * 若數字位數為偶數，則 `x` 與 `revertedNumber` 應完全相等；若為奇數，則中間的數字可以透過 `revertedNumber // 10` 移除後比對。
  * 最後回傳 `x == revertedNumber or x == revertedNumber // 10`。

## 測試與優化

* 程式碼

```python
# 轉成字串
class Solution:
    def isPalindrome(self, x: int) -> bool:
         strs = str(x)
         for i in range(len(strs) // 2):
             if strs[i] != strs[-i-1]:
                 return False

         return True
```

```python
# 使用前後分解方法
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0 or (x % 10 == 0 and x != 0):
            return False

        revertedNumber = 0
        while x > revertedNumber:
            revertedNumber = revertedNumber * 10 + x % 10
            x //= 10

        return x == revertedNumber or x == revertedNumber // 10
```

## 時間與空間複雜度

* 時間複雜度：O(log(n))
  * 由於在迴圈中每次都會將 `x` 減少一位數，最終迴圈次數與數字位數成正比（只處理了一半位數）
* 空間複雜度：**O(1)**
  * 僅使用了常數空間（例如 `revertedNumber` 及數個變數）
