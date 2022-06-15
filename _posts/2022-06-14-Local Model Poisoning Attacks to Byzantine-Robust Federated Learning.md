---
layout: mypost
title: Local Model Poisoning Attacks to Byzantine-Robust Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Local Model Poisoning Attacks to Byzantine-Robust Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>拜占庭鲁棒联邦学习的局部模型中毒攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Minghong Fang, Xiaoyu Cao, Jinyuan Jia, Neil Zhenqiang Gong</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>29th USENIX Security Symposium 2020</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020 年 8 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>目前的主要攻击集中在对数据中毒攻击，但缺少对本地训练过程中的模型中毒攻击的研究，尽管有，也是不抗拜占庭攻击联邦学习的场景下，本文是第一次研究在抗拜占庭攻击的联邦学习场景下的局部模型中毒攻击</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>将寻找精心设计的局部模型表述为优化问题</td>
    </tr>
</table>

# 内容总结  

# 主要贡献

1. 首次对攻击拜占庭鲁棒联邦学习进行了系统研究。
2. 提出了针对拜占庭鲁棒联邦学习的局部模型中毒攻击。我们的攻击是在学习过程中操纵受损工作设备上的本地模型参数。
3. 推广了两种针对数据中毒攻击的防御方法，以抵御局部模型中毒攻击。我们的结果表明，尽管其中一种方法在某些情况下有效，但在其他情况下成功率有限。

# 拜占庭鲁棒联邦学习



# 威胁模型

+ 攻击者的目标：操纵所学的全局模型，使其在测试示例时具有高错误率。
+ 攻击者的能力：攻击者控制的工作设备数量少于 50% ，攻击者可以任意操纵从这些工作设备发送到主设备的本地模型。
+ 攻击者的背景知识：
  1. 攻击者是否知道聚合规则
  2. 攻击者是否知道良性工作设备上的本地训练数据集和本地模型

# 局部模型中毒攻击

想法：通过在联邦学习的每次迭代中精心制作从受感染的工作设备发送到主设备的本地模型来操纵全局模型。

+ 优化问题

![优化问题](优化问题.png)

全知识：`$w_1,...,w_c,w_{c+1},...,w_m$` 已知，直接求解优化问题

部分知识：`$w_1,...,w_c$` 已知，用 `$w_1,...,w_c$` 估计 `$w$`

聚合规则未知：猜测聚合函数