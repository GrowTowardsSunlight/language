### 格式

plt.scatter(x, y, marker,markersize,color,cmap,alpha)

关键字参数都是可选项。

marker:点的形状[[注](https://matplotlib.org/api/markers_api.html#module-matplotlib.markers)]

markersize:点的大小，缩写为s

color:点的颜色，缩写为c

cmap:只有c是浮点数数组时，才能使用cmap,根据c的值来映射颜色，不同的值映射到不同的颜色。

alpha:透明度,默认为1，0为完全透明。比1大时和1效果一样，都是完全不透明。


🌰栗子

#### 根据数据映射颜色
```python
x = np.linspace(0, 10, 100)
y = x**2
plt.scatter(x, y, c= y, cmap='inferno')
plt.colorbar()
```

#### 根据数据控制点的大小
```python
x,y,color,size = (np.random.rand(100) for i in range(4))
plt.scatter(x, y, c=color, s=100*size, cmap='viridis',alpha=0.3)
```

#### 随机漫步

数据点移动若干次的轨迹

```python
from random import choice
# -*- coding: utf-8 -*-
class RandomWalk():
  #一个生成随机漫步数据的类
 
    def __init__(self,num_points=5000):
        self.num_points=num_points
        self.x_values=[0]
        self.y_values=[0]
 
    def fill_walk(self):
       #计算随机漫步包含的所有点
 
        while len(self.x_values)<self.num_points:
        #决定前进方向以及沿这个方向前进的距离
            x_direction=choice([-1,1])
            x_distance=choice([0,1,2,3,4])
            x_step=x_direction*x_distance
 
            y_direction=choice([-1,1])
            y_distance=choice([0,1,2,3,4])
            y_step=y_direction*y_distance
 
            #拒绝原地踏步
            if x_step==0 and y_step==0:
                continue
 
            #计算下一个点的x和y值
            next_x=self.x_values[-1]+x_step
            next_y=self.y_values[-1]+y_step
 
            self.x_values.append(next_x)
            self.y_values.append(next_y)
```
```
rw=RandomWalk(10000)
rw.fill_walk()
 
#设置绘图窗口的尺寸
plt.figure(dpi=128,figsize=(12,6))
point_numbers=list(range(rw.num_points))
plt.scatter(rw.x_values,rw.y_values,c=point_numbers,cmap=plt.cm.Blues,s=1)

plt.colorbar()

#突出起点和终点
plt.scatter(0,0,c='green',s=100)
plt.scatter(rw.x_values[-1],rw.y_values[-1],c='red',s=100)

#不设刻度
plt.xticks([])
plt.yticks([])
```
