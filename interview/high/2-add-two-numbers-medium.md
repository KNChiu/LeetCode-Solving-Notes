---
description: Recursion, Linked List, Math
---

# 2 - Add Two Numbers - Medium

## 釐清需求與邊界條件

* 輸入：兩個非空的鏈結串列，每個節點代表一個 0-9 的數字
* 輸出：一個新的鏈結串列，表示兩數相加的結果
* 限制條件：
  * 數字是反序儲存，如 342 會表示為 2->4->3
  * 每個串列長度在 1-100 之間
  * 節點值在 0-9 之間
  * 確認不會有前導零
  * 需要處理進位情況

## 口述解法

* 建立一個dummy node作為回傳結果的頭
* 設置一個進位值 carry 和當前節點 curr
* 當 l1、l2 或 carry 任一還有值時：
  * 計算當前位置的和：l1的值(如果存在) + l2的值(如果存在) + 進位值
  * 使用 divmod 取得新的進位值和當前位置的值
  * 建立新節點存放當前位置的值
  * 移動所有指針到下一個位置
* 返回 dummy.next 作為結果

## 測試與優化

* 程式碼

```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        carry, curr = 0, dummy
        while l1 or l2 or carry:
            s = (l1.val if l1 else 0) + (l2.val if l2 else 0) + carry
            carry, val = divmod(s, 10)
            curr.next = ListNode(val)
            curr = curr.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None

        return dummy.next
```

## 時間與空間複雜度

* 時間複雜度：O(max(N, M))
  * 其中 N 和 M 是兩個鏈結串列的長度。需要遍歷兩個串列的所有節點。
* 空間複雜度：O(max(N, M))
  * 需要建立一個新的鏈結串列來存放結果。不考慮輸出所需的空間的話，則是 O(1)。
