# Ranking-Based Autoencoder for Extreme Multi-label Classification

## 背景

-   XML的挑战

    -   计算复杂度
    -   标签间依赖
    -   数据标签噪声

-   现有深度模型不能兼顾词袋模型和文本模型

-   有一些模型对于数据集的大小、稀疏度和噪声比较敏感

-   现有模型可解释性不强

    

# 思路

>   Chih-Kuan Yeh, Wei-Chieh Wu, Wei-Jen Ko, and Yu-
>   Chiang Frank Wang. 2017. Learning deep latent
>   space for multi-label classification.

>   Sanghyun Woo, Jongchan Park, Joon-Young Lee, and
>   In So Kweon. 2018. Cbam: Convolutional block
>   attention module. In Proc. of European Conf. on
>   Computer Vision (ECCV).

-   希望找到数据$(x_i,y_i)$的$x_i,y_i$之间共同存在的潜在空间，将其通过线性变换转至该空间的$x_h,y_h$，尽可能使得二者接近。
-   还需要找到一个变换，将潜在空间转回原本的标签空间。
-   学习的时候，需要学习三个变换：$x_h=\mathcal{F}(x), y_h=\mathcal{E}(y), y'=\mathcal{D}(y_h)$，推理的时候，$\hat{y}=\mathcal{D}(\hat{x_h})=\mathcal{D}(\mathcal{F}(\hat{x}))$
-   一般使用的均方误差难以表示标签之间的关联关系，也难以直接生成可比的标签得分（？），并且对标签噪声敏感。
-   新的loss函数有三个目标：
    -   尽量省时
    -   能够生成可比的标签得分
    -   能够处理带噪声的标签
-   为了既能够处理文本数据，也可以处理词袋数据，使用了改进的embedding模块，在空间上和通道上（使用了Woo, 2018论文中的命名）分别进行attention，加入了TF-IDF的影响，并且通过一个刺激网络来增加feature的区分度。并用average pooling来对一个数据进行整合。

## 实现

-   x经过embedding layer和一层全连接的处理得到在潜在空间上的向量$x_h$，y经过两层全连接层得到潜在空间上的向量$y_h$。通过特别设计的loss函数在训练时最小化$x_h$和$y_h$之间的误差。所得的$y_h$（在推理中为$x_h$）送入Decoder，两层全连接复原到标签空间，输出标签的概率分布。

-   loss函数
    $$
    \mathcal{L}(D)=\min_{F,E,D}\mathcal{L}_h(x_h,y_h)+\lambda\mathcal{L}_{ae}(y,y')
    $$
    参数$\lambda$用来平衡两个局部loss的大小。为了减少开支，并且隐藏空间的维度较小，$L_h$使用均方误差。

    $L_{ae}$被分为两个部分$L_P,L_N$。

