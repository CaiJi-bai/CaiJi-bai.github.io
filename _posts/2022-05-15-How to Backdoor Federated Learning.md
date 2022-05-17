---
layout: mypost
title: How to Backdoor Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>How to Backdoor Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>如何后门联邦学习</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Jack</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>the 12th ACM Workshop</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020年10月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>联邦学习本质上是易受 model poisoning 攻击的，这是一种本文提出的新的攻击方法。联邦学习给了所有的参与者对最终模型的直接影响能力，因此这个攻击比只针对数据集的投毒攻击更厉害。</td>
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

# 为什么会受到模型中毒攻击

联邦学习通常容易受到后门和其他模型中毒攻击影响的主要原因：

1. 当有数百万参与者进行训练时，不可能确保他们都不是恶意的。
2. 联邦学习的一个假设就是 device 上的数据分布是 Non-IID 的，并且为了聚合的安全性，会引入安全聚合，这样就很难进行异常检测了。
3. 深度学习的能力很强，即便是在主任务上不引人任何 backdoor，device 还是容易从 subtask 上引入 backdoor。

# 联邦学习

联邦学习可以从数以万计设备上学习一个聚合的模型，这个用户数量 n 是非常非常大的。在第 t 轮，服务端选取 m 个用户组成一个集合 `$S_m$`，然后把当前的联合模型 `$G^t$` 发给他们。在这个过程中 m 的选择需要权衡效率和训练速度。然后被选中的用户基于 `$G^t$` 模型和本地数据训练得到本地模型 `$L^{t+1}$`，并且把差值 `$L{t+1}-Gt$` 返回给服务器。然后更新完新的模型就是：

![]()

全局学习率 `$\eta$` 控制着模型更新的比例，当 `$\eta=n/m$` 时候，新的模型就是这 m 个用户的平均值了。

# 怎么进行后门攻击实验

