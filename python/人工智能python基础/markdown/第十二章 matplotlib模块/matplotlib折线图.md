* [格式](#格式)

* [线条颜色](#线条颜色)
* [线条风格](#线条风格)
* [线条宽度](#线条宽度)
* [数据点标记的形状和大小](#数据点标记的形状和大小)
* [seaborn风格](#seaborn风格)

- [设置坐标轴](https://github.com/zyxhzsh/artificial-intelligence/blob/master/人工智能python基础/markdown/第十二章%20matplotlib模块/matplotlib环境配置.md)
- [图例](https://github.com/zyxhzsh/artificial-intelligence/blob/master/人工智能python基础/markdown/第十二章%20matplotlib模块/matplotlib环境配置.md)
- [添加文字和箭头](https://github.com/zyxhzsh/artificial-intelligence/blob/master/人工智能python基础/markdown/第十二章%20matplotlib模块/matplotlib环境配置.md)



### 格式

plot([x], y, '格式化字符串', 关键字参数)

plot([x], y, '格式化字符串', [x1], y1, '格式化字符串',关键字参数(应用于所有的集合))

（1）x,y:数组或标量。通常是一维数组，也可以是标量或二维数组。

如果是二维数组，每列代表单独的数据集。如plt.plot(a[0], a[1],'o-')。

（2）格式化字符串：'[marker][line][color]'任意顺序均可，都可以缺省。

数据点标记的形状，线条风格，线条颜色。可选项，

颜色只能用缩写，但只有color时可以用[matplotlib.colors](https://matplotlib.org/api/colors_api.html#module-matplotlib.colors)中的任意格式。如全称('green')或hex strings('#008000').

HTML,CSS中，#hex，6位，用于表示颜色。

线条风格只能用缩写。

（3）关键字参数：
可选项，关键字参数可以用全称，也可以用缩写。值可以用全称，也可以用缩写。

color='颜色'，linestyle='线条风格'，linewidth=线宽

marker='数据点标记的形状'，markersize=数据点标记的大小

label='图例'  [详情]()


关键字参数的缩写：
```
c: color    ls: linestyle    lw: linewidth    markersize: ms
```

**格式化字符串与关键字参数可以同时使用，发生冲突时，关键字参数优先**

**指定多个集合时，任何关键字参数都应用于所有的集合**

```python
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use('seaborn-whitegrid')
import numpy as np 
```

- 下面两条语句，一个使用格式化字符串和关键字参数，另一个只使用关键字参数。两个语句等价。
```
plot(x, y, 'go--', linewidth=2, markersize=12)
plot(x, y, color='green', marker='o', linestyle='dashed',
...      linewidth=2, markersize=12)
```

### 线条颜色

颜色的缩写是单个字母。
```
character   color
'b'         blue
'g'         green
'r'         red
'c'         cyan
'm'         magenta
'y'         yellow
'k'         black
'w'         white
```
设置线条颜色
```python
offsets = np.linspace(0, np.pi, 5)
colors = ['blue','g','r','yellow','pink']       #每个元素都是fmt
for offset, color in zip(offsets, colors):
    plt.plot(x, np.sin(x-offset), color=color)  #color可缩写为c
```

### 线条风格

linestyle可缩写为ls
```
character   line style   description
'-'         solid        实现   
'--'        dashed       虚线   
'-.'        dashdot      点划线
':'         dotted       点
```
设置线条风格
```python
x = np.linspace(0, 10, 11)
offsets = list(range(8))
linestyles = ['solid', 'dashed', 'dashdot', 'dotted', '-', '--', '-.',':']       #每个元素都是fmt
for offset, linestyle in zip(offsets, linestyles):
    plt.plot(x, x+offset, linestyle=linestyle)  #linestyle可缩写为ls
```

#### 线条宽度

linewidth可缩写为lw

```python
x = np.linspace(0, 10, 11)
offsets = list(range(0,12,3))
linewidths = (i*2 for i in range(1, 5))    #每个元素都是fmt
#画4条线，线宽分别是2，4，8，16

for offset, linewidth in zip(offsets, linewidths):
    plt.plot(x, x+offset, linewidth=linewidth)  #linewidth可缩写为lw
```

#### 数据点标记的形状和大小

数据点标记的形状：marker
```
character   description
'.'         point marker
','         pixel marker
'o'         circle marker
'v'         triangle_down marker
'^'         triangle_up marker
'<'         triangle_left marker
'>'         triangle_right marker
'1'         tri_down marker
'2'         tri_up marker
'3'         tri_left marker
'4'         tri_right marker
's'         square marker
'p'         pentagon marker
'*'         star marker
'h'         hexagon1 marker
'H'         hexagon2 marker
'+'         plus marker
'x'         x marker
'D'         diamond marker
'd'         thin_diamond marker
'|'         vline marker
'_'         hline marker
```
数据标记点的大小：makersize

可缩写为ms

```python
x = np.linspace(0, 10, 11)
offsets = list(range(0,12,3))
makers = ['*', '+', 'o', 's']    #每个元素都是fmt

for offset, marker in zip(offsets, markers):
    plt.plot(x, x+offset, marker= marker,markersize= 5) 

#makersize可缩写为ms, markersize可以不设。
```
### seaborn风格

plt.plot前一行加上如下语句：

sns.set()
