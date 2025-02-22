---
description: Array, Two Pointers, Binary Search
---

# 167 - Two Sum II - Input Array Is Sorted - Medium

## 釐清需求與邊界條件

* 輸入：已排序（非遞減順序）的整數陣列 numbers
* 輸出：找到兩個數字，其和等於目標值 target，返回這兩個數字的索引值 +1
* 限制條件：
  * 不能使用同一個元素兩次
  * 要求使用常數額外空間
  * 邊界條件：
    * 陣列長度至少為 2
    * 索引 1 必須小於索引 2
    * 保證有解

## 口述解法

*   優化後的解法使用雙指針技巧：

    主要函數 twoSum：

    1. 初始化左指針 l = 0 和右指針 r = len(numbers) - 1
    2. 當 l <= r 時，執行以下步驟：
       * 如果 numbers\[l] + numbers\[r] == target，找到解答，返回 \[l+1, r+1]
       * 如果兩者和 < target，表示要往大的方向移動，左指針右移（l += 1）
       * 如果兩者和 > target，表示要往小的方向移動，右指針左移（r -= 1）

## 測試與優化

* 程式碼
* 優化前
  * 原始解法使用雙重迴圈，時間複雜度為 O(n²)

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        for i in range(len(numbers)):
            for j in range(len(numbers)):
                if target - numbers[i] == numbers[j] and i != j:
                    return i+1, j+1
```

* 優化後
  * 使用雙指針技巧，利用陣列已排序的特性，時間複雜度降為 O(n)

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l = 0
        r = len(numbers) - 1

        while l <= r:
            if numbers[l] + numbers[r] == target:
                return l+1, r+1
            if numbers[l] + numbers[r] < target:
                l += 1
            else:
                r -= 1
```

* 空間複雜度從 O(1) 維持不變

## 時間與空間複雜度

* 時間複雜度：O(n)
  * 最壞情況下需要遍歷整個陣列一次
* 空間複雜度：O(1)
  * 只使用兩個指針變數，不管輸入大小，額外空間使用量固定
