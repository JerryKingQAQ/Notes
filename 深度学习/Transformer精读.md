# Transformer精读

## 特点

- 第一个完全使用attention机制的encoder-decoder结构模型



## Encoder-Decoder

encoder将输入的词转化为机器学习可以理解的向量

decoder将向量转化为词

auto-regressive：自回归 输出t-1作为输出t的输入



## LayerNormal

每一行做成均值为0 方差为1

![image-20230311151439436](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230311151439436.png)



## Attention

- Q：query
- K：key
- V：value

 将Source中的构成元素想象成是由一系列的<Key,Value>数据对构成，此时给定Target中的某个元素Query，通过计算Query和各个Key的相似性或者相关性，得到每个Key对应Value的权重系数，然后对Value进行加权求和，即得到了最终的Attention数值。所以本质上Attention机制是对Source中元素的Value值进行加权求和，而Query和Key用来计算对应Value的权重系数。

![image-20230311152704274](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230311152704274.png)



![image-20230311153507893](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230311153507893.png)

自注意力机制：K V Q 都是自己本身 复制三次进入模型



![image-20230311154839073](C:\Users\Jerry\AppData\Roaming\Typora\typora-user-images\image-20230311154839073.png)

\1. Transformer为何使用多头注意力机制？（为什么不使用一个头）
2.Transformer为什么Q和K使用不同的权重矩阵生成，为何不能使用同一个值进行自身的点乘？ （注意和第一个问题的区别）
3.Transformer计算attention的时候为何选择点乘而不是加法？两者计算复杂度和效果上有什么区别？
4.为什么在进行softmax之前需要对attention进行scaled（为什么除以dk的平方根），并使用公式推导进行讲解
5.在计算attention score的时候如何对padding做mask操作？
6.为什么在进行多头注意力的时候需要对每个head进行降维？（可以参考上面一个问题）
7.大概讲一下Transformer的Encoder模块？
8.为何在获取输入词向量之后需要对矩阵乘以embedding size的开方？意义是什么？
9.简单介绍一下Transformer的位置编码？有什么意义和优缺点？
10.你还了解哪些关于位置编码的技术，各自的优缺点是什么？
11.简单讲一下Transformer中的残差结构以及意义。
12.为什么transformer块使用LayerNorm而不是BatchNorm？LayerNorm 在Transformer的位置是哪里？
13.简答讲一下BatchNorm技术，以及它的优缺点。
14.简单描述一下Transformer中的前馈神经网络？使用了什么激活函数？相关优缺点？
15.Encoder端和Decoder端是如何进行交互的？（在这里可以问一下关于seq2seq的attention知识）
16.Decoder阶段的多头自注意力和encoder的多头自注意力有什么区别？（为什么需要decoder自注意力需要进行 sequence mask)
17.Transformer的并行化提现在哪个地方？Decoder端可以做并行化吗？
19.Transformer训练的时候学习率是如何设定的？Dropout是如何设定的，位置在哪里？Dropout 在测试的需要有什么需要注意的吗？
20解码端的残差结构有没有把后续未被看见的mask信息添加进来，造成信息的泄露。



\1. 每个头对应一套Wq、Wk、Wv参数矩阵，对应q、k、v的一个表征空间，用多头能在多个表征空间进行attention，提取多种patten信息，提高泛化能力。
\2. 如果不用参数矩阵，直接用Q和K点乘，那么attention的过程就是一个确定性的过程，没有任何需要学习的参数，表达能力和泛化能力有限。
\3. 点乘是全矩阵运算，可以并行化；加法通常需要一个FFN来计算相似性。二者复杂度差不多，但是点乘由于可以利用高效矩阵运算速度更快。
\4. 当维度很大时，点乘之后的结果数据量级很大。对于softmax函数而言，一旦输入很大，会进入函数的饱和区，梯度值很小。因而需要scaled。如果输入q和k各自都是均值为0，方差为1的分布，q与k的点积将是均值为0，方差为dk，为了将其方差控制在1，需要除以dk的平方根。
\5. 在decoder的mask multi-head attention，即第一个attention模块做mask操作。具体方法：对k向量第t步以后的值在进入softmax之前置一个非常大的负数，在进入softmax之后这个负数对应的位置会变成0，即对应的权重变成0，从而对应的v不会参与计算。之所以不在softmax之后直接置0，是为了保证权重和为1。
\6. 多头的输出最后会concat到一起继续进行下一层的运算。为了保证concat后输出维度不变，每个head的维度都是d_model / h。
\7. 包含6个相同的block。每个block包含两个sublayer：多头自注意力机制+position-wise的FFN。每个sublayer都采用了残差连接和layernorm。
9、attention机制没有考虑序列的顺序信息因而有信息损失。位置编码通过在attention的输入中增加位置的emedding信息来考虑序列的顺序信息。具体方式：将当前位置的输入单词embedding和位置序号的embedding相加，结果进入attention。