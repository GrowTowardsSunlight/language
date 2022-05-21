* [Series对象](#Series对象)

* [DataFrame对象](#DataFrame对象)

* [数据的查看](#数据的查看)

numpy在下量化的数值计算中表现优异。

但是numpy模块在处理带标签数据时，有些力不从心。如为数据添加标签，处理缺失值，分组和透视表等方面。

pandas库基于numpy，该工具是为了解决数据分析任务而创建的，提供了高效地操作大型数据集所需的工具。

### Series对象

Series是带标签数据的一维数组,支持多种数据类型。有多种数据类型时dtype为object。

pd.Series(data, index = index,dtype = dtype)

data：可以是列表，字典或numpy数组

index：用于索引的标签，是可选参数

dtype：数据类型，为可选参数。全是整数默认int64，有浮点数无字符默认float64。有字符默认object。

index缺省，默认标签为整数序列。index若不缺省，用户设定的为标签，这时用整数索引仍然有效。

dtype会强制类型转换，若无法转换，如字符'a'无法转出浮点数，就会报错。

* [用列表创建](#用列表创建)
* [用一维numpy数组创建](#用一维numpy数组创建)
* [用字典创建](#用字典创建)
* [数字运算操作函数](#数字运算操作函数)
* [数字运算操作函数](#数字运算操作函数)
* [数据为标量](数据为标量)

#### 用列表创建

index缺省
```python
import pandas as pd

data = pd.Series([1.5,2,4.5,6])
data
#data[0]为1.5，data[1]为2.0
```
```
0    1.5
1    2.0
2    4.5
3    6.0
dtype: float64
```
增加index
```python
import pandas as pd

data = pd.Series([1.5,2,4.5,6], index=['a','b','c','d'])
data
#data['a']和data[0]都为1.5
```
```
a    1.5
b    2.0
c    4.5
d    6.0
dtype: float64
```
多种数据类型
```python
import pandas as pd

data = pd.Series([1.5,'s',4.5,6])
data
#data[1]为's'
```
```
0    1.5
1      s
2    4.5
3      6
dtype: object
```

#### 用一维numpy数组创建

```
import numpy as np
import pandas as pd

x = np.arange(5)
pd.Series(x)
```
```
0    0
1    1
2    2
3    3
4    4
dtype: int64
```

### 用字典创建

默认以键为index，值为data。

如果指定index，则会到字典的键中筛选，找不到的值设为NaH。

```python
population_dict = {'BejJing':2154,
                    'ShangHai':2424,
                    'ShenZhen':1303,
                    'HangZhou':981}

population = pd.Series(population_dict)
population
```
```
BejJing     2154
ShangHai    2424
ShenZhen    1303
HangZhou     981
dtype: int64
```
```python
population = pd.Series(population_dict, index = ['BejJing','HangZhou','c','d'])
population
```
```
BejJing     2154.0
HangZhou     981.0
c              NaN
d              NaN
dtype: float64
```
### 数据为标量
```python
 pd.Series(5, index = [100,200,300])
```
```
100    5
200    5
300    5
dtype: int64
```

### DataFrame对象

DataFrame是带标签数据的多维数组。

pd.DataFrame(data,index=index,columns=columns)

data:可以是列表，字典或numpy数组

index:行标签，是可选参数

columns:列标签，为可选参数

若标签缺省，默认标签为整数序列。

* [通过Series对象创建](#通过Series对象创建)
* [通过Series对象字典创建](#通过Series对象字典创建)
* [通过字典列表对象创建](#通过字典列表对象创建)
* [通过numpy二维数组创建](#通过numpy二维数组创建)

### 通过Series对象创建
```python
population_dict = {'BejJing':2154,
                    'ShangHai':2424,
                    'ShenZhen':1303,
                    'HangZhou':98}

population = pd.Series(population_dict)
pd.DataFrame(population)    #比Series多了列标签
```

### 通过Series对象字典创建

```python
GDP_dict = {'BejJing':30320,
            'ShangHai':32680,
            'ShenZhen':24222,
            'HangZhou':13468}

GDP = pd.Series(GDP_dict)
pd.DataFrame({'population':population,      #'population'为列标签
              'GDP':GDP,'country':'China'}) #'GDP'为列标签
```
数量不够会自动补齐

### 通过字典列表对象创建

列表里的元素都是字典。字典索引作为index,字典键作为columns
```python
data = [{'a':i,'b':2*i} for i in range(3)]
pd.DataFrame(data)
```
不存在的键，默认值为NaN。
```python
data = [{'a':1,'b':1},{'b':3,'c':4}]
pd.DataFrame(data)
```
### 通过numpy二维数组创建
```python
data = np.random.randint(10,size=(3,2))
pd.DataFrame(data,columns=['foo','bar'],index=['a','b','c'])
```

### 数据的查看


- **查看前k行**：df.head(k)

k默认为5

- **查看后k行**：df.tail(k)

k默认为5

- **查看总体信息**：df.info()

```python
import pandas as pd,numpy as np

dates = pd.date_range(start='2019-01-01',periods=6)
'''
DatetimeIndex(['2019-01-01', '2019-01-02', '2019-01-03', '2019-01-04',
               '2019-01-05', '2019-01-06'],
              dtype='datetime64[ns]', freq='D')'''
df = pd.DataFrame(np.random.randn(6,4),index=dates,columns=['A','B','C','D'])
#randn函数返回一个或一组样本，具有标准正态分布。

df.head(1)
df.tail(2)
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
DatetimeIndex: 6 entries, 2019-01-01 to 2019-01-06
Freq: D
Data columns (total 4 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   A       6 non-null      float64
 1   B       6 non-null      float64
 2   C       6 non-null      float64
 3   D       6 non-null      float64
dtypes: float64(4)
memory usage: 240.0 bytes
```
