* [向量化运算](#向量化运算)
* [矩阵运算](#矩阵运算)
* [广播运算](#广播运算)
* [比较运算和掩码](#比较运算和掩码)

### 向量化运算

向量化运算：每个元素都进行了相应的运算

- 数组与数字的加减乘除

```python
x1 = np.arange(1,6)
print(x1)
print('x1+5:',x1+5)
print('x1-5:',x1-5)
print('x1*5:',x1*5)
print('x1/5:',x1/5)
```
```
[1 2 3 4 5]
x1+5: [ 6  7  8  9 10]
x1-5: [-4 -3 -2 -1  0]
x1*5: [ 5 10 15 20 25]
x1/5: [0.2 0.4 0.6 0.8 1. ]
```
- 两个数组的加减乘除

```python
x1 = np.arange(1,6)
x2 = np.arange(6,11)
print('x1+x2:',x1+x2)
print('x1-x2:',x1-x2)
print('x1*x2:',x1*x2)
print('x1/x2:',x1/x2)
```
```
x1+x2: [ 7  9 11 13 15]
x1-x2: [-5 -5 -5 -5 -5]
x1*x2: [ 6 14 24 36 50]
x1/x2: [0.16666667 0.28571429 0.375      0.44444444 0.5       ]
```
- 数组取反，乘方，求整数商，求余数
```python
x1 = np.arange(1,6)
print(x1)
print('-x1:',-x1)
print('x1**3:',x1**3)
print('x1//2:',x1//2)
print('x1%2:',x1%2)
```
```
[1 2 3 4 5]
-x1: [-1 -2 -3 -4 -5]
x**3: [  1   8  27  64 125]
x//2: [0 1 1 2 2]
x1%2: [1 0 1 0 1]
```
- 绝对值，三角函数，反三角函数，指数，对数
```python
x2 = np.array([1,-1,2,-2,0])
np.abs(x2)  #或者python自带的abs(x2)  绝对值
#out:array([1, 1, 2, 2, 0])
theta = np.linspace(0,np.pi,3)
#array([0.        , 1.57079633, 3.14159265])
三角函数
print('sin(theta):',np.sin(theta)) 
print('cos(theta):',np.cos(theta))
print('tan(theta):\n',np.tan(theta))
反三角函数
x=[1,0,-1]
print('arcsin(x):',np.arcsin(x)) 
print('arccos(x):',np.arccos(x))
print('arctan(x):\n',np.arctan(x))
指数
x=np.arange(3)
np.exp(x)
#array([1.        , 2.71828183, 7.3890561 ])
对数
x = np.array([1,2,4,8,10])
print('ln(x):',np.log(x))       #若需要其他底用换底公式
print('log2(x):',np.log2(x))
print('log10(x):',np.log10(x))
```
```
sin(theta): [0.0000000e+00 1.0000000e+00 1.2246468e-16]
cos(theta): [ 1.000000e+00  6.123234e-17 -1.000000e+00]
tan(theta): [ 0.00000000e+00  1.63312394e+16 -1.22464680e-16]

arcsin(x): [ 1.57079633  0.         -1.57079633]
arccos(x): [0.         1.57079633 3.14159265]
arctan(x): [ 0.78539816  0.         -0.78539816]

ln(x): [0.         0.69314718 1.38629436 2.07944154 2.30258509]
log2(x): [0.         1.         2.         3.         3.32192809]
log10(x): [0.         0.30103    0.60205999 0.90308999 1.        ]
```

### 矩阵运算

```python
x = np.arange(9).reshape(3,3)
x
```
```
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])
```
- 矩阵转置
```python
y = x.T
y
```
```
array([[0, 3, 6],
       [1, 4, 7],
       [2, 5, 8]])
```
- 矩阵乘法
```python
x = np.array([[1,0],
             [1,2]])
y = np.array([[0,1],
             [1,1]])
np.dot(x,y)    #或python自带的x.dot(y)
#np.dot(y,x)或y.dot(x)是y乘以x
```
```
array([[0, 1],
       [2, 3]])
```

### 广播运算

如果两个数组的形状在维度上不匹配，那么数组的形式会沿着维度为1的维度进行扩展，以匹配另一个数组的形状。

若扩展也无法让两个数组的形状一样，就会报错。

```python
x = np.arange(3).reshape(1,3)
x + 5   

#3*3与1*3相加
x1 = np.ones((3,3))
x2 = np.arange(3).reshape(1,3)
print(x1+x2)    #1*3不能匹配3*3，所以扩展成3*3，三行相同。

#3*1与1*3相加
x3 = np.arange(3).reshape(1,3)
x4 = np.arange(3).reshape(3,1)
print(x3+x4)  #1*3扩展成3*3，三行相同。3*1扩展成3*3，三列相同
```
```
array([[1., 2., 3.],
       [1., 2., 3.],
       [1., 2., 3.]])

[[0 1 2]
 [1 2 3]
 [2 3 4]]
```

### 比较运算和掩码

通过操作比较运算获得的布尔数组，可以方便地对数据进行统计和处理。

- 数组与数组或者数组与数的比较操作，得到布尔数组。
```python
x1 = np.random.randint(100,size=(10,10))
x2 = np.random.randint(50,size=(10,10))
#x1>50   数组与数比较
x1>x2    #数组与数组比较
```
```
array([[ True,  True, False,  True,  True, False,  True,  True,  True,
         True],
       [ True, False, False,  True, False, False,  True,  True, False,
         True],
       [ True,  True,  True,  True,  True,  True,  True,  True,  True,
         True],
       [False,  True,  True, False,  True,  True,  True, False,  True,
         True],
       [ True,  True, False,  True,  True, False,  True,  True,  True,
         True],
       [False,  True, False,  True,  True,  True, False,  True,  True,
         True],
       [ True,  True,  True,  True,  True,  True,  True, False,  True,
         True],
       [ True,  True,  True,  True, False, False,  True,  True,  True,
         True],
       [ True,  True,  True,  True, False,  True,  True,  True,  True,
         True],
       [ True,  True,  True,  True,  True,  True,  True, False,  True,
         True]])
```

- 操作布尔数组
```python
x = np.random.randint(10,size=(3,4))
print(x>5)
np.sum(x>5)           #统计大于5的元素个数
np.all(x>0)           #判断是不是所有的数字都大于0
np.any(x==6)          #判断是不是至少有一个元素大于6
np.all(x<8,axis=1)    #按行进行判断，是否一行所有元素都小于8。某次输出为array([False, False,  True])
(x<9)&(x>5)           #可以使用逻辑运算符，这里返回布尔数组
np.sum((x<9)&(x>5) )  #逻辑运算符与sum一起使用
```
- 将布尔数组作为掩码
```python
x = np.random.randint(10,size=(3,4))
print(x2>5)     #布尔数组
x2[x2>5]        #以布尔数组为掩码，取出所有大于5的数据