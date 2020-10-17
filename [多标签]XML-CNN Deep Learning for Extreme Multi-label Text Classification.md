# Deep Learning for Extreme Multi-label Text Classification
## 背景
### 关于extreme multi-label classification
有多篇文章，有一个很大的label集合，对每一篇文章选取一些label作为标签。

与multi-class classification不同的地方在于，multi-class每篇文章有且只有一个类别。而multi-label每一篇文章可能有多个label，并且label之间并不一点独立，意味着特征空间的维度之间并不完全独立。这一点在进行学习时需要注意。

其次，可选的label的空间极大，导致最终输出是非常稀疏的，这意味着训练数据中每个标签对应的实例也可能很少。

### 以往的工作
以往的multi-label任务都基于传统机器学习方法，主要有两种：
1. 目标标签嵌入：将稀疏的高维的输出向量降维到较低维度。重点在于需要设计一个压缩过程以及解压缩过程。
2. tree based ensemble method：利用树对样本空间进行划分。

### 思索
希望借助深度学习方法来实现此任务。当前有的深度学习的类似任务是multi-class。最终选择借助CNN网络来实现。（实际上和CNN-kim非常类似）

## 模型
### 思路
希望通过卷积来压缩上下文的信息。在已有的词级别的文字embedding上，进行一维卷积操作。其中卷积核大小可变。

卷积结果输入进行了改进的池化层：Dynamic max Pooling。max pooling是提取区域内最显著特征的方法。但由于文本的特性：较长、含义在时间维度上不断变化，在普通max pooling上改进，将输入的m维向量分成p块分别进行max pooling之后拼接，相当于在文本的p个部分分别提取核心属性。既降低维度浓缩了文本，也保留了一定程度上的文本位置信息。

然后输入一个单隐层的全连接网络。特别之处在于，隐层的维度远远小于输入和输出层。由于输出层的维度过大（也就是label的数量），权重矩阵难以训练，于是将其分为两个较小的矩阵进行训练。同时，也可以提高整个模型对于高复杂性任务的表达能力。

loss function改为binary cross-entropy loss+sigmoid。这一选择是实验得到的。
