---
description: Stack Array, Two Pointers, Dynamic Programming, Monotonic Stack
---

# 42 - Trapping Rain Water - Hard

## 釐清需求與邊界條件

* 輸入：輸入是一個非負整數陣列，代表每個位置的高度
* 輸出：計算能夠接住多少雨水
* 限制條件：
  * 陣列長度 < 3 時，無法接住水，返回 0
  * 高度為 0 的位置可能接住水
  * 最左邊和最右邊的柱子不能接住水

## 口述解法

* 對於每個位置，能接住的水量取決於這個位置左右兩側最高柱子的較小值減去當前位置的高度。
  1. 建立兩個陣列 left 和 right，分別記錄每個位置左側和右側的最大高度
  2. 從左向右遍歷，更新 left 陣列：
     * left\[i] = max(left\[i-1], height\[i])
  3. 從右向左遍歷，更新 right 陣列：
     * right\[i] = max(right\[i+1], height\[i])
  4. 遍歷每個位置，計算可以接住的水量：
     * water += min(left\[i], right\[i]) - height\[i]

## 測試與優化

* 程式碼

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        left = [height[0]] * n
        right = [height[-1]] * n

        for i in range(1, n):
            left[i] = max(left[i - 1], height[i])
            right[n - i - 1] = max(right[n - i], height[n - i - 1])

        return sum(min(l, r) - h for l, r, h in zip(left, right, height))
```

* 優化方向
  * 可以使用雙指針方法來將空間複雜度優化到 O(1)：

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        l = 0
        r = n-1
        max_left = 0
        max_right = 0
        water = 0

        while l <= r:
            max_left = max(max_left, height[l])
            max_right = max(max_right, height[r])

            if max_left < max_right:
                water += max_left - height[l]
                l += 1
            else:
                water += max_right - height[r]
                r -= 1

        return water
```

## 時間與空間複雜度

* 優化前(遍歷所有):
  * 時間複雜度：O(n)
    * 需要遍歷陣列 3 次
  * 空間複雜度：O(n)
    * 需要兩個額外的陣列來存儲左右最大值
* 優化後(雙指針):
  * 時間複雜度：O(n)
    * 只需遍歷一次
  * 空間複雜度：O(1)
    * 只需要幾個變數
