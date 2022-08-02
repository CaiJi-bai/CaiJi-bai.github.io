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

设 `$i$` 为这个权重 `$\hat{\omega}_i$` 在 `$\hat{\theta}$` 中的索引；不失一般性，让 `$\hat{\omega}_i$ > 0`。

攻击者的目标是用他们的权重 `$\hat{\omega}_i$` 替换全局模型 `$\theta$` 中的权重 `$\omega_i$` 的值。

令 `$T=t$` 为攻击者插入后门时的迭代，并且对于所有 `$T>t$`，攻击者在训练中缺席。在任何一轮 `$T>t$` 中，良性设备可能会以负梯度更新 `$\omega_i$`。 如果 `$\omega_i$` 是良性全局最优值 `$\theta^*$` 使用的权重，则任何更新向量都有可能擦除攻击者的后门。每一轮 FL，攻击者更新未被擦除的概率都会降低。

### 神经毒素

直觉：随机梯度下降（SGD）中梯度的稀疏性，经验上已知，聚合的良性梯度的 `$\ell_2$` 范数的大部分包含在非常少量的坐标中。

方法：确保攻击只更新良性代理不太可能（不经常）更新的坐标，我们就可以维护模型中的后门并创建更强大的攻击。

![算法1](算法1.png)

1. 攻击者从上一轮下载梯度，并使用它来近似下一轮的良性梯度。
2. 攻击者计算良性梯度的 `$top-k%$` 坐标并将其设置为约束集。
3. 对于 PGD 的一些 epochs，攻击者在中毒数据集 `$\hat{D}$` 上计算梯度更新，并将该梯度投影到约束集，即观察到的良性梯度的 `$bottom-k%$` 坐标。  
4. PGD 逼近位于 `$bottom-k%$` 坐标跨度内的最优解。

# 实验

### 任务

![所有任务的实验参数](所有任务的实验参数.png)

![NLP任务的触发句和目标](NLP任务的触发句和目标.png)

### 指标和方法

攻击细节：在我们所有的实验中，攻击者控制了少量受感染的设备，并通过将中毒梯度上传到服务器来实施攻击。 我们使用固定频率攻击模型进行少发攻击，我们现在定义的术语。

少发攻击：攻击者仅参加AttackNum回合，这是回合总数的子集。AttackNum量化了攻击者的实力。

固定频率攻击：攻击者在他们参与的每个迭代中只控制一个设备。

服务器防御：范数裁剪防御

后门持久性指标：

![定义3.1](定义3.1.png)

### 实验结果

![调整遮罩比率k对任务1的寿命的影响](调整遮罩比率k对任务1的寿命的影响.png)

+ 神经毒素提高持久性

![三个触发器对任务1的影响](三个触发器对任务1的影响.png)

+ 神经毒素使困难攻击更容易。

![具有不同长度触发句的 LSTM 在 Reddit 数据集上的基线和神经毒素的攻击准确率](具有不同长度触发句的 LSTM 在 Reddit 数据集上的基线和神经毒素的攻击准确率.png)

+ 神经毒素使单字触发器攻击成为可能。
+ 当我们减少触发长度，增加攻击的难度和影响时，神经毒素在基线上的改善增加。

![神经毒素对差分隐私防御的影响](神经毒素对差分隐私防御的影响.png)
![重构损失检测防御](重构损失检测防御.png)
![SparseFed](SparseFed.png)

+ 神经毒素对评估的防御是鲁棒的。

+ 神经毒素使强攻击变得更强。
+ 神经毒素不会降低良性准确性。
+ 神经毒素在规模上表现良好。

### 分析

the Hessian trace and top eigenvalue

# 总结

先前对 FL 后门攻击的研究表明，FL 协议很容易受到攻击。我们通过引入神经毒素来补充这一工作，神经毒素是一种攻击算法，它利用更新稀疏化来攻击未被充分代表的参数。我们根据经验评估了神经毒素对先前攻击的影响，我们发现，在大多数情况下，通过在现有攻击的基础上添加一行代码，它将先前工作的持久性提高了 2-5 倍。

# 参考

1. [百度](https://www.baidu.com){:target="_blank"}