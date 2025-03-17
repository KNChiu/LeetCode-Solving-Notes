# Arrays & Hashing

### Sort

```
sort()
時間複雜度: O(n log n)
```

#### 由小到大(大到小)依據數值排序:

```python
nums = [5, 6, 1, 2, 3, 4]
nums.sort()                # [1, 2, 3, 4, 5, 6]
nums.sort(reverse = True)  # [6, 5, 4, 3, 2, 1]  
```

#### 由自訂方式排序:

```python
nums = [5, 6, 1, 2, 3, 4]
# 取偶數(小到大排序)
nums.sort(key=lambda x: (x % 2, x))
# [2, 4, 6, 1, 3, 5]

# 取平方合(小到大排序)
nums = [[5, 6], [1, 2], [3, 4]]
nums.sort(key=lambda x: x[0] ** 2 + x[1] ** 2)
# [[1, 2], [3, 4], [5, 6]]
```

***

### Hash Table

自訂格式 Dict: defaultdict()

```python
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
ans = defaultdict(list)
for s in strs:
    k = ''.join(sorted(s))
    ans[k].append(s)
# defaultdict(<class 'list'>, {'aet': ['eat', 'tea', 'ate'], 'ant': ['tan', 'nat'], 'abt': ['bat']})
```

計數器: Counter()

```
Counter()
時間複雜度: O(n)

most_common()
時間複雜度: O(n log n)
```

```python
nums = [1,1,1,2,2,3]

cnt = Counter(nums)
print(cnt.most_common())  # 計數數量大到小排序
```
