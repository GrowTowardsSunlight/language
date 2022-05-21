numpy通用函数同样适用于pandas。numpy的向量化运算,矩阵化运算,广播运算在pandas中也使用。而pandas中特有的是索引对齐

一般来说，纯粹的计算在numpy里执行得更快。numpy更侧重于计算，pandas更侧重于数据处理。

* [向量化运算](#向量化运算)
* [矩阵运算](#矩阵运算)
* [执行相同运算_numpy与pandas的对比](#执行相同运算_numpy与pandas的对比)

* [索引对齐](#索引对齐)
* [排序](#排序)
* [统计](#)
* [apply自定义每行或每列相应操作](#apply自定义每行或每列相应操作)

* [大量数据的高性能计算](大量数据的高性能计算)

### 向量化运算

每个元素都进行了相应的运算。

- pandas对象与数字的加减乘除

- pandas对象与pandas对象的加减乘除

- 取反，乘方，求整数商，求余数

- 绝对值，三角函数，反三角函数，指数，对数

与- [numpy数组的向量化运算](https://github.com/zyxhzsh/artificial-intelligence/blob/master/人工智能python基础/markdown/第十章%20numpy模块/numpy数组的运算.md)使用的符号和函数相同。
```python
x = pd.DataFrame(np.arange(4).reshape(1,4))
x + 5       #每个元素都加5
np.exp(x)   #每个元素都进行指数运算

y = pd.DataFrame(np.arange(4,8).reshape(1,4))
x*y     #x与y相同位置的元素相乘，若形状不同则广播运算。
```

### 矩阵化运算

- 转置：df.T

- 乘法：df1.dot(df2)或np.dot(df1,df2)
```python
生成一个矩阵
np.random.seed(42)
df1 = pd.DataFrame(np.random.randint(10,size=(10,10)))
df2 = pd.DataFrame(np.random.randint(10,size=(10,10)))

df1.T   #转置

%timeit df1.dot(df2)
或%timeit np.dot(df1,df2)     
#%timeit:ipython中统计运行时间的魔术方法(多次运行取平均值)
```

### 执行相同运算_numpy与pandas的对比

以乘法为🌰
```python
np1 = np.array(df1)     #把DataFrame对象转换成numpy对象
np2 = np.array(df2)

#numpy远比pandas块
%timeit np1.dot(np2)    
%timeit np.dot(np1,np2)
%timeit np.dot(df1.values,df2.values)
```
python的for循环完成矩阵乘法
```python
for i in x2:
    res = []
    for j in i:
        res.append(int(j))
    x3.append(res)

def f(x,y):
    res = []
    for i in range(len(x)):
        row = []
        for j in range(len(y[0])):
            sum_row = 0
            for k in range(len(x[0])):
                sum_row+=x[i][k]*y[k][j]
            row.append(sum_row)
        res.append(row)
    return res

%timeit f(x)
```
小结：
```
f(df1,df2)>f(np1,np2)>df1.dot(df2)> np.dot(df1,df2)>np.dot(df1.values,df2.values)>np.dot(np1,np2)>np1.dot(np2)  
```  

### 广播运算

如果两个数组的形状在维度上不匹配，那么数组的形式会沿着维度为1的维度进行扩展，以匹配另一个数组的形状。

若扩展也无法让两个数组的形状一样，就会报错。
```python
np.random.seed(42)
x = pd.DataFrame(np.random.randint(10,size=(3,3)),columns=list('ABC'))
```
```python
x.iloc[0]                #取0行
x/x.iloc[0]              #每一行都除以0行 
x.A
x.div(x.A,axis=0)        #每一列都除以A列 
x.div(x.iloc[0],axis=1)  #每一行都除以0行 
当axis缺省时默认为1，1为行，0为列
```

### 索引对齐

以加为例。
```python
A = pd.DataFrame(np.random.randint(0,20,size=(2,2)),columns=list('AB'))

B = pd.DataFrame(np.random.randint(0,10,size=(3,3)),columns=list('ABC'))
A+B
A.add(B,fill_value = 0)
```
pandas会自动对齐两个对象的索引，没有的值用numpy的NaN表示。

缺失值也可以用fill_value来填充，填充以后再相加。

### 排序

```python
df = pd.DataFrame({
    'col1': ['A', 'A', 'B', np.nan, 'D', 'C'],
    'col2': [2, 1, 9, 8, 7, 4],
    'col3': [0, 1, 9, 4, 2, 3],})
```

#### 按列数据或行数据排序

一个标签下进行排序的数据，数据类型必须相同。若同时有字符串和数字，会报错。

DataFrame.sort_values(by=,axis=0,ascending=True, inplace=False, kind='quicksort', na_position=‘last’)

axis=0或'index'时，by指定列名，按照指定列中数据大小排序。

axis=1或'columns'时,by指定索引值，按照指定行中数据大小排序。

ascending：True表示升序排列，默认为True。

inplace：是否用排序后的数据集替换原来的数据，默认为False

kind：{‘quicksort’, ‘mergesort’, ‘heapsort’},  设置排序的算法，默认为‘quicksort’

na_position：{‘first’,‘last’}，设定缺失值的显示位置
```python
df.sort_values(by=['col2'])     #按照列col2的数据进行递增排序
df.sort_values(by=['col2','col3'],ascending=False)    #先依据第二数据降序排序，若第二列相同则按第三列排
df.sort(by=0,axis=1)    #因为第一行中数据的数据类型有字符和数字，不能比较，所以报错。
```
#### 按照标签名进行排序

DataFrame.sort_index(axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last')

axis：0表示按行名排序，1表示按列名排序，默认为0。

ascending：True表示升序排列，默认为True。

inplace：是否用排序后的数据集替换原来的数据，默认为False

kind：{‘quicksort’, ‘mergesort’, ‘heapsort’},  设置排序的算法，默认为‘quicksort’

na_position：{‘first’,‘last’}，设定缺失值的显示位置
```python
df.sort_index()         #按行名排序
df.sort_index(axis=1)   #按列名排序
```

### 统计

* [每列的总体面貌](#每列的总体面貌)
* [取值的集合](#取值的集合)
* [一列中每种元素的个数](#统计一列中每种元素的个数)
* [每列中非空元素个数](#每列中非空元素个数)
* [每列或每行元素求和](#每列或每行元素求和)
* [每列或每行的最值](#每列或每行的最值)
* [每列或每行的均值_方差_标准差](#每列或每行的均值_方差_标准差)
* [每列的任意分位数](#每列的任意分位数)
* [相关系数](#相关系数)

#### 每列的总体面貌

df.describe()

数值型：返回每列中非空元素个数，均值，标准差，最值，25%，50%，75%分位数。

字符型：返回每列中非空元素个数，取值的集合，出现频率最高的值和出现的次数。

```python
df2=pd.DataFrame([['a','b','c','d'],
                 ['e','a','c','f'],
                 ['d','c','r','g']],columns=list('ABCD'))
df2.describe()
```

#### 取值的集合

np.unique(numpy)

np.unique(DataFrame)
```python
y = np.random.randint(3,size=20)
print(y)
np.unique(y)    #numpy对象
'''
[2 2 2 1 2 1 1 2 1 2 2 0 2 0 2 2 0 0 2 1]
array([0, 1, 2])'''
y1 = pd.DataFrame(y, columns=['A'])
np.unique(y1)   #pandas对象
'''
array([0, 1, 2])'''
```

#### 一列中每种元素的个数
```python
from collections import Counter
Counter(y)
'''
Counter({2: 11, 1: 5, 0: 4})'''
y1['A'].value_counts()  #这是Series对象中的方法
'''
2    11
1     5
0     4
Name: A, dtype: int64'''
```

#### 每列中非空元素个数

df.count()
```
b    4
a    4
c    4
dtype: int64
```

#### 每列或每行元素求和

df.sum(axis=0)

axis可缺省，默认为0。0表示每列元素求和，1表示每行元素求和。

#### 每列或每行的最值

最小值：df.min(axis=0) 

最大值：df.max(axis=0)

最大值的坐标：df.idxmax(axis=0)

最小值的坐标：df.idxmin(axis=0)

axis可缺省，默认为0。0表示列，1表示行。

#### 每列或每行的均值_方差_标准差

均值：df.mean(axis=0)

方差：df.var(axis=0)（贝塞尔校正）

标准差：df.std(axis=0)（贝塞尔校正）

axis可缺省，默认为0。0表示列，1表示行。

样本方差是是关于总体方差的无偏估计量，既样本方差的估计量的期望等于总体方差。而没有修正的方差公式，它的期望是不等于总体方差的。

[样本方差](https://blog.csdn.net/Hearthougan/article/details/77859173)要除以（n-1）而不是除以n。[store](https://github.com/zyxhzsh/math-is-good/blob/master/python中的数学/样本方差为何除以n-1.pdf)

#### 每列或每行的中位数_众数

中位数：df.median(axis=0)

众数：df.mode(axis=0)。若有多个众数会显示多行。

axis可缺省，默认为0。0表示列，1表示行。

#### 每列的任意分位数

分位数（Quantile），亦称分位点，是指将一个随机变量的概率分布范围分为几个等份的数值点。

df.quantile(0.75)

#### 相关系数

df.corr()   #相关系数矩阵

df.corrwith(df['a'])         #看一列的相关系数

### apply自定义每行或每列相应操作

apply(method):使用method方法默认对每一列进行相应操作。

axis可缺省，默认为0。0表示列，1表示行。

```python
df.apply(np.cumsum)     #对数据累加

df.apply(lambda x:x.max()-x.min())  #自定义函数，每列的最大值减最小值           

自定义函数
def my_describe(x):
    return pd.Series([x.count(),x.mean(),x.max(),x.idxmin(),x.std()],index=['Count','mean','max','idxmin','std'])
df.apply(my_describe)
```

### 大量数据的高性能计算

- **pd.eval('表达式')**:减少复合代数式计算中间过程的内存分配，从而提升速度。若内存够用，eval反而速度更慢。

```python
df1, df2, df3, df4 = (pd.DataFrame(np.random.random((10000,1000))) for i in rangge(4))
```
```python
%timeit (df1+df2)/(df3+df4)
'''
60.3 ms ± 1.68 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)'''

%timeit pd.eval('(df1+df2)/(df3+df4)')
'''
30 ms ± 1.04 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)'''

判断结果是否一样
np.allclose ((df1+df2)/(df3+df4), pd.eval('(df1+df2)/(df3+df4)'))
```

- **query()**


df[(df.A<0.5)&(df.B>0.5)]等于

df.query('(A<0.5)&(B>0.5)')
```python
由于数据较小，query()更慢。

df = pd.DataFrame({'A': range(1, 6),
                   'B': range(10, 0, -2),
                   'C C': range(10, 5, -1)})

%timeit df[(df.A<0.5)&(df.B>0.5)]
'''
574 µs ± 11.2 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)'''
%timeit df.query('(A<0.5)&(B>0.5)')
'''
2.01 ms ± 39.5 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)'''


判断结果是否一样
np.allclose(df[(df.A<0.5)&(df.B>0.5)],df.query('(A<0.5)&(B>0.5)'))
```