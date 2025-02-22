---
description: Tree, Depth-First Search, Breadth-First Search, Binary Tree
---

# 104 - Maximum Depth of Binary Tree - Easy

## 釐清需求與邊界條件

* 輸入：
  * 一個二元樹的根節點
  * 需要計算從根節點到最遠葉節點的最大深度&#x20;
* 輸出：最大深度
* 限制條件：
  * 節點數範圍是 \[0, 10^4]&#x20;
  * 節點值範圍是 \[-100, 100]
  * 特殊情況: 空樹(root = None)返回0 只有根節點返回1 非平衡樹時也要考慮

## 口述解法

* 基本情況:
  * 如果節點為空,返回0
* 遞迴計算:&#x20;
  * 遞迴獲取左子樹的最大深度
  * 遞迴獲取右子樹的最大深度
  * 當前深度 = max(左子樹深度,右子樹深度) + 1 返回計算結果

## 測試與優化

* 程式碼

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if root is None:
            return 0
        l, r = self.maxDepth(root.left), self.maxDepth(root.right)
        return 1 + max(l, r)
```

## 時間與空間複雜度

* 時間複雜度：
  * O(n) 需要訪問每個節點一次
* 空間複雜度：
  * O(h)，h是樹的高度
  * 最好情況(平衡樹): O(log n)
  * 最壞情況(鏈表): O(n)&#x20;
  * 遞迴調用會使用調用堆疊空間
