* [数组的属性](#数组的属性)

### 通用函数

* [数值排序](#数值排序)
* [获得排序后元素在原数组中的索引](#获得排序后元素在原数组中的索引)
* [数值求和](#数值求和)
* [数值求积](#数值求积)
* [中位数_均值_方差_标准差](#中位数_均值_方差_标准差)

### 数组的属性

```python
x = np.random.randint(1,10,(3,5))
x
```
```
array([[7, 8, 9, 5, 8],
       [8, 6, 7, 2, 9],
       [7, 8, 2, 6, 6]])
```

- 数组的形状
```python
x.shape  #几行几列
(3, 5)
```
- 数组的维度

```python
x.ndim
2
```
- 数组的大小

```python
x.size      #元素个数
15
```
- 数组的数据类型

```python
x.dtype
dtype('int64')
```

### 数值排序
```python
x = np.random.randint(20,50,size=10)
print(x)
y = np.sort(x)  #产生新的排序数组,原数组不变。
print(y)
print(x)
x.sort()        #对数组排序，python内置函数,无返回值，原数组改变。
print(x)
```
```
[34 38 35 37 28 41 46 37 46 40]
[28 34 35 37 37 38 40 41 46 46]
[34 38 35 37 28 41 46 37 46 40]
[28 34 35 37 37 38 40 41 46 46]
```

### 获得排序后元素在原数组中的索引

```python
x = np.random.randint(20,50,size=10)
print(x)
i = np.argsort(x)
print(i)
```
```
[42 24 26 49 48 20 21 41 38 32]
[5 6 1 2 9 8 7 0 4 3]
```
最小的元素在原数组中为x[5],最大的元素在原数组中为x[3]

### 最大值和最小值

```python
x = np.random.randint(20,50,size=10)
print(x)
print('max:',np.max(x))
print('min:',np.min(x))
print('max_index:',np.argmax(x))
print('min_index:',np.argmin(x))
```
```
[43 31 26 37 22 34 46 47 43 32]
max: 47
min: 22
max_index: 7
min_index: 4
```

### 数值求和

np.sum(数组，axis = )

不写axis是对所有元素求和，axis=1是按行求和，axis=0是按列求和。

所有元素求和
```python
x = np.arange(1,6)
np.sum(x)     #或者python内置的x.sum()，统计数组中元素的和
```
按行求和
```python
x1 = np.arange(6).reshape(2,3)
print(x1)
np.sum(x1,axis = 1)     #求出每行的和
```
```
[[0 1 2]
 [3 4 5]]
array([ 3, 12])
```
按列求和
```python
np.sum(x1,axis = 0)     #求出每列的和
```
```
array([3, 5, 7])
```

### 数值求积

np.prod(数组，axis = )

不写axis是对所有元素求积，axis=1是按行求积，axis=0是按列求积。

以按行求积为例
```python
x1 = np.arange(6).reshape(2,3)
print(x1)
np.prod(x1,axis = 1)     #求出每行的和
```
```
[[0 1 2]
 [3 4 5]]
array([ 0, 60])
```

### 中位数_均值_方差_标准差

```
x = np.random.normal(0,1,size = 10000)
 
import matplotlib.pyplot as plt

plt.hist(x, bins = 50)
plt.show()
```
```python
np.median(x)    #中位数
np.mean(x)      #均值。或用python自带的x.mean()  
np.var(x)       #方差。或用python自带的x.var()
np.std(x)       #标准差。或用python自带的x.std()
```