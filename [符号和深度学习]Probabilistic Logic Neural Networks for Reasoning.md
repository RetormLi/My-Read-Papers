# Probabilistic Logic Neural Networks for Reasoning
# 成果：pLogicNet
1. 用MLN和一阶逻辑定义了所有可能的三元组的联合分布？
2. 可以使用EM算法进行优化。E-step预测缺失的三元组，M-step更新逻辑规则的权重。

# MLN: Markov Logic Network
1. 使用一阶逻辑
2. 可以存在不确定性
3. 逻辑规则的权重通过概率网络的学习得到

# 背景
1. 知识图推理的两种方法：Markov Logic Network, knowledge graph embedding method
2. knowledge graph embedding method:
o TransE: defines each relation as a translation vector
o DistMult models the symmetric relation with a bilinear scoring function
o ComplEx: models the asymmetric relations by using a bilinear scoring function in complex space
o RotaE: models multiple relation patterns by defining each relation as a rotation in complex space
3. 在知识图推理上进行强化学习：训练可以寻找推理路径的Agent
