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



