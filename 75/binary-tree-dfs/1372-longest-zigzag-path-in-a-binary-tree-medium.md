---
description: Tree, Depth-First Search, Dynamic Programming, Binary Tree
---

# 1372 - Longest ZigZag Path in a Binary Tree - Medium

## 釐清需求與邊界條件

* 輸入：一個二元樹的根節點，需要找出最長的之字形路徑長度
* 之字形路徑定義:&#x20;
  * 從任意節點開始
  * 每次移動時需要交替左右方向
  * 直到無法繼續移動為止
  * 路徑長度 = 訪問節點數 - 1
* 限制條件：
  * 節點數範圍: 1 \~ 5\*10^4&#x20;
  * 節點值範圍: 1 \~ 100

## 口述解法

* 主要函數 longestZigZag():&#x20;
  * 使用全域變數 ans 來記錄最長路徑長度
  * 呼叫 dfs() 來遍歷整棵樹
* 內部函數 dfs(root, l, r):
* 遞迴終止條件:當節點為空時返回
* 參數說明:
  * root: 當前節點&#x20;
  * l: 往左走的累積長度&#x20;
  * r: 往右走的累積長度
* 執行步驟:
  * 更新全域 ans 為當前最大值 max(ans, l, r)&#x20;
  * 往左子樹遞迴:&#x20;
    * dfs(root.left, r + 1, 0)&#x20;
      * r + 1 表示接續上一個右轉的長度
      * 0 表示重新開始計算右轉長度
    * 往右子樹遞迴:&#x20;
      * dfs(root.right, 0, l + 1)&#x20;
        * 同理,但方向相反

## 測試與優化

* 程式碼

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def longestZigZag(self, root: TreeNode) -> int:
        def dfs(root, l, r):
            if root is None:
                return
            nonlocal ans
            ans = max(ans, l, r)
            dfs(root.left, r + 1, 0)
            dfs(root.right, 0, l + 1)

        ans = 0
        dfs(root, 0, 0)
        return ans
```

* 測資與注意事項
  * 空樹
  * 只有根節點

## 時間與空間複雜度

* 時間複雜度：O(N)
  * N為節點總數 需要遍歷每個節點一次
* 空間複雜度：O(H)
  * H為樹高
  * 最壞情況下為 O(N)
  * 當樹退化為鏈表時 平均情況為 O(logN), 當樹為平衡二元樹時
