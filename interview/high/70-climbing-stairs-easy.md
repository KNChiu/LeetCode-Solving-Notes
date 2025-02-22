---
description: Memoization, Math, Dynamic Programming
---

# 70 - Climbing Stairs - Easy

## 釐清需求與邊界條件

* 輸入：整數 n，代表樓梯階數（1 ≤ n ≤ 45）
* 輸出：整數，代表所有可能的爬樓梯方式數量
* 限制條件：
  * 每次可以爬 1 或 2 階

## 口述解法

*   這是一個典型的動態規劃問題，可以發現：

    * 到達第 n 階的方法 = 從第 n-1 階(爬 1 階的方法) + 從第 n-2 階(爬 2 階的方法)
    * 因此可以得出遞迴公式：dp\[n] = dp\[n-1] + dp\[n-2]

    主要解法步驟：

    1. 處理基礎案例：n ≤ 2 時直接返回 n
    2. 創建 dp 陣列存儲中間結果
    3.  設定初始值：

        dp\[1] = 1 (爬 1 階的方法)

        dp\[2] = 2 (爬 2 階的方法)
    4. 使用遞迴公式計算 dp\[3] 到 dp\[n]
    5. 返回 dp\[n]
* 優化解法：
  * 觀察到我們只需要前兩個數字，可以使用兩個變數替代整個陣列

## 測試與優化

* 程式碼
* 原本方法(建立陣列紀錄)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        dp = [0] * (n + 1)
        dp[1] = 1
        dp[2] = 2
        for i in range(3, n + 1):
            dp[i] = dp[i-1] + dp[i-2]
        return dp[n]
```

* 優化(空間優化)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        f0, f1 = 0, 1
        for _ in range(n):
            f0, f1 = f1, f0 + f1
        return f1
```

## 時間與空間複雜度

* 原始解法：
  * 時間複雜度：O(n)，需要遍歷 1 到 n
  * 空間複雜度：O(n)，需要一個長度為 n+1 的 dp 陣列
* 優化解法：
  * 時間複雜度：O(n)，仍需遍歷 1 到 n
  * 空間複雜度：O(1)，只使用兩個變數
