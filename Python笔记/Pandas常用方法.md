# Pandas

## Pandas.concat()

`concat` 是 Pandas 中的一个函数，全称为 **pandas.concat**。它用于将多个 Pandas 对象（如 Series 或 DataFrame）沿着指定的轴（行或列）拼接在一起。

### 作用

`pandas.concat` 的主要作用是**将多个 Pandas 对象合并成一个单一的对象**。它类似于 SQL 中的 `UNION` 或 `JOIN` 操作，但更加灵活，支持多种拼接方式。

### 主要参数

`pandas.concat` 函数的语法如下：

Python

复制

```
pandas.concat(objs, axis=0, join='outer', ignore_index=False, keys=None, levels=None, names=None, verify_integrity=False, sort=False, copy=True)
```

#### 参数说明

1. **objs**：
   - **类型**：列表或字典，包含要拼接的 Pandas 对象（Series 或 DataFrame）。
   - **说明**：这是必须提供的参数，指定要拼接的对象。
2. **axis**：
   - **类型**：整数或字符串，默认为 `0`。
   - **说明**：
     - `axis=0` 或 `axis='index'`：沿着行方向拼接（默认值）。(必须保证列属性相同)
     - `axis=1` 或 `axis='columns'`：沿着列方向拼接。
3. **join**：
   - **类型**：字符串，默认为 `'outer'`。
   - **说明**：
     - `'outer'`：取并集，保留所有索引或列。
     - `'inner'`：取交集，只保留共同的索引或列。
4. **ignore_index**：
   - **类型**：布尔值，默认为 `False`。
   - **说明**：
     - 如果为 `True`，则忽略原始索引，重新生成连续的整数索引。
     - 如果为 `False`，则保留原始索引。
5. **keys**：
   - **类型**：列表或元组，默认为 `None`。
   - **说明**：
     - 如果提供，会为每个拼接的对象添加一个额外的索引层级（MultiIndex）。
     - 通常用于标识每个对象的来源。
6. **levels**：
   - **类型**：列表或元组，默认为 `None`。
   - **说明**：
     - 用于指定 MultiIndex 的层级值。
     - 通常与 `keys` 参数一起使用。
7. **names**：
   - **类型**：列表或元组，默认为 `None`。
   - **说明**：
     - 用于指定 MultiIndex 的层级名称。
     - 通常与 `keys` 参数一起使用。
8. **verify_integrity**：
   - **类型**：布尔值，默认为 `False`。
   - **说明**：
     - 如果为 `True`，则在拼接后检查索引是否唯一。
     - 如果索引重复，会抛出 `ValueError`。
9. **sort**：
   - **类型**：布尔值，默认为 `False`。
   - **说明**：
     - 如果为 `True`，则在拼接后按列名排序。
     - 仅在 `axis=1` 时有效。
10. **copy**：
    - **类型**：布尔值，默认为 `True`。
    - **说明**：
      - 如果为 `True`，则返回一个新的对象。
      - 如果为 `False`，则返回一个视图（不推荐，可能会导致意外行为）。



## DataFrame筛选

在 Pandas 中，当你使用布尔索引对 DataFrame 进行筛选时，只需要传入一个布尔值的 Pandas Series（或布尔数组），而不需要关心这个 Series 的列属性名称。布尔索引的关键在于布尔值序列的长度必须与 DataFrame 的行数一致。

### 布尔索引的工作原理
布尔索引的核心是通过布尔值序列（`True` 或 `False`）或者布尔取值的pandas.series数据类型来决定哪些行应该被保留。具体来说：
- **`True`**：表示该行满足条件，应该被保留。
- **`False`**：表示该行不满足条件，应该被丢弃。

布尔值序列的长度必须与 DataFrame 的行数一致，这样 Pandas 才能逐行匹配布尔值，决定是否保留该行。

### 示例
假设我们有以下 DataFrame `df1`：

```python
import pandas as pd

df1 = pd.DataFrame({
    'id': [1, 8, 15, 24, 32, 40, 48, 56],
    'value': ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
})
```

我们定义一个筛选函数：

```python
def filter_rows(id_series):
    return id_series % 8 == 0
```

然后执行以下代码：

```python
filtered_df = df1[filter_rows(df1['id'])]
```

#### 逐步解析
1. **提取 `'id'` 列**：
   ```python
   id_series = df1['id']
   print(id_series)
   ```
   输出：
   ```
   0     1
   1     8
   2    15
   3    24
   4    32
   5    40
   6    48
   7    56
   Name: id, dtype: int64
   ```

2. **调用筛选函数**：
   ```python
   mask = filter_rows(df1['id'])
   print(mask)
   ```
   输出：
   ```
   0    False
   1     True
   2    False
   3     True
   4     True
   5     True
   6     True
   7     True
   Name: id, dtype: bool
   ```

3. **使用布尔索引**：
   ```python
   filtered_df = df1[mask]
   print(filtered_df)
   ```
   输出：
   ```
   id value
   1   8     B
   3  24     D
   4  32     E
   5  40     F
   6  48     G
   7  56     H
   ```

### 关键点
- **布尔值序列的长度**：布尔值序列的长度必须与 DataFrame 的行数一致。Pandas 会逐行匹配布尔值，决定是否保留该行。
- **布尔值序列的来源**：布尔值序列可以来自任何地方，只要它是一个布尔值的 Pandas Series 或布尔数组即可。它不需要与 DataFrame 的列名有任何关联。

### 示例 2：直接传入布尔数组
你也可以直接传入一个布尔数组，而不需要通过函数生成布尔值序列：

```python
# 直接创建一个布尔数组
mask = [False, True, False, True, True, True, True, True]

# 使用布尔数组进行筛选
filtered_df = df1[mask]
print(filtered_df)
```

输出：
```
   id value
1   8     B
3  24     D
4  32     E
5  40     F
6  48     G
7  56     H
```

### 示例 3：使用其他列生成布尔值序列
布尔值序列可以来自 DataFrame 的任何列，甚至可以是多个列的组合条件：

```python
# 使用其他列生成布尔值序列
mask = df1['id'] % 8 == 0
filtered_df = df1[mask]
print(filtered_df)
```

输出：
```
   id value
1   8     B
3  24     D
4  32     E
5  40     F
6  48     G
7  56     H
```

### 总结
布尔索引的核心是布尔值序列，而不是序列的列名。只要布尔值序列的长度与 DataFrame 的行数一致，Pandas 就可以正确地进行筛选。你可以通过函数生成布尔值序列，也可以直接传入布尔数组，甚至可以结合多个列的条件生成布尔值序列。