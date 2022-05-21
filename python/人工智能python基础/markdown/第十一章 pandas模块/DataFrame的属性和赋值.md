* [DataFrame的属性](#DataFrame的属性)
* [DataFrame的赋值](#DataFrame的赋值)

### DataFrame的属性

返回用numpy数组表示的数据：data.values

返回行索引：data.index返回行索引

返回列索引：data.columns

形状：data.shape

行数：len(data)或df.shape[0]

列数：df.shape[1]

返回每列数据的数据类型：data.dtypes

```python
population_dict = {'BejJing':2154,
                    'ShangHai':2424,
                    'ShenZhen':1303,
                    'HangZhou':981}

population = pd.Series(population_dict)

GDP_dict = {'BejJing':30320,
            'ShangHai':32680,
            'ShenZhen':24222,
            'HangZhou':13468}

GDP = pd.Series(GDP_dict)

data = pd.DataFrame({'pop':population,'GDP':GDP})
```
```python
data.values    #data.values返回用numpy数组表示的数据
data.index    #返回行索引
data.columns  #返回列索引
data.shape    #形状(4, 2)
data.dtypes   #返回每列数据的数据类型
'''
array([[ 2154, 30320],
       [ 2424, 32680],
       [ 1303, 24222],
       [  981, 13468]])'''

'''
Index(['BejJing', 'ShangHai', 'ShenZhen', 'HangZhou'], dtype='object')'''

'''Index(['pop', 'GDP'], dtype='object')'''
'''
pop    int64
GDP    int64
dtype: object'''
```
### DataFrame的赋值

* [增加新列](#增加新列)
* [修改赋值](#修改赋值)
* [修改标签](#修改赋值)

### 增加新列

df['新列名'] = 列表

或者

df['新列名'] = Series对象

列表或Series对象的长度必须和df的行数相同。
```python
s1 = pd.Series([1,2,3,4,5,6],index=pd.date_range('20190101',periods=6))
df['E'] = s1
```

### 修改赋值

先索引，后赋值。

- 标量的绝对索引赋值：

data.loc[['行名','列名']] = 新值

- 标量的相对索引赋值：

data.iloc[[i,j]] = 新值

- 对一列修改赋值：

df['列名'] = np.array([new]\*len(df))或者df['列名'] = new

```python
df.loc['20190101','A'] = 0
df.iloc[0,0] = 2
df['D']=np.array(['c']*len(df))
```
### 修改标签

df.index = 新值

df.columns = 新值
```python
df.index = [i for i in range(len(df))]
df.columns = [i for i in range(df.shape[1])]
```