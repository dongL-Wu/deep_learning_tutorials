# 数据操作

为了能够完成各种数据操作，我们需要某种方法来存储和操作数据。通常包括两件重要的事：
获取数据 和 数据计算。


## 创建数据及数据运算

tensor 初始化可以利用相关函数，例如`torch.ones()`、 `torch.zeros()`、`torch.randn()`

查看tensor的形状有以下几种方法:

```pytorch
x = torch.arange(12)
print(x.shape)
print(x.size())

# 输出tensor 元素的总数
print(x.numel())
```



数据运算一般是按元素进行运算，包括加、减、乘、除以及幂运算等等。




### 不同对象转换

主要针对numpy 和tensor 的互相转化

```pytorch
A = x.numpy()
B = torch.tensor(A)
```

如果要将大小为1的tensor 转化为 python 标量， 我们可以调用item 函数 或者python 内置函数。

```pytorch
a = torch.tensor([3.5])
a, a.item(), float(a), int(a)

```

## 广播机制

一般来说都是在形状相同的tensor 上进行运算。如果在形状不同的情况下，我们是可以通过**广播机制**来进行按元素操作。流程如下：

1. 通过适当复制元素来扩展一个或者两个数组，保证tensor 形状相同；
2. 对生成的数组执行按元素操作；

`在大多数情况下，沿着数组中长度为1的轴进行传播。在下面的例子中， a 按列进行复制， b 按行进行复制 `

```pytorch

import torch

a = torch.arange(3).reshape(3, 1)
b = torch.arange(2).reshape(1, 2)

c = a + b

```



## 索引和切片

tensor 中的元素可以通过索引访问， **需要注意 `[]` 里的格式**。 如果不是单一维度时，在`[]` 中用 逗号隔开(不需要像C++ 中用多个`[]`)。

```pytorch
import torch
x = torch.arange(12).reshape(3,4)

print(x[-1])
print(x[1:3])

# 打印第一行和第二行数据
print(x[0:2, :])

```


### 节省内存

运行一些操作可能会导致为新结果分配内存， 例如`Y = X + Y`中，`Y` 将指向新分配的内存处的张量。
使用切片法可以将操作结果分配给先前的数组， 例如Y[:] = <expression>.

```pytorch
Z = torch.zeros_like(Y)
print('id(Z):', id(Z))
Z[:] = X + Y
print('id(Z):', id(Z))

```

## 常见function

* sum()

    * function: 对tensor 所有元素求和，并返回tensor(单个数)

* mean()

    * function: 对tensor 所有元素求均值，并返回tensor(单个数)

