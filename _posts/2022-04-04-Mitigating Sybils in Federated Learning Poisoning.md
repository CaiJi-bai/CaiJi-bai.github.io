---
layout: mypost
title: Mitigating Sybils in Federated Learning Poisoning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Mitigating Sybils in Federated Learning Poisoning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>减轻联邦学习中毒中的 Sybils</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Clement Fung, Chris J.M. Yoon, Ivan Beschastnikh</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CoRR, August 2018</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2018年8月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>联邦学习方法容易受到各种攻击，包括模型中毒，在有女巫的情况下，这种情况会大大恶化。现有的防御方法需要事先了解女巫的数量信息，作者想设计一种不需要事先了解预期的女巫数量的防御方法。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td>了解联邦学习中女巫中毒攻击的防御</td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>提出一种新防御方法：FoolsGold，主要方法是保留诚实节点的更新，同时惩罚女巫的贡献，核心是History，Pardoning和Logit三个部分的设计。</td>
    </tr>
</table>

# 内容总结  

1. 引言  
通过实验评估了联邦学习对基于女巫的中毒攻击的脆弱性。
2. 背景  
介绍了机器学习、随机梯度下降、联邦学习、针对 ML 的针对性中毒攻击和女巫攻击。  
3. 假设和威胁模型  
介绍了联邦学习设置、女巫攻击和攻击能力。
4. SGD的挑战与防御  
介绍了SGD面临的三个挑战和 Multi-Krum 防御方法。
5. FoolsGold设计

   - 五个设计目标  

   - 算法的具体实现   
   （1）聚合每次迭代的历史向量  
   （2）计算余弦相似度  
   （3）找到每个客户端与其他客户端的最大余弦相似度  
   （3）对诚实客户端的更新进行赦免  
   （5）Logit  
   （6）更新参数

6. 评估  
    * 典型攻击场景评估
    * 与 Multi-Krum 比较
    * 不同的客户端数据分布
    * 了解 FoolsGold 的攻击
    * 设计元素的效果
    * 性能开销
7. 限制  
    * FoolsGold 对单个女巫攻击的防御很差，作者将其与 Multi-Krum 结合防御效果更好。
    * FoolsGold 需要应对知识渊博的女巫攻击，作者从历史机制和相似度选择两个方面提出了相关该进办法。
8. 相关工作  
回顾了有关安全 ML、sybils 防御和其他 ML 中毒防御的更广泛的文献。
9.  结论  
作者提出了 FoolsGold 方法，一种利用客户端贡献相似性的防御。经过各种评估表明，在所有情况下，作者的防御方法都能够胜过之前的工作。FoolsGold 对联邦学习算法的更改最小，依赖于余弦相似度等标准技术，并且不需要事先了解预期的女巫数量。

另一篇 FoolsGold 描述论文：The Limitations of Federated Learning in Sybil Settings (RAID -> CCF B)