---
description: Array, String, Backtracking, Depth-First Search, Matrix
---

# 79: Word Search - Medium

## 釐清需求與邊界條件

* 輸入：
  * 一個 m x n 的字元矩陣 `board`
  * 一個字串 `word`
* 輸出：如果 `word` 存在於矩陣中則返回 `True`，否則返回 `False`
* 邊界條件：
  * `board`大小: 1 ≤ m, n ≤ 6
  * `word`長度: 1 ≤ word.length ≤ 15
  * 字元只包含大小寫英文字母
  * 相同的格子不能使用多次
  * 必須是水平或垂直相鄰的格子（不包括對角線）

## 口述解法

*   使用深度優先搜索（DFS）從矩陣中的每個格子開始尋找可能的匹配路徑。

    #### 主要函數 `exist`:

    1. 獲取矩陣的尺寸 m 和 n
    2. 對矩陣中的每個格子 (i, j) 嘗試以它為起點進行深度優先搜索
    3. 如果任何一個起點能找到匹配的單詞，則返回 True，否則返回 False

    #### 內部函數 `dfs(i, j, k)`:

    1. 檢查當前格子 (i, j) 的字元是否匹配單詞的第 k 個字元，不匹配則返回 False
    2. 如果 k 是單詞的最後一個索引（即已經匹配完整個單詞），則返回 True
    3. 暫時標記當前格子為已訪問（把字元改為空字符串）
    4. 遞歸檢查四個方向的相鄰格子（上、下、左、右）
    5. 如果任何一個方向能夠匹配剩餘的單詞，則返回 True
    6. 恢復當前格子的原始字元（回溯）
    7. 如果沒有找到匹配，則返回 False

## 測試與優化

* 程式碼

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m, n = len(board), len(board[0])

        def dfs(i: int, j: int, k: int) -> bool:
            if board[i][j] != word[k]:
                return False

            if k == len(word) - 1:
                return True

            board[i][j] = ''

            for x, y in (i, j - 1), (i, j + 1), (i - 1, j), (i + 1, j): 
                if 0 <= x < m and 0 <= y < n and dfs(x, y, k + 1):
                    return True

            board[i][j] = word[k]
            return False

        return any(dfs(i, j, 0) for i in range(m) for j in range(n))

```

* 優化建議:
  * **提前檢查字符頻率**：在開始 DFS 前，可以比較 `board` 中的字符頻率與 `word` 中的字符頻率，如果 `word` 中有字符在 `board` 中不存在或數量不足，可以直接返回 False。
  * **優先從稀有字符開始搜索**：可以找出 `word` 中最稀有的字符（在 `board` 中出現次數最少），優先從這些位置開始 DFS，減少搜索數量。

## 時間與空間複雜度

* 時間複雜度：O(m \* n \* 4^L)
  * 其中 m 和 n 是矩陣的尺寸，L 是單詞的長度
  * 對於每個起始位置 (i, j)，最多有 4^L 種可能的路徑（每一步都有最多 4 個方向可選）
  * 由於我們最多只訪問每個格子一次，實際複雜度可能低於這個上限
* 空間複雜度：O(L)
  * L 是單詞的長度，這是遞歸最大深度
