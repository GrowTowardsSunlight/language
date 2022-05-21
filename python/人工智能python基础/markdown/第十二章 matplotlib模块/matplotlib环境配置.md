* [显示图片](#显示图片)
* [设置样式](#设置样式)
* [保存图像](#保存图像)

## 设置坐标轴

* [坐标轴的范围](#坐标轴的范围)
* [坐标轴的样式](#坐标轴的样式)
* [对数坐标](#对数坐标)
* [坐标轴刻度](#坐标轴刻度)
* [图像名字和轴标签](#图像名字和轴标签)

* [图例](#图例)
* [添加文字和箭头](#添加文字和箭头)

### 显示图片

- ipython中可用魔术方法%matplotlib inline

- pycharm中必须用plt.show()

```python
%matplotlib inline
import matplotlib.pyplot as plt

x = [1,2,3,4]
y = [1,4,9,16]
plt.plot(x,y)   #折线图
plt.ylabel('suqares')
#这里只是生成了图像，pycharm中需要plt.show()显示。而ipython里可以设置魔术方法，生成了就会显示。
```

### 设置样式

```python
风格存在这里plt.style.available中

临时改变风格：
with plt.style.context('seaborn-dark'):
    plt.plot(x,y)

永久改变风格：
plt.style.use('seaborn-dark')
```

### 保存图像

```python
import numpy as np
x = np.linspace(0,10,100)
plt.plot(x, np.exp(x))
plt.savefig('/Users/orange/Pictures/caicai.png')
```

## 设置坐标轴

plt.aixs([xmin, xmax, ymin, ymax],'样式'])

[xmin, xmax, ymin, ymax]和'样式'都是可选项，若同时使用，则xmin, xmax, ymin, ymax]生效，而样式失效。

### 坐标轴的范围

设置x轴的范围：plt.xlim(a, b)

设置y轴的范围：plt.ylim(c, d)

设置x轴和y轴的范围：plt.axis([xmin, xmax, ymin, ymax])


```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x))
plt.xlim(-1, 7)
plt.ylim(-1.5, 1.5)
```

```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x))
plt.axis([-1, 7, -1.5, 1.5])
```

### 坐标轴的样式

plt.axis('value')

```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x))
plt.axis('equal')
```
?plt.aixs查询样式（ipython中）
```
    Value       Description

    'on'        Turn on axis lines and labels. Same as ``True``.
    'off'       Turn off axis lines and labels. Same as ``False``.
    'equal'     Set equal scaling (i.e., make circles circular) by
                changing axis limits.
    'scaled'    Set equal scaling (i.e., make circles circular) by
                changing dimensions of the plot box.
    'tight'     Set limits just large enough to show all data.
    'auto'      Automatic scaling (fill plot box with data).
    'normal'    Same as 'auto'; deprecated.
    'image'     'scaled' with axis limits equal to data limits.
    'square'    Square plot; similar to 'scaled', but initially forcing
                ``xmax-xmin = ymax-ymin``.
```

### 对数坐标

默认为线性坐标，设置对数坐标：

plt.xscale('log')
plt.yscale('log')
```python
x = np.logspace(0, 5, 100)
plt.plot(x, np.log(x))
plt.xscale('log')   #将x轴设为对数坐标
```

### 坐标轴刻度

plt.xticks(np.arange(start,stop,step),fontsize=)

plt.yticks(np.arange(start,stop,step),fontsize=)

plt.tick_params(axis = 'both', labelsize=15)#xy轴同时设置数字的字体大小

fontsize为数字的字体大小
```python
x = np.linspace(0, 10, 100)
plt.plot(x, x**2)
plt.xticks(np.arange(0, 12, 1),fontsize=15)
plt.yticks(np.arange(0, 110, 10),fontsize=15)
#或者plt.xticks(np.arange(start=0, stop=12, step=1))
```

### 图像名字和轴标签

plt.xlabel('x',fontsize=)

plt.ylabel('y',fontsize=)

```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x))
plt.title('A Sine Curve',fontsize = 20)
plt.xlabel('x',fontsize=20)
plt.ylabel('sin(x)',fontsize=20)
plt.tick_params(axis = 'both', labelsize=15)
```

### 图例

label = '' 

plt.legend(loc='图例的位置',frameon=Flase,fontsize=)

plt.legend()的作用是显示图例，没有就不显示。

frameon给图例加个框。
```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x),label = 'Sin')
plt.plot(x, np.cos(x),label = 'Cos')
plt.ylim(-1.5,2)    #y轴的范围
plt.legend(loc='best',frameon=True,fontsize=15)
```

### 添加文字和箭头

文字：plt.text(横坐标,纵坐标,'要添加的文字',fontsize=)

箭头：plt.annotate('要添加的文字',xy=(指向的位置的横坐标，纵坐标),xytext(放文字的地方的横坐标，纵坐标),arrowprops=dict(facecolor='black',shrink=0.1))

arrowprops设置箭头的属性。
```python
x = np.linspace(0, 2*np.pi, 100)
plt.plot(x, np.sin(x), 'b-')
plt.annotate('local min', xy=(1.5*np.pi, -1), xytext=(4.5, 0 ), arrowprops=dict(facecolor='black', shrink=0.1))
