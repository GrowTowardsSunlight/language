for 元素 in 可迭代对象:
	执行语句		#从可迭代对象中，依次取出每个元素，并进行相应的操作。


### 迭代对象

- 直接迭代

for i in 列表、元组、集合、字符串

- 变换迭代

for key,value in 字典.item():

for i in 字典.keys():  #等价于 for i in 字典：

for i in 字典.values():

- range()

range(start, stop, step) 

必须有结束位置，但不包括结束位置。起始位置默认为0，步长默认为1

### 循环控制

break结束整个循环

continue结束本次循环

for与else的配合
```python
如果for循环全部执行完毕，没有被break终止，则执行else块。
products_scores = [89,90,99,76,67,78,85,92,77,82]
#如果低于75分的产品超过2个，则该组产品不合格
i= 0
for score in products_scores:
		if score <75:
			i+=1
		if i == 2:
			print('产品抽检不合格')
			break
else:
	print('产品抽验合格')