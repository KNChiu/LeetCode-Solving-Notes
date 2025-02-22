---
description: Database
---

# 1757 - Recyclable and Low Fat Products - Easy

## 釐清需求與邊界條件

* 輸入：一個包含產品資訊的 DataFrame
  * 有三個欄位：product\_id、low\_fats、recyclable
* 輸出：符合條件的 product\_id
* 限制條件：
  * low\_fats 為 'Y' 且 recyclable 為 'Y' 的產品
  * DataFrame 可能為空
  * 所有欄位都不會有 null 值 low\_fats 和 recyclable 只會有 'Y' 或 'N' 兩種值

## 口述解法

* 建立兩個條件：low\_fats == 'Y' 和 recyclable == 'Y'
* 使用 & 運算符合併兩個條件
* 返回符合條件的 product\_id 欄位

## 測試與優化

* 程式碼

```python
class Solution:
    def find_products(self, products: pd.DataFrame):
        return products[(products["low_fats"] == "Y") & (products["recyclable"] == "Y")]["product_id"]
        
```

* 測資與注意事項

## 時間與空間複雜度

* 時間複雜度：O(n)
  * n 是 DataFrame 的行數，需要遍歷整個 DataFrame 進行條件判斷
* 空間複雜度：O(k)
  * k 是符合條件的行數，只需要儲存符合條件的 product\_id
