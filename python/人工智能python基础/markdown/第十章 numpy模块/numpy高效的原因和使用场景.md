引例：求100万个数的倒数

for 循环实现
```python
def compute_reciprocals(values):
    res=[]
    for value in values:    
    #列表里的元素可以是各种类型的。每遍历到一个元素，就要判断其类型，然后查找适用这个类型的函数。
        res.append(1/value)
    return res


values = list(range(1,1000000))
%timeit compute_reciprocals(values)
#%timeit:ipython中统计运行时间的魔术方法(多次运行取平均值)
```
```
103 ms ± 1.84 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
```
numpy数组实现
```python
import numpy as np

values = np.arange(1,1000000)  
#数据类型唯一，只要查询一次所需要的操作函数即可。
%timeit 1/values
```
```
2.25 ms ± 37.7 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
```
速度是数量级的提升

### numpy为什么高效

（1）numpy是由c语言编写的

c编译型语言；python解释型语言

c语言执行时，对代码进行整体编译，速度更快。

（2）numpy数组是连续单一类型的存储，这种存储结构，契合计算机底层的一些高效的数据处理方式。

numpy数组内的数据类型必须是统一的，而Python列表支持任意类型数据的填充。numpy数组内的数据连续存储在内存中，而python列表的数据分散在内存中。

numpy数组数据类型唯一，只要查询一次所需要的操作函数即可。

列表里的元素可以是各种类型的，每遍历到一个元素，就要判断其类型，然后查找适用这个类型的函数。

（3）python语言执行时有线程锁，无法实现真正的多线程并行，而C语言可以。

### 什么时候用numpy

在数据处理的过程中，遇到使用Python for循环实现一些向量化，矩阵化操作的时候，要优先考虑用numpy。

如两个向量的点乘，矩阵乘法。