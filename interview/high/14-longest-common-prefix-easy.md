---
description: Trie, String
---

# 14 - Longest Common Prefix - Easy

## 釐清需求與邊界條件

* 輸入：字串陣列
* 輸出：找出所有字串共同的前綴
* 限制條件：
  * 如果沒有共同前綴，返回空字串 ""
  * 陣列長度範圍：1 <= strs.length <= 200
  * 字串長度範圍：0 <= strs\[i].length <= 200

## 口述解法

* 先將字串陣列排序
* 只需要比較第一個（字典序最小）和最後一個（字典序最大）字串
*   逐字符比較這兩個字串，直到：

    * 找到不同的字符
    * 或達到較短字串的長度


* 這個解法的巧妙之處在於：
  * 排序後，字典序最小和最大的字串之間的所有字串，其共同前綴一定不會比這兩個字串的共同前綴更長
  * 不需要比較所有字串，只需要比較兩個字串

## 測試與優化

* 程式碼

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        strs.sort()
        same_start = ""
        
        for i in range(min(len(strs[0]), len(strs[-1]))):
            if strs[0][i] != strs[-1][i]:
                break
            else: 
                same_start += strs[0][i]

        return same_start
```

* 測資與注意事項
  * 優化建議：
    * 可以先檢查陣列是否為空，以及第一個字串是否為空
    * 可以使用 Python 的 zip 函數來簡化比較過程
    * 可以不用創建新字符串，而是直接返回子字符串
  *   時間複雜度分析：

      * O(S)，其中 S 是所有字串中最短字串的長度
      * 不再需要排序，降低了時間複雜度（原來是 O(n log n + m)）

      空間複雜度分析：

      * O(1)，只使用了常數額外空間

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # 檢查邊界條件
        if not strs:
            return ""
        if len(strs) == 1:
            return strs[0]
            
        # 找出最短字串的長度，避免 index out of range
        min_len = min(len(s) for s in strs)
        if min_len == 0:
            return ""
            
        # 使用 zip 和 all 來比較每個位置的字符
        for i, chars in enumerate(zip(*strs)):
            if not all(c == chars[0] for c in chars):
                return strs[0][:i]
        
        # 如果循環結束都沒有返回，說明最短的字串就是共同前綴
        return strs[0][:min_len]
```

## 時間與空間複雜度

* 時間複雜度：O(n log n + m)
  * 排序需要 O(n log n)，其中 n 是字串數量
  * 比較兩個字串需要 O(m)，其中 m 是最短字串的長度
* 空間複雜度：O(n)
  * 排序可能需要 O(1) 到 O(n) 的額外空間，取決於排序算法
  * 存儲結果字串需要 O(m) 空間
  * 總體空間複雜度：O(1) 到 O(n)
