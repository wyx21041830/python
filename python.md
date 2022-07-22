# 魔法函数

魔法函数可以为你写的类增加一些额外功能，方便使用者理解。举个简单的例子，我们定义一个“人”的类People，当中有属性姓名name、年龄age。让你需要利用sorted函数对一个People的数组进行排序，排序规则是按照name和age同时排序，即name不同时比较name，相同时比较age。由于People类本身不具有比较功能，所以需要自定义，你可以这么定义People类：

```python3
class People(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
        return

    def __str__(self):
        return self.name + ":" + str(self.age)

    def __lt__(self, other):
        return self.name < other.name if self.name != other.name else self.age < other.age


if __name__=="__main__":

    print("\t".join([str(item) for item in sorted([People("abc", 18),
        People("abe", 19), People("abe", 12), People("abc", 17)])]))
```

输出结果：

```python3
abc:17	abc:18	abe:12	abe:19
```

上个例子中的__lt__函数即less than函数，即当比较两个People实例时自动调用。

# 第三方库

Matplotlib 是一个 Python 的 2D绘图库

NumPy是Python科学计算的基础工具包，包括统计学、线性代数、矩阵数学、金融操作等等很多Python数据计算工作库都依赖它。支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。

Pandas是一个用于Python数据分析的库，它的主要作用是进行数据分析。Pandas提供用于进行结构化数据分析的二维的表格型数据结构DataFrame，类似于R中的数据框，能提供类似于数据库中的切片、切块、聚合、选择子集等精细化操作，为数据分析提供了便捷。







# numpy库函数

np.array()  #类似matlab矩阵

```python3
#.array()
a=np.array([[0,1,2],[2,3,4]])
#常见属性：dtype查看数组元素类型和shape查看数组尺寸
print(a.shape)
print(a.dtype)
#常见方法：astype用于转换数组元素的类型和reshape用于转换数组尺寸
a=a.astype(np.double).reshape((2,3))
```

`特殊矩阵`：`zeros`函数生成0矩阵 、`ones`函数生成1矩阵、`empty`函数生成随机元素的矩阵 、`eye`函数生成对角矩阵和`fill`函数对所有矩阵元素进行填充

```python
print(np.zeros(6))
print(np.zeros((2,3)))   #0矩阵  二重括号
print(np.empty((2,3)))  #返回随机元素
print(np.eye(3,dtype=np.uint8))

a=np.empty((3,4),dtype=np.uint8) #对角阵
a.fill(255)
print(a)

[0. 0. 0. 0. 0. 0.]
[[0. 0. 0.]
 [0. 0. 0.]]
[[0. 0. 0.]
 [0. 0. 0.]]
[[1 0 0]
 [0 1 0]
 [0 0 1]]
[[255 255 255 255]
 [255 255 255 255]
 [255 255 255 255]]

```

`随机数值`：`random`函数生成[0,1)的元素 、`randomint`函数生成[low,high)之间的整数元素，`rand函数`生成均匀分布，`randn函数`生成正态分布和`normal`函数生成正态分布的数据



**定长分割：`arange`函数和`linspace`函数都用于生成一个序列****

```python
import numpy as np
print (np.arange(5)) #生成[0,5)的序列 默认步长为1
print(np.arange(5,11))# 生成[5,11)的序列
print(np.arange(5,11,2))#生成[5,11)的序列 步长为2
print(np.arange(5.5,11,1.5))#支持浮点数
print(np.arange(3,15).reshape(3,4))


print(np.linspace(0,5,6)) #0到5之间返回6个等距数值. matlab相同
print(np.linspace(0,5,6,endpoint=False)) #0到5之间返回6个等距数值 右开
```

`重复构造`：`repeat`函数用于重复数组元素 和`tile`函数用于重复数组







# 绘图：plot

## matplotlib库

import matplotlib.pyplot as plt

```python

import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(-1, 1, 50) # [-1, 1]内均匀取50个点
y1 = 2 * x + 1
y2 = x ** 2
plt.figure()
plt.plot(x, y1) # 以x为横坐标，y为纵坐标作图，直线/平滑曲线连接
plt.scatter(x, y2) # 散点图   
plt.show() # 显示图

```

![image-20220711130740438](C:\Users\86172\AppData\Roaming\Typora\typora-user-images\image-20220711130740438.png)

## 细节

```python
import matplotlib.pyplot as plt
x = np.linspace(-1, 1, 50) # [-1, 1]内均匀取50个点  
y1 = 2 * x + 1
y2 = x ** 2
#中文
plt.rcParams['font.sans-serif']=['SimHei']
plt.rcParams['axes.unicode_minus'] = False
plt.figure()
#标题
plt.title("标题")
#标签 label
plt.plot(x,y1,label="曲线1")

plt.plot(x,y1,'.',label="曲线2")  # '.'  的散点图   也可用‘*’  ‘o’

plt.plot(x,y2,label="曲线3")
#横纵坐标
plt.xlabel("横坐标")
plt.ylabel("纵坐标")
#legend  图例  依次
#plt.legend("1" "2" "3")  不行#不能直接加逗号
plt.legend(["1", "2" ,"3"])
plt.grid () #显示网格
plt.show()


```

![image-20220711132938767](C:\Users\86172\AppData\Roaming\Typora\typora-user-images\image-20220711132938767.png)

# numda函数

定义f=lamba   形参1,形参2：  表达式

调用： f(实参1，实参2)

```python
def calc(x,y):
    return x**y
#换成匿名函数
calc = lambda x,y:x**y
print(calc(2,5))

def calc(x,y):
    if x > y:
        return x*y
    else:
        return x / y
#三元运算换成匿名函数
calc = lambda x,y:x * y if x > y else x / y
print(calc(2,5))

```

