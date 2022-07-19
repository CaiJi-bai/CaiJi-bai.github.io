---
layout: mypost
title: DBA-Distributed Backdoor Attacks against Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>DBA: Distributed Backdoor Attacks against Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>针对联邦学习的分布式后门攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Chulin Xie, Keli Huang, Pin-Yu Chen, Bo Li</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>8th ICLR 2020: Addis Ababa, Ethiopia [深度学习顶级会议]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020 年 4 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>当前的攻击并没有充分利用 FL 的分布式学习方法，因为它们将相同的全局触发模式嵌入到所有敌对方。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td>了解分布式后门攻击</td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>多触发器后门攻击</td>
    </tr>
</table>

# 内容总结

# 威胁模型

### 攻击者能力

基于 Kerckhoffs 的理论（Shannon，1949），我们认为这里的强攻击者完全控制其局部训练过程，例如后门数据注入和更新局部训练超参数，包括E和lr。这种场景非常实用，因为每个本地数据集通常由一个本地方拥有。然而，攻击者无法影响中央服务器的权限，例如更改聚合规则，也无法篡改其他方的训练过程和模型更新。

### 攻击目标

![公式2](公式2.png)

### 分布式后门攻击因素


# 实验

+ 数据集：Lending Club Loan Data, MNIST, CIFAR-10 and Tiny-imagenet
+ 数据分布：Non-IID
+ 训练模型：SGD


### 分布式后门攻击 V.S. 集中式后门攻击

+ 攻击场景：发攻击 (Attack A-M) 和单发攻击 (Attack A-S)

![Attack A-M 和 A-S](Attack A-M 和 A-S.png)

### 分布式攻击的稳健性

![两种鲁棒强化学习方法的攻击有效性比较](两种鲁棒强化学习方法的攻击有效性比较.png)

### 通过特征可视化和特征重要性进行解释

![特征分析结果](特征分析结果.png)

# 分布式后门攻击触发因素分析

### scale 的影响

![scale的影响](scale的影响.png)

### 触发器位置的影响

![触发器位置的影响](触发器位置的影响.png)

### 触发器间隙的影响

![触发器间隙的影响](触发器间隙的影响.png)

### 触发器大小的影响

![触发器大小的影响](触发器大小的影响.png)

### 中毒间隔的影响

![中毒间隔的影响](中毒间隔的影响.png)


### 中毒率的影响

![中毒率的影响](中毒率的影响.png)

### 数据分布的影响



# 参考

1. [百度](https://www.baidu.com){:target="_blank"}