* [具名元组](#namedtuple具名元组)
* [用具名元组模仿扑克牌](#用具名元组模仿扑克牌)
* [计数器工具](#counter计数器工具)
* [抽10张牌统计大于10的比例](#抽10张牌统计大于10的比例)
* [双向队列](#deque双向队列)



容器数据类型是组合数据类型的扩展

### namedtuple具名元组

```
p = (1,2)
```
点的坐标,仅看数据，很难知道表达的是一个坐标。

具名元组就是给元组和元素中的元素起名字。

构造一个新的元组子类：
```python
collections.namedtuple(typename, field_names, *, rename = False, defaults = None, module = None)
```
typename为元组名字，field_names为域名(元素的名字)

具名元组是元组的子类，可以调用属性，可以索引，可以解包赋值。
```python
Point = collections.namedtuple('point',['x','y'])
p = Point(1, y = 2)
print(p)
print(p.x)                  #调用属性
print(p.y)                  #调用属性
print(p[0])                 #可以索引
x,y = p                     #可以解包赋值  
print(x,y)
print(ifinstance(p,Point))    
print(ifinstance(p,tuple))  #是元组的子类
```
```
point(x=1, y=2)
1
2
1
1 2
True
True
```

### 用具名元组模仿扑克牌

模拟一副没有王的扑克牌
```python
Card = collections.namedtuple('Card',['rank', 'suit'])
ranks = [str(n) for n in range(2,11)] +list('JQKA')
suits = ['spades','diamonds','clubs','hearts']
print('ranks',ranks)
print('suits',suits)
cards = [Card(rank,suit) for rank in ranks for suit in suits]      #列表推导
cards
```
```
ranks ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
suits ['spades', 'diamonds', 'clubs', 'hearts']

[Card(rank='2', suit='spades'),
 Card(rank='2', suit='diamonds'),
 Card(rank='2', suit='clubs'),
 Card(rank='2', suit='hearts'),
 Card(rank='3', suit='spades'),
 Card(rank='3', suit='diamonds'),
 Card(rank='3', suit='clubs'),
 Card(rank='3', suit='hearts'),
 Card(rank='4', suit='spades'),
 Card(rank='4', suit='diamonds'),
 Card(rank='4', suit='clubs'),
 Card(rank='4', suit='hearts'),
 Card(rank='5', suit='spades'),
 Card(rank='5', suit='diamonds'),
 Card(rank='5', suit='clubs'),
 Card(rank='5', suit='hearts'),
 Card(rank='6', suit='spades'),
 Card(rank='6', suit='diamonds'),
 Card(rank='6', suit='clubs'),
 Card(rank='6', suit='hearts'),
 Card(rank='7', suit='spades'),
 Card(rank='7', suit='diamonds'),
 Card(rank='7', suit='clubs'),
 Card(rank='7', suit='hearts'),
 Card(rank='8', suit='spades'),
 Card(rank='8', suit='diamonds'),
 Card(rank='8', suit='clubs'),
 Card(rank='8', suit='hearts'),
 Card(rank='9', suit='spades'),
 Card(rank='9', suit='diamonds'),
 Card(rank='9', suit='clubs'),
 Card(rank='9', suit='hearts'),
 Card(rank='10', suit='spades'),
 Card(rank='10', suit='diamonds'),
 Card(rank='10', suit='clubs'),
 Card(rank='10', suit='hearts'),
 Card(rank='J', suit='spades'),
 Card(rank='J', suit='diamonds'),
 Card(rank='J', suit='clubs'),
 Card(rank='J', suit='hearts'),
 Card(rank='Q', suit='spades'),
 Card(rank='Q', suit='diamonds'),
 Card(rank='Q', suit='clubs'),
 Card(rank='Q', suit='hearts'),
 Card(rank='K', suit='spades'),
 Card(rank='K', suit='diamonds'),
 Card(rank='K', suit='clubs'),
 Card(rank='K', suit='hearts'),
 Card(rank='A', suit='spades'),
 Card(rank='A', suit='diamonds'),
 Card(rank='A', suit='clubs'),
 Card(rank='A', suit='hearts')]
```
洗牌
```python
from random import *

shuffle(cards)      #shuffle将序列类型的元素打乱重排
cards
```
抽牌
```python
choice(cards)   #随机抽一张牌
sample(cards, k = 5)     #随机抽5张不同的牌
```
### counter计数器工具

- **Counter()统计元素出现的次数**

对列表每个元素出现的次数进行统计

对字符串中每个字符出现的次数进行统计

counter()是字典的子类

counter()可以执行加减操作
```python
from collections import Counter
s = '牛奶奶找刘奶奶买牛奶'
colors = ['red','blue','green','blue','blue']
cnt_str = Counter(s)
cnt_color = Counter(colors)
print(cnt_str)
print(cnt_color)
print(isinstance(Counter(), dict))
```
```
Counter({'奶': 5, '牛': 2, '找': 1, '刘': 1, '买': 1})
Counter({'blue': 3, 'red': 1, 'green': 1})
True
```
```python
counter()执行加减操作
c = Counter(a=3,b=1)
d = Counter(a=1,b=2)
e = c+d
print(c)
print(d)
print(e)
```
```
Counter({'a': 3, 'b': 1})
Counter({'b': 2, 'a': 1})
Counter({'a': 4, 'b': 3})
```
- **most_common(n)最常出现的n个元素及其次数**

```python
cnt_color.most_common(2)
```
```
[('blue', 3), ('red', 1)]
```
- **elements()将统计好的元素展开**
```python
print(cnt_str)
list(cnt_str.elements())
```
```
Counter({'奶': 5, '牛': 2, '找': 1, '刘': 1, '买': 1})
['牛', '牛', '奶', '奶', '奶', '奶', '奶', '找', '刘', '买']
```

### 抽10张牌统计大于10的比例
```python
from random import *

cards = collections.Counter(tens=16, low_cards=36)  # #简单的设定牌，大于10的有16张，小于10的有36张
seen = sample(list(cards.elements()),k=10)
print(seen)
seen.count('tens')/10
```
```
['tens', 'low_cards', 'low_cards', 'tens', 'low_cards', 'low_cards', 'low_cards', 'low_cards', 'low_cards', 'tens']
0.3
```
### deque双向队列

```
列表访问数据非常快，但插入和删除操作非常慢，需要大量移动元素位置。比如用inser(0,v)和pop(0)在列表开始进行插入和删除操作。
```
双向列表可以在队列两边高效、快速的增加和删除元素。

双向队列的父类不是元组也不是列表
```python
from collections import deque

d = deque('cde')
d
```
```
deque(['c', 'd', 'e'])
```                                           
增加元素
```python
from collections import deque

d = deque('cde')
print(d)
d.append('f')       #右端插入
print(d)
d.append('g')       #右端插入
print(d)
d.appendleft('b')   #左端插入
print(d)
d.appendleft('a')   #左端插入
print(d)
```
```
deque(['c', 'd', 'e'])
deque(['c', 'd', 'e', 'f'])
deque(['c', 'd', 'e', 'f', 'g'])
deque(['b', 'c', 'd', 'e', 'f', 'g'])
deque(['a', 'b', 'c', 'd', 'e', 'f', 'g'])
```
删除元素
```python
d.pop()         #右端删除
d.popleft()     #左端删除
```