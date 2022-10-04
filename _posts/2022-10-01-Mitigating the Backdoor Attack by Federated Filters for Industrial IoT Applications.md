---
layout: mypost
title: Mitigating the Backdoor Attack by Federated Filters for Industrial IoT Applications
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>Mitigating the Backdoor Attack by Federated Filters for Industrial IoT Applications</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>通过应用联合过滤器减轻工业物联网中的后门攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Boyu Hou, Jiqiang Gao, Xiaojie Guo, Thar Baker, Ying Zhang, Yanlong Wen, Zheli Liu</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>IEEE Transactions on Industrial Informatics [SCI 1 区]</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2022 年 1 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>（1）基于模型计算过程分析的防御违反了联邦学习隐私保护的需求（2）IIoT 应用程序由于带宽有限且网络连接不稳定无法重新训练其模型或及时下载最新的全局模型</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>通过削弱恶意模型对受害者的影响来减轻后门攻击</td>
    </tr>
</table>

# 内容总结

# 主要贡献

1. 为联邦 IIoT 应用提出了一种有效的后门过滤器训练结构，以防御后门攻击。
2. 在 XAI 模型的帮助下提出了有效的过滤器训练方法。
3. 利用模糊标签翻转策略来清除可疑后门数据的后门触发区域。

# 预备知识

XAI 方法解释模型结果，以帮助研究人员评估模型是否学习了正确的特征。

# 防御方法

### 基于过滤器的防御体系结构

![联合后门过滤器的工作流](联合后门过滤器的工作流.png)

### 后门过滤器构造

![算法1](算法1.png)

+ 服务器借助 XAI 模型通过检测输入的重要特征来识别触发区域。
+ 利用区域的大小为特征制作数据集
+ 使用数据集训练分类器

### 模糊标签翻转策略

![算法2](算法2.png)

+ 对重要特征区域进行模糊
+ 标签反转

# 实验

+ 数据集：MINST 和 CIFAR 10
+ 训练模型：LeNet 和 ResNet
+ 评估指标：过滤器的有效性-识别后门图像的准确性；模糊标签翻转方法的性能-受害者模型在去触发数据上的准确性

### 实验结果

![过滤器性能](过滤器性能.png)

+ 过滤器的性能同时与分类器和 XAI 部分有关。
+ 只要后门攻击有效，过滤器的效果不受后门比例的影响。
+ XAI 模型和分类器都不是滤波器性能的决定性因素。
+ 过滤器行为与数据特征和网络结构密切相关。

![不同模糊次数对后门的影响](不同模糊次数对后门的影响.png)

+ 模糊标签翻转策略更适合消除像素级触发器。

# 总结

1. 本文提出了 FL 中的后门滤波器构造和基于模糊标签翻转策略的去触发器方法。该方法可以识别后门输入并校正模型结果。
2. 推理阶段的防御

# 问题

### 将触发器放到主体部分？
