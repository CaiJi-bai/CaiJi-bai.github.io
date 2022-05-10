---
layout: mypost
title: PrivFL_Practical Privacy-preserving Federated Regressions on High-dimensional Data over Mobile Networks
categories: [论文阅读]
---

<table border="1">
    <tr>
        <th>论文英文名字</th>
        <th>PrivFL: Practical Privacy-preserving Federated Regressions on High-dimensional Data over Mobile Networks</th>
    </tr>
    <tr>
        <th>论文中文名字</th>
        <th>PrivFL：移动网络上高维数据的实用隐私保护联合回归</th>
    </tr>
    <tr>
        <td>作者</td>
        <td>Kalikinkar Mandal, Guang Gong</td>
    </tr>
    <tr>
        <td>来源</td>
        <td>CCSW@CCS 2019: London, UK</td>
    </tr>
    <tr>
        <td>年份</td>
        <td>2019年11月</td>
    </tr>
    <tr>
        <td>作者动机</td>
        <td>解决联邦学习中的模型隐私保护问题</td>
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

1. 提出了 Dropout-robust 回归训练协议
2. 在三种不同的威胁模型中证明了训练协议的安全性，以对抗模拟范式中的半诚实对手
3. 实验评估

# 预备知识

**加法同态加密**：一个加法同态加密（HE）方案由一个四元组组成, `$HE=(KeyGen,Enc,Eval,Dec)$`。  

![同态加密](HE.png)  

# 系统模型和目标
+ 系统模型
系统中有 m 个用户和 1 个服务器，每个用户有一个数据集。
+ 系统目标
  + 
# 回归协议
**主要目标**：为基于适合移动设备的加密原语的回归模型开发安全的训练协议，并且对用户掉线场景具有鲁棒性。  
+ Dropout-robust 安全缩放操作
+ 整体思路