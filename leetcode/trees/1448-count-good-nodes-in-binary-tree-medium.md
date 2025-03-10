---
description: Tree, Depth-First Search, Breadth-First Search, Binary Tree
---

# 1448 - Count Good Nodes in Binary Tree - Medium

## 釐清需求與邊界條件

* 輸入：一個二元樹的根節點
* 輸出：好節點的總數
* 限制條件：
  * 好節點的定義：從根到該節點的路徑上，沒有任何節點的值比該節點大
  * 節點數範圍：1 到 10^5 個
  * 節點值範圍：-10^4 到 10^4

## 口述解法

* 在遍歷過程中使用變數mx，記錄從根到當前節點路徑上的最大值
* 當遇到新節點時：&#x20;
  * 比較當前節點值與路徑最大值(mx)
  * 如果當前節點值大於等於路徑最大值，這是個好節點(好節點數量+1)
  * 更新路徑最大值，繼續遍歷左右子樹

## 測試與優化

* 程式碼

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        def dfs(root: TreeNode, mx: int):
            if root is None:
                return
            
            nonlocal ans
            if mx <= root.val:
                ans += 1
                mx = root.val

            dfs(root.left, mx)
            dfs(root.right, mx)

        ans = 0
        dfs(root, -1000000)
        return ans
```

* 測資與注意事項
  * nonlocal關鍵字避免重複傳遞計數器
  * 遞迴時只傳遞必要的參數

## 時間與空間複雜度

* 時間複雜度：O(n)
  * 其中n是節點數 每個節點都需要被訪問一次
* 空間複雜度：O(h)
  * h是樹的高度
  * 遞迴調用棧的深度等於樹的高度
  * 最壞情況下（樹退化為鏈表）為O(n)&#x20;
  * 平均情況下（平衡樹）為O(log n)
