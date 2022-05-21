条件为真，执行语句；条件为假，while循环结束

while 判断条件:

	执行语句

### while与风向标

```python
albert_age = 18
flag = True
while flag:
	guess = int(input(">>:"))
	if guess > albert_age:
		print("猜大了")
	elif guess < albert_age:
		print("猜小了")
	else:
		print("猜对了")
		flag = False  #当诉求得到满足时，改变风向标
```
```python
flag = True
while flag:
	pass
	while flag:
		pass
		while flag:
			flag = False  #循环逐层判断，当flag为False时，循环会逐层退出。
```
### 循环控制

break结束整个循环

continue结束本次循环 

```python
albert_age = 18
#猜数字，使用break，不需要风向标了。
while True:
	guess = int(input(">>:"))
	if guess > albert_age:
		print("猜大了")
	elif guess < albert_age:
		print("猜小了")
	else:
		print("猜对了")
		break  #当诉求得到满足时，跳出循环
```
while与else配合
```python
如果while循环全部执行完毕，没有被break终止，则执行else块。
count = 0
while count <= 5:
	count += 1
	print('Loop',count)  #没有break，正常执行
else:
	print('循环正常执行完')