# Semantic-Unit-Based Dilated Convolution for Multi-Label Text Classification

## 任务目标
不同于XML，本模型对应的任务更加接近于普通的multi-class分类。label的数量更少，可能稀疏的情况较小。（但实验结果显示低频标签比高频标签表现更好）

使用的两个数据集：
- RCV1-v2：新闻数据集。每条新闻有103个topic中的数个
- Ren-CECps：情感分类数据集，采集自中文博客。8个情感标签，3个情绪极性标签。

## 思路
希望改进Seq2Seq模型，输入一个文本直接输出其对应的label。
然而Seq2Seq是词级别的信息预测。作者认为，label的预测应该源于文段中的semantic unit，即表达了文段含义的重要短语。

## 实现
作为Seq2Seq模型，主要两个部分：

### Encoder
编码部分分为三个部分：
- Multi-level Dilated Convolution：负责提取文本中的semantic unit信息。使用了Dilated CNN的思想，并且作为超参数限制了多层CNN的层间联系。以防止gridding effect (?)。
- LSTM（RNN?） Encoder：作为Seq2Seq的词层面信息的基础。这种信息又被称为source annotation。
- Hybrid Attention：希望能够获得在semantic units指导下的词级别信息。RNN decoder(?)的输出先attend semantic unit的信息，所得到的矩阵再attend LSTM encoder的输出。

另外，作者还发现了在标准Seq2Seq model中是否加入attention区别不大。

## 问题
这个任务是否适合Seq2Seq就值得商榷。labels本身就不具有序列属性。

其次，消融测试并没有提到MDC和LSTM Encoder的分别的作用，这有点难以令人信服。

另外，如此复杂的模型训练起来开销会不会太大？何况对比的模型都是非常简单的模型，最终得到的结果也并非巨大的提升。
