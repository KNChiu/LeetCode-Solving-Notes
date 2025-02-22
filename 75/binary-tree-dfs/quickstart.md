---
description: Tree, Depth-First Search, Binary Tree
---

# 872 - Leaf-Similar Trees - Easy

## 釐清需求與邊界條件

* 輸入：兩個二元樹的根節點 root1 和 root2
* 輸出：布林值，表示兩棵樹的葉子序列是否相同
* 限制條件：
  * 節點數量在 1-200 之間
  * 節點值在 0-200 之間
  * 葉子節點定義：沒有左右子節點的節點
* 需要注意的邊界情況：&#x20;
  * 只有一個節點的樹
  * 不平衡的樹
  * 空樹（題目說明至少有一個節點，所以不用考慮）

## 口述解法

* 使用深度優先搜索(DFS)來收集每棵樹的葉子節點值
* 對每棵樹：&#x20;
  * 如果當前節點是葉子節點(左右子節點都是None)，將值加入結果列表
  * 如果有左子節點，遞迴處理左子樹
  * 如果有右子節點，遞迴處理右子樹
  * 比較兩個葉子序列是否相同

## 測試與優化

* 程式碼

```python
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def leafSimilar(self, root1, root2) -> bool:
        def dfs(root, nums) -> None:
            if root.left == root.right:
                nums.append(root.val)
                return
            if root.left:
                dfs(root.left, nums)
            if root.right:
                dfs(root.right, nums)

        l1, l2 = [], []
        dfs(root1, l1)
        dfs(root2, l2)
        return l1 == l2
```

* 測資與注意事項

```python
#Case 1: 單節點
root1 = TreeNode(1)
root2 = TreeNode(1)
#預期結果：True

#Case 2: 相同結構但不同葉子值
root1 = TreeNode(1, TreeNode(2), TreeNode(3))
root2 = TreeNode(1, TreeNode(2), TreeNode(4))
#預期結果：False
```

## 時間與空間複雜度

* 時間複雜度：
  * O(N)，其中 N 是較大的樹的節點數量
  * 需要遍歷每棵樹的所有節點一次
* 空間複雜度：
  * O(H + L)，其中： H 是較深的樹的高度（遞迴調用棧的空間）&#x20;
  * L 是葉子節點的數量（存儲葉子值序列的空間）&#x20;
  * 最壞情況下 H 可能達到 N（不平衡樹）
