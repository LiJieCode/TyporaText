# Notes







## Numpy

- 拼接和分割

```python 
# vstack
# hstack
# concatenate

# split
# vsplit
# hsplit
```





## Pandas

### 常用API

- 创建

```python
# 列表创建
# 字典创建
# Series创建

# date 是定义好的数据
df = pd.DataFrame(data, index = ['A','B','C','D'], columns = ['a','b','c','d'])
```

- 增删改查数据

```python
# 增加一列 / ...为增加或插入的内容
df['a'] = ...
# 增加一行
df.loc['a'] = ...    # loc 标签索引
df.append()

# 指定位置插入一行
# DataFrame 没有这种功能的函数，下面有自定义的
# 指定位置插入一列
df.insert(2, 'a', ...)

# 删除一列
del(df['a'])  /  del df['a']
# 删除一行
df.drop('a')  # 删除后产生一个新DataFrame，原数据不变
df.drop('a', inplace = True)  # 直接修改原数据，不会产生新的
# 下面三个方式一样    -- 删除列
pd1.drop(columns = 'A') 
pd1.drop('A',axis = 1)
pd1.drop('A',axis = 'columns')


# 改
# 修改某一个数
df.loc['index', 'columns'] = ...


# 查
df['a'] / df.a
df.loc['a']
df.loc['index', 'columns'] 
df['b']['a1']  # 先输入列，再输入行
df[['a', 'b']]
```

> DataFrame数据，任意行位置增加一行数据，自定义函数
>
> ```python 
> def insert_row(row_number, df, row_value):
>     # Starting value of upper half
>     start_upper = 0
>   
>     # End value of upper half
>     end_upper = row_number
>   
>     # Start value of lower half
>     start_lower = row_number
>   
>     # End value of lower half
>     end_lower = df.shape[0]
>   
>     # Create a list of upper_half index
>     upper_half = [*range(start_upper, end_upper, 1)]
>   
>     # Create a list of lower_half index
>     lower_half = [*range(start_lower, end_lower, 1)]
>   
>     # Increment the value of lower half by 1
>     lower_half = [x.__add__(1) for x in lower_half]
>   
>     # Combine the two lists
>     index_ = upper_half + lower_half
>   
>     # Update the index of the dataframe
>     df.index = index_
>   
>     # Insert a row at the end
>     df.loc[row_number] = row_value
>    
>     # Sort the index labels
>     df = df.sort_index()
>   
>     # return the dataframe
>     return df
> ```
>
> 

- 高级索引 

```python
# 1、loc 标签索引  只能用标签检索
df.loc['a']
# 2、iloc 位置索引  只能用位置检索
df.iloc[0:2]
# 3、ix 标签与位置混合索引 
df.ix[0:2,'A':'B']
```

- 索引

```python
### 3、常见的index数据类型
# index , 索引
# int64index , 整数索引
# MultiIndex , 层级索引
# DatetimeIndex , 时间戳索引
df.index  # 行索引
df.columns  # 列索引
```

- 函数应用

```python 
# apply  通过apply将函数应用到行或者列
# applymap  通过applymap将函数应用到每个数据上


# 排序
# sort_index
df.sort_index(ascending = False, axis = 1)  # 默认升序(ascending=True)，axis = 0
df.sort_index(axis=1)
df.sort_index(ascending = False)
# sort_values
df.sort_values(by = 'a')  # 按指定列排序，默认axis = 0
df.sort_values(by = 2, axis=1)  # 按指定行排序，指明axis = 1


# 唯一值和成员属性
# unique()
df['a'].unique()
df['a'].value_counts()
df['a'].is_unique
# 'DataFrame' object has no attribute 'unique'
# isin() 判断是否在。。。
df.isin([1])


## 处理缺失数据
# df.isnull()  # 判断是否存在缺失值
# df.dropna()  # 默认丢弃出现nan的行
# df.dropna(axis = 1)  # 丢弃所在列
# df.fillna(-1)  # 空缺值填充-1
```

- 层级索引

```python 
# Series 
ps = pd.Series(np.random.randn(12),index = [['a','a','a','b','b','b','c','c','c','d','d','d'],
                                              [0,1,2,0,1,2,0,1,2,0,1,2]])

ps.swaplevel()

# DataFrame 层级索引
# 用到再学吧
```

> 

- 统计方法

```python
# 1、count 非nan值的数量
# 2、describe 针对Series或者各DataFrame列计算汇总统计
# 3、min、max 计算最小值最大值
# 4、argmin、argmax 得到最大（小）值的索引位置（整数）
# 5、inxmin、idxmax 得到最大（小）值的索引
# 6、quantile 计算样本的分位数（0或1）
# 7、sum 和
# 8、mean 平均值
# 9、median 中位数
# 10、mad 根据平均值计算平均绝对离差
# 11、var 方差
# 12、std 标准差
# 13、skew 样本值的偏度（三阶矩）
# 14、kurt 样本值的峰读（四阶矩）
# 15、cumsum 样本值的累计和
# 16、diff 计算一阶差分
# 17、pct_change 计算百分数变化
```

- 关联两个 DataFrame

```python
# pd.merge(left, right, how='inner'[, on=None][, left_on=None, right_on=None][, suffixes=('_left', '_right')])
# left: 合并时左边的DataFrame
# right: 合并时右边的DataFrame
# how: 合并的方式, 默认'inner', 另外还有'outer', 'left', 'right'
# on: 需要合并的列名, 必须两边都有的列名，并以 left 和 right 中的列名的交集作为连接键
# left_on: left Dataframe中用作连接键的列
# right_on: right Dataframe中用作连接键的列
# suffixes=('_left', '_right'): 当左右表有重复列时，命名方式，默认是'_x', '-y'

left = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                     'A': ['A0', 'A1', 'A2', 'A3'],
                     'B': ['B0', 'B1', 'B2', 'B3']})

right = pd.DataFrame({'key': ['K0', 'K1', 'K2', 'K3'],
                      'C': ['C0', 'C1', 'C2', 'C3'],
                      'D': ['D0', 'D1', 'D2', 'D3']})

# pd.merge(left, right, how='inner'[, left_index = True,right_index = True])  # 用索引关联
# merge用索引关联，可以简化为join
# left2.join(right2, how = 'inner')  # 用索引关联


# concat
pd.concat([df1, df2]) # 默认外连接(join = 'inner')，垂直连接(axis = 0)
pd.concat([df1,df2],axis = 1,join = 'inner') # 内连接，水平连接
```

- 重塑和轴向旋转

```python 
# 见 11pandas数据规整
```

- 分组聚合

```python 
df = pd.DataFrame({'fruit':['apple','banana','orange','apple','banana','banana'],
                    'color':['red','yellow','yellow','cyan','cyan','cyan'],
                    'price':[8.5,6.8,5.6,7.8,6.4,8.8],
                    'number': [1,2,3,4,5,6]})
# seq1:
# seq2:
# seq3:
# seq4:


# as_index = False DataFrame显示，默认是True
# 多个字段分组
df.groupby(by = ['color', 'fruit'], as_index = False)


# 多个字段聚合
df.groupby(by = ['color'], as_index = False).agg({'price': 'max', 'number': 'count'})
# 一个字段多个聚合逻辑
df.groupby(by = ['color'], as_index = False).agg({'price': ['max', 'min'], 'number': 'count'})

```

- 其他

```python
# rename   # 修改行或者列的别名  直接在原数据上修改
df.rename(index = {'a1': 1, 'b1': 2, 'c1': 3, 'd1': 4})
df.rename(columns={'a':'aa','b':'bb'})

# reindex  # 修改行或者列的顺序  直接在原数据上修改
df.reindex(index = ['c1', 'b1', 'a1'])
df.reindex(columns = ['a', 'b'])

df.size  # 返回有多少数据
df.ndim  # 返回数据的维度，几维数据，比如 2x4 的二维表格，返回 2
df.shape # 返回每一维的大小
df.index.name = '...'
df.head(n)
df.tail(n)
```

