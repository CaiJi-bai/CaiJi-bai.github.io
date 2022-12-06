---
layout: mypost
title: Distributed Swift and Stealthy Backdoor Attack on Federated Learning
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Distributed Swift and Stealthy Backdoor Attack on Federated Learning</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>联邦学习中分布式迅速和隐形的后门攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Agnideven Palanisamy Sundar, Feng Li, Xukai Zou, Tianchong Gao</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>IEEE NAS 2022: Philadelphia, PA, USA [ ]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2022 年 10 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>相同的触发器用于在推理时在原本良性的全局模型中诱发后门。这种单一触发攻击可以相对容易地检测和删除，因为它们破坏了 FL 的分布式特性。</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>使用相当大的离散触发器进行本地训练，同时使用较小的推理触发器来调用攻击。</td>
    </tr>
</table>

# 内容总结

# 威胁模型

1. 访问权限：攻击者无法访问良性客户端的数据集或训练过程，也无法访问有关全局模型的信息。
2. 训练权限：攻击者可以修改恶意客户端的本地训练数据集，并在训练时间内与其他恶意客户端协调。
3. 测试权限：攻击者不能在推理过程中修改模型，但可以向测试数据记录中添加触发器补丁。

# 方法

# 两种类型的触发器模式

1. 显著的推理触发器：攻击在推理时使用的触发器模式，以调用后门。
2. 分散的离散触发器：恶意客户端使用离散触发器进行本地训练。以推理触发器为基础开始，通过在特定的选定方向上扩展与推理触发器相邻的像素来生成离散触发器。

### 攻击方案

![攻击概述](攻击概述.png)

所有离散触发器在相同的小正方形区域中重叠。该区域形成推理触发器。必须确保在推理触发区域以外的任何区域中的任何离散触发对之间没有重叠。

使用离散触发器进行本地模型训练，在推理时使用推理触发器触发后门。

### 了解离散和推理触发器贡献

![公式3](公式3.png)

![公式4](公式4.png)

![公式4-1](公式4-1.png)

![公式5](公式5.png)

![公式6](公式6.png)

# 实验

+ 数据集：CIFAR-10 和 TinyImageNet
+ 数据分布：non-iid
+ 模型：ReNet18

![触发器](触发器.png)

### 实验结果

**攻击效率**

![触发器对比实验结果](触发器对比实验结果.png)

**与单触发攻击的比较**

![攻击响应图](攻击响应图.png)

![持久性实验结果](持久性实验结果.png)

**隐蔽性**

![特征图](特征图.png)

![防御的影响](防御的影响.png)

# 参考

1. [DeepLIFT：通过传播激活差异学习重要特征](https://www.modb.pro/db/175986){:target="_blank"}