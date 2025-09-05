---
description: Array, Two Pointers, Binary Search, Sorting
---

# 2824: Count Pairs Whose Sum is Less than Target - Easy

## 釐清需求與邊界條件

* #### 輸入:
  * `nums`: 一個整數陣列，長度為 n (1 ≤ n ≤ 50)
  * `target`: 一個整數目標值
* #### 輸出:
  * 返回一個整數，表示所有滿足 `nums[i] + nums[j] < target` 且 `i < j` 的配對數量
* #### 邊界條件:
  * 陣列長度至少為 1，最多 50
  * 陣列元素可能為負數、零或正數
  * 需要考慮 i < j 的條件（避免重複計算和自己與自己配對）
  * 如果陣列長度為 1，直接返回 0

## 口述解法

*   #### 主要函數 (`countPairs`):

    這個解法使用了**雙指針技巧**，是一個經典的優化方法：

    **步驟說明:**

    1. **排序陣列**: 首先將 `nums` 進行排序，這是使用雙指針的前提
    2. **初始化變數**:
       * `ans = 0`: 記錄符合條件的配對數量
       * `l = 0`: 左指針指向陣列開始
       * `r = len(nums)-1`: 右指針指向陣列結尾
    3. **雙指針遍歷**:
       * 當 `l < r` 時進行循環
       * **如果 `nums[l] + nums[r] < target`**:
         * 關鍵洞察：由於陣列已排序，`nums[l]` 與從 `l+1` 到 `r` 的所有元素配對都會小於 target
         * 因此可以一次性增加 `r - l` 個配對
         * 左指針右移 `l += 1`
       * **如果 `nums[l] + nums[r] >= target`**:
         * 當前配對太大，需要減小和值
         * 右指針左移 `r -= 1`

## 測試與優化

* 程式碼

```python
class Solution:
    def countPairs(self, nums: List[int], target: int) -> int:
        nums.sort()

        ans = 0
        l = 0
        r = len(nums)-1
        
        while l < r:
            if nums[l] + nums[r] < target:
                ans += r - l
                l += 1
            else:
                r -= 1

        return ans
```

* 測資與注意事項

## 時間與空間複雜度

* 時間複雜度：O(n log n)
  * **排序階段**: O(n log n)
  * **雙指針遍歷**: O(n) - 每個元素最多被訪問一次
  * **總體**: O(n log n) + O(n) = O(n log n)
* 空間複雜度：O(1) 或 O(n)
  * **輔助空間**: O(1) - 只使用了常數個變數
  * **排序空間**: Python 的 sort() 在最壞情況下: O(n)
