---
layout: mypost
title: Defending against Backdoors in Federated Learning with Robust Learning Rate
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Defending against Backdoors in Federated Learning with Robust Learning Rate</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>以鲁棒的学习率防御联邦学习中的后门</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Mustafa Safa Özdayi, Murat Kantarcioglu, Yulia R. Gel</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>35th AAAI 2021: Virtual Event</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2021 年 5 月 18 日</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>防御后门攻击</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>根据代理更新的符号信息，仔细调整聚合服务器的每个维度和每轮的学习率。</td>
    </tr>
</table>

# 内容总结  

# 聚合方法

(1) FedAvg

![公式1](公式1.png)

(2) [(Sun et al. 2019)](https://caiji-bai.github.io/posts/2022/05/21/Can-You-Really-Backdoor-Federated-Learning.html) 表明，当 FedAvg 与 (Geyer, Klein, and Nabi 2017) 中介绍的权重裁剪和噪声添加相结合时，可以使 FedAvg 在某些设置中对后门攻击具有鲁棒性。

![公式2](公式2.png)

(3) [(Fung, Yoon, and Beschastnikh 2020)](https://caiji-bai.github.io/posts/2022/05/21/Can-You-Really-Backdoor-Federated-Learning.html) 试图通过引入每个客户端的学习率而不是在服务器端使用单一的学习率来使 FL 变得健壮。

![公式3](公式3.png)

(4) 在 (Bernstein et al. 2018) 中，作者开发了一种通信高效的分布式 SGD 协议，其中代理只通信其梯度的符号。在这种情况下，服务器聚合接收到的符号并将聚合的符号返回给使用它在本地更新其模型的代理。 我们将他们的聚合技术称为符号聚合。

![公式4](公式4.png)

# 鲁棒的学习率（RLR）

+ 后门任务和主任务

`$\Delta_{adv}$` 应该将模型的参数引导到 `$w_{adv}$`，可以最大限度地减少主任务和后门攻击任务的损失。

`$\Delta_{hon}$` 想要将模型参数移向只会最小化主任务损失的模型参数。

+ 鲁棒的学习率

通过扩展 (Bernstein et al. 2018) 中提出的方法来构建一种防御，我们将其称为鲁棒学习率（RLR）。

![公式5](公式5.png)

与 FedAvg 结合后的更新规则：

![公式6](公式6.png)

由于我们只调整学习率，因此该方法与聚合函数无关。例如，我们可以将它与更新裁剪和噪声添加简单地结合起来，如 (2) 中所示。

# 实验

+ 数据集：Fashion MNIST（IID）和 Federated EMNIST（No-IID）
+ 模型：具有两层卷积层，一层最大池层和带 Dropout 的两个全连接层的五层卷积神经网络
+ 评价指标：验证准确率、基类准确率和后门准确率
<br>
+ **木马基类和相应目标类示例**

![样本示例](样本示例.png)

木马模式是一个 5×5 的加号，IID（上）和 No-IID（下）。

+ 实验结果

![IID 训练曲线](IID 训练曲线.png)

![No-IID 训练曲线](No-IID 训练曲线.png)

![不同聚合的准确率](不同聚合的准确率.png)

RLR 防御提供了最好的保护，并且对验证准确性的影响最小。

+ 优化

在防止后门任务方面，具有 RLR 率的 FedAvg 比其他方法的性能要好得多，但它也会降低收敛速度。  
是否可以在没有 RLR 的情况下开始，然后在训练期间的某个时间点切换到 RLR ？  
在模型即将收敛和/或怀疑存在后门攻击时切换到 RLR，以在训练期间清理后门模型，缩短收敛时间。

+ 文中提出的防御为什么有效？

![参数归因实验结果](参数归因实验结果.png)

![特征归因实验结果](特征归因实验结果.png)

# 总结

在这项工作中，作者从对抗的角度研究了 FL，并构建了一种简单的防御机制，特别是针对后门攻击。 防御背后的关键思想是**根据代理更新的符号信息调整聚合服务器每维度和每轮的学习率**。 通过实验，说明文中的防御大大降低了后门的准确性，而整体验证准确性的降级最小。总体而言，它优于文献中最近提出的一些防御措施。

