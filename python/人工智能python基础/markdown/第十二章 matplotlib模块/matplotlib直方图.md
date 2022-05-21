plt.hist(x,bins,density=False,关键字参数)

bins:划分的区间数

density：True求概率密度,否则求频次。

关键字参数
```
character      description  

color           颜色 
range           x轴的范围,元组表示。
bottom          y轴的起始位置
histtype        线条的类型   "bar":方形，           "barstacked":柱形,
                            "step":"未填充线条"    "stepfilled":"填充线条"


align           对齐方式    "left":左，"mid":中间，"right":右

orientation    {"horizontal", "vertical"}
log             对数坐标轴

cumulative      累计概率分布，bool。
```
### 频次直方图
```python
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

plt.hist(x, bins=50, facecolor='g', alpha=0.75)
```

### 概率密度直方图

将频次当做频次，再除以区间长度。

density= True
```python
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

plt.hist(x, bins=50, color='g', density=True)
plt.xlabel('Smarts')
plt.ylabel('Probability')
plt.title('Histogram of IQ')
plt.text(60, 0.025, r'$\mu=100,\ \sigma=15$')
plt.xlim(40, 160)
plt.ylim(0, 0.03)
```
获得真正的高斯分布的概率密度图像
```python
from scipy.stats import norm
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)

_,bins,__=plt.hist(x,50,density=True)   #bins获得分配的区间

y = norm.pdf(bins,mu,sigma)     #计算符合高斯分布的概率密度，把bins中的点放进去，计算出这些点对应的正态分布的值是多少。
plt.plot(bins, y ,'r--',lw=3)
```

### 累计概率分布

cumulative=True


