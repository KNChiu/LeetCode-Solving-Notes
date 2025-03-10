---
description: Tree, Depth-First Search, Breadth-First Search, Binary Tree
---

# 104 - Maximum Depth of Binary Tree - Easy

## 釐清需求與邊界條件

* **輸入**: 二叉樹的根節點 `root`
* **輸出**: 二叉樹的最大深度（整數）
* **邊界條件**:
  * 如果樹為空（`root == None`），應返回 0
  * 如果只有根節點，應返回 1
  * 節點數量可能在 \[0, 10^4] 範圍內

## 口述解法

* **主要函數**: `maxDepth(root)` - 返回樹的最大深度
* **內部函數**: `dfs(root, cnt)` - 遞歸函數計算深度
  * **步驟**:
    1. 如果當前節點為空，返回當前深度計數 `cnt`
    2. 遞歸計算左子樹深度: `left_depth = dfs(root.left, cnt + 1)`
    3. 遞歸計算右子樹深度: `right_depth = dfs(root.right, cnt + 1)`
    4. 返回左右子樹深度的最大值

## 測試與優化

* 程式碼

```python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        def dfs(root, cnt):
            if root is None:
                return cnt

            left_depth = dfs(root.left, cnt + 1)
            right_depth = dfs(root.right, cnt + 1)

            return max(left_depth, right_depth) 

        return dfs(root, 0)
```

* 優化寫法(不需要 dfs())

```python
def maxDepth(self, root: TreeNode) -> int:
    if not root:
        return 0
    return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```

## 時間與空間複雜度

* 時間複雜度：O(n)
  * 需要訪問每個節點一次
* 空間複雜度：
  * O(h)，h是樹的高度
  * 最好情況(平衡樹): O(log n)
  * 最壞情況(鏈表): O(n)&#x20;
