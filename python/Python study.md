# Python study

[TOC]

#### pass 语句

作用：一般用来填充语法空白

```python
if x >= 0:
    pass
else:
	x = -x #求绝对值
```

#### if 语句实现北京出租车计价器功能

```python
# 1. 北京出租车计价器
#     收费标准:
#       1. 3公里以内收费 13元
#       2. 基本单价 2.3 元/公里(超过3公里以外)
#       3. 空驶费: 超过15公里后,每公里加收单价的50%空驶费
#          (即3.45元/公里)
#     要求: 输入公里数,打印出费用金额(以元为单位精确到分)
# if 语句

ps = input("该文件为：北京出租车计价器（请按任意键开始计算）")
x = int(input("请输入您乘坐里程："))
if x <= 3:
    print("您需要支付的费用为：", 13)
elif 3 < x <= 15:
    price = 13 + (x - 3) * 2.3
    print("您需要支付的费用为：", price)

else:
    price = 13 + (x - 3) * 2.3 + x  * 3.45
    print("您需要支付的费用为：", price)


```

#### 求三个值的最大值，最小值，平均值

```python
# 2. 输入三个任意的数:
#     1) 打印出最大数是多少?
#     2) 打印出最小数是多少?
#     3) 打印出三个数的平均值是多少?

ps = input("该文件为：求三个数的最大值，最小值&平均值（请按任意键开始计算）")
x = int(input("请输入第一个数字："))
y = int(input("请输入第二个数字："))
z = int(input("请输入第三个数字："))

max = x
min = x
if y > max:
    max = y
else:
    min = y

if z > max:
    max = z
else:
    min = z
mean = (x + y + z) / 3
print("最大值为：", max)
print("最小值为：", min)
print("平均值值为：", mean)



```

#### BMI 计算

```python
#    BMI指数(Body Mass Index) 又称身体质量指数
#     BMI计算公式:  BMI = 体重(公斤) / 身高的平方(米)
#     如:  一个69公斤的人,身高是173厘米 则BMI如下:
#        BMI = 69 / 1.73 ** 2    得23.05
#     标准表:
#       BMI < 18.5       体重过轻
#       18.5 <= BMI < 24 正常范围
#       BMI >= 24        体重过重
#     输入身高和体重,打印出BMI值,并打印体重状况

ps = input("该文件为：BMI指数的计算（请按enter键开始计算）")
weight = input("请输入体重（公斤）：")
high = input("请输入身高（米）：")
BMI = float(weight) / float(high) ** 2
print("BMI指数为：", BMI)
```

## LINUX 上的 `Shebang` 符号(`#!`)

- `#!`这个符号叫做 `Shebang` 或者 `Sha-bang`
- `Shebang` 通常在 `Unix` 系统脚本的中 **第一行开头** 使用
- 指明 **执行这个脚本文件** 的 **解释程序**

### 使用 Shebang 的步骤

- 1. 使用 `which` 查询 `python3` 解释器所在路径

```bash
$ which python3
```

- 2. 修改要运行的 **主 python 文件**，在第一行增加以下内容

```python
#! /usr/bin/python3
```

- 3. 修改 **主 python 文件** 的文件权限，增加执行权限

```bash
$ chmod +x cards_main.py
```

- 4. 在需要时执行程序即可

```bash
./cards_main.py
```

