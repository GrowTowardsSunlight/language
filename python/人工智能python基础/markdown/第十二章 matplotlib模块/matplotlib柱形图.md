### 竖向柱形图

plt.bar(x, y, width=0.8, bottom=None, align='center', 关键字参数)

### 横向柱形图

plt.barh(x, y, width=0.8, bottom=None, align='center', 关键字参数)

**y**：柱的高度

**align**： {'center', 'edge'}默认为center。center是将柱的中间与x坐标对齐。

当width为正时，edge是将柱的左边缘与x坐标对齐；当width为负时，edge是将柱的右边缘与x坐标对齐。

**width**：竖向柱形图柱的宽度

**height**：横向柱形图柱的宽度

**bottom**：柱状图的底的y坐标。

关键字参数：
```
Property            Description

alpha               透明度，0为完全透明，1为不透明。比1大时和1效果相同。
label               图例
color               颜色
edgecolor           边缘颜色
```
```python
x = np.arange(1, 6)
plt.bar(x, 2*x, align ='center', width=0.5, alpha=0.5, color='yellow', edgecolor='red')
plt.tick_params(axis='both', labelsize=13)
plt.xticks(x,('G1','G2','G3','G4','G5'))    #将下轴上的数字替换成字符
```
### 设置多个颜色
```python
colors=['red','yellow','blue','green','grey']
x = ['G'+str(i) for i in range(5)]
y = 1/(1+np.exp(-np.arange(5)))
plt.bar(x, y, align ='center', width=0.5, alpha=0.5, color=colors, edgecolor='red')
plt.tick_params(axis='both', labelsize=13)
```

### 累加柱形图

```python
x = np.arange(5)
y1 = np.random.randint(20, 30, size=5)
y2 = np.random.randint(20, 30, size=5)
plt.bar(x, y1, width=0.5, label='man')
plt.bar(x, y2, width=0.5,bottom=y1, label='man')
plt.legend()
```

### 并列柱形图

x要有一个合适的偏移量。可以设为前一个柱的宽度。
```python
x = np.arange(15)
y1 = x+1
y2 = y1+np.random.random(15)
plt.bar(x, y1, width=0.3, label='man')
plt.bar(x+0.3, y2, width=0.3, label='woman')
plt.legend()
```

### seaborn绘制柱形图

竖向：sns.barplot(x, y, linwidth)

横向：sns.barplot(y, x, linwidth)

把plt.bar和plt.barh改成sns.barplot即可。seaborn绘图更好看。但是用sns.barplot不知道怎么画并列柱形图。
```python
import seaborn as sns

x = np.arange(1, 6)
sns.barplot(x, 2*x, linewidth=0.3, label='man')
```
