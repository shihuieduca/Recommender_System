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





