# [EMNLP]问题形式
# How Much Reading Does Reading Comprehension Require?  A Critical Investigation of Popular Benchmarks

# 背景
一般来说，阅读理解问题的形式如下：（问题，文本，答案）。正常说来，我们需要问题和文本两部分的内容，才能得到答案。
但是随着大量的数据集和模型的不断提出，作者发现，除了设计的benchmark外，很难衡量一个数据集和模型乃至这个benchmark本身真正的好坏。
更具体的说，很多模型的解释性不足，追求end-to-end，但是跳过了在问题解释的逻辑上至关重要的一些步骤。

# 问题
1. 任务的难度是难以被量化的。我们到底需要多少问题和文本才能回答这个问题。
2. 发现在单单提供问题、单单提供文本的情况下，使用现有模型进行回答的准确度很多时候甚至超过了数据集的baseline，有时甚至超过了同一个模型输入问题和文本的准确度。

# 实验目标
o 数据集
1. **CBT**: cloze-style RC dataset
2. **CNN**: cloze-style news article RC dataset
3. **Who-did-what**: cloze-style, pairs of new articles.
4. **bAbI**: set of 20 tasks to help researchers identify and rectify the failings of their reading comprehension systems.
5. **SQuAD**: QA dataset to found the exact span in the passage.
6. **Generating Corrupt Data**: The dataset they create to avoid information lacking.

o 模型
1. **Key-Value Memory Networks**
2. **Gated Attention Reader**
3. **QA Net**

# 结果
在单单提供问题、单单提供文本的情况下，使用现有模型进行回答的准确度很多时候甚至超过了数据集的baseline，有时甚至超过了同一个模型输入问题和文本的准确度。

# 结论
1. 提供严格的阅读理解baseline
2. 测试完整文本是否是必要的
3. 小心完形填空数据集
