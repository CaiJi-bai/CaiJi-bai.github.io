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
        <td>Jack</td>
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



# 参考

1. [百度](https://www.baidu.com){:target="_blank"}