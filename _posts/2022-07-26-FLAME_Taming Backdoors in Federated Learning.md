---
layout: mypost
title: FLAME_Taming Backdoors in Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>FLAME: Taming Backdoors in Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>在联邦学习中驯服后门</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Thien Duc Nguyen, Phillip Rieger, Hossein Yalame, Helen Möllering, Hossein Fereidooni, Samuel Marchal, Markus Miettinen, Azalia Mirhoseini, Ahmad-Reza Sadeghi, Thomas Schneider, Shaza Zeitouni</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>31th USENIX Security Symposium 2022 [CCF 网络与信息安全 A 类会议]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2022 年 8 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>基于检测和过滤恶意模型更新的后门攻击防御只考虑非常特定和有限的攻击者模型，而基于差分隐私激励的噪声注入的防御显著恶化了聚合模型的良性性能。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td>经典阅读</td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>估计注入的足够噪音量，以确保消除后门。为了最小化所需的噪声量，使用了模型聚类和权重裁剪的方法。</td>
    </tr>
</table>

# 内容总结

# 预备知识

### HDBSCAN

HDBSCAN 是一种基于密度的聚类算法，它利用 n 维空间中数据点的距离将彼此靠近的数据点组合成一个簇。 因此，集群的数量是动态确定的。不适合任何集群的数据点被视为异常值。

然而，虽然 HDBSCAN 的前身 DBSCAN 使用预定义的最大距离来确定两个点是否属于同一个集群，但 HDBSCAN 根据点的密度独立确定每个集群的最大距离。因此，在 HDBSCAN 中，最大距离和聚类总数都不需要预先定义。

### 差分隐私

DP 是一种隐私技术，旨在确保输出不会泄露参与者的个人数据记录。DP 的正式定义如下：

![定义1](定义1.png)

其中 `$\epsilon$` 表示隐私界限，`$\delta$` 表示打破这个界限的概率。较小的 `$\epsilon$` 和 `$\delta$` 值表示更强的隐私。

实现差分隐私的一种常用方法是向算法输出中添加随机高斯噪声 `$N(0, \sigma^2)$`

# 威胁模型

### 对手的目标

同时保证主任务和后门任务的准确率。（不被聚合器识别）

### 对手的能力

1. 假设对手 `$\mathcal{A}$` 完全控 `$k<\frac{n}{2}$` 个客户端及其训练数据、过程和参数。
2. `$\mathcal{A}$` 完全了解聚合器的操作，包括潜在应用的后门防御。
3. `$\mathcal{A}$` 无法控制在聚合器和诚实的客户端上执行的任何进程。

# 问题设置和目标

### 后门表征

![公式2](公式2.png)

![公式3](公式3.png)

![良性模型和后门模型的权重向量](良性模型和后门模型的权重向量.png)

### 防御目标

1. 有效性：为了防止对手实现其攻击目标，必须消除后门模型更新的影响，以便聚合的全局模型不会显示后门行为。
2. 性能：必须保持全局模型的良性性能，以保持其效用。
3. 独立于数据分布和攻击策略：防御方法必须适用于一般的对手模型，即它不得要求事先了解后门攻击的方法，或对本地客户端的特定数据分布进行假设，例如，数据是 iid 还是 non-iid。

# FLAME 概述和设计

### 高级想法

+ 动机：早期工作使用聚合模型的差分隐私启发噪声来消除后门。它们根据经验确定要使用的足够的噪声量。然而，在 FL 设置中，这是具有挑战性的，因为通常不能假设聚合器能够访问训练数据，特别是中毒的数据集。因此，**需要一种通用方法来确定多少噪声足以有效地消除后门**。另一方面，**模型中注入的噪声越多，其良性性能受到的冲击就越大**。
+ FLAME 概述：FLAME 估计在 FL 设置中移除后门所需的噪声级，而无需广泛的经验评估和访问训练数据。此外，为了有效地限制所需的噪声量，FLAME 使用一种新颖的基于聚类的方法来识别和删除具有高影响的对抗性模型更新，并应用动态权重裁剪方法来限制对抗性模型的影响，这些模型按比例放大以提高其性能。

![FLAME防御的高级想法](FLAME防御的高级想法.png)

### 设计挑战

1. 过滤掉动态场景中角度偏差较大的逆向模型
2. 限制扩大后门的影响
3. 为后门消除选择合适的噪声级

### FLAME 设计

![FLAME工作流图](FLAME工作流图.png)

![算法1](算法1.png)

+ 动态模型过滤



+ 自适应剪裁和去噪



# 安全分析

### FLAME 的噪声边界检验



### 攻击和数据分布假设



# 实验

+ 数据集：word prediction, image classification and an IoT intrusion detection
+ 评估指标：BA - Backdoor Accuracy, MA - Main Task Accuracy, TPR - True Positive Rate and TNR - True Negative Rate

![实验数据集](实验数据集.png)

### 实验结果

+ 防止后门攻击

FLAME 的有效性

![FLAME的有效性](FLAME的有效性.png)

与现有防御的比较

![与现有防御相比FLAME的有效性](与现有防御相比FLAME的有效性.png)

+ 对自适应攻击的弹性

![模型对齐攻击的弹性](模型对齐攻击的弹性.png)

+ 客户端数量的影响

![中毒模型率的影响](中毒模型率的影响.png)

![客户端数量的影响](客户端数量的影响.png)

+ non-iid 数据维度的影响

![non-iid数据维度的影响](non-iid数据维度的影响.png)

# 总结

在本文中，我们介绍了 FLAME，一个用于 FL 的弹性聚合框架，它消除了后门攻击的影响，同时保持了聚合模型对主要任务的性能。我们提出了一种方法来近似需要注入到全局模型中以中和后门的噪声量。此外，结合我们的动态聚类和自适应裁剪，FLAME 可以显著降低后门删除的噪声规模，从而保持全局模型的良性性能。此外，我们为 FLAME 设计、实现并测试了高效安全的两方计算协议，以确保客户端训练数据的隐私性，并阻止对客户端更新的推理攻击。


# 参考

1. [深度学习之-神经元权重以及偏置的介绍](https://blog.csdn.net/fishing95826/article/details/106676786){:target="_blank"}