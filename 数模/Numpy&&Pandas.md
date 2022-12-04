# Numpy&&Pandas

## Numpy

### Numpy属性

```python
array = np.array([[1, 2, 3],
                  [2, 3, 4]])

print(array)
print("number of dim:", array.ndim)  # 输出维数
print("shape:", array.shape)  # 输出行列数(形状)
print("size:",array.size)  # 输出大小
```

```python
[[1 2 3]
 [2 3 4]]
number of dim: 2
shape: (2, 3)
size: 6
```



### array与矩阵

```python
a = np.array([[2, 23, 4],
              [1, 3, 4]], dtype=np.float64)  # dtype设置数据类型
print("a=\n",a)
print(a.dtype)

b = np.zeros((4, 4))  # 生成零矩阵
print("b=\n", b)

c = np.ones((3, 4), dtype=np.int64)  # 生成一矩阵
print("c=\n", c)

d = np.arange(10, 20, 2)  # 生成一个序列 第三个值是步长
print("d=\n", d)

e = np.arange(12).reshape((3, 4))  # 生成从0到11的数列 再进行reshape成矩阵形式
print("e=\n", e)

f = np.linspace(1,10,5)  # 生成一个线段 第三个值是划分的区间数 --> 可自动计算出步长
print("f=\n",f)
```

```python
a=
 [[ 2. 23.  4.]
 [ 1.  3.  4.]]
float64
b=
 [[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
c=
 [[1 1 1 1]
 [1 1 1 1]
 [1 1 1 1]]
d=
 [10 12 14 16 18]
e=
 [[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
f=
 [ 1.    3.25  5.5   7.75 10.  ]
```



### Numpy基础运算

```python
a = np.array([10, 20, 30, 40])
b = np.arange(4)
c = a + b

print("c=\n", c)  # 矩阵加法运算

d = b ** 2
print("d=\n", d)  # 计算次方

print("b==3 :\n", b == 3)  # 输出

print('\n')

# 矩阵乘法运算
e = np.arange(4).reshape((2, 2))
f = np.array([[1, 1],
              [0, 1]])

g = e * f  # 对应元素相乘
g_dot = np.dot(e, f)  # 线性代数的运算结果
g_dot_2 = e.dot(f)  # 线性代数运算结果(形式2)

print("g=\n", g)
print("g_dot=\n", g_dot)

print('\n')

h = np.random.random((2, 4))  # 随机生成2行4列的数字矩阵
print("h=\n", h)
print("h_sum=\n",np.sum(h))  # 求和
print("h_sum_axis_0=\n",np.sum(h,axis=0))  # axis=0时是列方向求和
print("h_sum_axis_1=\n",np.sum(h,axis=1))  # axis=1时是行方向求和
print("h_max=\n",np.max(h))  # 取最大值 最小值同
```

```python
c=
 [10 21 32 43]
d=
 [0 1 4 9]
b==3 :
 [False False False  True]


g=
 [[0 1]
 [0 3]]
g_dot=
 [[0 1]
 [2 5]]


h=
 [[0.26129464 0.94204984 0.65042524 0.36467811]
 [0.64557583 0.4527813  0.76753195 0.27361134]]
h_sum=
 4.35794824861742
h_sum_axis_0=
 [0.90687047 1.39483114 1.41795719 0.63828945]
h_sum_axis_1=
 [2.21844783 2.13950042]
h_max=
 0.9420498361489045
```



### Numpy基础运算(2)

```python
a = np.arange(2, 14).reshape((3, 4))
print("a=\n", a)

print("argmin=\n", np.argmin(a))  # 求出矩阵最小值索引
print("argmax=\n", np.argmax(a))  # 求出矩阵最大值索引

print("mean=\n", np.mean(a))  # 求出平均值(推荐)
print("average=\n", np.average(a))  # 求出平均值

print("median=\n", np.median(a))  # 求出中位数

print("cumsum=\n", np.cumsum(a))  # 累加(类似斐波那契数列)
print("diff=\n", np.diff(a))  # 累差

print("nonzeros=\n", np.nonzero(a))  # 输出非零数的索引

print("\n")

b = np.arange(14, 2, -1).reshape((3, 4))
print("b=\n", b)
print("b_sort=\n", np.sort(b))  # 每一行进行排序
print("transpose=\n", np.transpose(b))  # 转置 行变列 列变行

print("clip=\n", np.clip(b, 5, 9))  # 小于5变为5 大于9变为9 (截断)
```

```python
a=
 [[ 2  3  4  5]
 [ 6  7  8  9]
 [10 11 12 13]]
argmin=
 0
argmax=
 11
mean=
 7.5
average=
 7.5
median=
 7.5
cumsum=
 [ 2  5  9 14 20 27 35 44 54 65 77 90]
diff=
 [[1 1 1]
 [1 1 1]
 [1 1 1]]
nonzeros=
 (array([0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2], dtype=int64), array([0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3], dtype=int64))


b=
 [[14 13 12 11]
 [10  9  8  7]
 [ 6  5  4  3]]
b_sort=
 [[11 12 13 14]
 [ 7  8  9 10]
 [ 3  4  5  6]]
transpose=
 [[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
clip=
 [[9 9 9 9]
 [9 9 8 7]
 [6 5 5 5]]
```

