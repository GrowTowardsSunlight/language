df.plot？


### 线性图

df.plot()

x为行标签，y为每一列，每列都对应一条线。
```python
df = pd.DataFrame(np.random.randn(1000, 4).cumsum(axis=0),columns=list('ABCD'),index=np.arange(1000))

df.plot()
#df.plot?
```

### 柱形图

竖向：df.plot.bar(stacked=False)

横向：df.plot.bah(stacked=False)

stacked:累加

x为行标签，y为每一列。多组数据。

```python
df2 = pd.DataFrame(np.random.rand(10, 4), columns=['a','b','c','d'])
df2.plot.bar()
#df2.plot.bar(stacked=True)
```

### 直方图

df.plot.hist(x, bins)

或者df.plot(x, bins, kind='hist')

bins：确定区间的划分。如果是整数，表示等宽的bin的个数。如果是序列，表示bin的边缘，包括第一个bin的左边缘和最后一个bin的右边缘。


```python
df3 = pd.DataFrame({'A':np.random.randn(1000)+10, 'B':np.random.randn(1000), 'C':np.random.randn(1000)-10})

df3.plot.hist()     #每列都画直方图

df3['A'].plot.hist(cumulative=True) #A列的累加直方图
或df3['A'].plot(cumulative=True,kind='hist')
```

### 概率密度图

df.plot(kind='kde') 

kind： The kind of plot to produce.
```
    - 'line' : line plot (default)
    - 'bar' : vertical bar plot
    - 'barh' : horizontal bar plot
    - 'hist' : histogram
    - 'box' : boxplot
    - 'kde' : Kernel Density Estimation plot
    - 'density' : same as 'kde'
    - 'area' : area plot
    - 'pie' : pie plot
    - 'scatter' : scatter plot
    - 'hexbin' : hexbin plot.
```
```python
df3 = pd.DataFrame({'A':np.random.randn(1000)+10, 'B':np.random.randn(1000), 'C':np.random.randn(1000)-10})

df3['A'].plot.hist(kind='kde') 
```

### 散点图

df.plot(kind='scatter') 

### 多子图

df.plot(subplots=True,figsize,layout,sharex=False)

subplots:多子图
```python
df = pd.DataFrame(np.random.randn(1000, 4).cumsum(axis=0),columns=list('ABCD'),index=np.arange(1000))

df.plot(subplots=True,figsize=(6,12))   #默认设置

df.plot(subplots=True,figsize=(6,12),layout=(2,2),sharex=False)   #
```