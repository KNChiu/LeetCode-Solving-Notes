# 2667 - Create Hello World Function - Easy

## 釐清需求與邊界條件

* 輸入：任何參數
* 輸出：返回另一個函數，返回的函數不管接收什麼參數，都返回 "Hello World" 字串
* 限制條件：
  * 無參數
  * 一個或多個參數
  * 不同類型的參數 (數字、字串、物件、None等)

## 口述解法

* 使用 \*\*kwargs 來接收關鍵字參數
* 可以使用 lambda 表達式來簡化代碼:

## 測試與優化

* 程式碼

```python
def createHelloWorld():
    def helloWorld(*args, **kwargs):
        return "Hello World"
    return helloWorld
```

```python
def createHelloWorld():
    return lambda *args, **kwargs: "Hello World"
```

## 時間與空間複雜度

* 時間複雜度：O(1)&#x20;
  * 不管輸入什麼參數，都是常數時間返回字串
* 空間複雜度：O(1)
  * 只儲存固定的字串 "Hello World" 不管輸入參數的大小，所需空間都是常數
