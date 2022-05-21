plt.errorbar(x,y,yerr=,fmt=)

yerr:误差范围

### 基本误差图
```python
x = np.linspace(0, 10, 50)
dy = 0.5

y= np.sin(x) + dy*np.random.randn(50)

plt.errorbar(x, y, yerr=dy, fmt='+b')
```

### 柱形图中的误差图

关键字参数yerr=

```
yerrs = (2, 3, 4, 1, 2)

x = np.arange(1, 6)
plt.bar(x, 2*x, align ='center', width=0.5, alpha=0.5, color='yellow', edgecolor='red', yerr=yerrs)
plt.tick_params(axis='both', labelsize=13)
```