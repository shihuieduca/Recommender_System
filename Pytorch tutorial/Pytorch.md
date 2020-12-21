### Pytorch

---

- GPU加速
- 自动求导
- 常用网络层



#### All is about Tensor

- How to denote string？

  **One-hot** or **Embedding**（word2vec、glove）



- **Data Type**（常用）

  torch.FloatTensor

  torch.ByteTensor

  torch.IntTensor

  torch.LongTensor

```Python
import torch

a = torch.randn(2, 3)
print(a.type())
# torch.FloatTensor
print(type(a))
# <class 'torch.Tensor'>
print(isinstance(a, torch.FloatTensor))
# True
# 注意：同一个tensor在CPU和GPU上的数据类型是不同的
# data2 = data1.cuda()
# data1是torch.DoubleTensor类型，data2是torch.cuda.DoubleTensor


# Pytorch中的标量表示
torch.tensor(1.)
torch.tensor(1.3)


# dimension为0 获取标量的shape 通常是作为loss
a = torch.tensor(2.2)
print(a.shape)
# torch.Size([])
print(len(a.shape))
# 0
print(a.size())
# torch.Size([])


# dimension为1的向量/张量 通常是作为bias
print(torch.tensor([1.1]))
# tensor([1.1000])
print(torch.tensor([1.1, 2.2]))
# tensor([1.1000, 2.2000])
print(torch.FloatTensor(1))
# tensor([1.4013e-45])
print(torch.FloatTensor(2))
# tensor([1.4013e-45, 0.0000e+00])
data = np.ones(2)
print(data)
# [1. 1.]
print(torch.from_numpy(data))
# tensor([1., 1.], dtype=torch.float64)


# dimension为2的tensor
a = torch.randn(2, 3)
print(a)
# tensor([[ 0.6904,  0.0651,  0.1951],
#         [ 0.1305, -0.4781, -0.3094]])
print(a.shape)
# torch.Size([2, 3])
print(a.size(0))
# 2
print(a.size(1))
# 3
print(a.shape[1])
# 3


# dimension为3的tensor  通常是作为RNN Input Batch
a = torch.rand(1, 2, 3)
print(a)
# tensor([[[0.2623, 0.2000, 0.0821],
#          [0.6272, 0.3985, 0.9047]]])
print(a.shape)
# torch.Size([1, 2, 3])
print(a[0])
# tensor([[0.2623, 0.2000, 0.0821],
        # [0.6272, 0.3985, 0.9047]])
print(list(a.shape))
# [1, 2, 3]

# dimension为4的tensor  通常是作为图片的输入  CNN [b, c, h, w]
a = torch.rand(2, 3, 28, 28)
print(a)
print(a.shape)
# torch.Size([2, 3, 28, 28])
# 2表示图片数量 3表示图片通道 28和28表示图片的长宽

# Mixed
a = torch.rand(2, 3, 28, 28)
print(a.shape)
# torch.Size([2, 3, 28, 28])
print(a.numel())
# number of size
# 4704=2*3*28*28
print(a.dim())
# 相当于len(a.shape)
# 4
a = torch.tensor(1)
print(a)
print(a.dim())
# 0 数字是0维的
```



- 创建Tensor

```Python
import numpy as np
import torch

# Import from numpy
a = np.array([2, 3.3])
print(torch.from_numpy(a))
# tensor([2.0000, 3.3000], dtype=torch.float64)

a = np.ones([2, 3])
print(torch.from_numpy(a))
# tensor([[1., 1., 1.],
#         [1., 1., 1.]], dtype=torch.float64)

# Import from list
a = torch.tensor([2., 3.2])  # 直接加numpy或list
print(a)
# tensor([2.0000, 3.2000])
b = torch.FloatTensor([2., 3.2])  # 尽量少用这种写法
print(b)
# tensor([2.0000, 3.2000])
b = torch.FloatTensor(2, 3)  # 表示维度
print(b)
# tensor([[-1.1889e+29,  7.3008e-43,  2.8026e-45],
#         [ 0.0000e+00,  1.4013e-45,  0.0000e+00]])
c = torch.tensor(([[2., 3.2], [1., 22.369]]))
print(c)
# tensor([[ 2.0000,  3.2000],
#         [ 1.0000, 22.3690]])
# 注：torch.tensor后面只能加现成数据 numpy或list
#    torch.Tensor和torch.FloatTensor类似，后面只能跟shape数据维度

# uninitialized
# 有很大的随机性 不好处理 需要先覆盖 只能当做容器使用

# 随机初始化
a = torch.rand(3, 3)
# 接收shape [0, 1]分布
print(a)
# tensor([[0.3999, 0.3781, 0.6612],
#         [0.6034, 0.0887, 0.1459],
#         [0.7097, 0.3635, 0.1479]])
print(torch.rand_like(a))
# 接收tensor
# tensor([[0.9165, 0.4140, 0.2966],
#         [0.3955, 0.1095, 0.7095],
#         [0.1717, 0.2079, 0.7766]])
print(torch.randint(1, 10, (3, 3)))
# [min, max) 自定义分布
# tensor([[2, 1, 8],
#         [6, 3, 5],
#         [1, 9, 4]])
print(torch.randn(3, 3))
# 正态分布 均值为0 方差为1

print(torch.full([2, 3], 7))
# tensor([[7., 7., 7.],
#         [7., 7., 7.]])
print(torch.full([], 7))
# tensor(7.)  标量
print(torch.full([1], 7))
# tensor([7.]) dimension为1

# 生成等差数列 arange
print(torch.arange(0, 10))
# tensor([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
print(torch.arange(0, 10, 2))
# tensor([0, 2, 4, 6, 8])

# 生成等分 linspace/logspace
print(torch.linspace(0, 10, steps=4))
# tensor([ 0.0000,  3.3333,  6.6667, 10.0000])  从0-4等分切成4份
print(torch.linspace(0, 10, steps=10))
# tensor([ 0.0000,  1.1111,  2.2222,  3.3333,  4.4444,  5.5556,  6.6667,  7.7778,
#          8.8889, 10.0000])
print(torch.linspace(0, 10, steps=11))
# tensor([ 0.,  1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10.])
print(torch.logspace(0, -1, steps=10))
# 10的多少次方
# tensor([1.0000, 0.7743, 0.5995, 0.4642, 0.3594, 0.2783, 0.2154, 0.1668, 0.1292,
#         0.1000])
print(torch.logspace(0, 1, steps=10))
# tensor([ 1.0000,  1.2915,  1.6681,  2.1544,  2.7826,  3.5938,  4.6416,  5.9948,
#          7.7426, 10.0000])

# zeros ones eye
print(torch.ones(3, 3))
# tensor([[1., 1., 1.],
#         [1., 1., 1.],
#         [1., 1., 1.]])
print(torch.zeros(3, 3))
# tensor([[0., 0., 0.],
#         [0., 0., 0.],
#         [0., 0., 0.]])
print(torch.eye(3, 4))
# tensor([[1., 0., 0., 0.],
#         [0., 1., 0., 0.],
#         [0., 0., 1., 0.]])

# 随机打散
print(torch.randperm(10))
# tensor([9, 7, 0, 8, 2, 6, 3, 1, 4, 5])
```



- 索引与切片

```python
import torch

# Indexing
a = torch.rand(4, 3, 28, 28)
print(a[0].shape)
# 索引从0开始
# torch.Size([3, 28, 28])
print(a[0, 0].shape)
# torch.Size([28, 28])
print(a[0, 0, 2, 4])
# 完全索引
# tensor(0.7040)

# 选前/后N个
a = torch.rand(4, 3, 28, 28)
print(a[:2].shape)
# torch.Size([2, 3, 28, 28])
print(a[:2, :1, :, :].shape)
# torch.Size([2, 1, 28, 28])
print(a[:2, 1:, :, :].shape)
# torch.Size([2, 2, 28, 28])
print(a[:2, -1:, :, :].shape)
# torch.Size([2, 1, 28, 28])

# select by steps 隔行采样
a = torch.rand(4, 3, 28, 28)
print(a[:, :, 0:28:2, 0:28:2].shape)
# torch.Size([4, 3, 14, 14])
print(a[:, :, ::2, ::2].shape)
# torch.Size([4, 3, 14, 14])

# select by specific index
a = torch.rand(4, 3, 28, 28)
print(a.shape)
# torch.Size([4, 3, 28, 28])
print(a.index_select(0, torch.tensor([0, 2])).shape)
# torch.Size([2, 3, 28, 28])
print(a.index_select(2, torch.arange(8)).shape)
# torch.Size([4, 3, 8, 28])

# ...表示任意多的维度
a = torch.rand(4, 3, 28, 28)
print(a.shape)
# torch.Size([4, 3, 28, 28])
print(a[...].shape)
# torch.Size([4, 3, 28, 28])
print(a[:, 1, ...].shape)
# torch.Size([4, 28, 28])
print(a[..., :2].shape)
# torch.Size([4, 3, 28, 2])
```





