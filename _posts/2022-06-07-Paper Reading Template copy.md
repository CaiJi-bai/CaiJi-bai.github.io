---
layout: mypost
title: FLARE Defending Federated Learning against Model Poisoning Attacks via Latent Space Representations
categories: [Test]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>FLARE: Defending Federated Learning against Model Poisoning Attacks via Latent Space Representations</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>FLARE: 通过潜在空间表示保护联邦学习免受模型中毒攻击</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Ning Wang, Yang Xiao, Yimin Chen, Yang Hu, Wenjing Lou, Y. Thomas Hou</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>17th AsiaCCS 2022: Nagasaki, Japan</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2022 年 5 月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>专注于分析模型参数的现有防御措施在检测这种精心设计的有毒模型方面效果有限</td>
    </tr>
    <tr>
        <td>阅读动机</td>
        <td></td>
    </tr>
    <tr>
        <td>创新点</td>
        <td>利用模型的倒数第二层表示 (PLRs) 来表征对每个局部模型更新的对抗性影响</td>
    </tr>
</table>

# 内容总结  

# 预备知识

1. MPAs 分类
   + 非目标攻击：使模型收敛到次优最小值或使模型完全发散
   + 目标攻击（后门攻击）：对手希望模型只对一组选定的样本进行错误分类，对其在主要任务上的性能影响最小
     + 语义后门攻击：
     + 木马后门攻击：
2. MPAs 防御对策
   + 拜占庭弹性聚合规则（BRARs）：在全局模型聚合过程中通过统计方法选择数据，如 KRUM 。
   + 使用异常检测方法来检测恶意的本地模型更新并将它们排除在聚合之外。

# 系统模型

+ 具有信任分数的联邦学习

![联邦学习系统模型](联邦学习系统模型.png)

在系统启动时，PS 初始化 `$\theta$` 。然后每次训练迭代的工作如下：
1. PS 首先选择多个客户端并将 `$\theta$` 分发给他们；
2. 每个选定的客户端，比如 `$C_i$` ，初始化  `$\omega_i = \theta$` 并使用其本地数据训练模型；
3. 本地训练结束后，`$C_i$` 将其模型更新 `$\delta_i$` 提供给 PS；  
4. PS 使用客户端提供的本地模型更新来计算每个客户端 `$C_i$` 的信任分数 `$S_i$` ；
5. 5 最后，PS 聚合由信任分数加权的局部模型更新，并通过以下方式更新全局模型：`$\theta = \theta + \sum_iS_i\delta_i$`。

在 FL 任务结束时，PS 输出最终的全局模型。

+ 威胁模型
  + 假设恶意客户端的数量少于 `$0.5n$`
  + 每个恶意客户端都是白盒对手

# 倒数第二层表示

+ 什么是倒数第二层？

![CNN结构](CNN结构.png)

函数 `$g$` 的输出是一个 PLR，用 `$r \in \mathbb{R}^o$` 表示。

+ 它在分离 MPA 中的作用

![命题1](命题1.png)

![命题2](命题2.png)

+ 可视化 PLR 分布

![PLRs可视化](PLRs可视化.png)

# FLARE: 防御 MPAs

+ FLARE 概述

![FLARE设计](FLARE设计.png)

+ 详细设计
