# SGM: Sequence Generation Model for Multi-Label Classification
## 背景
现有类multi-class分类方法完成multi-label任务，往往忽视了label之间的相关性。并且，文本的不同部分可能对不同label有不同的指向效果。

而考虑相关性的链式多二分类器如Classifier Chains是阶乘级的复杂度上升，难以在大型数据集中实现。

另外一些考虑相关性的模型，如ML-DT等，只考虑一阶或二阶的相关性，不考虑高阶的相关性。

## 思路
希望用Seq2Seq的方法，来处理multi-label的任务。并且，这样的模型在时序上依赖于前一个状态，即考虑了label之间的依赖性。

另外，加入attention来处理预测每个标签时对文本不同部分的注意力不同的问题。并在decoder中加入新的global embedding步骤来防止信息丢失以及连续出错。

## 实现
在训练时，每个样本的label按训练集中的出现频率排序。一方面使训练集更一致、方便学习，另一方面有可能考虑到低频标签对高频标签的依赖性。

- embedding层是对one-hot表示训练后的稠密词向量表示。
- encoder采用常见的LSTM encoder。
- 在编码之后加入attention层来使得更好地聚焦当前时间步下关注的文本。
- decoder层为基于当前attend文本，过去状态，上一时间步的label的global embedding三个部分的预测。并且加入了mask，去除之前预测过的标签的干扰。用softmax输出预测标签分布，并取最大者作为当前时刻的预测标签。
- 由于可能会出现一次预测不好会导致后续连续出错的情况，猜想是序列预测时对全文信息的损失。于是在每次预测标签之后，计算新的global embedding向量，加入下一次decode步骤。在这里受到highway network的启发，采取类似的形式来按权重组合上一个最优label的embedding以及其余全局的embedding。
- 训练时使用交叉熵loss函数，并且在寻找最优预测路径(?)时使用beam search，减少单次效果不好的影响。

## 实验
1. sort步骤和mask步骤是有效的
2. 调试了GE层的gate系数的值
3. 通过可视化这证明了attention的作用
4. label间的关系的确被捕捉了。并且GE使得信息更加丰富与平滑
5. 大量label时，模型无法解决
