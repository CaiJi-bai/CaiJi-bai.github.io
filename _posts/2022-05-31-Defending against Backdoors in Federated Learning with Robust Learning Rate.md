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
        <th>以稳健的学习率防御联邦学习中的后门</th>
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

(2) [(Sun et al. 2019)](https://caiji-bai.github.io/posts/2022/05/21/Can-You-Really-Backdoor-Federated-Learning.html)表明，当 FedAvg 与 (Geyer, Klein, and Nabi 2017) 中介绍的权重裁剪和噪声添加相结合时，可以使 FedAvg 在某些设置中对后门攻击具有鲁棒性。

![公式2](公式2.png)

(3) [(Fung, Yoon, and Beschastnikh 2020)](https://caiji-bai.github.io/posts/2022/05/21/Can-You-Really-Backdoor-Federated-Learning.html)试图通过引入每个客户端的学习率而不是在服务器端使用单一的学习率来使 FL 变得健壮。

![公式3](公式3.png)

(4) 在 (Bernstein et al. 2018) 中，作者开发了一种通信高效的分布式 SGD 协议，其中代理只通信其梯度的符号。在这种情况下，服务器聚合接收到的符号并将聚合的符号返回给使用它在本地更新其模型的代理。 我们将他们的聚合技术称为符号聚合。

![公式4](公式4.png)