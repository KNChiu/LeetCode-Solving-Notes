---
description: Tree, Depth-First Search, Binary Tree
---

# 437 - Path Sum III - Medium

## 釐清需求與邊界條件

* 目標:&#x20;
  * 找出二元樹中所有路徑和等於 targetSum 的路徑數量
  * 路徑可以從任意節點開始到任意節點結束，但必須是向下的
* 限制條件：
  * 節點數範圍: 0-1000
  * 節點值範圍: -10^9 到 10^9
  * targetSum 範圍: -1000 到 1000
* 注意事項:
  * 需考慮空樹的情況
  * 路徑不一定要從根節點開始或在葉節點結束

## 口述解法

* 使用前綴和(prefix sum)搭配深度優先搜索(DFS)
* 主要函數:
  * 使用前綴和(prefix sum)的概念來解決問題
  * 建立一個Counter來記錄累積和出現的次數，初始化{0:1}表示空路徑
* 內部函數:
  * 如果當前節點為空，返回0
  * 計算當前路徑累積和 s
  * 檢查是否存在 (當前累積和 s - targetSum) 的前綴和，存在代表找到符合的路徑
  * 將當前累積和加入Counter
  * 遞迴處理左右子樹
  * 回溯時移除當前累積和的計數
  * 返回所有找到的路徑數量

## 測試與優化

* 程式碼

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        def dfs(node, s):
            if node is None:
                return 0
            s += node.val
            ans = cnt[s - targetSum]
            cnt[s] += 1
            ans += dfs(node.left, s)
            ans += dfs(node.right, s)
            cnt[s] -= 1
            return ans

        cnt = Counter({0: 1})
        return dfs(root, 0)
```

* 測資與注意事項
  * Counter 用於記錄到此為止累積總和出現的次數。
  * 能在常數時間內查詢有多少先前的路徑總和滿足 s - targetSum，從而快速計算符合條件的路徑數量。

## 時間與空間複雜度

* 時間複雜度：O(N) ，其中N是樹的節點數，每個節點只被訪問一次
* 空間複雜度：O(H)，其中H是樹的高度
  * 在最壞情況下（例如樹為鏈狀），遞迴的深度為 H，因此需要 O(H) 的棧空間。&#x20;
  * Counter 空間：在最壞情況下，每個節點的累積總和都是獨一無二的，因此需要 O(H) 的空間來存儲累積總和。
