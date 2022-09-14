---
layout: mypost
title: Backdoor attacks-resilient aggregation based on Robust Filtering of Outliers in federated learning for image classification
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Backdoor attacks-resilient aggregation based on Robust Filtering of Outliers in federated learning for image classification</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>图像分类联邦学习中基于异常值鲁棒过滤的后门攻击弹性聚合</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Nuria Rodríguez Barroso, Eugenio Martínez-Cámara, M. Victoria Luzón, Francisco Herrera</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>Knowledge-Based Systems, Volume 245 [CCF 人工智能 C 类期刊]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2022 年 6 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>FL 设置中的客户端的模型更新遵循高斯分布，并且那些在该分布中具有异常行为的客户端可能是对抗性客户端。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>一维异常检测</td>
    </tr>
</table>

# 内容总结

# 主要贡献


# 基于异常值鲁棒过滤的模型中毒后门攻击防御

学习轮 t 中全局模型的更新公式：

![公式1](公式1.png)

模型替换的目的：用其后门模型 `$L_{adv}^t$` 替换全局模型 `$G^t$`

![公式2,3,4](公式2,3,4.png)

### 假设

1. 客户端的模型更新遵循某个学习轮的高斯分布，因为全局聚合模型倾向于收敛到一个共同的解决方案。 基于中心极限定理 [44] 直观地证明了这一点，该定理指出独立随机变量的总和非常接近高斯分布。 让客户局部权重的分布是每个随机变量，然后，它们的线性组合接近于高斯分布。 因此，聚合超过聚合，结果将收敛到高斯分布。 特别是，更新的每个维度的数据分布收敛到单变量高斯分布。
2. 由于对抗性客户端的模型更新具有双重目标，我们假设它代表特定学习轮次的客户端更新分布中的异常值。

### RFOut-1d 

(**R**obust **F**iltering of **1-d**imensional **Out**liers)

由于更新的高维性 (通常来自神经网络)，并且为了避免通过应用降维技术的信息丢失，我们对模型更新的每个维度执行单变量异常检测。

对于每个维度 `$i\in{1,...,m}$`，其中 m 是模型更新向量的维度，我们考虑每个客户端在该维度上的局部模型更新形成的向量 `$L_i=(L_1^t[i],L_2^t[i],...,L_n^t[i])$`，其中 n 是参与聚合的客户数量。

异常检测方法：标准差方法

![公式5](公式5.png)

在参数的每个维度 i 中得到的聚合模型 `$G^t$` 为：

![公式6和7](公式6和7.png)

![算法1](算法1.png)

# 实验

# 参考

1. [百度](https://www.baidu.com){:target="_blank"}