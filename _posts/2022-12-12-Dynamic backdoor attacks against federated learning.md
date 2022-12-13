---
layout: mypost
title: Dynamic backdoor attacks against federated learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Dynamic backdoor attacks against federated learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>针对联邦学习的动态后门攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Anbu Huang</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CoRR [ ]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2020 年 11 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>目前现有的研究主要集中在静态后门攻击，即注入的中毒模式没有改变，然而，FL 是一个在线学习框架，攻击者可以动态改变对抗目标，传统算法需要从头开始学习新的目标任务，这可能在计算上很昂贵并且需要大量的对抗训练样例。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>将元学习引入后门攻击</td>
    </tr>
</table>

# 内容总结

# 主要贡献

1. 联邦学习设置下的动态后门攻击
2. 提出共生网络
3. 将元学习与 FL 设置下的后门攻击联系起来

# 动态后门攻击

![动态后门攻击示例](动态后门攻击示例.png)

# 共生网络

![公式6](公式6.png)

# 元学习和后门攻击

![正常任务训练和元学习任务训练](正常任务训练和元学习任务训练.png)

# 算法

![算法1](算法1.png)

![算法2](算法2.png)

# 实验

![持久性和性能评估](持久性和性能评估.png)

![快速适应评估](快速适应评估.png)

# 总结

# 参考

1. [百度](https://www.baidu.com){:target="_blank"}