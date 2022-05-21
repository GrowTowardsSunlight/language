* [Series对象的索引](#Series对象的索引)
* [DataFrame的索引](#DataFrame的索引)
* [DataFrame的切片](#DataFrame的切片)
* [布尔索引](#布尔索引)
* [多级索引](#多级索引)

```python
population_dict = {'BeiJing':2154,
                    'ShangHai':2424,
                    'ShenZhen':1303,
                    'HangZhou':981}

population = pd.Series(population_dict)

GDP_dict = {'BeiJing':30320,
            'ShangHai':32680,
            'ShenZhen':24222,
            'HangZhou':13468}

GDP = pd.Series(GDP_dict)

data = pd.DataFrame({'population':population,'GDP':GDP})
```

## Series对象的索引


data['标签']

```python
type(data.GDP)    #DataFrame的一列是Series对象
'''
pandas.core.series.Series'''

GDP['BeiJing']
```

## DataFrame的索引

* [获取列](#获取列)
* [获取行](#获取行)
* [获取标量](#获取标量)

### 获取列

仍然有行标签。若只取一列则为Series对象。

- 获取一列：data['列名']或者data.列名

- 获取多列：data.[['列名1','列名2',...'列名k']]


```python
data['population']
data.population
'''
BejJing     2154
ShangHai    2424
ShenZhen    1303
HangZhou     981
Name: population, dtype: int64
'''
data[['GDP','pop']]
```
### 获取行

- 绝对索引获取一行：df.loc['行名']

- 绝对索引获取多行：df.loc[['行名1','行名2',...'行名k']]

- 相对索引取一行：df.iloc[i]  #取下标为i的行
```python
data.loc['BeiJing']
data.loc[['BeiJing','ShangHai']]

data.iloc[0]        #取下标为0的行
data.iloc[[0,3]]    #取下标为0和3的行
```

### 获取标量

- 绝对索引获取标量：

```python
data.loc['行名']['列名']或data.loc['行名','列名'] #返回的是Series

或者data.loc[['行名'],['列名']]  #返回的是DataFrame
```

- 相对索引获取标量：data.loc\[i][j]或data.loc[[i,j]]

- 转成numpy数组再取值：data.values[i][j]
```python
data.loc['BeiJing','GDP']或data.loc['BeiJing']['GDP'] 
data.iloc[0,1]
data.values[0][1]
```

## DataFrame的切片

* [行切片](#行切片)
* [列切片](#列切片)
* [行列同时切片](#行列同时切片)
* [行切片_列分散取值](#行切片_列分散取值)
* [行分散取值_列切片](#行分散取值_列切片)
* [行列都分散取值](#行列都分散取值)

```python
dates = pd.date_range(start='2019-01-01',periods=6)
'''
DatetimeIndex(['2019-01-01', '2019-01-02', '2019-01-03', '2019-01-04',
               '2019-01-05', '2019-01-06'],
              dtype='datetime64[ns]', freq='D')'''
df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=['A','B','C','D'])
#randn函数返回一个或一组样本，具有标准正态分布。
```

### 行切片

**开始位置和结束位置都可以缺省，与列表的索引一样,可以用反向索引。**


- 绝对索引获取行切片：df['行标签a':'行标签b']或df.loc['行标签a':'行标签b']

取行标签a至行标签b的所有行，包括a行和b行。

- 相对索引行获取行切片：df.iloc[行标签i:行标签j]

取行标签i至行标签j的所有行，不包括j行。相对索引从0开始。

```python
df['2019-01-01':'2019-01-03']
df.loc['2019-01-01':'2019-01-03']
df.iloc[0:3]
```

### 列切片

**开始位置和结束位置都可以缺省，与列表的索引一样，可以用反向索引。**

- 绝对索引获取列切片：df.loc[:,'列标签c':'列标签d']

取列标签c至列标签d的所有列，包括c列和d列。

- 相对索引行获取列切片：df.iloc[列标签i:列标签j]

取列标签i至列标签j的所有列，不包括j列。相对索引从0开始。

```python
df.loc[:,'A':'B']
df.iloc[:,0:2]
```

### 行列同时切片

- 绝对索引获取切片：df.loc['行标签a':'行标签b','列标签c':'列标签d']

取行标签a至行标签b的所有行，包括a行和b行。取列标签c至列标签d的所有列，包括c列和d列。

- 相对索引获取切片：df.iloc[行标签i1:行标签i2:,列标签j1:列标签j2]

取行标签i1至行标签i2的所有行，不包括i2行。取列标签j1至列标签j2的所有列，不包括j2列。

```python
df.loc['2019-01-01':'2019-01-03','A':'B']
df.iloc[0:3,0:2]
```

### 行切片_列分散取值

行标签连续取,列标签分散取。

- 绝对索引获取切片：df.loc['行标签a':'行标签b',['列标签c','列标签d']]

- 相对索引获取切片：df.loc[行标签i1:行标签i2:,[列标签j1,列标签j2]
```python
df.loc['2019-01-01':'2019-01-03',['A','C']]
df.iloc[0:3,[0,2]]
```

### 行分散取值_列切片

行标签分散取,列标签连续取。只能用相对索引，不能用绝对索引。

- 相对索引获取切片：df.loc[[行标签i1,行标签i2],列标签j1:列标签j2]
```python
df.iloc[[0,3],0:3]
```

### 行列都分散取值

行标签分散取,列标签分散取。只能用相对索引，不能用绝对索引。


- 相对索引获取切片：df.iloc[[行标签i1,行标签i2],[列标签j1,列标签j2]]
```python
df.iloc[[0,3],[0,3]]
```

## 布尔索引

比较操作返回布尔数组，布尔数组可以作为掩码。

```python
dates = pd.date_range(start='2019-01-01',periods=6)
'''
DatetimeIndex(['2019-01-01', '2019-01-02', '2019-01-03', '2019-01-04',
               '2019-01-05', '2019-01-06'],
              dtype='datetime64[ns]', freq='D')'''
df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=['A','B','C','D'])
#randn函数返回一个或一组样本，具有标准正态分布。
```
```python
df > 0
df[df>0]
df.A>0
df[df.A>0]
```

isin()方法
```python
df2 = df.copy()
df2['E']=['one','one','two','three','four','three']     #新增一列
ind = df2['E'].isin(['two','four'])
df2[ind]    #取出E列中值为two或four的行
```

### 多级索引

用于多维数据

以行多级索引为例
```python
import pandas as pd,numpy as np


base_data = np.array([[1771,11115],
                      [2154,30320],
                      [2141,14070],
                      [2424,32680],
                      [1077,7806],
                      [1303,24222],
                      [798,4789],
                      [981,13468]])

data = pd.DataFrame(base_data,index=[['BeiJing','BeiJing','ShangHai','ShangHai','ShenZhen','ShenZhen','HangZhou','HangZhou'],[2008,2018]*4],columns=['population','GDP'])

data.index.names=['city', 'year']

data['GDP']

上海的GDP信息:
data.loc['ShangHai','GDP']         #返回Series
data.loc['ShangHai']['GDP']        #返回Series
data.loc[['ShangHai'],['GDP']]     #返回DataFrame

取上海2018年的信息
data.loc['ShangHai',2018]


取上海2018年的GDP信息
data.loc['ShangHai',2018]['GDP']
```