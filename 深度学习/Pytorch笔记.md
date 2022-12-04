# Pytorch笔记

## 基础知识

```
dir()  # 打开，看见
help()  #说明书
```



### Tensor

张量，矩阵形式。同时包装了神经网络所需要的理论基础参数 



### Pytorch两个类

#### Dataset

**作用：**将数据进行分类以及编号。

提供一种方式去获取数据及其label。

- 如何获取每一个数据及其label
- 告诉我们总共有多少数据



继承重载Dataset类

```python
from torch.utils.data import Dataset
from PIL import Image
import os


class MyData(Dataset):
    # 初始化类
    def __init__(self, root_dir, label_dir):
        self.root_dir = root_dir  # self相当于类的全局变量
        self.label_dir = label_dir
        self.path = os.path.join(self.root_dir, self.label_dir)  # 字符串拼接
        self.img_index = os.listdir(self.path)  # 获得path路径下的索引

    # 获取类中item
    def __getitem__(self, idx):
        img_name = self.img_index[idx]  # 获取索引的名称
        img_item_path = os.path.join(self.root_dir, self.label_dir, img_name)  # 组成完整路径
        img = Image.open(img_item_path)
        label = self.label_dir

        return img, label

    def __len__(self):
        return len(self.img_index)  # 返回索引长度


root_dir = "hymenoptera_data/train"
ants_label_dir = "ants"
bees_label_dir = "bees"

ants_dataset = MyData(root_dir, ants_label_dir)
bees_dataset = MyData(root_dir, bees_label_dir)
train_dataset = ants_dataset + bees_dataset

img, label = bees_dataset[0]  # python类的特殊方法 内置的__getitem__使其可以这样返回
img.show()
```



#### Dataloader

**作用：**对后面的网络提供不同的数据形式



### TensorBoard

#### 打开写入数据

```python
from torch.utils.tensorboard import SummaryWriter

writer = SummaryWriter("logs")  # 创建实例  比如事件文件夹

# writer.add_image()
for i in range(100):
    writer.add_scalar("y=3x", 3*i, i)  # 标量、数


writer.close()
```

在终端中输入进入tensorboard  port更改端口

```
tensorboard --logdir logs --port 6007
```



#### 打开图片数据

```python
#  使用numpy.array数据类型
writer = SummaryWriter("logs")  # 创建实例  比如事件文件
image_path = "hymenoptera_data/train/ants/6743948_2b8c096dda.jpg"
img_PIL = Image.open(image_path)
img_array = np.array(img_PIL)  # 将PIL image数据转换为numpy.array数据类型

writer.add_image("test", img_array, 1, dataformats='HWC')  # add_image对输入数据有要求 也要注意dataformats形式 使用nparray
```

```python
#  使用Tensor数据类型 使用TransForm先进行转换
from PIL import Image
from torch.utils.tensorboard import SummaryWriter
from torchvision import transforms


img_path = "hymenoptera_data/train/ants/7759525_1363d24e88.jpg"
img = Image.open(img_path)

writer = SummaryWriter("logs")

tensor_trans = transforms.ToTensor()  # 返回一个ToTensor的对象 实例化
tensor_img = tensor_trans(img)

writer.add_image("Tensor_img", tensor_img)

writer.close()
```



### TransForm

对图片进行操作的一个库



#### 实例化 ToTensor

使用ToTensor方法

```python
from PIL import Image
from torchvision import transforms

img_path = "hymenoptera_data/train/ants/7759525_1363d24e88.jpg"
img = Image.open(img_path)

tensor_trans = transforms.ToTensor()  # 返回一个ToTensor的对象 实例化 作用如图
tensor_img = tensor_trans(img)  # 使用实例化的对象去完成转换为Tensor的操作
```

| <img src="C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220707221126717.png" alt="image-20220707221126717"  /> | ![image-20220708155958187](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220708155958187.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |



#### 归一化 Normalize

使用Normalize方法

```python
# Normalize
# output[channel] = (input[channel] - mean[channel]) / std[channel]
print(img_tensor[0][0][0])
trans_norm = transforms.Normalize([1, 3, 5], [3, 2, 1])
img_norm = trans_norm(img_tensor)
print(img_norm[0][0][0])

writer.add_image("Normalize", img_norm, 1)
```



#### 变换大小 Resize

Resize the input image to the given size.

```python
# Resize
print(img.size)
trans_resize = transforms.Resize((1024, 20))
img_resize = trans_resize(img)
# img_resize PIL -> Tensor
img_resize = trans_totensor(img_resize)
writer.add_image("Resize", img_resize)
```

##### 等比缩放

使用compose方法可以一次性使用多种方法

```python
# Compose - resize - 2 等比缩放
trans_resize_2 = transforms.Resize(512)
trans_compose = transforms.Compose([trans_resize_2, trans_totensor])  # 使用多种方法
img_resize_2 = trans_compose(img)
writer.add_image("Resize", img_resize_2, 1)
```



#### 随机裁剪 RandomCrop

```python
# RandomCrop
trans_random = transforms.RandomCrop(50) # 使用序列或者数值
trans_compose_2 = transforms.Compose([trans_random, trans_totensor])
for i in range(10):
    img_crop = trans_compose_2(img)
    writer.add_image("RandomCrop", img_crop, i)
```



### Torchvision数据集使用

[torch.utils.data — PyTorch 1.12 documentation](https://pytorch.org/docs/stable/data.html)

#### dataset

dataset相当于初始化数据集

```python
import torchvision
from torch.utils.tensorboard import SummaryWriter

dataset_transform = torchvision.transforms.Compose([
    torchvision.transforms.ToTensor()
])

train_set = torchvision.datasets.CIFAR10(root="./dataset", train=True, transform=dataset_transform, download=True)
test_set = torchvision.datasets.CIFAR10(root="./dataset", train=False, transform=dataset_transform, download=True)

writer = SummaryWriter("CIFAR10")

for i in range(10):
    img, label = test_set[i]
    writer.add_image("CIFAR10", img, i)

writer.close()
```

#### dataloader

将数据集和神经网络建立联系

```python
import torchvision

# 测试集
from torch.utils.data import DataLoader
from torch.utils.tensorboard import SummaryWriter

test_data = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(), )

test_loader = DataLoader(dataset=test_data, batch_size=64, shuffle=True, num_workers=0, drop_last=False)

# 测试数据集中第一张样本
img, target = test_data[0]
# print(img.shape)
# print(target)

writer = SummaryWriter("DataLoader")

for epoch in range(2):
    step = 0
    for data in test_loader:
        imgs, targets = data
        # print(imgs.shape)
        # print(targets)
        writer.add_images("Epoch:{}".format(epoch), imgs, step)
        step = step + 1
```

- 当数据数不能被batch——size整除时，使用drop_last舍弃（防止报错） 


## 神经网络

### 卷积层

| Conv2d参数           |                            |
| -------------------- | -------------------------- |
| in_channels          | 输入通道数                 |
| out_channels         | 输出通道数                 |
| kernel_size          | 卷积核大小                 |
| stride=1             | 卷积的步进大小             |
| padding=0            | 对原始图像设置内边距的大小 |
| dilation=1           | 空洞卷积 可以看文档的动画  |
| groups=1             | 分组卷积                   |
| bias=True            | 偏置                       |
| padding_mode='zeros' | 若有padding 填充的数字     |
| device=None          |                            |

outchannel = 2时，会使用两个卷积核对原始图像进行卷积操作，分别生成两个输出，最后再将两个输出进行叠加。

#### 卷积后的Shape

![image-20220709165339579](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220709165339579.png)

#### 基础的卷积操作

```python
class NN(nn.Module):
    def __init__(self):
        super(NN, self).__init__()
        self.conv1 = Conv2d(in_channels=3, out_channels=3, kernel_size=3, stride=1, padding=0)

    def forward(self, x):
        x = self.conv1(x)
        return x
```



### 池化层

保留特征，减少数据量

#### 最大池化

| Maxpool参数    |                                                              |
| -------------- | ------------------------------------------------------------ |
| kernel_size    | the size of the window to take a max over                    |
| stride         | the stride of the window. Default value is **kernel_size** 默认步长是卷积核大小 |
| padding        | implicit zero padding to be added on both sides              |
| dilation       | a parameter that controls the stride of elements in the window |
| return_indices | if True, will return the max indices along with the outputs. Useful for torch.nn.MaxUnpool2d later |
| ceil_mode      | when True, will use ceil instead of floor to compute the output shape 当卷积核在操作时超过边界，保留最大化操作 |



#### 代码示例

```python
input = torch.tensor([[[1, 2, 0, 3, 1],
                      [0, 1, 2, 3, 1],
                      [1, 2, 1, 0, 0],
                      [5, 2, 3, 1, 1],
                      [2, 1, 0, 1, 1]]], dtype=torch.float32)

torch.reshape(input, (-1, 1, 5, 5))
print(input.shape)


class NN(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.maxpool1 = MaxPool2d(kernel_size=3, ceil_mode=True)

    def forward(self, input):
        output = self.maxpool1(input)
        return output


nerual = NN()
output = nerual(input)
print(output)
```



### 非线性激活

**中心思想：**输入越小时，输出接近0（越小）。输出大时，输出接近1（越大）

为网络引入非线性特征。

#### 代码示例

```python
class NN(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.relu1 = ReLU()  # inplace = false时不会对input进行变换
        self.sigmoid1 = Sigmoid()

    def forward(self, input):
        output = self.sigmoid1(input)
        return output
```



### 线性层(全连接层)

在神经网络中，我们通常用线性层来完成两层神经元间的线性变换。

![在这里插入图片描述](https://img-blog.csdnimg.cn/552592c89de343469fbe39f8eb54f50c.PNG#pic_center)

```python
class NN(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.liner1 = Linear(in_features=196608, out_features=10)  # 线性层的输入与输出

    def forward(self, input):
        output = self.liner1(input)
        return output
```



### 损失函数

通过某些函数计算input和target之间的差值。

#### 代码示例

```python
from torch import nn
loss = nn.CrossEntropyLoss()
result_loss = loss(outputs, targets)
# result_loss.backward() 反向传播可以计算出梯度等
```



### 优化器

通过梯度下降法对参数进行优化。

```python
optim = optim.SGD(nerual.parameters(), lr=0.01)  # 使用随机梯度下降法

for data in dataloader:
    imgs, targets = data
    outputs = nerual(imgs)
    result_loss = loss(outputs, targets)
    optim.zero_grad()  # 把每一个可调节参数的梯度调为0
    result_loss.backward()  # 反向传播计算梯度
    optim.step()  # 对参数进行调优
```



### 一套可训练的神经网络

```python
import torchvision
from torch.utils.data import DataLoader
from torch import nn
from torch.nn import Conv2d, MaxPool2d, Flatten, Linear, Sequential
from torch import optim

dataset = torchvision.datasets.CIFAR10("../dataset", train=False, transform=torchvision.transforms.ToTensor(),
                                       download=True)
dataloader = DataLoader(dataset, batch_size=1)


class UseConv2d(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.model1 = Sequential(  # 使用squential简化代码
            Conv2d(in_channels=3, out_channels=32, kernel_size=5,
                   stride=1, padding=2),
            MaxPool2d(kernel_size=2),
            Conv2d(in_channels=32, out_channels=32, kernel_size=5,
                   stride=1, padding=2),
            MaxPool2d(kernel_size=2),
            Conv2d(in_channels=32, out_channels=64, kernel_size=5,
                   stride=1, padding=2),
            MaxPool2d(kernel_size=2),
            Flatten(),
            Linear(in_features=1024, out_features=64),
            Linear(in_features=64, out_features=10)
        )

    def forward(self, x):
        x = self.model1(x)
        return x


loss = nn.CrossEntropyLoss()
nerual = UseConv2d()
optim = optim.SGD(nerual.parameters(), lr=0.01)  # 使用随机梯度下降法
for epoch in range(20):
    running_loss = 0.0
    for data in dataloader:
        imgs, targets = data
        outputs = nerual(imgs)
        result_loss = loss(outputs, targets)
        print(outputs)
        print(targets)
        optim.zero_grad()  # 把每一个可调节参数的梯度调为0
        result_loss.backward()  # 反向传播计算梯度
        optim.step()  # 对参数进行调优
        running_loss = running_loss + result_loss
    print(running_loss)
```



### 使用已有的网络模型

```python
vgg16_true = torchvision.models.vgg16()

vgg16_true.classifier.add_module('add_linear', nn.Linear(in_features=1000, out_features=10))  # 可以对最后的全连接层修改参数使得接入自己的网络 添加

vgg16_true.classifier[6] = nn.Linear(4096, 10)  # 修改
```



#### 保存和加载

```python
# 保存
vgg16 = torchvision.models.vgg16()

# 保存方式1
torch.save(vgg16, "vgg16_method1.pth")  # 保存模型结构和+参数

# 保存方式2
torch.save(vgg16.state_dict(), "vgg16_method2.pth")  # 将参数保存成字典的形式

#加载
# 方式1 --> 保存方式1，加载模型
import torchvision

model = torch.load("vgg16_method1.pth")
# print(model)

# 方式2 --> 保存方式2，加载参数
vgg16 = torchvision.models.vgg16()
vgg16.load_state_dict(torch.load("vgg16_method2.pth"))
print(model)
```



### 步骤

准备数据

加载数据

准备模型

设置损失函数

设置优化器

开始训练

最后验证

结果聚合展示

![image-20220719191046479](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20220719191046479.png)

### 使用GPU

网络模型，数据（输入，标注），损失函数有cuda方法

```python
# 创建网络模型
nerual_network = UseConv2()
if torch.cuda.is_available():
    nerual_network = nerual_network.cuda()

# 损失函数
loss_fn = nn.CrossEntropyLoss()
if torch.cuda.is_available():
    loss_fn = loss_fn.cuda()

# 数据
imgs, targets = data
    if torch.cuda.is_available():
    imgs = imgs.cuda()
    targets = targets.cuda()
```



## 读入数据

### 图片数据分类

```python
# -*- coding = utf-8 -*-
# @File : rename.py
# @Software : PyCharm

import csv
import os
import shutil


def copyfile(src, des):
    for file in os.listdir(src):
        # 遍历源文件夹中的文件
        full_file_name = os.path.join(src, file)
        result_file_name = os.path.join(des, file)
        print("要被复制的文件全名:", full_file_name)
        # 开始复制
        shutil.copyfile(full_file_name, result_file_name)


with open("./CASME2 label.CSV", mode="r") as f:
    reader = csv.reader(f, delimiter=";")
    header = next(reader)

    pos_dir = os.path.join('test', 'positive')
    neg_dir = os.path.join('test', 'negative')
    sur_dir = os.path.join('test', 'surprise')
    oth_dir = os.path.join('test', 'others')

    for row in reader:
        print("{}:{}, {}:{}, {}:{}".format(
            header[0], row[0],
            header[1], row[1],
            header[2], row[2],
        ))

        file_dir = os.path.join(row[0], row[1])

        if row[2] == 'positive':
            copyfile(file_dir, pos_dir)
        elif row[2] == 'negative':
            copyfile(file_dir, neg_dir)
        elif row[2] == 'surprise':
            copyfile(file_dir, sur_dir)
        else:
            copyfile(file_dir, oth_dir)
```



### 改变通道维度

```python
# [C x H x W] 改变成 [H × W × C]
plt.imshow(grid.numpy().transpose((1, 2, 0)))  # 0 1 2 分别代表着原来的位置 (1,2,0) 就可以实现转化
```

