---
layout: mypost
title: Attack of the Tails Yes, You Really Can Backdoor Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Attack of the Tails: Yes, You Really Can Backdoor Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>尾巴的攻击：是的，你真的可以后门联邦学习</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Hongyi Wang, Kartik Sreenivasan, Shashank Rajput, Harit Vishwakarma, Saurabh Agarwal, Jy-yong Sohn, Kangwook Lee, Dimitris S. Papailiopoulos</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>34th NeurIPS 2020</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020 年 12 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td></td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td></td>
    </tr>
</table>

# 内容总结  

# 主要贡献

1. 如果一个模型容易受到对抗性示例 [28-32] 形式的推理时攻击，那么在温和的条件下，相同的模型将容易受到后门训练时攻击。
2. 提出边缘案例后门（edge-case backdoor）
3. 实验证明

# 边缘案例后门

首先正式定义一个 p-edge-case 示例集如下:

![定义1](定义1.png)

p 值较小的 p-edge-case 可以看作是一组标记示例，其中输入特征是从特征分布的重尾中选择的。 请注意，我们对标签没有任何条件，即可以考虑任意标签。

如何构造一个 p-edge-case 示例集？

假设对手有一组候选的边缘案例样本和一些良性样本。用良性样本提供一个预训练的预测模型，并收集最后一层的输出向量。通过拟合一个聚类数等于类数的高斯混合模型，我们可以获得一个生成模型，攻击者可以使用该模型测量给定样本的概率密度，并在需要时过滤掉。

![可视化对数概率密度](可视化对数概率密度.png)

根据访问模型提出三种不同的攻击策略：
1. 黑盒攻击：攻击者在本地制作的数据集 `$D' = D\cupD_{edge}$` 上执行标准的本地训练，无需修改，旨在最大化 D' 上的全局模型的准确性。
2. PGD 攻击：攻击者对 `$D' = D\cupD_{edge}$` 的损失应用投影梯度下降，约束条件是局部模型不会偏离全局模型太多。
3. 模型替换的 PGD 攻击：该策略结合了 (2) 中的过程和 [13] 中的模型替换攻击，其中模型参数在发送到服务器之前被缩放，以抵消其他诚实的贡献节点。

# 实验

数据集：CIFAR 10/ImageNet/EMNIST/Reddit/Sentiment 140
模型：VGG-9/VGG-11/LeNet/LSTMs
评估指标：测试准确率

# 总结

在本文中，我们提出了支持存在难以检测和防御的后门 FL 攻击的理论和实验证据。我们引入了边缘案例后门攻击，目标是预测子任务，这些子任务不太可能在训练或测试数据集中找到，但很自然。 这些边缘案例后门的有效性和持久性表明，在当前形式下，联邦学习系统容易受到对抗性代理的影响，突出了当前鲁棒性保证的不足。


