---
description: Array Hash, Table
---

# 1 - Two Sum - Easy

## 釐清需求與邊界條件

* 輸入：一個整數陣列 nums 和目標值 target
* 輸出：找出兩個數字的索引，使它們的和等於 target
* 限制條件：
  * 陣列長度至少為 2（因為需要兩個數）
  * 數字可以是正數、負數或零
  * 陣列中的數字和 target 都是整數

## 口述解法

* 復述問題並說明想法
  * 創建一個哈希表(hashmap)來儲存遍歷過的數字及其索引
  * 遍歷陣列中的每個數字：
    * 計算當前數字與目標值的差值(complement)&#x20;
    * 如果差值存在於哈希表中，表示找到解，返回當前索引和哈希表中差值的索引&#x20;
    * 否則將當前數字和其索引存入哈希表

## 測試與優化

* 程式碼

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap:
                return [i, hashmap[complement]]
            hashmap[nums[i]] = i
        return []
```

* 測資與注意事項
  * 使用哈希表可以將查找時間從 O(n) 降低到 O(1)
  * 空間換時間的策略，可以先寫出暴力解 O(n²) 再優化
  * &#x20;一次遍歷即可完成，不需要嵌套循環

## 時間與空間複雜度

* 時間複雜度：O(n)&#x20;
  * 只需要遍歷一次陣列，哈希表的查找操作是 O(1)
* 空間複雜度：O(n)
  * 最壞情況下需要將整個陣列存入哈希表
  * 最好情況是在遍歷到第二個數時就找到解，空間為 O(1)
