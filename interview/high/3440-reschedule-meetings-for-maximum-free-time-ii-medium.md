---
description: Greedy, Array, Enumeration
---

# 3440 - Reschedule Meetings for Maximum Free Time II - Medium

## 釐清需求與邊界條件

* 輸入：
  * eventTime: 整個事件的總時長
  * startTime\[]: 會議開始時間陣列
  * endTime\[]: 會議結束時間陣列
  * 長度均為 n 的陣列
* 輸出：最大連續空閒時間長度
*   限制條件：

    * 可以移動一個會議的時間(保持相同時長)
    * 會議不能重疊
    * 會議不能超出 eventTime
    * 會議可以改變相對順序



    * n ≥ 1
    * 所有時間都是非負整數
    * startTime\[i] < endTime\[i]
    * 原始會議時間不重疊

## 口述解法

* 維護最大的三個空位，一定有一個空位不在會議左右兩側，把會議移到這個空位。&#x20;
* 設最大的三個空位所在的位置（下標）分別是a,b,c。
* 枚舉要重新安排（移除）的會議
  * 分類討論：
    * 如果會議左右兩側的空位沒有a，那麼把會議移到a。&#x20;
    * 否則如果會議左右兩側的空位沒有b，那就把會議移到b。&#x20;
    * 否則把會議移到c。



* 主要函數 maxFreeTime:

1. 計算相鄰會議間的空閒時間 (使用 get 函數)
2. 找出三個最大的空閒時段 (a, b, c)
3. 嘗試移動每個會議，計算可能的最大空閒時間

## 測試與優化

* 程式碼

```python
class Solution:
    def maxFreeTime(self, eventTime: int, startTime: List[int], endTime: List[int]) -> int:
        n = len(startTime)

        def get(i):
            if i == 0:
                return startTime[0]
            elif i == n:
                return eventTime - endTime[-1]
            else:
                return startTime[i] - endTime[i-1]
                
        a, b, c = 0, -1, -1
        for i in range(1, n + 1):
            sz = get(i)
            if sz > get(a):
                a, b, c = i, a, b
            elif b < 0 or sz > get(b):
                b, c = i, b
            elif c < 0 or sz > get(c):
                c = i

        ans = 0
        for i, (s, e) in enumerate(zip(startTime, endTime)):
            sz = e - s
            if i != a and i + 1 != a and sz <= get(a) or \
               i != b and i + 1 != b and sz <= get(b) or \
               sz <= get(c):
                ans = max(ans, get(i) + sz + get(i + 1))
            else:
                ans = max(ans, get(i) + get(i + 1))
        return ans


```

## 時間與空間複雜度

* 時間複雜度：O(n)
  * 遍歷所有會議時間: O(n)
  * get 函數: O(1)
* 空間複雜度：O(1)
  * 只使用固定變數 (a, b, c)
