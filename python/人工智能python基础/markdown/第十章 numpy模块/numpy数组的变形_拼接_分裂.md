* [数组的变形](#数组的变形)
* [数组的拼接](#数组的拼接)
* [数组的分裂](#数组的分裂)

### 数组的变形

x2 = x1.reshape(m,n)

数组大小要一样。返回的是视图，不是副本。如果对变形后的元素进行修改，原来的数组也会被修改。
```python
x1 = np.random.randint(0,10,(12,))
print(x1)
print(x1.shape)
x2=x1.reshape(4,3) 
print(x2)
x2[0,0]=14
print(x1)
```
```
[7 1 7 1 3 5 2 5 9 7 3 8]
(12,)
[[7 1 7]
 [1 3 5]
 [2 5 9]
 [7 3 8]]
[14  1  7  1  3  5  2  5  9  7  3  8]
```
**一维向量转二维行向量**
```python
x3 = x1.reshape(1,x1.shape[0])  一维向量转二维行向量。
或者x3 = x1[np.newaxis,:] 
```
```
array([[14,  1,  7,  1,  3,  5,  2,  5,  9,  7,  3,  8]])
```
**一维向量转二维行列向量**
```python
x4 = x1.reshape(x1.shape[0],1)  #一维向量转二维行向量。
或者x4 = x1[:,np.newaxis] 
```
```
array([[14],
       [ 1],
       [ 7],
       [ 1],
       [ 3],
       [ 5],
       [ 2],
       [ 5],
       [ 9],
       [ 7],
       [ 3],
       [ 8]])
```
**多维向量转一维向量**

flatten返回副本
```python
y1 = np.random.randint(0,10,(3,4))
print(y1)
y2 = y1.flatten()
y2[0]=12
print(y2)
print(y1)
```
```
[[6 8 1 8]
 [9 4 9 1]
 [6 0 5 7]]
[12  8  1  8  9  4  9  1  6  0  5  7]
[[6 8 1 8]
 [9 4 9 1]
 [6 0 5 7]]
```
ravel返回视图
```python
y3 = np.random.randint(0,10,(3,4))
print(y3)
y4 = y3.ravel()
y4[0]=12
print(y4)
print(y3)
```
```
[[6 5 1 3]
 [3 1 5 8]
 [2 3 8 1]]
[12  5  1  3  3  1  5  8  2  3  8  1]
[[12  5  1  3]
 [ 3  1  5  8]
 [ 2  3  8  1]]
```
reshpae返回的是视图
```python
y5 = np.random.randint(0,10,(3,4))
print(y5)
y6 = y5.reshape(-1)
y6[0]=12
print(y6)
print(y5)
```
```
[[3 4 7 6]
 [4 4 2 5]
 [5 6 0 7]]
[12  4  7  6  4  4  2  5  5  6  0  7]
[[12  4  7  6]
 [ 4  4  2  5]
 [ 5  6  0  7]]
```

### 数组的拼接

```python
x1 = np.array([1,2,3],
              [4,5,6])
x2 = np.array([7,8,9],
              [0,1,2])  
```
**水平拼接,返回副本** 

np.hstack([x1,x2])或者np.c_[x1,x2]

行数必须相等           
```python
x3 = np.hstack([x1,x2])
#x3 = np.c_[x1,x2] 与hstack等价
x3[0][0] = 12
print(x3)
print(x1)
```
```
[[12  2  3  7  8  9]
 [ 4  5  6  0  1  2]]
[[1 2 3]
 [4 5 6]]
```
**垂直拼接,返回副本**

np.vstack([x1,x2])或者np.r_[x1,x2]

列数必须相等 
```python
x3 = np.vstack([x1,x2])
#x3 = np.r_[x1,x2] 与hstack等价
x3[0][0] = 12
print(x3)
print(x1)
```
```
[[12  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [ 0  1  2]]
[[1 2 3]
 [4 5 6]]
​
```
### 数组的分裂

- split一维数组的分裂

np.split(数组,[s1,s2,...,sn])

s为分裂点，左边不包括s。
```python
x1 = np.arange(10)
print(x1)
a,b,c,d=np.split(x1,[2,5,7])
print(a)
print(b)
print(c)
print(d)
```
```
[0 1 2 3 4 5 6 7 8 9]
[0 1]
[2 3 4]
[5 6]
[7 8 9]
```

- hsplit按列分隔

np.hsplit(数组,[s1,s2,...,sn])

s为分裂划分的列，左边不包括s。
```python
x1 = np.arange(1,26).reshape(5,5)
print(x1)
a,b,c = np.hsplit(x1,[2,4])
print('a:\n',a)
print('b:\n',b)
print('c:\n',c)
```
```
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]
 [16 17 18 19 20]
 [21 22 23 24 25]]
a:
 [[ 1  2]
 [ 6  7]
 [11 12]
 [16 17]
 [21 22]]
b:
 [[ 3  4]
 [ 8  9]
 [13 14]
 [18 19]
 [23 24]]
c:
 [[ 5]
 [10]
 [15]
 [20]
 [25]]
```
- vsplit按行分隔

```python
x1 = np.arange(1,26).reshape(5,5)
print(x1)
a,b,c = np.vsplit(x1,[2,4])
print('a:\n',a)
print('b:\n',b)
print('c:\n',c)
```
```
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]
 [16 17 18 19 20]
 [21 22 23 24 25]]
a:
 [[ 1  2  3  4  5]
 [ 6  7  8  9 10]]
b:
 [[11 12 13 14 15]
 [16 17 18 19 20]]
c:
 [[21 22 23 24 25]]
```