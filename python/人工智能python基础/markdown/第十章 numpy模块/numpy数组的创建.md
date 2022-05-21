* [使用列表创建](#使用列表创建)

### 从头创建数组

#### 固定元素

* [创建长度为n的数组，值都为0](#创建长度为n的数组_值都为0)
* [创建一个m行n列的数组，值都为1](#创建一个m行n列的数组_值都为1)
* [创建一个m行n列的数组，值都为a](#创建一个m行n列的数组_值都为a)
* [创建一个n阶单位矩阵](#创建一个n阶单位矩阵)

#### 序列元素

* [创建一个线性序列数组，从a开始，到b结束，步长为c](#创建一个线性序列数组_从a开始_到b结束_步长为c)
* [创建一个k个元素的数组，这k个数均匀的分配到a~b](#创建一个k个元素的数组_这k个数均匀的分配到a-b)
* [创建一个k个元素的数组，形成k^a-k^b的等比数列](#创建一个k个元素的数组_形成k的a次幂-k的b次幂的等比数列)

#### 随机元素

* [创建一个m行n列的，在0~1之间均匀分布的随机数构成的数组](#创建一个m行n列的_在0-1之间均匀分布的随机数构成的数组)
* [创建一个m行n列的，均值为u，标准差为σ的正态分布随机数构成的数组](#创建一个m行n列的_均值为u_标准差为σ的正态分布随机数构成的数组)
* [创建一个m行n列的_在闭a_开b之间随机整数构成的数组](#创建一个m行n列的_在闭a_开b之间随机整数构成的数组)
* [随机重排数组](#随机重排数组)
* [随机采样](#随机采样)


### 使用列表创建

- 一维数组
```python
import numpy as np

x = np.array([1,2,3,4,5])
print(x)
print(x.shape)      #形状。x是一维数组，里面有五个元素。
print(type(x))      #x的类型
print(type(x[0]))   #x中元素的类型 

```
```
[1 2 3 4 5]
(5,)
<class 'numpy.ndarray'>
<class 'numpy.int64'>
```
创建的时候指定数组中元素的类型
```python
import numpy as np

x = np.array([1,2,3,4,5],dtype='float32')
print(x)
print(type(x))      #x的类型
print(type(x[0]))   #x中元素的类型 
```
```
[1. 2. 3. 4. 5.]
<class 'numpy.ndarray'>
<class 'numpy.float32'>
```

- 二维数组

将一维数组用[]方括号扩起来
```python
x = np.array([[1,2,3],
            [4,5,6],
            [7,8,9]])

print(x)
print(x.shape)          #形状
print(type(x))          #x的类型:3*3的二维数组
print(type(x[0][0]))    #x中元素的类型 
```
```
[[1 2 3]
 [4 5 6]
 [7 8 9]]
(3, 3)
<class 'numpy.ndarray'>
<class 'numpy.int64'>
```

### 从头创建数组

### 创建长度为n的数组_值都为0

dytype默认为float64

np.zeros(k, dtype=)
```python
np.zeros(6)
```
```
array([0, 0, 0, 0, 0, 0])
```
### 创建一个m行n列的数组_值都为1

dytype默认为float64

np.ones((m,n), dtype=)
```python
np.ones((2,4), dtype=float)
```
```
array([[1., 1., 1., 1.],
       [1., 1., 1., 1.]])
```
### 创建一个m行n列的数组_值都为a

dytype默认为int64

x=np.full((m,n), a,dtype=)
```python
x=np.full((2,4), 8,dtype=float)
print(x)
print(type(x[0][0]))
```
```
[[8. 8. 8. 8.]
 [8. 8. 8. 8.]]
<class 'numpy.float64'>
```
### 创建一个n阶单位矩阵

dytype默认为float64

np.eye(n)
```python
x=np.eye(6)
print(x)
print(type(x[0][0]))
```
```
[[1. 0. 0. 0. 0. 0.]
 [0. 1. 0. 0. 0. 0.]
 [0. 0. 1. 0. 0. 0.]
 [0. 0. 0. 1. 0. 0.]
 [0. 0. 0. 0. 1. 0.]
 [0. 0. 0. 0. 0. 1.]]
<class 'numpy.float64'>
```
### 创建一个线性序列数组_从a开始_到b结束_步长为c

dytype默认为int64

np.arange(a,b,c,dtype=)

不包含结束位置
```python
np.arange(1,10,1)
```
```
array([1, 2, 3, 4, 5, 6, 7, 8, 9])
```
### 创建一个k个元素的数组_这k个数均匀的分配到a-b

闭区间

dytype默认为float64

np.linspace(a,b,k,dtype=)
```python
np.linspace(12.3,14,4,dtype=float)
```
```
array([12.3       , 12.86666667, 13.43333333, 14.        ])
```
### 创建一个k个元素的数组_形成k的a次幂-k的b次幂的等比数列

闭区间

dytype默认为float64

np.logspace(k,a,b,dytype=)
```python
np.logspace(0,9,10)
```
```
array([1.e+00, 1.e+01, 1.e+02, 1.e+03, 1.e+04, 1.e+05, 1.e+06, 1.e+07,
       1.e+08, 1.e+09])
```
### 创建一个m行n列的_在0-1之间均匀分布的随机数构成的数组


元素类型为float64

np.random.random((m,n))
```python
np.random.random((4,3))
```
```
array([[0.86474187, 0.04700149, 0.35218557],
       [0.68337211, 0.03394915, 0.87154515],
       [0.55232577, 0.78574479, 0.19603174],
       [0.57916444, 0.96973412, 0.45160423]])
```
### 创建一个m行n列的_均值为u_标准差为σ的正态分布随机数构成的数组

元素类型为float64

np.random.normal(u,σ,(m,n))
```python
np.random.normal(0,1,(3,4))
```
```
array([[ 0.26208879, -0.41423134,  1.04013797, -0.40255765],
       [-0.19991625, -0.86496747, -0.41088682, -0.24784142],
       [-1.02359979, -0.09196083, -0.14250367, -0.32956742]])
```
### 创建一个m行n列的_在闭a_开b之间随机整数构成的数组

np.random.randint(a,b,size=(m,n))

```
或者np.random.randint(a,b,(m,n))
或者np.random.randint(b,size=(m,n))   #此时默认a为0
```
```python
import numpy as np

np.random.randint(1,8,(3,4))
```
```
array([[3, 2, 1, 5],
       [3, 3, 7, 3],
       [3, 7, 4, 1]])
```
### 随机重排数组

- np.random.permutation()

原数组不变，产生新数组
```python
import numpy as np

x = np.random.randint(1,8,(3,4))
print(x,'\n')
print(np.random.permutation(x),'\n')  #产生新数组
print(x)
```
```
[[5 4 7 2]
 [7 6 3 2]
 [7 5 3 4]] 

[[7 5 3 4]
 [7 6 3 2]
 [5 4 7 2]] 

[[5 4 7 2]
 [7 6 3 2]
 [7 5 3 4]]
```
- np.random.shffle()

修改原数组
```python
import numpy as np

x = np.random.randint(1,8,(3,4))
print(x,'\n')
print(np.random.shuffle(x),'\n')  #修改原数组
print(x)
```
```
[[5 6 7 6]
 [1 2 1 3]
 [2 7 5 1]] 

None 

[[2 7 5 1]
 [1 2 1 3]
 [5 6 7 6]]
```
### 随机采样

np.random.choice(数组,size=(m,n),p = )

p概率是可选项
```python
x = np.arange(10,25,dtype=float)
print(x)
np.random.choice(x,size=(4,3))
```
```
[10. 11. 12. 13. 14. 15. 16. 17. 18. 19. 20. 21. 22. 23. 24.]
array([[20., 15., 12.],
       [16., 15., 14.],
       [11., 23., 24.],
       [21., 22., 15.]])
```
```python
np.random.choice(x,size=(5,6),p=x/np.sum(x))
```
```
array([[22., 13., 15., 13., 10., 12.],
       [23., 12., 15., 12., 24., 15.],
       [16., 21., 22., 17., 17., 12.],
       [18., 18., 21., 20., 22., 11.],
       [17., 17., 24., 20., 11., 24.]])
```