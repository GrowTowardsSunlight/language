* [排列组合迭代器](#排列组合迭代器)
* [拉链](#拉链)
* [无穷迭代器](#无穷迭代器)
* [锁链](#锁链chain)
* [枚举](#枚举)
* [分组](#分组)

itertools模块提供了很多产生迭代器的方法。

迭代器需要用迭代的方式拿出元素，或者用list的方式转化成列表。

### 排列组合迭代器

- **笛卡尔积product**

笛卡尔积：k个集合中各取一个元素的所有有序对。

以两个元素的笛卡尔积为例：有序对的第一个对象取自第一个集合，第二个对象取自第二个集合。

A×B = {(x,y)\|x∈A∧y∈B}

```python
import itertools

for i in itertools.product('ABC','01'):
    print(i)
```
```
('A', '0')
('A', '1')
('B', '0')
('B', '1')
('C', '0')
('C', '1')
```
```python
for i in itertools.product('ABC', repeat=3):  #相当于有三个'ABC'
    print(i)
```
```
('A', 'A', 'A')
('A', 'A', 'B')
('A', 'A', 'C')
('A', 'B', 'A')
('A', 'B', 'B')
('A', 'B', 'C')
('A', 'C', 'A')
('A', 'C', 'B')
('A', 'C', 'C')
('B', 'A', 'A')
('B', 'A', 'B')
('B', 'A', 'C')
('B', 'B', 'A')
('B', 'B', 'B')
('B', 'B', 'C')
('B', 'C', 'A')
('B', 'C', 'B')
('B', 'C', 'C')
('C', 'A', 'A')
('C', 'A', 'B')
('C', 'A', 'C')
('C', 'B', 'A')
('C', 'B', 'B')
('C', 'B', 'C')
('C', 'C', 'A')
('C', 'C', 'B')
('C', 'C', 'C')
```

- **排列permutations**

排列长度可以缺省，默认为全排列
```python
for i in itertools.permutations('ABCD',3):   #3是排列的长度，可以缺省，默认为全排列
    print(i)
```
```
('A', 'B', 'C')
('A', 'B', 'D')
('A', 'C', 'B')
('A', 'C', 'D')
('A', 'D', 'B')
('A', 'D', 'C')
('B', 'A', 'C')
('B', 'A', 'D')
('B', 'C', 'A')
('B', 'C', 'D')
('B', 'D', 'A')
('B', 'D', 'C')
('C', 'A', 'B')
('C', 'A', 'D')
('C', 'B', 'A')
('C', 'B', 'D')
('C', 'D', 'A')
('C', 'D', 'B')
('D', 'A', 'B')
('D', 'A', 'C')
('D', 'B', 'A')
('D', 'B', 'C')
('D', 'C', 'A')
('D', 'C', 'B')
```
```python
for i in itertools.permutations(range(3),3):  #排列的长度可以缺省，默认为
    print(i)
```
```
(0, 1, 2)
(0, 2, 1)
(1, 0, 2)
(1, 2, 0)
(2, 0, 1)
(2, 1, 0)
```

- 组合combinations

组合的长度不能缺省

```python
for i in itertools.combinations('ABCD',2):      #2是组合的长度，不能缺省
    print(i)
```
```
('A', 'B')
('A', 'C')
('A', 'D')
('B', 'C')
('B', 'D')
('C', 'D')
```
```python
for i in itertools.combinations(range(4),3):
    print(i)
```
```
(0, 1, 2)
(0, 1, 3)
(0, 2, 3)
(1, 2, 3)
```

- **元素可重复的组合**

combinations_with_replacement
```python
for i in itertools.combinations_with_replacement('ABC',2):
    print(i)
```
```
('A', 'A')
('A', 'B')
('A', 'C')
('B', 'B')
('B', 'C')
('C', 'C')
```
与下面这个笛卡尔积对比
```python
for i in itertools.product('ABC',repeat=2):
    print(i)
```
```
('A', 'A')
('A', 'B')
('A', 'C')
('B', 'A')
('B', 'B')
('B', 'C')
('C', 'A')
('C', 'B')
('C', 'C')
```
### 拉链

- 短拉链zip

zip是python内置的。

长度不一时，执行到最短的对象处就停止。
```python
for i in zip('ABC','012','xyz'):
    print(i)

for i in zip('ABC',[0,1,2,3,4,5]):
    print(i)
```
```
('A', '0', 'x')
('B', '1', 'y')
('C', '2', 'z')
('A', 0)
('B', 1)
('C', 2)
```

- 长拉链zip_longest

长度不一时，执行到最长的对象处就停止，缺省元素用none或指定字符代替。
```python
for i in itertools.zip_longest('ABC','012345'):
    print(i)
```
```
('A', '0')
('B', '1')
('C', '2')
(None, '3')
(None, '4')
(None, '5')
```
```python
for i in itertools.zip_longest('ABC','012345',fillvalue='?'):
    print(i)
```
```
('A', '0')
('B', '1')
('C', '2')
('?', '3')
('?', '4')
('?', '5')
```
### 无穷迭代器

如果不停止或设置停止对象，就会一直迭代下去。

- **计数count(start,step=1)**

设置初值和步长，步长可以缺省，默认为1，可以无穷无尽地返回数。
```python
itertools.count(10)  #需要用迭代的方式拿出元素，或者用list的方式转化成列表。
```
- **循环cycle(iterable**

创建一个迭代器，返回iterable中所有元素，无限重复
```python
itertools.cycle('ABC')  #需要用迭代的方式拿出元素，或者用list的方式转化成列表。
```
- **重复**

创建一个迭代器，不断重复object。除非设定参数times，否则将无限重复。
```python
for i in itertools.repeat(10,3):
    print(i)
```
```
10
10
10
```
### 锁链chain

把一组迭代对象串联起来，形成一个更大的迭代器。
```python
for i in itertools.chain('ABC',[1,2,3]):
    print(i)
```
```
A
B
C
1
2
```
### 枚举

enumerate(iterable,start=0)

python内置函数。

产生由两个元素组成的元祖，结构是(index,item)，其中index从start开始，item从iterable中取。
```python
for i in enumerate('Python',start=1):
    print(i)
```
```
(1, 'P')
(2, 'y')
(3, 't')
(4, 'h')
(5, 'o')
(6, 'n')
```

### 分组

groupby(iterable,key=None)

创建一个迭代器，按照key指定的方式，返回iterable中连续的键和组。

一般来说，要预先对数据进行排序。

key为None时，默认把连续重复元素分组。
```python
for key,group in itertools.groupby('AAAABBBBCCDAABBB'):
    print(key, list(group))  #因为group也是一个可迭代对象，所以用list显式表达
print(type(group))
```
```
A ['A', 'A', 'A', 'A']
B ['B', 'B', 'B', 'B']
C ['C', 'C']
D ['D']
A ['A', 'A']
B ['B', 'B', 'B']
<class 'itertools._grouper'>
```
```python
#对数据排序
animals = ['duck','eagle','rat','giraffe','bear','bat','dolphin','shark','lion']
animals.sort(key=len)
print(animals)

#对数据分组
for key,group in itertools.groupby(animals,key=len):
    print(key,list(group))
```
```
['rat', 'bat', 'duck', 'bear', 'lion', 'eagle', 'shark', 'giraffe', 'dolphin']
3 ['rat', 'bat']
4 ['duck', 'bear', 'lion']
5 ['eagle', 'shark']
7 ['giraffe', 'dolphin']
```
按照首字母的顺序分组
```python
#对数据排序
animals = ['duck','eagle','rat','giraffe','bear','bat','dolphin','shark','lion']
animals.sort(key=lambda x:x[0])
print(animals)

#对数据分组
for key,group in itertools.groupby(animals,key=lambda x:x[0]):
    print(key,list(group))
```
```
['bear', 'bat', 'duck', 'dolphin', 'eagle', 'giraffe', 'lion', 'rat', 'shark']
b ['bear', 'bat']
d ['duck', 'dolphin']
e ['eagle']
g ['giraffe']
l ['lion']
r ['rat']
s ['shark']
```