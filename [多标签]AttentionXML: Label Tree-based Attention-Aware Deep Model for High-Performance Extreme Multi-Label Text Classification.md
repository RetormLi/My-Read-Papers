# Label Tree-based Attention-Aware Deep Model for High-Performance Extreme Multi-Label Text Classification
## 背景
希望能够更好地处理XMTC问题。针对目前深度学习处理XMTC的几种方法：
- 1-vs-All：训练n个二分类器。训练分为此类或者不分为此类
- Embedding-based：特征空间压缩
- Instance or label tree based：每层对数据进行划分，叶结点用二分类器判断label
- Deep learning based methods：各种深度学习
现存表现较好的一些方法，要么无法捕捉文本和标签之间的相似性，要么错误地处理了label的序列性。

作者希望能够用上更为复杂的深度学习方法，比如attention，但又不希望造成巨大的算力和空间负担
## 思路
为了缩减每个深度学习模型的规模，我们利用probabilistic label tree对数据集进行划分。每一次训练对tree的一层的划分进行学习。这样复杂度就会被大大减小。
## PLT
希望将label的分类进行划分，并且划分次数和分块大小可控。于是希望得到一个宽度很大，层数很浅的决策树。
对于一个样本，先生成一个二叉树，每一个分支处用k-Means二聚类得到两个基本等大的分块。在叶结点的处，每个叶节点允许有M个兄弟节点。
然后从底向上递归开始压缩路径。从叶节点的父结点层开始，每log K层压缩一次，压缩H次时直接连接至根节点。这样我们可以得到深度为H+1，每层的分叉树不超过K的树。
我们可以把叶节点当做是否为label的分类器，而每个中间结点都是一个用来划分的伪分类器。我们需要在每一层得到一个分类器，将文本进行划分，预测子树中是否会出现label。如果预测值较小，则直接剪枝。预测到叶结点层，我们就得到了二分类的label预测。
这个预测的过程可以表示为路径上由根到叶是否存在子树有label的条件概率的链式连乘。注意在实际情况下的z值并非是二值的。
## Attention-Aware Deep Model
### 深度模型
- Word Representation Layer：预训练模型的稠密词向量。
- Bidirectional LSTM Layer：上下文表示
- Multi-label Attention：训练每个标签分别对应的不同的attention parameter。和上下文表示线性组合得到attended表示
- Fully Connected and Output Layer：一层或者两层全连接加一层输出层。注意对于一个模型只训练一个此层的参数，在全部attended表示间共享。
- loss function：BCE
### 训练方法
按照PLT自顶向下。先在第一层以全部样本为输入正常训练。然后递归地选出上一层的前C大的预测值对应的结点，并将这些结点的子结点样本划分作为训练集训练下一层分类器。其余样本全部剪枝。每个模型的参数初始化采用上一层模型的参数，但attention层除外。
### 预测方法
对每个标签用沿树链式法则计算后验概率，得到分类概率。注意预测分类概率并不归一化。
