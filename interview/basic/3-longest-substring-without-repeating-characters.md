---
description: Hash Table, String, Sliding Window
---

# 3: Longest Substring Without Repeating Characters

## 釐清需求與邊界條件

* 輸入：一個字串 s,包含英文字母、數字、符號和空格
* 輸出：
  * 找出最長的子字串(連續字元序列),且該子字串中不能有重複字元
  * 輸出是該子字串的長度
* 限制條件：
  * 空字串的情況 → 返回 0
  * 字串長度限制: 0 ≤ s.length ≤ 5 \* 10^4
  * 單一字元重複的情況 → 返回 1

## 口述解法

*   使用滑動窗口(Sliding Window)配合計數器的解法:

    主要函數 `lengthOfLongestSubstring`:

    1. 初始化:
       * ans: 記錄最長無重複子字串的長度
       * cnt: 使用 Counter 記錄窗口內每個字元出現的次數
       * left: 窗口左邊界
    2. 執行步驟:
       * 遍歷字串,right 為窗口右邊界
       * 將當前字元加入計數器
       * 當發現重複字元時(cnt\[x] > 1):
         * 移動左邊界直到重複消除
         * 每移動一次左邊界,對應減少該字元的計數
       * 更新最大長度 ans

## 測試與優化

* 程式碼

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ans = 0
        cnt = Counter()
        left = 0

        for right, x in enumerate(s):
            cnt[x] += 1

            while cnt[x] > 1:
                cnt[s[left]] -= 1
                left += 1

            ans = max(ans, right - left + 1)
        return ans
```

* 測資與注意事項
  * 可以使用 dictionary 代替 Counter,因為我們只需要記錄字元是否出現
  * 可以用 set 來檢查重複,但需要權衡時間複雜度

## 時間與空間複雜度

* 時間複雜度：O(n)
  * 雖然有雙層迴圈,但左指針 left 最多移動 n 次
  * 每個字元最多被訪問兩次(右指針和左指針各一次)
* 空間複雜度：O(k)
  * k 是字符集大小(題目中包含字母、數字、符號等)
  * Counter/字典最多存儲 k 個不同字符
  * 在實際應用中,k 可以視為常數(ASCII 為 256 或 Unicode)
