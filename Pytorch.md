# Pytorch

## 基本的函数、工具包

- nn.functional中函数与nn.Module中的layer的主要区别是后者继承Module类，会自动提取可学习的参数。而nn.functional更像是纯函数。

```python
import numpy as np
import torch
# 导入 pytorch 内置的 mnist 数据
from torchvision.datasets import mnist 
#导入预处理模块
import torchvision.transforms as transforms
from torch.utils.data import DataLoader
#导入nn及优化器
import torch.nn.functional as F
import torch.optim as optim
from torch import nn

#定义预处理函数，这些预处理依次放在Compose函数中。
transform = transforms.Compose([transforms.ToTensor(),transforms.Normalize([0.5], [0.5])])
```

- transforms.Compose可以把一些转换函数组合在一起；



## 定义网络

一般网络框架图

![img](https://gitee.com/Lighters_c/picgo-bed/raw/master/897d6f01d379942106da1e6670e0a363.png)



```python
class Net(torch.nn.Module):
    def __init__(self):
        super(Net4, self).__init__()
        self.conv = torch.nn.Sequential(
            OrderedDict(
                [
                    ("conv1", torch.nn.Conv2d(3, 32, 3, 1, 1)),
                    ("relu1", torch.nn.ReLU()),
                    ("pool", torch.nn.MaxPool2d(2))
                ]
            ))
 
        self.dense = torch.nn.Sequential(
            OrderedDict([
                ("dense1", torch.nn.Linear(32 * 3 * 3, 128)),
                ("relu2", torch.nn.ReLU()),
                ("dense2", torch.nn.Linear(128, 10))
            ])
        )
```

如果要对每层定义一个名称，我们可以采用Sequential的一种改进方法，在Sequential的基础上，通过add_module()添加每一层，并且为每一层增加一个单独的名字。

==反向传播的实现==

- Pytorch提供了自动反向传播的功能，使用nn工具箱,我们无需自己编写反向传播，直接让损失函数(loss)调用backward()即可，非常方便和高效！

### nn.Module

nn.Module可以是神经网络的某个层(layer),也可以是包含多层的神经网络。在实际使用中，最常见的做法是继承nn.Module，生成自己的网络/层；nn中已实现了绝大多数层，包括==全连接层、损失层、激活层、卷积层、循环层==等等，这些层都是nn.Module的子类，能够自动检测到自己的Parameter，并将其作为学习参数



### nn.functional

总的来说，两种功能都是相同的，但PyTorch官方推荐：具有学习参数的（例如，conv2d, linear, batch_norm)采用nn.Xxx方式。没有学习参数的（例如，maxpool, loss func, activation func）等根据个人选择使用nn.functional.xxx或者nn.Xxx方式。



## 训练模型

层、模型、损失函数和优化器等都定义或创建好，接下来就是训练模型。

训练模型时需要注意使模型处于训练模式，即调用 `model.train()` 。调用 `model.train()` 会把所有的module设置为训练模式。如果是测试或验证阶段，需要使模型处于验证阶段，即调用 `model.eval()` 。调用 `model.eval()` 会把所有的training属性设置为False。

缺省情况下梯度是累加的，需要手工把梯度初始化或清零，调用optimizer.zero_grad()即可。训练过程中，正向传播生成网络的输出，计算输出和实际值之间的损失值。 调用loss.backward()自动生成梯度，然后使用 ==optimizer.step()== 执行优化器，把梯度传播回每个网络。



## 优化器

使用优化器的一般步骤为：

1. 建立优化器实例

   ```python
   import torch.optim as optim
   optimizer = optim.SGD(model.parameters(), lr=lr, momentum=momentum)
   ```

2. 向前传播

```python
out = model(img)
loss = criterion(out, label)
```

3. 清空梯度

```python
optimizer.zero_grad()
```

4. 反向传播

```python
loss.backward()
```

5. 更新参数

```python
optimizer.step()
```

