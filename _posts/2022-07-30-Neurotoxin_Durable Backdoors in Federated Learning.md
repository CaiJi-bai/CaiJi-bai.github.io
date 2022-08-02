---
layout: mypost
title: Neurotoxin_Durable Backdoors in Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Neurotoxin: Durable Backdoors in Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>神经毒素: 联合学习中的持久后门</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Zhengming Zhang, Ashwinee Panda, Linyue Song, Yaoqing Yang, Michael W. Mahoney, Prateek Mittal, Kannan Ramchandran, Joseph Gonzalez</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>39th ICML 2022: Baltimore, MD, USA [CCF 人工智能 A 类会议]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020 年 7 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>先前的工作表明，可以将后门插入到 FL 模型中，但这些后门通常不持久，即，在攻击者停止上传中毒更新后，它们不会保留在模型中。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>提出了神经毒素，这是对现有后门攻击的一种简单的单行修改，它通过攻击在训练期间幅度变化较小的参数来发挥作用。</td>
    </tr>
</table>

# 内容总结

# 主要贡献

1. 介绍了神经毒素，这是一种新型模型中毒攻击，旨在将更耐用的后门插入 FL 系统。
2. 对三个自然语言处理任务（Reddit 的下一个单词生成以及 IMDB 和 Sentiment140 的情感分类）、两个模型架构（LSTM 和 Transformer）以及三个计算机视觉数据集（CIFAR-10、CIFAR-100 和 EMNIST的分类）、两个模型架构（ResNet 和 LeNet）进行了广泛的实证评估，以防御 FL 系统。

# 联合学习中的持久后门

### 动机

先前的工作已经证明重新训练模型在消除后门方面的有效性

### 为什么后门消失了

设 `$\hat{\theta}$` 是攻击者的局部模型，它使中毒数据集 `$\hat{D}$` 上的损失函数 `$L$` 最小化。

考虑一个玩具问题，其中攻击者的模型 `$\hat{\theta}$` 与全局模型 `$\theta$` 仅在一个坐标上不同。

设 i 为这个权重 `$\hat{\omega_i}$` 在 `$\hat{\theta}$` 中的索引；不失一般性，让 `$\hat{\omega}_i$ > 0`。

攻击者的目标是用他们的权重 `$\hat{\omega_i}$` 替换全局模型 `$\theta$` 中的权重 `$\omega_i$` 的值。

令 T = t 为攻击者插入后门时的迭代，并且对于所有 T > t，攻击者在训练中缺席。在任何一轮 T > t 中，良性设备可能会以负梯度更新 `$\omega_i$`。 如果 `$\omega_i$` 是良性全局最优值 `$\theta^*$` 使用的权重，则任何更新向量都有可能擦除攻击者的后门。每一轮 FL，攻击者更新未被擦除的概率都会降低。

# 参考

1. [百度](https://www.baidu.com){:target="_blank"}