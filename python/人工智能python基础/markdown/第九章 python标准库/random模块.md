* [随机种子](#随机种子)
* [产生随机整数](#产生随机整数)
* [产生随机浮点数](#产生随机浮点数)
* [获取序列类型的随机项](#获取序列类型的随机项)
* [将序列类型中元素随机排列](#将序列类型元素随机排列)
* [产生符合概率分布的随机数](#产生符合概率分布的随机数)
* [实现简单的微信红包分配](#实现简单的微信红包分配)
* [产生4位随机验证码](#产生4位由数字和英文字母构成的随机验证码)


random库提供各种伪随机数。

伪随机性：相同的随机种子会产生相同的随机数。

除了加密解密算法外，基本可以满足大多数工程应用。

### 随机种子

相同的随机种子会产生相同的随机数。

如果不设置随机种子，默认以当前时间为随机种子，来产生伪随机数。

```python
from random import*

seed(10)
print(random())
seed(10)
print(random())

print(random())     #以当前时间为随机种子
```
```
0.5714025946899135
0.5714025946899135
0.4288890546751146
```
### 产生随机整数

产生[a,b]之间的随机整数:randint(a, b)

产生[0,a)之间的随机整数:randrange(a)

产生[a,b)之间的以step为步长的随机整数:randrange(a,b,step)
```python
numbers1 = [randint(1,10) for i in range(10)] 
numbers2 = [randrange(10) for i in range(10)]
numbers3 = [randrange(0,10,2) for i in range(10)]
print(numbers1)
print(numbers2)
print(numbers3)
```
```
[10, 1, 4, 8, 8, 5, 3, 1, 9, 8]
[5, 1, 3, 5, 0, 6, 2, 9, 5, 6]
[6, 4, 4, 6, 2, 4, 4, 2, 6, 2]
```

### 产生随机浮点数

产生[0.0,1.0）之间的随机浮点数：radom()

产生[a,b]之间的随机浮点数：uniform(a,b)
```python
numbers4 = [random() for i in range(10)]
numbers5 = [uniform(2.1,3.4) for i in range(10)]

print(numbers4)
print(numbers5)
```
```
[0.8179828644296319, 0.6578909387591091, 0.5334837356527721, 0.8551257407736, 0.14968813497140154, 0.5672354768631239, 0.3741748177480889, 0.6013045471136395, 0.11291570189443623, 0.7755127010728279] 

[2.2255875831396583, 2.316272869531222, 3.149684677632182, 3.332002101490538, 2.6632009533169314, 2.6383050812727915, 2.419126438982982, 2.45711440955525, 2.9024286022664163, 2.331998533936943]
```

### 获取序列类型的随机项

从序列类型中随机返回一个元素。choice(seq)

对序列类型进行k次重复采样，k大小不限，可设置权重:choices(seq,weights=None,k)

从序列a中随机抽取k个元素，k小于或等于序列长度，将k个元素生以list形式返回。

(1)
```python
choice(['any','ball','cell'])
'any'
```
```python
choice('python')
'h'
```
(2)
```python
choice(['any','ball','cell'], [5,8,2],k=10)
```
```
['any', 'ball', 'ball', 'ball', 'ball', 'ball', 'any', 'cell', 'ball', 'cell']
```
(3)
```python
sample([10,20,30,40,50],k=3)  #k不能大于列表的元素个数
```
```
[40, 50, 10]
```

### 将序列类型中元素随机排列

shuffle(seq)将序列类型中元素随机排列,返回打乱后的序列
```python
numbers = ['one','two','three',6]
shuffle(numbers)
numbers
```
```
['two', 'one', 'three', 6]
```

### 产生符合概率分布的随机数

产生一个符合高斯分布的随机数：gauss(mean,std)

mean是均值，std是标准差。
```python
number = gauss(0,1)
number
-1.0351174165411274
```
```python
产生1万个符合高斯分布的随机数，画出直方图
import matplotlib.pyplot as plt

res = [gauss(0,1) for i in range(100000)]

plt.hist(res, bins=1000)
plt.show()
```

### 实现简单的微信红包分配
```python
import random


def red_packet(total,num):

    sum = 0  #验证分配给每个人的红包总和是否为最开始的total
    for i in range(1,num):  #给n-1个人分配，剩下的钱分给最后一个人
        per = random.uniform(0.01,total/(num-i+1)*2)     #均匀分布的期望为(a+b)/2,这样保证了每个人获得红包的期望是最开始的total/num。
        total = total - per
        sum+=per
        print('第{}位红包金额为：{:.2f}元'.format(i,per))
    else:
        print('第{}位红包金额为：{:.2f}元'.format(num,total))
        sum+=total
    print(sum)

red_packet(10,5)
```
```
第1位红包金额为：3.70元
第2位红包金额为：1.58元
第3位红包金额为：2.71元
第4位红包金额为：1.43元
第5位红包金额为：0.58元
10.0
```
执行1000W次来验证红包分配是随机的。ls[]记录单次发放红包的金额，把结果放到res[]中。res[]中有发1000w次红包的每次的结果。然后对结果进行平均，得到每个人平均每次获得的红包的期望。
```python
import random


def red_packet(total,num):

    ls= []
    for i in range(1,num):  #给n-1个人分配，剩下的钱分给最后一个人
        per = random.uniform(0.01,total/(num-i+1)*2)     #均匀分布的期望为(a+b)/2,这样保证了每个人获得红包的期望是最开始的total/num。
        ls.append(per)
        total = total - per
    else:
        ls.append(total)

    return ls

res = []
for i in range(10000000):
    ls = red_packet(10,5)
    res.append(ls)

res = np.array(res)     #把每个位置的1000w个数做平均
#print(res[:10])  #打印前十次发红包的结果
np.mean(res,axis=0)
```
```
array([2.00439064, 2.00403338, 2.0014823 , 1.99923914, 1.99085454])
```
### 产生4位由数字和英文字母构成的随机验证码
```python
import random
import string

print(string.digits)
print(string.ascii_letters)

s = string.digits + string.ascii_letters
v =random.sample(s,4)   #从s中随机取4个不同的字符，这是因为sample是取k个不同位置的元素，而s中又没有相同的字符。
print(v)
print(''.join(v))  #将4个字符聚合输出
```
```
0123456789
abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
['Z', '3', '9', 'g']
Z39g
```