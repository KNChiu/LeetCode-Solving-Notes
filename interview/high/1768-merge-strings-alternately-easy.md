---
description: Two Pointers, String
---

# 1768 - Merge Strings Alternately - Easy

## 釐清需求與邊界條件

* 輸入：兩個字串 word1 和 word2
* 輸出：合併後的字串，以交替方式合併
* 限制條件：
  * 兩個字串長度可能不同
  * 字串可能為空
  * 需要處理剩餘字串

## 口述解法

* 復述問題並說明想法
  * 本來需要建立兩個指標遍歷兩個輸入
  * 依序將 word1 和 word2 的字元交替加入結果字串

## 測試與優化

* 程式碼

```python
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        return "".join(a + b for a, b in zip_longest(word1, word2, fillvalue=''))

```

* 測資與注意事項
  * 使用 Python 的字串串接方法 join() 來提高效能
  * 使用 zip\_longest 來處理不等長的情況

## 時間與空間複雜度

* 時間複雜度：O(n + m)
  * 其中 n 和 m 是兩個字串的長度
* 空間複雜度：O(n + m)
  * 需要創建一個新字串來存儲結果 結果字串的長度等於兩個輸入字串的長度之和
