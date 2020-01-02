# python的数据类型和变量

## python关键字（略）

​	python中有一些关键字，自己设置变量的时候不要用他们

## 变量的定义与赋值

1. python不需要为变量指定数据类型，赋值的时候自动指定类型  

2. python中字符串用引号标起来  

## input()函数

从**键盘输入**的时候要用到input()  

用两个案例来说明input的用法    

1. 和100比大小  
   首先，本案例使用Vim编辑文本  

```
vim testhundred.py
```

进入vim后按**i**进步编辑模式。输入代码  

```python
number = int(input("请输入整数"))
if number <= 100:
		print("数字小于等于100")
else:
		print("数字大于100")
```

按**ESC**并输入 **:wq** 退出vim  
在Linux中，给文件添加可执行权限  

```
chmod +x testhundred.py
```

运行程序  

```
./testhundred.py
```

2. 求利息  
   vim编辑

```
vim investment.py
```

进入vim后按**i**进入编辑模式。输入代码  

```python
amount = float(input("输入金额"))
inrate = float(input("输入利率"))
period = float(input("输入期数"))
value = 0
year = 1
while year <= period:
		value = amount * (1 + inrate)
		print("年数{}总额{:.2f}".format(year,value))
		amount = value
		year = year + 1
```

```
chmod +x investment.py
```

```
./investment.py
```

## python字符串的格式化  

用 **{}**

```python
{:5d}
```

表示5个字符宽度的整数（字符宽度包括小数点，宽度不足用空格补足）

```python
{:7.2f}
```

表示7个字符宽度，而且是浮点数（2f表示到小数点后两位，小数点占一位宽度）  

## 单行定义多个变量或赋值  

利用了元组（tuple），用 **,** 逗号间隔就能创建元组（不需要括号）  
只有当你想用一个变量表示一个元组的时候，才需要用括号  
**示例**  

```python
a , b = 1 , 2
#以上应该理解为，1,2这个元组赋值给了a,b这个元组
#这也说明不可以使用a,b=1,c来表示三个元素的元组
#因此本例中 a = 1     b = 2
```

另外我们可以用一个变量表示一个元组，**示例2**  

```python
date = ("yechenyang", "25", "male")
name, age, 性别 = date
```

则name会被赋值为yechenyang，依此类推

