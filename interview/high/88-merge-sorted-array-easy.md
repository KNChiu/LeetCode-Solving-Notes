---
description: Array, Two Pointers, Sorting
---

# 88 - Merge Sorted Array - Easy

## 釐清需求與邊界條件

* 輸入：兩個已排序的整數陣列 nums1 和 nums2，以及它們的有效長度 m 和 n
  * nums1 的實際長度為 m+n，後面 n 個位置預留給合併結果
* 輸出：要求直接修改 nums1 而不是返回新陣列
* 限制條件：
  * 當 nums2 為空 (n=0)&#x20;
  * 當 nums1 的有效元素為空 (m=0)&#x20;
  * 當陣列只有一個元素

## 口述解法

* 從後往前比較兩個陣列的元素，將較大的放入 nums1 的末尾
* 設置三個指針：
  * p：指向 nums1 的最後位置 (m+n-1)&#x20;
  * p1：指向 nums1 有效元素的最後位置 (m-1)&#x20;
  * p2：指向 nums2 的最後位置 (n-1)
* 當 p2 >= 0 時（即 nums2 還有元素未處理）：
  * 比較 nums1\[p1] 和 nums2\[p2] 將較大的數字放到 nums1\[p] 的位置
* 當 nums2 處理完畢，算法結束 （nums1 剩餘的元素已經在正確位置）

## 測試與優化

* 程式碼

```python
class Solution:
    def merge(self, nums1: list[int], m: int, nums2: list[int], n: int) -> list[int]:
        p =  m + n - 1
        p1 = m - 1
        p2 = n - 1
        
        while p2 >= 0:
            if p1 >= 0 and nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            
            p -= 1
```

## 時間與空間複雜度

* 時間複雜度：O(m+n)
  * 最壞情況下需要遍歷兩個陣列的所有元素
* 空間複雜度：O(1)
  * 只使用了幾個指針變數，不需要額外空間
