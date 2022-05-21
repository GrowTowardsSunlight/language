### 规则多子图

设置图片之间横向和纵向的间隔：plt.subplot_adjust(hspace,wspace)

plt.subplot(abc):总共有a行b列个网格，设置第c个图

plt.subplot(321):总共有3x1个网格，设置第1个图。
```python
x = np.random.random(10)
y = np.random.random(10)

plt.subplots_adjust(hspace=0.5, wspace=0.3)

plt.subplot(321)
plt.scatter(x,y,s=80, c='b',marker='>')

plt.subplot(322)
plt.scatter(x,y,s=80, c='g',marker='*')

plt.subplot(323)
plt.scatter(x,y,s=80, c='r',marker='s')

plt.subplot(324)
plt.scatter(x,y,s=80, c='c',marker='p')

plt.subplot(325)
plt.scatter(x,y,s=80, c='m',marker='+')

plt.subplot(326)
plt.scatter(x,y,s=80, c='y',marker='H')
```

### 不规则多子图

每个图占的网格数量不同。

grid = plt.GridSpec(m, n, wspace, hspace)划分成mxn的网格

plt.subplot(grid[a,b:c])把a行，b到c列网格都分给这个子图。
```python
def f(x):
    return np.exp(-x)*np.cos(2*np.pi*x)

x = np.arange(0.0, 3.0, 0.01)
grid = plt.GridSpec(2, 3, wspace=0.4, hspace=0.3)

plt.subplot(grid[0,0])
plt.plot(x,f(x))

plt.subplot(grid[0,1:])
plt.plot(x,f(x),'r--',lw=2)

plt.subplot(grid[1,:])
plt.plot(x,f(x),'g-',lw=3)
```