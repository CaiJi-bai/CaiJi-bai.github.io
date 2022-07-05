---
layout: mypost
title: Poisoning Attack in Federated Learning using Generative Adversarial Nets
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Poisoning Attack in Federated Learning using Generative Adversarial Nets</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>使用生成对抗网络的联邦学习中的中毒攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Jiale Zhang, Junjun Chen, Di Wu, Bing Chen, Shui Yu</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>18th IEEE International Conference On Trust, Security And Privacy In Computing And Communications</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2019 年 8 月</td>
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

# 威胁模型

1. 攻击模型
   + 他们恰好控制一个非共谋的恶意代理，其索引为 `$m$` （限制恶意更新在全局模型上的影响）；
   + 数据以 i.i.d 方式在代理之间分布（使得更容易区分良性和可能的恶意更新，并且更难实现攻击隐匿）；
   + 恶意代理可以访问训练数据 `$D_m$` 的子集以及从与其对抗目标的一部分的训练和测试数据相同的分布中提取的辅助数据 `$D_{aux}$`（？？？）
2. 对手目标
   + 确保在服务器上学习的分类器对辅助数据进行有针对性的错误分类
   + ![公式1](公式1.png)
3. 隐形指标
给定来自代理的更新，服务器可以检查两个关键属性。首先，服务器可以单独验证更新是否会改善或恶化全局模型在验证集上的性能。其次，服务器可以检查该更新在统计上是否与其他更新有很大不同。我们注意到，这些属性都没有作为标准联邦学习的一部分进行检查，但我们使用这些属性来提高成功攻击的门槛。
+ 正确性检查：如果生成的模型的验证精度远低于通过聚合所有其他更新获得的模型的验证精度，服务器可以将更新标记为异常。阈值确定服务器可以容忍的性能变化程度。`$w_i^t=w_G^{t-1}+\delta_i^t$` `$w_{G\\i}^t=w_G^{t-1}+\sum_i\delta_i^t$`
+ ![公式2](公式2.png)
+ 权重检查：特定更新和其他更新之间的成对距离范围指示了该更新与其他更新之间的差异。为了使恶意代理不被标记为异常，我们需要（一个公式）。此条件确保恶意代理和任何其他代理的距离范围与任何其他两个代理的距离范围没有太大差异。
+ ![公式3](公式3.png)


# 问题

1. 什么是联邦学习中的共谋？