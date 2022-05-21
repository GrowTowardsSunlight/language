python处理时间的模块

[time和calendar ](https://www.runoob.com/python3/python3-date-time.html)

### time sleep()

推迟调用线程的运行,参数以秒为单位
```python
time.sleep(1)  #进程挂起1秒
```
### 获取现在的时间

```
time.localtime()    #本地时间
time.gmtime()       #UTC世界统一时间
time.ctime()        #直观的获得本地时间，格式化输出
```
```python
import time

t_local = time.localtime()
t_UTC = time.gmtime()
print('t_local', t_local)    #本地时间
print('t_UTC', t_UTC)        #UTC世界统一时间
print(time.ctime())
```
```
t_local time.struct_time(tm_year=2020, tm_mon=2, tm_mday=20, tm_hour=17, tm_min=13, tm_sec=50, tm_wday=3, tm_yday=51, tm_isdst=0)
t_UTC time.struct_time(tm_year=2020, tm_mon=2, tm_mday=20, tm_hour=9, tm_min=13, tm_sec=50, tm_wday=3, tm_yday=51, tm_isdst=0)
Thu Feb 20 18:05:45 2020
```
年月日，小时，分，秒，周几(0为周一，6为周日)，一年的第几天，是否为夏令时。

### 时间戳与计时器

时间戳：有固定的计时起点，现在的时间与起点的差值就是一个时间戳。

获得时间戳的方法
```python
time.time()     #返回自纪元以来的秒数，记录sleep。
time.perf_counter()     #随机选取一个时间计时起点 ，记录现在时间到该时间点的间隔秒数,记录sleep的时间。
time.process_time()     #随机选取一个时间计时起点，记录现在时间到该时间点的间隔秒数,不记录sleep的时间，会把sleep的时间去掉
```
perf_counter()精度较time()更高一些，但一般time的精度已经够用了。

两个计时起点相同的时间戳之间的差值就实现了计时的功能。
```python
t_1_start = time.time()
t_2_start = time.perf_counter()
t_3_start = time.process_time()
print(t_1_start)
print(t_2_start)
print(t_3_start)

res = 0
for i in range(1000000):
    res += i

time.sleep(5)

t_1_end = time.time()
t_2_end = time.perf_counter()
t_3_end = time.process_time()

print('time方法:{:.3f}秒'.format(t_1_end - t_1_start))
print('perf_counter方法:{:.3f}秒'.format(t_2_end - t_2_start))
print('process_time方法:{:.3f}秒'.format(t_3_end - t_3_start))
```
```
1582194703.463341
24214.344425253
3.85562
time方法5.111秒
perf_counter方法5.111秒
process_time方法:0.109秒
```

### 自定义格式化输出

time.strftime

%Y年，%m月，%d月份中的号，%A星期几，%H小时，%M分钟，%S秒钟
```python
lctime = time.localtime()
time.strftime('%Y-%m-%d %A %H:%M:%S', lctime)
```
```
'2020-02-20 Thursday 18:44:15'
```
