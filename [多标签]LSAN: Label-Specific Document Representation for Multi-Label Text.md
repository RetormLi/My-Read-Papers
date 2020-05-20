# LSAN: Label-Specific Document Representation for Multi-Label Tex
## 思路
- 由于文本可能长而复杂，很多信息是噪声或者冗余。希望准确地捕捉文本的有效语义特征。
- 希望考虑文本和标签之间的语义联系
- 希望考虑标签之间的语义相关性
- 希望合并地考虑文本和标签
## 实现
1. embed之后，仍然用双向LSTM获得文本上下文表示
2. Label-Specific Attention Network：获得文本的标签关联表示
- Self-Attention：描述每个词对每个标签的贡献。即label-word attention score。具体计算方式类似单隐层神经网络，关键在于训练内部称为self-attention的参数矩阵。每一个神经网络对应一个标签。将文本的上下文表示乘上每个标签的attention向量得到面向标签的对于文本的新的表示，但是并未有实际标签的信息参与。
- Label-Attention：计算标签和词之间的相关程度。先使用与训练的与词向量同维度的标签向量表示。用标签表示矩阵和文本表示矩阵相乘表示标签和文本之间的相似程度（这里最好使用softmax归一）然后再乘上文本表示矩阵，获得基于标签的文本表示。
3. Adaptive Attention Fusion Strategy：融合上一层的两个部分的信息
关键在于获得两部分的权重。用两个全连接矩阵计算两个部分的权重值，注意此处有约束：权重值之和为1（怎么带约束训练？）
4. 输出层：以上层的融合信息为输入，训练单隐层神经网络。loss函数为交叉熵。

